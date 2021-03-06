Effective Objective-C (6) 理解“属性”这一概念
===

“属性”是Objective-C的一项特性，用于封装对象中的数据。

实例变量一般通过`存取方法`(access method)来访问，`获取方法`(getter)用于读取变量值，`设置方法`(setter)用于写入变量值。

Objective-C 2.0引入一种新的`点语法`

## `@property`

编译器自动编写访问属性所需的方法，此过程叫做`自动合成`。
这个过程又编译器在编译期执行。生成存取方法代码，自动向类中添加适合类型的实例变量，并在属性名前面加下划线，作为实例变量名字。
也可以用`@synthesize`语法来指定实例变量的名字。

使用`@dynamic`关键字，会告诉编译器： 不要自动创建实现属性所用的实例变量，也不要为期创建创建存取方法。

## 属性特质

属性可以拥有的特质分为四类：

### 原子性

- `nonatomic` (非原子的) 不使用同步锁
- `atomic` (原子的) 使用同步锁

### 读/写权限

- `readwrite` (读写) 拥有`获取方法`(getter)与`设置方法`(setter)
- `readonly` (只读) 仅拥有`获取方法`(getter)

### 内存管理语义

- `assign` 设置方法只会执行针对`纯量类型`(如CFCGFloat或NSInteger等)的简单赋值操作。
- `strong` 表明该属性定义了一种`拥有关系`。为这种属性设置新值时，设置方法会先保留新值，并释放旧值，然后再将新值设置上去。
- `weak` 定义一种`非拥有关系`。为这种属性设置新值时，设置方法既不保留新值，也不释放旧值。此特质同`assign`类似，然而在属性所指的对象遭到摧毁时，属性值也会清空。
- `unsafe_unretained` 同`assign`，但适应于`对象类型`，表达一种`非拥有关系`，当目标对象遭到摧毁时，属性值不会自动清空
- `copy` 所属关系与`strong`类似。设置方法不是保留新值，而是将其`拷贝`(copy)

### 方法名
