[toc]

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

