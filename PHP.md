# PHP

[Personal Home Page](https://www.php.net/)

---

## 基本格式 (Basic Format)

- 以 `<?php` 开头, 以 `?>` 结尾
  - 如果整个文件都是 `php`, 那么 `?>` 可以省略
- 句末必须要加 `分号 ;`
  - 唯一的例外是 `?>` 之前的一句可以不加 `;`, 但是不推荐

```php
echo 'hello world';
```

- `string` 相关见 `数据类型 -> string`

---

## 变量 (Variable)

- 变量使用 `$` 打头定义

```php
$firstName = 'Aelita';
```

- 变量传递的是数值

```php
$a = 1;
$b = $a;
$a = 2;

echo $b; // 1
```

- 若想传递 `引用地址`, 在被引用的变量前使用 `&`

```php
$a = 1;
$b = &$a;
$a = 2;

echo $b; // 2
```



### 可变变量

- `变量` 可以作为其他 `变量` 的名称的一部分
  - 可以配合 `${}` 任意操作

```php
$foo = 'bar';
$$foo = 'baz';
$$$foo = 'bazz';

echo $foo; // bar

echo $bar; // baz
echo $$foo; // baz
echo ${$foo}; // baz
echo $${'foo'}; // baz

echo $baz; // bazz
echo $$bar; // bazz
echo $$$foo; // bazz
echo ${$bar}; // bazz
echo ${$$foo}; // bazz
echo $${$foo}; // bazz
echo $$${'foo'}; // bazz
```

---

## 常量 (Constant)

- 使用 `const` 定义, 不需要加 `$`
  - 只能在 `top-level` 使用
- 使用 `define(constant_name, value)` 定义

```php
const CONSTANT = 'constant';
define('NAME', 'value');

echo CONSTANT; // constant
echo NAME; // value

// ❌❌❌❌❌
if (true) {
  const FOO = 'bar'; // ERROR
}
```

- 一般使用 `UPPER_CASE`
- 使用 `defined(constant_name)` 来检查一个 `常量` 是否被定义 (返回 `boolean`)

```php
const CONSTANT = 'constant';
defined(CONSTANT); // true
defined(FOO); // false
```

- `常量` 名称可以动态拼接 (不推荐)
  - 仅限 `define()`

```php
$foo = 'BAR';
define('FOO' . $foo, 4);
echo FOOBAR; // 4
```

- 有很多 `全局常量`, 比如 `PHP_VERSION` / `__LINE__` 等等

---

## 表达式 (Expression)

- 基本上任何一句都是 `表达式`
- 任何可以 evaluate to 一个值的句子都是 `表达式`

---















