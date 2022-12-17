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

## 流程控制 (Control Structures)

[PHP: Control Structures - Manual](https://www.php.net/manual/en/language.control-structures.php)



### if / else / elseif / else if

- `elseif` 和 `else if` 没有区别, 但在 `HTML` 中只能使用 `elseif`

```php
if ($condition1) {
  // executed when $condition1 is `true`
} elseif ($condition2) {
  // executed when $condition2 is `true`
} else if ($condition3) {
  // executed when $condition3 is `true`
} else {
  // executed when $condition1, 2, 3 are all `false`
}
```



### 循环 (Loop)

- `continue` 可以跳过当前循环执行并开始下一次
- `break` 会结束当前循环
- 除了 `do-while` 都有两种格式 (方便 `HTML` 中使用, 服务端不建议)

#### while

```php
while ($condition) {
  // executed if $condition is true and will run again
}

while ($condition):
	// 另一种格式
endwhile;

while (true) {
  // infinite loop
}
```

#### do-while

- 和 `while` 的区别在于它保证代码块中的代码至少执行一次

```php
do {
  // executed at least once and when $condition is true
} while ($condition);
```

#### for

- 若有多个表达式, 则判断是否继续循环的条件以最后一个的结果为准

```php
for ($i = 0; $i < 15; $i++) {
  // the same as in JavaScript
}

for ($i = 0, $length = count('test'); print $i, $i < 15; print $i, $i++) {
  // 多个表达式, 用 `,` 分割, JavaScript中也可以
}

for ($i = 0; $ < 15; $i++):
	// 另一种格式
endfor;
```

#### foreach

- 用于迭代 `可迭代` 的变量
- `as` 之后是每一次遍历到的值
- 默认传递 `数值`, 但也可以使用 `&` 可以让其传递 `引用` , 即修改时也会修改原数组
- ❗ `as` 之后的变量在循环结束后不会被清除, 要小心 (尤其是传递 `引用` 时), 为可迭代变量最后一个元素

```php
$arr = [1, 2];

foreach ($arr as $num) {
  echo $num;
}

foreach ($arr as $key => $value) {
  // 另一种键值对提取方式
}

foreach ($arr as &$num) {
  $num += 1; // 会修改原数组, 因为 `&` 代表传递 `引用` 而不是 `数值`
}

// ❗
$num = 3; // as之后的变量可以继续使用, 所以要小心, 尤其是传递 `引用` 时
print_r($arr); // [1, 3] 被改变了, 因为 $num 是引用并且循环结束后没有被销毁

foreach ($arr as $num):
	// 另一种格式
endforeach;
```

















