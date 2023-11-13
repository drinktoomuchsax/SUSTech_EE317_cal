### 美化界面如下：

 - 修改符号使其符合用户直觉，如“ = ”、“ CLC”
 - 更改配色
 - 更改排版布局，使其放松不拥挤

![enter image description here](https://img1.imgtp.com/2023/10/09/SzfkS6q5.png)

---
### BUG解决

常规计算器点按加减乘除会互相切换，但这份代码没有实现这个功能，当按下某一个算法符号后，不能切换其他的算法符号。

例如我想要计算“1 + 1”的结果，但是误触到“ - ”后，不能直接点按“ + ”更改算法符号，需要全部清除后重新输入。

通过在加减乘除的监听事件中修改如下代码实现直接切换的功能，以加法为例：

```java
case R.id.jian: {
	                    if (ss.length() == 0) {
	                        edit.setText("0 - ");
	                        ss = "0 - ";
	                        break;
	                    }
	                    if (ss.contains("+")||ss.contains("-")||ss.contains("x")||ss.contains("/")) {
	                        ss = ss.substring(0,ss.length()-3);
	                        ss += " - ";
	                        edit.setText(ss);
	                        break;
	                    }
```
具体演示见视频。


----
### 源码
> **below is "MainActivity.java"**

```java
	package com.example.myapplication;

	import androidx.appcompat.app.AppCompatActivity;

	import android.os.Bundle;
	import android.view.View;
	import android.widget.Button;
	import android.widget.EditText;
	import android.widget.Toast;

	public class MainActivity extends AppCompatActivity {

	    Button btn1, btn2, btn3, btn4, btn5, btn6, btn7, btn8, btn9, btn0; // 数字按钮
	    Button jia, jian, cheng, chu, dian, sum, clear,back;// +号
	    EditText edit; // 显示文本


	    private String ss = "";//设置一个String类型的变量
	    private String ss1 = "1 + ";

	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.activity_main);
	        // 获取页面上的控件
	        btn1 = findViewById(R.id.btn1);
	        btn2 = findViewById(R.id.btn2);
	        btn3 = findViewById(R.id.btn3);
	        btn4 = findViewById(R.id.btn4);
	        btn5 = findViewById(R.id.btn5);
	        btn6 = findViewById(R.id.btn6);
	        btn7 = findViewById(R.id.btn7);
	        btn8 = findViewById(R.id.btn8);
	        btn9 = findViewById(R.id.btn9);
	        btn0 = findViewById(R.id.btn0);
	        jia = findViewById(R.id.jia);
	        jian = findViewById(R.id.jian);
	        cheng = findViewById(R.id.cheng);
	        chu = findViewById(R.id.chu);
	        sum = findViewById(R.id.calculation);
	        dian = findViewById(R.id.dian);
	        clear = findViewById(R.id.clear);
	        edit = findViewById(R.id.edit);
	        back = findViewById(R.id.back);


	        // 按钮的单击事件
	        btn1.setOnClickListener(new Click());
	        btn2.setOnClickListener(new Click());
	        btn3.setOnClickListener(new Click());
	        btn4.setOnClickListener(new Click());
	        btn5.setOnClickListener(new Click());
	        btn6.setOnClickListener(new Click());
	        btn7.setOnClickListener(new Click());
	        btn8.setOnClickListener(new Click());
	        btn9.setOnClickListener(new Click());
	        btn0.setOnClickListener(new Click());
	        jia.setOnClickListener(new Click());
	        jian.setOnClickListener(new Click());
	        cheng.setOnClickListener(new Click());
	        chu.setOnClickListener(new Click());
	        sum.setOnClickListener(new Click());
	        dian.setOnClickListener(new Click());
	        clear.setOnClickListener(new Click());
	        edit.setOnClickListener(new Click());
	        back.setOnClickListener(new Click());
	    }

	    // 设置按钮点击后的监听
	    class Click implements View.OnClickListener {
	        public void onClick(View v) {
	            switch (v.getId()) {                //switch循环获取点击按钮后的值
	                case R.id.clear: {
	                    ss = "";
	                    edit.setText(ss);//在edittext里面显示字符串ss
	                }
	                break;

	                case R.id.btn0: {
	                    ss += "0";
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.btn1: {
	                    ss += "1"; // ss=ss+1
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.btn2: {
	                    ss += "2";
	                    edit.setText(ss);
	                }
	                break;

	                case R.id.btn3: {
	                    ss += "3";
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.btn4: {
	                    ss += "4";
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.btn5: {
	                    ss += "5";
	                    edit.setText(ss);
	                }
	                break;

	                case R.id.btn6: {
	                    ss += "6";
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.btn7: {
	                    ss += "7";
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.btn8: {
	                    ss += "8";
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.btn9: {
	                    ss += "9";
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.dian: {
	                    if (ss.length() == 0) {
	                        break;
	                    } else {
	                        ss += ".";
	                        edit.setText(ss);
	                    }
	                }
	                break;
	                case R.id.jia: {
	                    if (ss.length() == 0) {
	                        edit.setText("0 + ");
	                        ss = "0 + ";
	                        break;
	                    }
	                    if (ss.contains("+")||ss.contains("-")||ss.contains("x")||ss.contains("/")) {
	                        ss = ss.substring(0,ss.length()-3);
	                        ss += " + ";
	                        edit.setText(ss);
	                        break;
	                    }

	                    ss += " + ";
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.jian: {
	                    if (ss.length() == 0) {
	                        edit.setText("0 - ");
	                        ss = "0 - ";
	                        break;
	                    }
	                    if (ss.contains("+")||ss.contains("-")||ss.contains("x")||ss.contains("/")) {
	                        ss = ss.substring(0,ss.length()-3);
	                        ss += " - ";
	                        edit.setText(ss);
	                        break;
	                    }

	                    ss += " - ";
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.cheng: {
	                    if (ss.length() == 0) {
	                        edit.setText("0 × ");
	                        ss = "0 × ";
	                        break;
	                    }
	                    if (ss.contains("+")||ss.contains("-")||ss.contains("x")||ss.contains("/")) {
	                        ss = ss.substring(0,ss.length()-3);
	                        ss += " x ";
	                        edit.setText(ss);
	                        break;
	                    }

	                    ss += " × ";
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.chu: {
	                    if (ss.length() == 0) {
	                        edit.setText("0 / ");
	                        ss = "0 / ";
	                        break;
	                    }
	                    if (ss.contains("+")||ss.contains("-")||ss.contains("x")||ss.contains("/")) {
	                        ss = ss.substring(0,ss.length()-3);
	                        ss += " / ";
	                        edit.setText(ss);
	                        break;
	                    }

	                    ss += " / ";
	                    edit.setText(ss);
	                }
	                break;
	                case R.id.calculation:

	                    getResult();

	                    break;
	                case R.id.back: {
	                    if (ss.contains(" ")){
	                        if (ss.indexOf(" ") == ss.length() - 3) {
	                            ss = ss.substring(0, ss.length() - 3);
	                            edit.setText(ss);
	                            break;
	                        }
	                    }

	                    ss = ss.substring(0, ss.length() - 1);
	                    edit.setText(ss);
	                    break;
	                }
	            }
	        }
	    }

	    private void getResult() {
	        double result = 0;
	        if (ss == null || ss.equals("")) return;
	        if (!ss.contains(" ")) return;
	        String s1 = ss.substring(0, ss.indexOf(" "));
	        String op = ss.substring(ss.indexOf(" ") + 1, ss.indexOf(" ") + 2);
	        String s2 = ss.substring(ss.indexOf(" ") + 3);
	        if (!s1.equals("") && !s2.equals("")) {
	//            float d1 = Float.parseFloat(s1);
	//            float d2 = Float.parseFloat(s2);
	            double d1 = Double.parseDouble(s1);
	            double d2 = Double.parseDouble(s2);
	            switch (op) {
	                case "+":
	                    result = d1 + d2;
	                    break;
	                case "-":
	                    result = d1 - d2;
	                    break;
	                case "×":
	                    result = d1 * d2;
	                    break;
	                case "/": {
	                    if (d2 == 0) {
	                        Toast.makeText(MainActivity.this, "不能除以零", Toast.LENGTH_SHORT).show();
	                        break;

	                    }
	                    result = d1 / d2 * 1.0;
	                }
	                break;
	            }
	//            edit.setText(result + "");
	//            ss = "" + result;
	            int r = (int) result;
	            if (r == result) {
	                edit.setText("" + r);
	                ss = "" + r;
	            } else {
	                ss = "" + result; //将double类型的result转成string类型的数据存储在ss中
	                ss = ss.substring(0,ss.length()-1);
	//                edit.setText(result+ "");
	                edit.setText(ss);

	            }
	        }


	    }

	}
```



> **below is "activity_main.xml"**
```xml
	<?xml version="1.0" encoding="utf-8"?>  
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"  
	  xmlns:app="http://schemas.android.com/apk/res-auto"  
	  xmlns:tools="http://schemas.android.com/tools"  
	  android:layout_width="match_parent"  
	  android:layout_height="match_parent"  
	  android:orientation="vertical"  
	  android:padding="30dp"  
	  android:background="#efefef">  
	  
	    <TextView  
	  android:layout_width="match_parent"  
	  android:layout_height="wrap_content"  
	  android:text="计算器"  
	  android:textSize="40sp"  
	  android:textColor="#999999"  
	  android:layout_marginBottom="30dp"  
	  android:gravity="center"/>  
	    <EditText  
	  android:id="@+id/edit"  
	  android:textSize="40dp"  
	  android:layout_width="match_parent"  
	  android:layout_height="100dp"  
	  android:gravity="end|bottom"  
	  />  
	  
	    <LinearLayout  
	  android:layout_width="match_parent"  
	  android:layout_height="wrap_content"  
	  android:orientation="horizontal">  
	        <Button  
	  android:id="@+id/clear"  
	  android:layout_width="0dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="5dp"  
	  android:layout_weight="1"  
	  android:text="clc"  
	  android:textSize="25dp"/>  
	  
	        <Button  
	  android:id="@+id/calculation"  
	  android:layout_width="0dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="5dp"  
	  android:layout_weight="1"  
	  android:text="="  
	  android:textSize="25dp" />  
	    </LinearLayout>  
	  
	    <GridLayout  
	  android:layout_width="match_parent"  
	  android:layout_height="wrap_content"  
	  android:rowCount="4"  
	  android:columnCount="4"  
	  >  
	  
	  
	        <Button  
	  android:id="@+id/btn1"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="1"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/btn2"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="2"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/btn3"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="3"  
	  android:textSize="25sp"/>  
	  
	        <Button  
	  android:id="@+id/jia"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_row="0"  
	  android:layout_margin="6dp"  
	  android:text="+"  
	  android:textSize="25sp" />  
	  
	        <Button  
	  android:id="@+id/btn4"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="4"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/btn5"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="5"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/btn6"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="6"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/jian"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="-"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/btn7"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="7"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/btn8"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="8"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/btn9"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="9"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/cheng"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="x"  
	  android:textAllCaps="false"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/btn0"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="0"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/dian"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="."  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/back"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="⬅"  
	  android:textSize="25sp"/>  
	        <Button  
	  android:id="@+id/chu"  
	  android:layout_width="70dp"  
	  android:layout_height="wrap_content"  
	  android:layout_margin="6dp"  
	  android:text="÷"  
	  android:textSize="25sp"/>  
	    </GridLayout>  
	</LinearLayout>
```

> **below is "theme.xml"**
```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Theme.MyApplication" parent="Theme.MaterialComponents.DayNight.DarkActionBar">
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/grey</item>
        <item name="colorPrimaryVariant">@color/darkGrey</item>
        <item name="colorOnPrimary">@color/white</item>
        <!-- Secondary brand color. -->
        <item name="colorSecondary">@color/teal_200</item>
        <item name="colorSecondaryVariant">@color/teal_700</item>
        <item name="colorOnSecondary">@color/black</item>
        <!-- Status bar color. -->
        <item name="android:statusBarColor" tools:targetApi="l">?attr/colorPrimaryVariant</item>
        <!-- Customize your theme here. -->
    </style>
</resources>
```

> **below is "color.xml"**
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="purple_200">#FFBB86FC</color>
    <color name="purple_500">#FF6200EE</color>
    <color name="purple_700">#FF3700B3</color>
    <color name="teal_200">#9cc679</color>
    <color name="teal_700">#79a852</color>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="grey">#a3a3a3</color>
    <color name="darkGrey">#5e5e5e</color>

</resources>
```
