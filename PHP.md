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

- `单引号 ''` 代表纯 `string`
- `双引号 ""` 中的 `变量 / 常量` 不会作为字符串处理
  - 可以在变量两头加上 `{}`, 但不是必要的
  - 也可以将[任意数量]的 `$` 提取到 `{}` 外围, 内部也可以保留任意数量 (见[可变变量](###可变变量))
    - 但若 `{}` 内没有了 `$`, 则需要加上 `引号` (单双视情况而定)

```php
$a = 'world';

echo 'hello $a'; // hello $a
echo 'hello {$a}'; // hello {$a}

echo "hello $a"; // hello world
echo "hello {$a}"; // hello world
echo "hello ${'a'}"; // hello world
```

- 使用 `.` 可以连接 `string`

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

## 数据类型 (Data Type)

- `php` 是 `弱类型` 语言, 类似 `JavaScript`
- 会自动推导类型
  - `75` 推导成 `int`
  - `'75'` 推导成 `string`



### 类型转换 (Type Juggling / Coercion)

- `php` 会在需要的时候隐式转换数据类型
  - 会根据上下文转换成需要的类型
  - 如果隐式转换不成功, 会抛出一个 `Error`
- `strict mode` 中, 除了 `int` -> `float` 的转换, 其他会报错
  - 使用 `declare(strict_types=1` 来开启 `strict mode`

```php
declare(strict_types=1);

function sum(float $x, float $y): float {
  return $x + $y;
}

var_dump(sum(2, 2)); // float(4)
```



### 类型转换 (Type Casting)

- 可以在 `数据` / `变量` 前加上 `(type)` 来强制转换数据的类型

```php
$x = (int)'5';
var_dump($x); // int(5)
```



### 标准类型 (Scalar Type)



#### boolean



#### integer



#### float



#### string



### 复合类型 (Compound Type)



#### array



#### object



#### callable



#### iterable



### 特殊类型 (Special Type)



#### resource



#### null

