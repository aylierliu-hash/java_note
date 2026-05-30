[toc]

![学习路线参考](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260527131324086.png)

![课程目录](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260527131427455.png)

![课程时长](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260527131500065.png)



# Day01-Java入门

## Java学习介绍

1. OOP
2. Java核心知识点
   1. API
   2. 集合
   3. BIO
   4. NIO
   5. 多线程
   6. 网络编程
3. 斯坦福大学真题练习
4. 阿里巴巴的编码规范
5. 手写Tomcat服务器，虚拟机，算法，数据结构
6. 老师多年经验心得

## 人机交互

### 人机交互小故事

只有命令行

MS-DOS

XEROX-->图形化界面

但是图形化界面

- 消耗内存
- 运行速度慢

### 打开CMD

`win+r`

`cmd`

### 常用CMD命令

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

对象调用方法，在该方法内需要使用该对象调用别的方法，可以直接使用this关键字，**不用再将对象作为参数传入**

> - 具体体现为方法`public void attack(Role1 target)`仅有一个参数
> - 另外注意，血量不能低于100，`remainBlood = remainBlood < 0 ?0 : remainBlood;`

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

ptg插件真好用👍

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



### 题目改进1

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



#### 补充：关于输入方法✍

大致分为两种：对于换行符`\n`的处理

1. 读取之后不消费换行符的：`next()`、`nextInt()`、`nextDouble()`、`nextBoolean()`、`nextLong()`、`nextFloat()`、`nextByte()`、`nextShort()`）
2. 读取后消费换行符的：`nextLine()`

------

不建议两种输入方法混用

在next()之后使用`nextLine()`，如果`next()`读取到`\n`之后停止，`nextLine()`就会直接读取这个`\n`，导致`nextLine()`没有读到`\n`以外的任何信息

------

另外，关于输入还需要知道



1. 所有输入的内容都会进入一个缓存区，输入方法优先从这里读取内容

   > 也就是只要是键盘录入的东西都会被读到，当然除非读取的数据类型数量不匹配

   ![从缓存区中读取数据](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260525152654660.png)

2. Scanner维护一个指针，用来标记缓存区内目前读取的位置

### 题目改进2：判断与统计

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
    static void main(String[] args) {
        Phone[] phones = new Phone[3];
        phones[0] = new Phone("华为", 5000, "黑色");
        phones[1] = new Phone("小米", 3000, "蓝色");
        phones[2] = new Phone("苹果", 8000, "白色");

        double sum = 0;
        for (int i = 0; i < phones.length; i++) {
            sum += phones[i].getPrice();
        }
        double avg = sum / phones.length;
        System.out.println("平均价格：" + avg);
    }
}
~~~

### 题目改进3：判断与统计

![题目要求](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260525153057233.png)

~~~java
package com.itheima.test2_4;

public class Person {
    private String name;
    private int age;
    private char gender;
    private String[] hobbies;


    public Person() {
    }

    public Person(String name, int age, char gender, String[] hobbies) {
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
        for (int i=0;i<hobbies.length;i++){
            System.out.print(hobbies[i] + " ");
        }
        System.out.println();
    }

    /**
     * 设置
     * @param hobbies
     */
    public void setHobbies(String[] hobbies) {
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
    static void main(String[] args) {
        Person[] persons = new Person[4];

        persons[0] = new Person("张三", 18, '男', new String[]{"看电影", "听歌"});
        persons[1] = new Person("李四", 19, '女', new String[]{"看电影", "听歌", "打篮球"});
        persons[2] = new Person("王五", 20, '男', new String[]{"看电影", "听歌", "看电影", "看电影"});
        persons[3] = new Person("赵六", 21, '女', new String[]{"看电影", "听歌", "编织"});

        int sumAge = 0;
        for (int i = 0; i < persons.length; i++) {
            sumAge += persons[i].getAge();
        }

        double avgAge = sumAge / persons.length;
        System.out.println("平均年龄：" + avgAge);

        for (int i = 0; i < persons.length; i++){
            if(persons[i].getAge() < avgAge){
                persons[i].showInfo();
            }
        }
    }
}
~~~

#### 补充1：关于`main()`方法的`public` `static` `void`修饰符

> 笔者在写代码时，偶然发现psvma指令生成出来的main()方法没有public了，故查阅资料

先说结论，

1. `main()`方法也是一个方法
2. ==可以不写，但是写全比较好==

---

在Java21之前，`main()`函数每个修饰符都是必须的：

- `public`：必须公开，以便JVM调用
- `static` ：必须静态，因为JVM没法创造包含`main()`方法的类的实例，所以必须是静态的，以便JVM直接调用
- `void`：无返回值

Java 21 引入了 未命名的类与实例 main 方法 预览特性（Java 23 正式落地，Java 25 已稳定）。新规则下：

- `public`：可以忽略，也就是可以是`public`也可以是默认的`protected`，但是不能是`private`的
- `static` ：可以非静态，在非静态情况下，JVM会先创建包含`main()`方法的类的实例对象，然后通过这个实例对象调用`main()`方法；如果是静态的，就按原来的方法运行
- `void`：无返回值，这个不变

#### 补充2：关于`main()`方法的参数`String[] args`

`main()`方法理论上也是方法，所以也是可以传入参数的

由于`main()`方法是程序的入口，由JVM直接调用，参数也由JVM传入

------

参数`String[] args`

- 参数名可以改为其他的

- 能传入多个`String`类型的参数

  > 举例实际应用，比如把配置文件的文件路径传入
  >
  > ~~~java
  > public class ConfigLoader {
  >     public static void main(String[] args) {
  >         String configPath = "application.properties"; // 默认路径
  >         if (args.length >= 1) {
  >             configPath = args[0];
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

#### 补充3：一个Java程序的运行

本质上，`main()`方法的参数是由JVM启动时在命令行读取并传递的

也就是说，**所有Java程序运行本质上都是通过命令行的**

IDEA等IDE集成环境给出了一个图形化操作界面，帮用户自动构建完整命令行命令

命令行本身是用户和操作系统交互的一个文本化界面

![一个Java程序的运行.drawio](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/%E4%B8%80%E4%B8%AAJava%E7%A8%8B%E5%BA%8F%E7%9A%84%E8%BF%90%E8%A1%8C.drawio.svg)

其实还有，可以给JVM在命令行设置参数、JVM在运行中和OS交流，在此不过多拓展

#### 补充4：关于`main()`方法必须在类中

Java21之后，就不需要如此了，“类的声明可以省略”，直接写`main()`也能跑

~~~java
void main() {
    System.out.println("Hello");
}
~~~

不过本质上是引入了一个未命名类，实质上还是有类

这是为了降低初学者门槛而设计的

### 题目改进4：添加和遍历

![题目要求](https://cdn.jsdelivr.net/gh/aylierliu-hash/image_hosting/images/image-20260526143808360.png)



# Day10-字符串

## 二级标题

