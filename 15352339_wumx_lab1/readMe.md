---
typora-root-url: C:\Users\Yan\Desktop\`
---

# <center>  **中山大学移动信息工程学院本科生实验报告** </center>

### <center> **（2017年秋季学期）** </center>

课程名称：移动应用开发                            任课教师： Guifeng Zheng

| 年级    | 15级                     | 专业（方向） | 移动        |
| ----- | ----------------------- | ------ | --------- |
| 学号    | 15352339                | 姓名     | 吴沐晓       |
| Email | wumx8@mail2.sysu.edu.cn | QQ     | 406495530 |
| 开始日期  | 10/6                    | 完成日期   | 10/7      |



### 实验题目

基本UI界面设计

---



### 实现内容

1. 熟悉 Android Studio 开发工具操作

2. 熟悉 Android 基本 UI 开发,并进行 UI 基本设计

3. 实现一个 Android 应用，界面呈现如下效果： 

<div align="center"> <img src="../../Pictures/1.png"  alt="lab1实例" align=center style="zoom:50%" /> </div>

---



### 课堂实验结果

* 实验截图

<div align="center"> <img src="../../Pictures/2.png"  alt="lab1课堂实验" align=center style="zoom:50%" /> </div>

* 实验步骤以及关键代码

   1. 新建一个空白项目，系统会自动生成一个helloworld布局并在`AndroidManifest.xml`中声明从`MainActivity`启动。`MainActivity`中已经重载了`onCreate()`方法，将自动加载`activity_main.xml`布局
   2. 如果系统自动生成的布局是相关布局则先改为限制布局
   3. 将需要的widgets拖动到布局中，按照需要编写限制关系（部分代码见下一要点）
   4. 在`drawable`文件夹中新建一个`shape.xml`通过其中的`corners`属性为`Button`部件加上圆角

    ```
     <?xml version="1.0" encoding="UTF-8"?>
     <shape
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <!-- 填充的颜色 -->
    <solid android:color="#FF3f51b5" />
    <!-- 设置按钮的四个角为弧形 -->
    <!-- android:radius 弧形的半径 -->
    <corners android:radius="10dip" />

    <!-- padding：Button里面的文字与Button边界的间隔 -->
    <padding
        android:left="10dp"
        android:top="5dp"
        android:right="10dp"
        android:bottom="5dp"
        />
     </shape>
    ```

* 实验遇到的困难以及解决思路

  1. 限制布局的依赖问题
    ```java
    compile 'com.android.support.constraint:constraint-layout:1.0.0-alpha7'
    ```
    在`build.gradle`中添加这条语句后一直提示失败，解决方法是需要在`SDK Tools`中安装限制布局先。

  2. 居中问题
    仅仅通过编写窗口小部件之间的限制关系是无法完成按钮的居中的。解决方法也很简单，通过使用一个垂直居中的引导线即可

  3. `radioGroup`的内部组织
    一开始的时候没有意识到两个`radioButton`需要互斥。之后得知可以使用`radioGroup`可以实现互斥。但在其内部两个按钮却默认是垂直排列。其实可以认为其内部是一个线性结构，修改它的`orientation`属性即可。
  ```
  <RadioGroup
    android:orientation="horizontal"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:checkedButton="@+id/radioButton2"
    android:id="@+id/radioGroup"
    android:layout_marginEnd="16dp"
    app:layout_constraintRight_toRightOf="parent"
    android:layout_marginRight="16dp"
    android:layout_marginStart="16dp"
    app:layout_constraintLeft_toLeftOf="parent"
    android:layout_marginLeft="16dp"
    app:layout_constraintTop_toBottomOf="@+id/editText">
    <RadioButton
        android:text="学生"
        android:layout_width="wrap_content"
        android:layout_weight="1"
        android:layout_height="wrap_content"
        android:id="@+id/radioButton2"
        android:layout_marginTop="20dp"
        android:layout_marginStart="5dp"
        android:layout_marginLeft="5dp"
        android:checked="true" />
    <RadioButton
        android:text="教职工"
        android:layout_width="wrap_content"
        android:layout_weight="1"
        android:layout_height="wrap_content"
        android:id="@+id/radioButton3"
        android:layout_marginTop="20dp"
        android:layout_marginStart="5dp"
        android:layout_marginLeft="5dp" />
  </RadioGroup>
  ```

---



### 课后实验结果

* 在课后我实现了rippleEffect

<div align="center"> <img src="../../Pictures/ripple.png"  alt="lab1_addRipple" align=center style="zoom:50%" /> </div>

  其实内容非常简单，安卓在5.0的版本时就已经支持rippleEffect。只需要新建一个xml将background属性改为它。其中的代码为
```
<?xml version="1.0" encoding="utf-8"?>
<ripple xmlns:android="http://schemas.android.com/apk/res/android"
android:color="#ff7fc8">
<item android:drawable="@drawable/shape" />
</ripple>
```

  但是这样5.0一下的安卓机就无法使用，如何解决这个问题我还没有解决。

---



### 实验思考以及感想

* 首先非常感谢郭霖的博客

  > [Android新特性介绍，ConstraintLayout完全解析](http://blog.csdn.net/guolin_blog/article/details/53122387)                       

  通过这篇文章我快速的进行了constraintLayout的入门。再加上pdf上给出的更多的信息我对其有了一个良好的认知。

* 对官方文档的查阅非常重要。一开始在使用radioButton的时候没有使用RadioGroup。于是我在官网上查阅了radio关键字于是找到了RadioGroup。但有一点疑问的是，查阅到的一般是使用在代码中的函数。在布局中的属性的使用方法没有查阅到。

