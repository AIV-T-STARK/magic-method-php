# Magic method
---
## __contruct()
- Hàm này được gọi khi khởi tạo đối tượng

```
Class VNPer {
    public function __construct() {
        echo 'Một object VNPer vừa được tạo';
    }
}

$me = new VNPer() //Một object VNPer vừa được tạo
```
```
Class VNPer {
    public $name;
    public $age;
    public function __construct($name, $age) {
        $this->name = $name;
        $this->age = $age;
    }
}

$me = new VNPer("Gia Hao", 20);
var_dump($me);
//object(VNPer)#1 (2) { ["name"]=> string(7) "Gia Hao" ["age"]=> int(20) }
```

## __destruct() 
- Hàm này được gọi khi đối tượng bị hủy
- Thường là khi kết thúc chương trình hoặc khai báo mới đối tượng.


## __set() và __get() 
- Với các thuộc tính không được public, để truy suất/thay đổi ta sẽ sử dụng method __get() và __set()
```
Class VNPer {
    private $name;
    private $age;

    public function __construct($name, $age) {
        $this->name = $name;
        $this->age = age;
    }

    public function __get($property) {
        return $this->$property;
    }

    public function __set($property, $value) {
        $this->$property = $value;
    }
}

$me = new VNPer("Gia Hao", 20);

echo $me->name; //Gia Hao
$me->age = 21;
echo $me->age; //21
```

## __isset() và __unset()
- __isset() is triggered by calling isset() or empty() on inaccessible (protected or private) or non-existing properties.
- __unset() is invoked when unset() is used on inaccessible (protected or private) or non-existing properties.
## __call($method, $params) 
- Hàm được gọi khi ta gọi đến một phương thức không tồn tại hoặc không public

## __callSatic($method, $params)
- Tương tự thằng __call() nhưng dùng cho phương thức tĩnh

## __toString()
- Được gọi khi ta dùng object như một chuỗi

```
Class VNPer {
    public function __toString() {
        return 'I am a VNPer';
    }
}

$me = new VNPer();
echo $me; //I am a VNPer
```

## __invoke()
- Được gọi khi ta sử dụng object như 1 hàm
```
Class A {
    public function __invoke($name) {
        var_dump($name);
    }
}
$var = new A();
$var();
```

## __sleep() và __wakeup()
- __sleep() được gọi khi ta sử dụng serialize()
```
class ConNguoi
{
    private $name = 'Nguyen Gia Hao';
    private $age = 20;

    public function __sleep()
    {
        
        return array('name');
    }
}

echo serialize(new ConNguoi());
//O:8:"ConNguoi":1:{s:14:"ConNguoiname";s:14:"Nguyen Gia Hao";}
```
- __wakeup() được gọi khi ta sử dụng deserialization()
```

```
## __clone()
- Được gọi khi chúng ta clone(sao chép) một object

## __debugInfo()
- được gọi khi chúng ta sử dụng var_dump()


## __autoload($calssName)
- Attempt to load undefined class
- Hiện tại được khuyến cáo không nên sử dụng, thay vào đó sử dụng spl_autoload_register()

```
<?php
include __DIR__ . '/classes/MyClass.php';
include __DIR__ . '/classes/Foo.php';
include __DIR__ . '/classes/Bar.php';


$obj = new MyClass;
$foo = new Foo;
$bar = new Bar;
```

- Thay vì viết như thế kia thì ta có thể sử dụng spl_autoload_register()
```
<?php
spl_autoload_register(function ($classname) {
    include __DIR__ . '/classes/' . $classname . '.php';
});

$myClass = new MyClass;
$foo = new Foo;
$bar = new Bar;
```
