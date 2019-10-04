> ****WIP***
# Object Oriented PHP

## Index

1. [Introduction](#1-introduction)
1. [Header one](#object-oriented-php)
1. [Header one](#object-oriented-php)
1. [Header one](#object-oriented-php)
1. [Header one](#object-oriented-php)

## 1. Introduction

**PHP**: Hypertext Preprocessor (or simply PHP) is a general-purpose programming language originally designed for web development. It was originally created by Rasmus Lerdorf in 1994; the PHP reference implementation is now produced by The PHP Group. PHP originally stood for Personal Home Page, but it now stands for the recursive initialism PHP: Hypertext Preprocessor. [Wikipedia]

**Object-oriented programming**: OOP is a programming paradigm based on the concept of "objects", which can contain data, in the form of fields, and code, in the form of procedures. A feature of objects is an object's procedures that can access and often modify the data fields of the object with which they are associated. [Wikipedia]

### 1.1. Object oriented concepts

1. Classes
2. Objects
3. Methods & Properties
4. Data Abstraction
5. Encapsulation
6. Inheritance
7. Polymorphism
8. Constructor & Destructors

#### 1.1.1. Classes
**Class** is a blueprint for creating objects (a particular data structure), providing initial values for state (member variables or attributes), and implementations of behavior (member functions or methods).

#### 1.1.2. Objects

**Object** is a realworld representation of the class.


```php
    class User{
        public function register(){
            echo "User registered";
        }
        public function login($username, $password){
            echo "Welcom ".$username;
        }
    }

    $user = new User();
    $user->register();

```

#### 1.1.3. Inheritance

**Inheritance** is a mechanism in which one class acquires the property of another class. For example, a child inherits the traits of his/her parents. With inheritance, we can reuse the fields and methods of the existing class. Hence, inheritance facilitates Reusability and is an important concept of OOPs.


```php
    class Books{
        public funOne(){
            echo "I am in funOne";
        }
    }

    $newOnject = new Books();
    $newObject->funOne();
```

### 1.1.4. 

### 1.1.8 Constructors and destructors

Constructor called everytime a object is created.

Destructor is called before script ends / object goes out of scope.

```php
    class User{
        public function __construct(){
            echo "constructor called";
        }
    }

    class User{
        public function __destruct(){
            echo "destructor called";
        }
    }

    $user = new User();
    // Results: 
    // constructor called
    // destructor called
```

### 1.2. Visibility / Access identifiers

> Apllies to both properties, variables and methods.

* **Private**: Accessible only in owner class.
* **Protected**: Accessible in owner class and extended class.
* **Public**: Accessible ouside the class

### 1.3. Abstract Classes

* Used as base classes.
* Can not be instantiated and used directly.
* Must be extended to use.
* If any class contains any property/method as abstract then class must be abstract as welll.

```php
    abstract class Books{
        abstract public funOne(){
            echo "I am in funOne";
        }
    }
```
