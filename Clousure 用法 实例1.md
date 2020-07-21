Clousure 用法 实例1

## 修改某个静态类的私有变量，此处为 `Bar` 的 `$value`
```php
<?php

class Bar
{
    public static $value = 'bar';

}


class Foo
{
    public static function getInitializer(Bar $bar)
    {
        return \Closure::bind(function () use ($bar) {
            $bar->value = "changed in Closure";
        }, null, Bar::class);
    }
}
$bar = new Bar;

call_user_func(Foo::getInitializer($bar));

var_dump($bar);

// $bar->value = 'changed outside';


?>
```
