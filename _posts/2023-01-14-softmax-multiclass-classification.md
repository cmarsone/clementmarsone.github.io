---
layout: post
title: Multiclass classification
---

## Implementing a multiclass perceptron from scratch

The **multiclass perceptron** can be implemented this way. 
We denote $K$ the number of classes, $N$ the number of (training) examples, $D$ the dimension of the data (after feature augmentation, at least with a "1" as first component).

The **output** of the network *(not equal to the predicted label)*, can be taken as the **softmax** among the $K$ separating hyperplanes (each hyperplane $\vec{w}_k$ separates class $k$ from the others).
$$ y_k^{(n)} = \text{softmax}\big( (\vec{w}_{k} \cdot \vec{x}^{(n)})_{k=1...K} \big) = \frac{ \exp(  \vec{w}_k\cdot\vec{x}^{(n)}   )}{\sum_\ell \exp(  \vec{w}_\ell\cdot\vec{x}^{(n)})}$$
This output can be **interpreted as the probability** that example $x^{(n)}$ belongs to the class $k$, according the classifier's current parameters
Indeed, one can easily check that for any $\vec{x}$, the sum of probabilities is indeed one : $\sum_k y_k = 1$.
The **total output of the network** is a vector $\vec{y}^{(n)} = \begin{pmatrix}y_1^{(n)} \\ y_2^{(n)} \\ .. \\ y_K^{(n)} \end{pmatrix}$ (for the sample number $n$).

The **true labels (ground truth)** of example $\vec{x}^{(n)}$ is then encoded as a one-hot vector, so that if the example is of the second class, it may be written : $\vec{t}^{n} = \begin{pmatrix} 0 \\ 1 \\ 0 \\ .. \\ 0 \end{pmatrix}$ where $\vec{t}^{(n)}$ or $\vec{t}^{n}$ is for truth and is shorter to write than $\vec{y}^{GT,(n)}$. More generally, the components $t_{n,k}$ of vector $\vec{t}_n \text{may be written using the Kronecker's delta :} t_{n,k} = \delta(k, k_{true}^{n})\text{, where } k_{true}^{n} \text{ is the true class of example number } n$.

From now on, **we drop the superscrip $a^{(n)}$ and instead write $a_n$ or just $a$**, when it's clear enough that the quantity $a$ relates to a single example, of generic index $n$. This helps to lighten the notations.

The Loss function that we should use is called the **cross-entropy loss function**, and is:

$$J = \frac1N \sum_n^N H(\vec{t}_{n}, \vec{y}_{n})$$

where the cross-entropy is a non-symmetric function: $$H(\vec{t}_{n}, \vec{y}_{n}) = -\sum_k^K t_{n,k} \log (y_{n,k})$$
    
    import numpy as np

    class MulticlassClassifier:
        def __init__(self):
            self.thetas = None

        def softmax(self, activations):
            exp_activations = np.exp(activations)
            sum_exp_activations = np.sum(exp_activations)
            softmax_activations = exp_activations / sum_exp_activations
            return softmax_activations
  
        def predict(self, X):
            z = np.dot(X, self.thetas)
            predictions = self.softmax(z)
            return predictions

        def loss(self, y_true, y_pred):
            epsilon = 1e-7
           y_pred = np.clip(y_pred, epsilon, 1. - epsilon)
           loss = - np.mean(y_true * np.log(y_pred))
           return loss

        def model_loss_gradients(self, X, y_true, thetas):
            y_pred = self.predict(X)
            gradients = np.dot(X.T, (y_pred - y_true)) / len(X)
            return gradients

        def gradient_descent(self, X, y_true, initial_thetas, learning_rate, n_iterations):
           self.thetas = initial_thetas
           for _ in range(n_iterations):
               gradients = self.model_loss_gradients(X, y_true, self.thetas)
               self.thetas -= learning_rate * gradients
           return self.thetas

        def fit(self, X, y_true, n_iterations):
            n_features = X.shape[1]
            n_classes = len(set(y_true))
            initial_thetas = np.random.randn(n_features, n_classes)
            learning_rate = 0.1
            y_true_onehot = self.one_hot_encoding(y_true)
            self.gradient_descent(X, y_true_onehot, initial_thetas, learning_rate, n_iterations)

        def one_hot_encoding(self,int_labels):
            n_labels = len(int_labels)
            n_unique_labels = len(set(int_labels))
            one_hot = np.zeros((n_labels, n_unique_labels))
            one_hot[np.arange(n_labels), int_labels] = 1
            return one_hot

        def predict(self, X):
            return np.argmax(self.predict(X), axis=1)

        def score(self, X, y_true):
            y_pred = self.predict(X)
            accuracy = np.mean(y_pred == y_true)
            return accuracy

        def get_parameters(self):
            return self.thetas
