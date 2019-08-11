# 重载

以下的内容主要讲解***重载***的相关内容：

- 定义：

  重载是在一个类里面，方法名相同，参数不同。***返回类型可以相同也可以不同***。每个重载的方法(或者构造方法) 都必须有一个独一无二的参数类型列表。

- 常用构造方法的地方是***构造器***的重载。

- 重载规则：

  1. 被重载的方法必须改变参数列表(参数个数或类型不一样)
  2. 被重载的方法可以改变返回类型
  3. 被重载的方法可以改变访问修饰符
  4. 被重载的方法可以声明新的或更广的异常检查
  5. 方法能够在同一个类中或者在一个子类中被加载
  6. 无法以返回值类型作为重载函数的区分标准

  ```java
  public class Overloading {
      public int test(){
          System.out.println("test1");
          return 1;
      }
   
      public void test(int a){
          System.out.println("test2");
      }   
   
      //以下两个参数类型顺序不同
      public String test(int a,String s){
          System.out.println("test3");
          return "returntest3";
      }   
   
      public String test(String s,int a){
          System.out.println("test4");
          return "returntest4";
      }  
      
      public static void main(String[] args){
          Overloading o = new Overloading();
          System.out.println(o.test());
          o.test(1);
          System.out.println(o.test(1,"test3"));
          System.out.println(o.test("test4",1));
      }
  }
  ```

  

  上面是对重载的介绍，提到重载就一定会提到***重写***了：

  

  区分点 | 重载方法| 重写方法

  ---| :--: | ---:

  参数列表|必须修改|一定不能修改

  返回类型|可以修改|一定不能修改

  异常|可以修改|可以减少或删除，一定不能抛出新的或者更广的异常

  访问|可以修改|一定不能做更严格的限制(可以降级限制)

  

  

  

  