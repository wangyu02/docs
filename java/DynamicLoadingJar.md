# 动态加载jar包

动态加载jar包是平台化过程中经常用到的，主要分成下面几步来完成

1. 定义一个抽象类AbstractAction

   ````java
   package com.java.loader
   
   public abstract class AbstractAction {
   	public abstract String action();
   }
   ````

   

2. 写个实体类继承TestAction

   ````java
   package com.java.jarLoader
   
   import com.java.loader.AbstractAction
   
   public class TestAction extends AbstractAction {
   	public String action() {
   		System.out.println("I am working");
   		return "this ActionTest class";
   	}
   }
   ````

   

3. 将TestAction所在的包导出成jar包的方式，放到制定的目录既可

   ````java
   D:\jarload\test.jar
   ````

   

4. 加载jar包

   ````java
   package com.java.main
   
   
   import java.io.BufferedReader;
   import java.io.File;
   import java.io.FileReader;
   import java.net.URL;
   import java.net.URLClassLoader;
    
   import com.java.loader.AbstractAction;
   import com.java.loader.AbstractAction;
   
   public class TestMain {
       public static void main(String[] args) {
           try {
               // 方法1
               File file = new File("D:\\jarload\\test.txt");
               BufferedReader in = new BufferedReader(new FileReader(file));
               String s = new String();
               URLClassLoader myClassLoader = new URLClassLoader(new URL[]{url}, Thread.currentThread().getContexntClassLoader());
               Class<? extends AbstractAction> myClass = (Class<? extends AbstractAction>) myClassLoader.loadClass("com.java.jarloader.TestAction");
               AbstractAction action1  = (AbstractAction) myClass.newInstance();
               String str = action.action();
               System.out.println(str1);
               
               // 方法2
               URL url1 = new URL("file:D:/jarload/test.jar");
               URLClassLoader myClassLoader = new URLClassLoader(new URL[] { url1 }, Thread.currentThread().getContextClassLoader());
               Class<?> myClass1 = (AbstractAction)myClass1.getnewInstance();
               String str1 = action1.action();
               System.out.print(str1);
           } catch (Exception ex) {
               ex.printStakeTrace();
           }
       }
   }
   ````



如果遇到接口的情况，我们将使用接口的方式完成上面的功能：

1. 将抽象类改成接口的形式InterfaceAction

   ````java
   package com.java.loader
   
   public interface InterfaceAction {
   	public String action();
   }
   ````

2. 实现接口TestAction

   ````java
   package com.java.jarloader
   
   import com.java.loader.InterfaceAction
   
   /**
   * 该部分还是使用两种方式来实现
   **/
   public class TestAction implements InterfaceAction {
   	@Override
   	public String action() {
   		System.out.println("I am working");
   		return "this.ActionTest class";
   	}
   }
   ````

3. 第三步保持不变，上面的内容形成了jar包

4. TestMain相关的内容稍作修改

   ````java
   package com.java.main
   
   public static void main(String[] args) {
   	try {
   		// 配置成文件格式
   		File file = new File("D:\\jarload\\test.txt");
   		BufferedReader in = new BufferedReader(new FileReader(file));
   		String s = new String();
   		while((s = in.readLine()) != null) {
   			URL url = new URL(s);
   			s = null;
   			URLClassLoader myClassLoader = new URLClassLoader(new URL[] { url }, Thread.currentThread().getContextClassLoader());
   			Class<?> myClass = (Class<?>) myClassLoader.loadClass("com.java.jarloader.TestAction");
   			InterfaceAct action = (InterfaceAction) myClass.newInstance();
   			String str = action.action();
   			System.out.print(str);
   			
   			// 第二种
   			URL url1 = new URL("file:D:/jarload/test.jar");
   				URLClassLoader myClassLoader1 = new URLClassLoader(new URL[] { url1 }, Thread.currentThread()
   						.getContextClassLoader());
   				Class<?> myClass1 = myClassLoader1.loadClass("com.java.jarloader.TestAction");
   				InterfaceAction action1 = (InterfaceAction) myClass1.newInstance();
   				String str1 = action1.action();
   				System.out.println(str1);
   		}
   	} catch(Exception ex) {
   		ex.printStackTrace();
   	}
   }
   ````

5. 最后结果运行