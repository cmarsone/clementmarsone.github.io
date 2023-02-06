---
layout: post
title: Programmation Avancée C++
author: Clément
---

### Un langage multi-paradigmes:
● Support du style *impératif*. Le code est une simple liste d'instructions. Ses éléments fondamentaux sont les fonctions et les structures de données
● Support du style *objet*. Le code s'articule autour de la définition d'objets modélisant les éléments du problème. Ses éléments fondamentaux sont les classes et les relations entre ces classes
● Support du style *générique*. Le code s'écrit en toute indépendance des types concrets. Une partie des calculs sont résolus à la compilation
● Support du style *fonctionnel*. Le code est basé sur l'utilisation de fonctions et de valeurs. Il n'y a pas de notion de mémoire ou de structure de contrôle

### Notion d'invariant (`const`)
● Un invariant est l'ensemble des propriétés mettant en œuvre les données membres d'une classe qui doivent rester vrai tout au long de la durée de vie d'une instance de cette classe.
● Une classe ne respectant plus ces invariants est dite *incohérente*

### Modèle agrégat
● La mission d'un agrégat est d'*être un ensemble de valeurs*
● La cohésion de ses valeurs ne suffit pas à construire une sémantique claire i.e. visibilité
● *Un agrégat n'a pas d'invariants*

#### Cas des `struct {};`
● Visibilité par défaut: `public`
● Pas d'invariant car le contenu est accessible par tous
● L'important c'est les valeurs

### Notion de classe: regroupement dans une même entité des données et des fonctions membres
● La mission d'une classe est de *fournir un service*
● Ce service s'appuie des données membres / valeurs et des méthodes membres / fonctions
● *Une classe a des invariants qu'elle protège*

Un *objet* est un élément d'une certaine classe : on parle de l'*instance d'une classe*.

#### Cas des `class {};`
● Visibilité par défaut: `private`
● Des invariants existent et sont protégés par le masquage des membres associés
● L'important c'est le comportement

### Encapsulation: mécanisme qui interdit d'accéder à certaines données depuis l'extérieur de la classe
● Force le respect de la sémantique de la classe. Il faut éviter de donner un accès extérieur aux données membres d'un objet quelconque.
● Notion de *visibilité*`public`, `protected` (depuis les fonctions qui sont membres ou `friends`), `private` (accessible par les classes filles)
● Notion de *membres spéciaux*: construction, affection, destruction
● Notion d'*assertion*

• L'ensemble des méthodes publiques est appelée l'*interface de l'objet*

#### Accesseurs
• On pourra accéder aux valeurs des données membres privées grâce à des méthodes spécifiques appelée *accesseurs*. Ces derniers sont publics et ne modifient pas l'état de l'objet (`const`)
• Au moindre invariant, il faut utiliser `private`
#### Modificateurs d'accès
• On pourra même modifier ces valeurs grâce à des fonctions spécifiques appelées *mutateurs*. Ces derniers sont publics et peuvent modifier l'état de l'objet ($\neq$ `const`)

### Constructeur

Lorsqu'on crée une nouvelle instance d'une classe, les données membres de cette instance ne sont pas initialisées par défaut. 

Un *constructeur* est une fonction membre qui sera appelée au moment de la création d'une nouvelle instance d'une classe. Il est également appelé lorsqu'une instance est créée grâce à l'opérateur `new`.

Le *constructeur par défaut* : c'est le constructeur sans argument. Si aucun constructeur n'est présent explicitement dans la classe, il est généré par le compilateur. Il faut de préférence privilégier la notation `T f{}` ($\neq$ `T f()`) pour expliciter l'appel au constructeur par défaut afin d'éviter le *most vexing parse*.

Le *constructeur de copie* : c'est un constructeur à un argument dont le type est celui de la classe. En général, l'argument est passé par référence constante. Plus rarement, il peut l'être par valeur ou référence non constante. Si il n'est pas explicitement présent dans la classe, il est généré par le compilateur. Notons encore que:
Si un constructeur de copie est fourni dans une classe, il sera très probable de devoir fournir l'opérateur d'assignation avec le même type d'argument.
Il est possible de rendre une classe non copiable en privatisant la déclaration du constructeur de copie et de l'opérateur d'assignation. Dans ce cas, il n'est pas nécessaire (recommandé) de fournir leur définition.

Les constructeurs de *conversion implicite* : il s'agit de constructeurs à un seul argument dont le type est différent de celui de la classe et qui ne sont pas déclarés explicit. Ces constructeurs rendent possible la conversion implicte du type d'argument vers le type de la classe.

Syntaxe pour une classe $A$:

`A(); // constructeur par défaut. Utliser la liste d'initiation si possible `

`A(const A &); // constructeur de copie`

`A(const T &); // constructeur de conversion implicite`

`explicit A(const T &); // les constructeurs à un seul paramètre doivent être explicit le plus souvent possible pour éviter les appels implicites de fonction`

### Destructeur

Le *destructeur* d'une classe est appelé lorsqu'une de ses instances doit être détruite lors d'une allocation dynamique `delete` ou `~A();`
Un appel explicite avec `delete` est nécessaire lorsqu'une instance a été allouée avec `new`.

### Surcharge d'opérateurs

*Opérateur d'affectation* permettant d'affecter une valeur à une instance de structure

### Polymorphisme: permet de modifier le comportement d'une classe en fonction de son type de paramètres
● Types : statique, dynamique, ad hoc, universel.
● Notion d'*héritage* public (polymorphisme) ou privé (factorisation de code)
● Notion de *fonction virtuelle*. Le mot-clé `virtual` permet d'indiquer les membres participant à l'aspect polymorphe d'une classe

#### Classe abstraite

Une *classe abstraite* est une classe pour laquelle on a défini une méthode mais on a explicitement indiqué qu'on ne fournira aucune implémentation de cette méthode. Elle fournit un contrat sans comportement par défaut et force ses sous-classes à l'implémenter sous peine d'erreur. Il est interdit de créer une instance d'une classe abstraite. Ce mécanisme est extrêmement puissant pour manipuler des concepts abstraits. On peut même avoir une classe pour laquelle toutes les méthodes sont abstraites, on parle alors de classe abstraite pure. Une classe héritant d'une classe abstraite doit fournir une implémentation des méthodes abstraites ou bien elle sera à son tour une classe abstraite

#### Pointeur de membre pointant un membre d'un objet i.e. variable ou méthode

Ce genre de pointeur, rarement utilisé, possède une syntaxe spéciale. L'étoile `*` est remplacée par `class::*` signifiant un pointeur sur un membre de cette classe, ou d'une classe dérivée. Ce genre de pointeur occupe plus de place qu'un pointeur classique, et occupe un nombre d'octets variable selon la classe.

## Gestion de ressources

Notion de catégorie de valeurs
● En plus de son type, une variable est classifiée selon sa catégorie de valeur
● La catégorie de valeur indique comment la durée de vie d'une valeur est gérée

Notion de lvalue
● Une lvalue est une valeur avec un nom, un identifiant
● La durée de vie d'une lvalue est la portée courante

Notion de rvalue
● Une rvalue est une valeur sans identifiant ou littérale
● La durée de vie d'une rvalue est l'expression courante
