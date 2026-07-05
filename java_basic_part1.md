[toc]

![学习路线参考](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260527131324086.png)

![课程目录](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260527131427455.png)

![课程时长](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260527131500065.png)



# Day01-Java 入门

## Java 学习介绍

1. OOP
2. Java 核心知识点
   1. API
   2. 集合
   3. BIO
   4. NIO
   5. 多线程
   6. 网络编程
3. 斯坦福大学真题练习
4. 阿里巴巴的编码规范
5. 手写 Tomcat 服务器，虚拟机，算法，数据结构
6. 老师多年经验心得

## 人机交互

### 人机交互小故事

只有命令行

MS-DOS

XEROX--> 图形化界面

但是图形化界面

- 消耗内存
- 运行速度慢

### 打开 CMD

`win+r`

`cmd`

### 常用 CMD 命令

#### 盘符名称+冒号



# day09-面向对象综合训练

## 文字版格斗游戏



![image-20260524225317839](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260524225317839.png)

### 自行作答

```java
package com.itheima.test1;

public class Role {
    private String name;
    private int blood;

    public Role() {
    }

    public Role(String name, int blood) {
        this.name = name;
        this.blood = blood;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getBlood() {
        return blood;
    }

    public void setBlood(int blood) {
        this.blood = blood;
    }

    public void attack(Role attacker, Role target, int damage) {
        target.setBlood(target.getBlood()-damage);
        if(target.getBlood()<=0){
            System.out.println(attacker.getName()+"KO了"+target.getName());
        }else{
            System.out.println(attacker.getName() + "攻击了" + target.getName()+"造成了"+damage+"点伤害，"+target.getName()+"还剩下"+target.getBlood()+"点血");
        }
    }
}
```

### 参考答案

对象调用方法，在该方法内需要使用该对象调用别的方法，可以直接使用 this 关键字，**不用再将对象作为参数传入**

> - 具体体现为方法 `public void attack(Role1 target)` 仅有一个参数
> - 另外注意，血量不能低于 100，`remainBlood = remainBlood < 0 ?0 : remainBlood;`

```java
//参考答案：attack()方法改进
package com.itheima.test1;

import java.util.Random;

public class Role1 {
    private String name;
    private int blood;

    public Role1() {
    }

    public Role1(String name, int blood) {
        this.name = name;
        this.blood = blood;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getBlood() {
        return blood;
    }

    public void setBlood(int blood) {
        this.blood = blood;
    }

    public void attack(Role1 target){
        //计算造成的伤害
        Random random = new Random();
        int damage = random.nextInt(20)+1;

        //剩余血量
        int remainBlood = target.getBlood()-damage;
        remainBlood = remainBlood < 0 ?0 : remainBlood;
        target.setBlood(remainBlood);

        //使用this关键字
        System.out.println(this.getName() + "攻击了" + target.getName()+"造成了"+damage+"点伤害，"+target.getName()+"还剩下"+target.getBlood()+"点血");
    }
}
```

```Java
package com.itheima.test1;

public class RoleTest1 {
    static void main(String[] args) {
        Role1 r1 = new Role1("乔峰", 100);
        Role1 r2 = new Role1("鸠摩智", 100);

        while(true){
            r1.attack(r2);
            if(r2.getBlood()<=0){
                System.out.println(r1.getName()+"KO了"+r2.getName());
                break;
            }
            r2.attack(r1);
            if(r1.getBlood()<=0){
                System.out.println(r2.getName()+"KO了"+r1.getName());
                break;
            }
        }

    }
}
```

### 题目改进

![题目要求](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260525145311043.png)

在此之间，先来讲讲另一种输出语句：`souf`

```java
System.out.printf("");
使用方法和C中的差不多
没有换行效果
```



| 格式符  | 类型           | 示例           |
| ------- | -------------- | -------------- |
| %d      | 十进制整数     | int            |
| %f      | 浮点数         | float / double |
| %s      | 字符串         | String         |
| %c      | 字符           | char           |
| %b      | 布尔值         | boolean        |
| %x / %X | 十六进制整数   | int            |
| %o      | 八进制整数     | int            |
| %e / %E | 科学计数法     | double         |
| %n      | 平台独立换行符 | 无参数         |

------

```java
package com.itheima.test1_1;

import java.util.Random;

public class Role {
    private String name;
    private int blood;
    private char gender;
    private String face;//题目要求，长相随机

    //容颜：

    String[] boyfaces= {"风流俊雅","气宇轩昂","相貌英俊","五官端正","相貌平平","一塌糊涂","面目狰狞"};
    String[] girlfaces ={"美奂绝伦","沉鱼落雁","婷婷玉立","身材娇好","相貌平平","相貌简陋","惨不忍睹"};

    public Role() {
    }

    public Role(String name, int blood, char gender) {
        this.name = name;
        this.blood = blood;
        this.gender = gender;
        this.setFace();
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getBlood() {
        return blood;
    }

    public void setBlood(int blood) {
        this.blood = blood;
    }

    public char getGender() {
        return gender;
    }

    public void setGender(char gender) {
        this.gender = gender;
    }

    public String getFace() {
        return face;
    }

    public void setFace() {
        Random random = new Random();
        int index = random.nextInt(girlfaces.length);
        if(gender == '女'){
            this.face = girlfaces[index];
        }else if(gender == '男'){
            this.face = boyfaces[index];
        }else{
            this.face = "默认面孔";
        }

    }

    //attack 攻击描述：
    String[] attacks_desc={
            "%s使出了一招【背心钉】，转到对方的身后，一掌向%s背心的灵台穴拍去。",
            "%s使出了一招【游空探爪】，飞起身形自半空中变掌为抓锁向%s。",
            "%s大喝一声，身形下伏，一招【劈雷坠地】，捶向%s双腿。",
            "%s运气于掌，一瞬间掌心变得血红，一式【掌心雷】，推向%s。",
            "%s阴手翻起阳手跟进，一招【没遮拦】，结结实实的捶向%s。",
            "%s上步抢身，招中套招，一招【劈挂连环】，连环攻向%s。"
    };

    //injured 受伤描述：
    String[] injureds_desc={
            "结果%s退了半步，毫发无损",
            "结果给%s造成一处瘀伤",
            "结果一击命中，%s痛得弯下腰",
            "结果%s痛苦地闷哼了一声，显然受了点内伤",
            "结果%s摇摇晃晃，一跤摔倒在地",
            "结果%s脸色一下变得惨白，连退了好几步",
            "结果『轰』的一声，%s口中鲜血狂喷而出",
            "结果%s一声惨叫，像滩软泥般塌了下去"
    };

    public void attack(Role target) {
        Random random = new Random();
        //随机获得攻击
        int indexAttack = random.nextInt(attacks_desc.length);
        System.out.printf(attacks_desc[indexAttack], this.name, target.name);

        //随机获得攻击值
        int damage = random.nextInt(20) + 1;
        target.setBlood((target.getBlood() - damage) < 0 ? 0 : target.getBlood() - damage);

        //受伤描述和血量对应
        int indexIngured = 0;
        int targetBlood = target.getBlood();
        if (targetBlood > 90) {
            indexIngured = 0;
        } else if (targetBlood > 80) {
            indexIngured = 1;
        } else if (targetBlood > 70) {
            indexIngured = 2;
        } else if (targetBlood > 60) {
            indexIngured = 3;
        } else if (targetBlood > 40) {
            indexIngured = 4;
        } else if (targetBlood > 20) {
            indexIngured = 5;
        } else if (targetBlood > 10) {
            indexIngured = 6;
        } else {
            indexIngured = 7;
        }
        System.out.printf(injureds_desc[indexIngured], target.name);
        System.out.println();
    }

    public void showInfo() {
        System.out.printf("姓名：%s，血量：%d，性别：%s， appearance：%s\n",getName(),getBlood(),getGender(),getFace());
    }

}
```

```java
package com.itheima.test1_1;

public class RoleTest {
    static void main(String[] args) {
        Role role1 = new Role("乔峰", 100, '男');
        Role role2 = new Role("鸠摩智", 100, '男');

        role1.showInfo();
        role2.showInfo();

        while(true){
            role1.attack(role2);
            if(role2.getBlood()<=0){
                System.out.println(role1.getName()+"KO了"+role2.getName());
                break;
            }
            role2.attack(role1);
            if(role1.getBlood()<=0){
                System.out.println(role2.getName()+"KO了"+role1.getName());
                break;
            }
        }
    }
}
```

## 两个对象的数组

![题目要求](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260525151003839.png)

### 自行作答

ptg 插件真好用 👍

```java
package com.itheima.test2;

public class Goods {
    private String id;
    private String name;
    private double price;
    private int store;

    public Goods() {
    }

    public Goods(String id, String name, double price, int store) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.store = store;
    }

    /**
     * 获取
     *
     * @return id
     */
    public String getId() {
        return id;
    }

    /**
     * 设置
     *
     * @param id
     */
    public void setId(String id) {
        this.id = id;
    }

    /**
     * 获取
     *
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     *
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     *
     * @return price
     */
    public double getPrice() {
        return price;
    }

    /**
     * 设置
     *
     * @param price
     */
    public void setPrice(double price) {
        this.price = price;
    }

    /**
     * 获取
     *
     * @return store
     */
    public int getStore() {
        return store;
    }

    /**
     * 设置
     *
     * @param store
     */
    public void setStore(int store) {
        this.store = store;
    }


}
```

```java
package com.itheima.test2;

public class GoodsTest {
    static void main(String[] args) {
        Goods[] goods = new Goods[3];

        goods[0] = new Goods("001", "电脑", 5000, 10);
        goods[1] = new Goods("002", "鼠标", 10, 20);
        goods[2] = new Goods("003", "游艇", 500, 5);


        for (int i = 0; i < goods.length; i++){
            System.out.println(goods[i].getId() + " " + goods[i].getName() + " " + goods[i].getPrice() + " " + goods[i].getStore());
        }
    }
}
```



### 题目改进 1

![题目要求](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260525151519323.png)



```java
package com.itheima.test2_2;

public class Car {
    private String brand ;
    private double price;
    private String color;


    public Car() {
    }

    public Car(String brand, double price, String color) {
        this.brand = brand;
        this.price = price;
        this.color = color;
    }

    /**
     * 获取
     * @return brand
     */
    public String getBrand() {
        return brand;
    }

    /**
     * 设置
     * @param brand
     */
    public void setBrand(String brand) {
        this.brand = brand;
    }

    /**
     * 获取
     * @return price
     */
    public double getPrice() {
        return price;
    }

    /**
     * 设置
     * @param price
     */
    public void setPrice(double price) {
        this.price = price;
    }

    /**
     * 获取
     * @return color
     */
    public String getColor() {
        return color;
    }

    /**
     * 设置
     * @param color
     */
    public void setColor(String color) {
        this.color = color;
    }


}
```



```java
package com.itheima.test2_2;

import java.util.Scanner;
/*
丰田
200000
白色
本田
150000
黑色
特斯拉
350000
红色
 */

public class CarTest {
    static void main(String[] args) {
        Car[] cars = new Car[3];

        Scanner scanner = new Scanner(System.in);

        for(int i = 0; i < cars.length; i++) {
            System.out.println("请输入第" + (i + 1) + "辆车的牌：");
            String brand = scanner.next();
            System.out.println("请输入第" + (i + 1) + "辆车的价格：");
            double price = scanner.nextDouble();
            System.out.println("请输入第" + (i + 1) + "辆车的颜色：");
            String color = scanner.next();
            cars[i] = new Car(brand, price, color);
        }

        for(int i = 0; i < cars.length; i++) {
            System.out.println(cars[i].getBrand() + " " + cars[i].getPrice() + " " + cars[i].getColor());
        }
    }
}
```



#### 补充：关于输入方法 ✍

大致分为两种：对于换行符 `\n` 的处理

1. 读取之后不消费换行符的：`next()`、`nextInt()`、`nextDouble()`、`nextBoolean()`、`nextLong()`、`nextFloat()`、`nextByte()`、`nextShort()`）
2. 读取后消费换行符的：`nextLine()`

------

不建议两种输入方法混用

在 next()之后使用 `nextLine()`，如果 `next()` 读取到 `\n` 之后停止，`nextLine()` 就会直接读取这个 `\n`，导致 `nextLine()` 没有读到 `\n` 以外的任何信息

------

另外，关于输入还需要知道



1. 所有输入的内容都会进入一个缓存区，输入方法优先从这里读取内容

   > 也就是只要是键盘录入的东西都会被读到，当然除非读取的数据类型数量不匹配

   ![从缓存区中读取数据](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260525152654660.png)

2. Scanner 维护一个指针，用来标记缓存区内目前读取的位置

### 题目改进 2：判断与统计

![题目要求](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260525152918924.png)

~~~java
package com.itheima.test2_3;

public class Phone {
    private String brand;
    private double price;
    private String color;


    public Phone() {
    }

    public Phone(String brand, double price, String color) {
        this.brand = brand;
        this.price = price;
        this.color = color;
    }

    /**
     * 获取
     * @return brand
     */
    public String getBrand() {
        return brand;
    }

    /**
     * 设置
     * @param brand
     */
    public void setBrand(String brand) {
        this.brand = brand;
    }

    /**
     * 获取
     * @return price
     */
    public double getPrice() {
        return price;
    }

    /**
     * 设置
     * @param price
     */
    public void setPrice(double price) {
        this.price = price;
    }

    /**
     * 获取
     * @return color
     */
    public String getColor() {
        return color;
    }

    /**
     * 设置
     * @param color
     */
    public void setColor(String color) {
        this.color = color;
    }


}
~~~

~~~java
package com.itheima.test2_3;

public class PhoneTest {
    static void main(String [] args) {
        Phone [] phones = new Phone [3];
        phones [0] = new Phone("华为", 5000, "黑色");
        phones [1] = new Phone("小米", 3000, "蓝色");
        phones [2] = new Phone("苹果", 8000, "白色");

        double sum = 0;
        for (int i = 0; i < phones.length; i++) {
            sum += phones [i].getPrice();
        }
        double avg = sum / phones.length;
        System.out.println("平均价格：" + avg);
    }
}
~~~

### 题目改进 3：判断与统计

![题目要求](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260525153057233.png)

~~~java
package com.itheima.test2_4;

public class Person {
    private String name;
    private int age;
    private char gender;
    private String [] hobbies;


    public Person() {
    }

    public Person(String name, int age, char gender, String [] hobbies) {
        this.name = name;
        this.age = age;
        this.gender = gender;
        this.hobbies = hobbies;
    }

    /**
     * 获取
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     * @return age
     */
    public int getAge() {
        return age;
    }

    /**
     * 设置
     * @param age
     */
    public void setAge(int age) {
        this.age = age;
    }

    /**
     * 获取
     * @return gender
     */
    public char getGender() {
        return gender;
    }

    /**
     * 设置
     * @param gender
     */
    public void setGender(char gender) {
        this.gender = gender;
    }

    /**
     * 获取
     * @return hobbies
     */
    public void getHobbies() {
        for (int i = 0; i < hobbies.length; i++){
            System.out.print(hobbies [i] + " ");
        }
        System.out.println();
    }

    /**
     * 设置
     * @param hobbies
     */
    public void setHobbies(String [] hobbies) {
        this.hobbies = hobbies;
    }

//    public String toString() {
//        return "Person{name = " + name + ", age = " + age + ", gender = " + gender + ", hobbies = " + hobbies + "}";
//    }

    public void showInfo() {
        System.out.println("姓名：" + getName());
        System.out.println("年龄：" + getAge());
        System.out.println("性别：" + getGender());
        System.out.print("爱好：");
        getHobbies();

    }
}
~~~

~~~java
package com.itheima.test2_4;

public class PersonTest {
    static void main(String [] args) {
        Person [] persons = new Person [4];

        persons [0] = new Person("张三", 18, '男', new String []{"看电影", "听歌"});
        persons [1] = new Person("李四", 19, '女', new String []{"看电影", "听歌", "打篮球"});
        persons [2] = new Person("王五", 20, '男', new String []{"看电影", "听歌", "看电影", "看电影"});
        persons [3] = new Person("赵六", 21, '女', new String []{"看电影", "听歌", "编织"});

        int sumAge = 0;
        for (int i = 0; i < persons.length; i++) {
            sumAge += persons [i].getAge();
        }

        double avgAge = sumAge / persons.length;
        System.out.println("平均年龄：" + avgAge);

        for (int i = 0; i < persons.length; i++){
            if(persons [i].getAge() < avgAge){
                persons [i].showInfo();
            }
        }
    }
}
~~~

#### 补充 1：关于 `main()` 方法的 `public` `static` `void` 修饰符

> 笔者在写代码时，偶然发现 psvma 指令生成出来的 main()方法没有 public 了，故查阅资料

先说结论，

1. `main()` 方法也是一个方法
2. ==可以不写，但是写全比较好==

---

在 Java21 之前，`main()` 函数每个修饰符都是必须的：

- `public`：必须公开，以便 JVM 调用
- `static` ：必须静态，因为 JVM 没法创造包含 `main()` 方法的类的实例，所以必须是静态的，以便 JVM 直接调用
- `void`：无返回值

Java 21 引入了 未命名的类与实例 main 方法 预览特性（Java 23 正式落地，Java 25 已稳定）。新规则下：

- `public`：可以忽略，也就是可以是 `public` 也可以是默认的 `protected`，但是不能是 `private` 的
- `static` ：可以非静态，在非静态情况下，JVM 会先创建包含 `main()` 方法的类的实例对象，然后通过这个实例对象调用 `main()` 方法；如果是静态的，就按原来的方法运行
- `void`：无返回值，这个不变

#### 补充 2：关于 `main()` 方法的参数 `String[] args`

`main()` 方法理论上也是方法，所以也是可以传入参数的

由于 `main()` 方法是程序的入口，由 JVM 直接调用，参数也由 JVM 传入

------

参数 `String[] args`

- 参数名可以改为其他的

- 能传入多个 `String` 类型的参数

  > 举例实际应用，比如把配置文件的文件路径传入
  >
  > ~~~java
  > public class ConfigLoader {
  >     public static void main(String [] args) {
  >         String configPath = "application.properties"; // 默认路径
  >         if (args.length >= 1) {
  >             configPath = args [0];
  >         }
  >         System.out.println("加载配置: " + configPath);
  >         // 读取配置文件...
  >     }
  > }
  > ~~~
  >
  > ~~~bash
  > # 在命令行中传参
  > java ConfigLoader /etc/myapp/dev.properties
  > ~~~
  >
  > 程序里就可以用 `args[0]` 拿到这个路径，然后加载配置。这样，同一个程序可以在不同环境（开发、测试、生产）使用不同的配置文件，无需重新编译。

#### 补充 3：一个 Java 程序的运行

本质上，`main()` 方法的参数是由 JVM 启动时在命令行读取并传递的

也就是说，**所有 Java 程序运行本质上都是通过命令行的**

IDEA 等 IDE 集成环境给出了一个图形化操作界面，帮用户自动构建完整命令行命令

命令行本身是用户和操作系统交互的一个文本化界面

![一个 Java 程序的运行.drawio](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/%E4%B8%80%E4%B8%AAJava%E7%A8%8B%E5%BA%8F%E7%9A%84%E8%BF%90%E8%A1%8C.drawio.svg)

其实还有，可以给 JVM 在命令行设置参数、JVM 在运行中和 OS 交流，在此不过多拓展

#### 补充 4：关于 `main()` 方法必须在类中

Java21 之后，就不需要如此了，“类的声明可以省略”，直接写 `main()` 也能跑

~~~java
void main() {
    System.out.println("Hello");
}
~~~

不过本质上是引入了一个未命名类，实质上还是有类

这是为了降低初学者门槛而设计的

### 题目改进 4：添加和遍历

![题目要求](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260526143808360.png)

```java
package com.itheima.test2_5;

public class Student {
    private int id;
    private String name;
    private int age;


    public Student() {
    }

    public Student(int id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }

    /**
     * 获取
     * @return id
     */
    public int getId() {
        return id;
    }

    /**
     * 设置
     * @param id
     */
    public void setId(int id) {
        this.id = id;
    }

    /**
     * 获取
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     * @return age
     */
    public int getAge() {
        return age;
    }

    /**
     * 设置
     * @param age
     */
    public void setAge(int age) {
        this.age = age;
    }

    public void show() {
        System.out.println("id: "+getId()+" name: "+getName()+" age: "+getAge());
    }
}

```

```
package com.itheima.test2_5;

/**
 * 定义一个长度为3的数组，数组存储1~3名学生对象作为初始数据，学生对象的学号，姓名各不相同。
 *
 * 学生的属性：学号、姓名、年龄。
 *
 * 要求1：再次添加一个学生对象，并在添加的时候进行学号的唯一性判断。
 * 注意若数组大小不够，创建新的数组载入新的数据
 *
 * 要求2：添加完毕之后，遍历所有学生信息。
 *
 * 要求3：通过id删除学生信息
 *
 * 如果存在，则删除，如果不存在，则提示删除失败。
 *
 * 要求4：删除完毕之后，遍历所有学生信息。
 *
 * 要求5：查询数组id为“heima002”的学生，如果存在，则将他的年龄+1岁
 * 这个id目前做不了，胡换成别的随便什么id
 */

public class StudentTest {
    static void main(String[] args) {
        Student[] students = new Student[3];


        Student s1 = new Student(1001, "张三", 18);
        Student s2 = new Student(1002, "李四", 19);
        Student s3 = new Student(1003, "王五",19);
        Student s4 = new Student(1004, "赵六",20);

        students[0] = s1;
        students[1] = s2;

        System.out.println("----------------添加学生3----------------");
        students = insertStudent(students, s3);
        printArr(students);

        System.out.println("----------------添加学生4----------------");
        students = insertStudent(students, s4);
        printArr(students);

        System.out.println("----------------删除学生3----------------");
        students = deleteStudent(students, 1003);
        printArr(students);
        System.out.println("----------------删除不存在的学生----------------");
        students = deleteStudent(students, 1003);
        printArr(students);

        System.out.println("----------------查询学生----------------");
        students = queryStudentAndUpdateAgeBy1(students, 1004);
        printArr(students);

    }
    public static void printArr(Student[] students){
        for (Student s: students){
            if(s!=null){
                s.show();
            }
        }
    }

    public static Student[] insertStudent(Student[] students, Student s){
        //判断数组是否已满
        for (int i = 0; i < students.length; i++) {
            if(students[i]==null){
                //数组未满，直接添加
                students[i]=s;
                return students;
            }
        }
        //数组已满，创建新的数组载入新的数据
        Student[] newStudents = new Student[students.length+1];
        for (int i = 0; i < students.length; i++) {
            newStudents[i]=students[i];
        }
        newStudents[students.length]=s;
        return newStudents;
    }

    public static Student[] deleteStudent(Student[] students, int id){
        //＿φ(．．*)1.增强for循环是局部变量，不能直接修改数组元素的值
//        for (Student s: students) {
//            if(s.getId()==id){
//                s = null;
//                System.out.println("删除成功");
//                return students;
//            }
//        }
        for (int i = 0; i < students.length; i++) {

            //＿φ(．．*)2.注意这里的非空检查，避免空指针异常
            //＿φ(．．*)3.另外注意这里使用短路与，在空指针时直接短路，不再继续判断后续条件（id是否等于id）
            if(students[i] != null && students[i].getId()==id){
                students[i]=null;
                System.out.println("删除成功");
                return students;
            }
        }
        System.out.println("未找到该学生");
        return students;
    }

    public static Student[] queryStudentAndUpdateAgeBy1(Student[] students, int id){
        for (int i = 0; i < students.length; i++) {
            if(students[i]!=null && students[i].getId()==id){
                students[i].setAge(students[i].getAge()+1);
                System.out.println("年龄更新成功");
                return students;
            }
        }
        System.out.println("未找到该学生");
        return students;
    }
}

```

＿φ(．．*)

1. 增强 for 循环中，每个遍历对象是局部变量，不影响原数据
2. 时刻注意 ==空指针异常==，也就是时刻注意使用 **非空检查**
   1. 出现异常给整个程序卡住
   2. 很容易出现的异常
3. 非空检查的 if 语句可以和业务查询语句条件 **短路与**

#### 补充 1：如何批量修改变量属性

##### 修改访问控制修饰符

![如何修改访问控制修饰符](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260530120328339.png)

![image-20260530120617127](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260530120617127.png)

##### 如何修改变量名

![image-20260530120810752](C:\Users\Aylier\AppData\Roaming\Typora\typora-user-images\image-20260530120810752.png)

![image-20260530120917478](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260530120917478.png)

##### 如何修改变量类型

![image-20260530120944038](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260530120944038.png)

![image-20260530121029761](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260530121029761.png)

![image-20260530121140096](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260530121140096.png)

p.s.这一章没有作业

# Day10-字符串

## API 和 API 帮助文档

### API

- API(Application Programming Interface)：应用程序接口
- Java API：指 JDK 中提供的各种功能的 Java 类

前面使用的 `Scanner` `Random` 就是 API 的一种

### API 帮助文档

[Overview (Java SE 26 & JDK 26)](https://docs.oracle.com/en/java/javase/26/docs/api/index.html)

如何使用帮助文档

1. 找到对应的 API
2. 类的描述
3. 构造方法
4. 成员方法

## 字符串概述

![常见字符串操作](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260705203703338.png)

开发中的常见应用

- 用户密码：字符串比较
- 游戏脏话屏蔽：字符串查找和替换
- 银行 app 金额转为大写：字符串转换

![学习内容](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260705204013750.png)

## String

- java.lang.String，是 Java 的核心包，使用时不用导包

- 代表所有 Java 程序中的字符串文字

- 字符串的内容不可改变，其对象在创建后不能被更改

  - > 比如将两个字符串拼接起来，返回的结果不会覆盖到任意一个组成其的字符串，而是会创建一个新的字符串；当然，至于在这个拼接过程中，字符串和变量名之间的联系就另说了

  - ![字符串不可变](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260706003806030.png)



### 创建 String 对象的方式

#### 直接创建赋值

```
String name = "AylerLiu";
```

#### `new`（显示调用构造方法）

| 构造方法                         | 说明 |
| :------------------------------- | :--: |
| `public String()`                |      |
| `public String(String original)` |      |
|                                  |      |
|                                  |      |































































