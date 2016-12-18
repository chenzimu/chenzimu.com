title: 控制反转(Ioc)和依赖注入(DI)
date: 2016-12-16 22:07:47
categories: [PHP,'设计模式']
tags: ['依赖注入','PHP','Laravel','控制反转','DI','Ioc']
---

# 问题的提出-紧耦合(Tight Coupling)

从一个例子开始，看下边一段代码：

```php

	class Address {

    }

    class Customer {

        private $address;

        public function __construct()
        {
            $this->address = new Address();
        }

    }
```

假如有一个Customer类，这个类需要使用Address类的对象，换句话说Customer类是依赖于Address对象的，这样的情况会有下边几个问题：

1. 创建address对象的控制权在类Customer手里;
2. Customer类在自身的构造函数中直接对Address类进行引用对实例化，这就造成了Customer类和Address类的紧耦合;
3. Customer知晓Address类的具体的类型以及所需的参数等，如果Customer需要使用其他类型的Address类(比如OfficeAddress或HomeAddress)，这样Customer类也会发生相应的变化。

> 所以如果在Customer类中Address类实例化失败的话，就会导致整个Customer类执行失败。

# 问题的解决

解决该问题的关键就在于将Address类实例化的控制权从Customer类转移到别人手中。换句话说如果我们可以将Address类实例化的控制权反转给第三方的一个方法，这个问题就能解决了。这个解决方法就是*控制反转*。

# 控制反转(Ioc)的原则

*Do not call us we will call you*

这句话来自好莱坞，这是好莱坞对待面试演员者的的原则。将这句话表达的意思应用到Customerr类中就是Address类对Customer类说：“我不需要你来对我进行实例化，我会利用别的方法实例化我自己，你该干嘛干嘛吧！”。

## Ioc的两个原则

1. 主类(这里是Customer类)不能直接用来实现依赖类(这里是Address类),所有的类都必须依赖于一层抽象。该抽象可以是一个接口(interface),也可以是一个抽象类(acstract class);
2. 抽象层不能依赖于实现细节，但是实现的细节必须依赖于抽象层。

# Ioc的实现方法

Ioc只是一个停留在理论方面的东西，如果谈到具体的实现方法，这里就需要提到*依赖注入*(dependency injection)了。一共有4种实现依赖注入的方法:

1. 构造函数注入
2. setter和getter方法注入
3. 接口实现注入
4. 服务定位器(service locator)注入

## 构造函数注入

这个方法很简单，就是将类的实例化或者实现直接传到类的构造函数中。


```php

	class Address {

    }

    class Customer {

        private $address;

        public function __construct(Address $address)
        {
            $this->address = new Address();
        }

    }

```

## setter和getter方法注入

通过类中的setter和getter方法来实现依赖的注入。

```php

	class Address {

    }

    class Customer {

        private $address;

        public function getter()
        {
            return $this->address;
        }

        public function setter(Address $address)
        {

            $this->address= $address;

        }

    }

```

## 接口实现注入

```php

	interface AddressInterface {
        public function setAddress;
    }


    class Address implements AddressInterface {
        public function setAddress() {
            echo 'set address';
        }
    }

    class Customer {

        private $address;

        public function __construct(Address $address)
        {
            $this->address = $address;
        }
    }

```

## 服务定位器(service locator)注入

Customer类通过服务定位器获取到Address类的实例对象，服务定位器并不会对Address进行实例化，它只是提供了一个获取到实例化对象的服务的方法。


文章来源自:https://www.codeproject.com/Articles/29271/Design-pattern-Inversion-of-control-and-Dependency