### 用原型和静态方法绑定 this


### private、public、static
#### static
- 说明

静态公有字段不会在子类里重复初始化，但我们可以通过原型链访问它们。
静态方法调用直接在类上进行，不能在类的实例上调用。静态方法通常用于创建实用程序函数。

- 静态方法的调用
  - 从另一个静态方法（CLASSNAME.staticMethod()）
  - 从类构造函数（this.constructor.staticMethod()）

#### public
- 说明：
  - public 方法：即 construtor.prototype.publicFunction（当寻找一个成员并且它不在对象本身里时，则从对象的构造函数的prototype成员里找。）

### private
- 说明：
  - private成员由构造函数产生

关键字	类本身	类的方法	类的实例	子类	子类方法	子类的实例
static	+	-	-	+	-	-
public	-	+	+	-	+	+
private	-	+	-	-	-	-
protected	-	+	-	-	+	-