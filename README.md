README

## 从 `/public/index.php` 入口
```php
// file:/public/index.php
require __DIR__.'/../vendor/autoload.php';
```

引入了 `autoload.php`

## 进入 `/local/vendor/autoload.php`

```
<?php
// file:/local/vendor/autoload.php
// autoload.php @generated by Composer

require_once __DIR__ . '/composer/autoload_real.php';

return ComposerAutoloaderInit53e7e9fbc7f3b93c224f3bd5f4f6ec3e::getLoader();

```

引入了 `/vendor/composer/autoload_real.php`
并调用了 `getLoader` 方法

## 进入 `/vendor/composer/autoload_real.php`
```
// ...
class ComposerAutoloaderInit53e7e9fbc7f3b93c224f3bd5f4f6ec3e
{
    private static $loader;

    public static function loadClassLoader($class)
    {
        if ('Composer\Autoload\ClassLoader' === $class) {
            require __DIR__ . '/ClassLoader.php';
        }
    }
    // 执行该方法
	public static function getLoader()
	{
	    if (null !== self::$loader) {
	        return self::$loader;
	    }
	    
	    // 此时上面的if不会执行，因为 self::$loader 是空
	    
		// 注册该class 和 上面的 loadClassLoader
	    spl_autoload_register(array('ComposerAutoloaderInit53e7e9fbc7f3b93c224f3bd5f4f6ec3e', 'loadClassLoader'), true, true);
	    // 赋值 $loader
	    self::$loader = $loader = new \Composer\Autoload\ClassLoader();
	    spl_autoload_unregister(array('ComposerAutoloaderInit53e7e9fbc7f3b93c224f3bd5f4f6ec3e', 'loadClassLoader'));
	
	    $useStaticLoader = PHP_VERSION_ID >= 50600 && !defined('HHVM_VERSION') && (!function_exists('zend_loader_file_encoded') || !zend_loader_file_encoded());
	    if ($useStaticLoader) {
	        require_once __DIR__ . '/autoload_static.php';
	
	        call_user_func(\Composer\Autoload\ComposerStaticInit53e7e9fbc7f3b93c224f3bd5f4f6ec3e::getInitializer($loader));
	    } 
