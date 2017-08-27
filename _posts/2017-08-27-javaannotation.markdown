---
layout:     post
title:      "关于Java中的注解"
date:       2017-08-27 15:37:00
author:     "CreeperSan"
header-img: "img/post/170507about/header.jpg"
tags:
    - Java
---
> 注解（也被称为元数据）为我们在代码中添加信息提供了一种方法，是我们可以在稍后某个时刻非常方便的使用这些数据
> 个人理解就是注解用来标记某个地方，然后在使用过程中，然后我们可以让注解部分自动按照注解处理器的定义来处理这些注解的对象、方法、等等。

### 简单例子
+ 注解的使用
```JAVA
public class Testable{
	public void excute(){
    	System.out.println("Test");
    }

	@Test
    void testExcute(){
    	excute()
    }
}
```
+ 注解的定义
```JAVA
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Test()
```
### JAVA中的元注解
1. @Target 【表示该注解可以用于什么地方。可能的ElementType参数包括】
	+ CONSTRUCTOR : 构造函数的声明
	+ FIELD : 域声明（包括emun实例）
	+ LOCAL_VARIABLE : 局部变量声明
	+ MEHOD : 方法声明
	+ PARAMETER : 参数声明
	+ TYPE : 类、接口（包括注解类型）或emun声明
2. @Retention【表示需要在什么级别保存该注解信息，可选的RetentionPolicy参数包括】
	+ SOURCE : 仅保留在源代码，注解将被编译器丢弃
	+ CLASS : 注解在Class文件中可用，但会被VM丢弃
	+ RUNTIME : VM将在运行期间也保留注解，因此可以通过反射机制读取注解的信息
3. @Documented 【将注解包含在JavaDoc中】
4. @Inherited【允许子类继承父类中的注解】

### 简单例子实现类似ButterKnife的效果
##### 步骤① 编写注解
```JAVA
//InjectView.class
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface InjectView{
	int value()
}
```
##### 步骤② 编写注解处理器
```JAVA
//InjectDecoder
public class InjectDecoder{

	public static void inject(Object object){
    	final Class<?> clazz = object.getClass();
        View view = null;
        Field[] fields = clazz.getDeclaredFields();
        for (Field field:fields){
            if (field.isAnnotationPresent(InjectView.class)){
                InjectView injectView = field.getAnnotation(InjectView.class);
                field.setAccessible(true);
                if (object instanceof Activity){
                    view = ((Activity)object).findViewById(injectView.value());
                }else if (object instanceof View){
                    view = ((View)object).findViewById(injectView.value());
                }else {
                    throw new UnsupportedOperationException("仅能Inject Activity或者View");
                }
                try {
                    field.set(object,view);
                } catch (IllegalAccessException e) {
                    e.printStackTrace();
                    throw new UnsupportedOperationException("反射写入变量失败");
                }
            }
        }
    }

}
```
##### 步骤③ 使用
```JAVA
public class FullscreenActivity extends AppCompatActivity {

    @InjectView(R.id.mainTextView)
    private TextView textView;
    @InjectView(R.id.mainTextViewTop)
    private TextView textViewTop;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_fullscreen);
        InjectDecoder.inject(this);
        textView.setText("我被设置了");
        textViewTop.setText("头部的我被设置了");
    }
}
```


