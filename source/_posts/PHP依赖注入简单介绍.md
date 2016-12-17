title: PHP依赖注入简单介绍
date: 2016-12-16 22:07:47
categories: [PHP,'设计模式']
tags: ['依赖注入','PHP','Laravel']
---

## 什么是依赖注入

依赖注入的一种软件的设计模式，依赖注入解决的是对象依赖的问题。

## 不使用依赖注入的情况

假设有一个类A，需要使用类B和类C的对象，如果不使用依赖注入的话通常会这样写代码:

```php

    class B {
        public function say() {
            echo 'I am b';
        }
    }

    class C {
        public function say() {
            echo 'I am c';
        }
    }

    class A {

        private $b;
        private $c;
        public function __construct()
        {
            $this->b = new B();
            $this->c = new C();
        }

        public function sayB() {
            return $this->b->say();
        }

        public function sayC() {
            return $this->c->say();
        }
    }

    $a = new A();

    echo $a->sayB();

    echo $a->sayC();
```

上边的代码乍看没有问题，但是会发现在A的构造函数中我们需要先对B和C进行实例化，然后才能调用BC中的方法。所以A是严重的依赖于BC的，因为此时BC中并没有构造函数，所以在对BC进行实例化的时候不用传递任何参数。试想这样一种情况，如果我们需要对BC添加构造函数，并在构造函数中添加参数，如：


```php

    class B {

        private $words;

        public function __construct($words)
        {
            $this->words = $words;
        }

        public function say() {
            echo $this->words;
        }
    }

    class C {

        private $words;

        public function __construct($words)
        {
            $this->words = $words;
        }

        public function say() {
            echo $this->words;
        }
    }

    class A {
        private $b;
        private $c;
        public function __construct()
        {
            $this->b = new B('I am b from constructor');
            $this->c = new C('I am c from constructor');
        }

        public function sayB() {
            return $this->b->say();
        }

        public function sayC() {
            return $this->c->say();
        }
    }

    $a = new A();

    echo $a->sayB();

    echo $a->sayC();
```

从上边的代码可以看出如果在BC中添加构造函数并添加参数的话，相应的A中构造函数对BC的实例化也需要进行修改(因为A与BC是高度耦合的)。这就违反了软件设计中的单一职责原则(single responsibility)，A不仅仅需要负责对自身的属性和方法的定义，还需要关心自己依赖的对象BC的实例化，而依赖注入就是为了解决这一问题的。

## 使用依赖注入


```php


	class B {

        private $words;

        public function __construct($words)
        {
            $this->words = $words;
        }

        public function say() {
            echo $this->words;
        }
    }

    class C {

        private $words;

        public function __construct($words)
        {
            $this->words = $words;
        }

        public function say() {
            echo $this->words;
        }
    }

    class A {
        private $b;
        private $c;

        // 将A需要依赖对象传递到A的构造函数中
        public function __construct(B $b, C $c)
        {
            $this->b = $b;
            $this->c = $c;
        }

        public function sayB() {
            return $this->b->say();
        }

        public function sayC() {
            return $this->c->say();
        }
    }

    $a = new A(new B('I am b outside a'),new C('I am c outside a'));

    echo $a->sayB();

    echo $a->sayC();

```

在上边的代码中，可以看到在A的构造函数中，将A需要的依赖BC传入到A的构造函数中，这样就将BC初始化的任务交给了“其它人”，这里可以对比没有用依赖注入的例子，在没有使用依赖注入的例子中，对BC进行初始化的任务是由A自身完成的。所以，使用依赖注入之后，A就只负责关心对自身的方法以及属性的定义，而对于自身的依赖BC或者别的依赖则不需要关心它们是怎么实现的，只需要调用它们就可以了，这就解决了上例中所违反的单一职责原则(single responsibility)。

*未完待续*

