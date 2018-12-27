# 安卓入门

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181218134041.png)





![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181217135647.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181217135828.png)

warp_content 包裹实际文本内容

match _parent 当前控件铺满父类容器

fill_parent 当前控件铺满父类容器

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181217150153.png)

drawable 下面四个文件夹指的是不同的分辨率机器，里面的文件名必须是一样的，不一样的就是其分辨率





![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181217215441.png)

## 监听事件

```java
/通过接口实现监听事件
public class helloworld extends AppCompatActivity implements View.OnClickListener {
    @Override
    public void onClick(View v) {
        Log.i("TAG", "第三种方式");
    }

    private Button loginButton;
    private Button button2;
    private Button button3;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_helloworld);
        /*button的监听事件
         */
        /*1、如何初始化一个button，先找到button的id
         * findViewById----返回的是一个view对象
         * findViewById通过gen目录下的R文件知道对应的id
         * */
        loginButton = findViewById(R.id.button1);
        /*2、通过设置监听器来实现我们需要的功能
         * ①匿名内部类监听事件*/
        loginButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //在当前方法中监听点击事件
                System.out.println("我是gavin的儿子");
            }
        });

        button2 = findViewById(R.id.button2);
        /*设置外部类
         * 就是在外部设置类
         * 然后在这边set的时候，可以不用重载接口函数*/
       MyOnClickListener onclicktwo=new MyOnClickListener(){
           @Override
           public void onClick(View v) {

               super.onClick(v);
               System.out.println("通过外部类方式监听");
           }
       };
        button2.setOnClickListener(onclicktwo);
        /*第三种方法，设置接口*/
        button3=findViewById(R.id.button3);
        button3.setOnClickListener(this);

    }
}

class MyOnClickListener implements View.OnClickListener {
    @Override
    public void onClick(View v) {
        System.out.println("我是gavin的孙子");
        Log.d("TAG", "onClick: ");
        /*改变其透明度*/
        //v.setAlpha(0.5f);
        /*setTextColor(0xFF0000FF);//0xFF0000FF是int类型的数据，
        分组一下0x|FF|0000FF，0x是代表颜色整数的标记，ff是表示透明度，
        0000FF表示颜色，注意：
        这里0xFF0000FF必须是8个的颜色表示，不接受0000FF这种6个的颜色表示。*/

        /*setBackgroundColor用法

     setBackgroundColor(Color.parseColor("#F5F5DC"));

      s etBackgroundColor(Color.argb(0,79,79,79));  //0完全透明  255不透明*/
        v.setBackgroundColor(Color.argb(150, 0, 0, 79));

    }
}
```

## 跑马灯效果

```java
public class textpaomadeng  extends android.support.v7.widget.AppCompatTextView {

/*重写TextView*/
    public textpaomadeng(Context context) {
        super(context);
    }

    public textpaomadeng(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    public textpaomadeng(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    @Override
    public boolean isFocused() {
        return true;/*这边是重点   使其强制聚焦*/

    }
}

```

```xml
<com.gavin.www.helloworld.textpaomadeng  //包名问题
        android:id="@+id/textView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:ellipsize="marquee"            //必须要加
        android:focusable="true"                //必须要加
        android:focusableInTouchMode="true"          //必须要加
        android:singleLine="true"               //必须要加，单行效果，若去掉，则自动换行
        android:text="@string/textView2" />
```

## 实现动态匹配（单选）

```java
/*     1、自动匹配AutoCompleteTextView
  2、需要一个适配器
  3、需要一个匹配数组，初始化数据源
  4、将适配器与控件绑定
  5、在控件内设置completionThreshold属性，设置输入几个字符后开始自动匹配
*/
     private  String[] res={"nanjing01","beijing01","nanjing02","nanhai"};
 
        autoCompleteTextView = findViewById(R.id.autoCompleteTextView);
        ArrayAdapter<String> adapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1,res );
     //绑定
        autoCompleteTextView.setAdapter(adapter);

```

```xml
<AutoCompleteTextView
        android:id="@+id/autoCompleteTextView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginStart="29dp"
        android:layout_marginLeft="29dp"
        android:layout_marginTop="142dp"
        android:hint="你输入你要搜索的关键词"
        android:completionThreshold="2"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
```

```xml
<string name="textView2">欢迎大家加入我的github项目,一起学习，一
        起发展"https://github.com/xu全栈工程师进阶学习站https://github.com/
        xunyegege/gavin_note" style="text-decoration: none;color: white;font-weigh
        t: bolder"我个人的学习及生活小记录a href="https://github.com/xu
        nyegege/report_gather" style="text-decoration: none;color: white;font-weight:       er"行业内最新最群的报告，工作日每日更新
</string>

```

### 多选

```
/*设置分隔符，比如 ,逗号    MultiAutoCompleteTextView指定的那个分隔符只有","*/
multiAutoCompleteTextView.setTokenizer(new    MultiAutoCompleteTextView.CommaTokenizer());
```

```java
自定义的通用类，可实现自定义分隔符。。。格式为' char '
    package com.gavin.www.helloworld;

import android.text.SpannableString;
import android.text.Spanned;
import android.text.TextUtils;
import android.widget.MultiAutoCompleteTextView.Tokenizer;

public class SemicolonTokenizer implements Tokenizer {
    private char charS;
    private String mSTring;

    public SemicolonTokenizer(char charS) {
        this.charS = charS;
        mSTring = String.valueOf(charS);
    }

    public int findTokenStart(CharSequence text, int cursor) {
        int i = cursor;

        while (i > 0 && text.charAt(i - 1) != charS) {
            i--;
        }
        while (i < cursor && text.charAt(i) == ' ') {
            i++;
        }

        return i;
    }

    public int findTokenEnd(CharSequence text, int cursor) {
        int i = cursor;
        int len = text.length();

        while (i < len) {
            if (text.charAt(i) == charS) {
                return i;
            } else {
                i++;
            }
        }

        return len;
    }

    public CharSequence terminateToken(CharSequence text) {
        int i = text.length();

        while (i > 0 && text.charAt(i - 1) == ' ') {
            i--;
        }

        if (i > 0 && text.charAt(i - 1) == charS) {
            return text;
        } else {
            if (text instanceof Spanned) {
                SpannableString sp = new SpannableString(text + mSTring);
                TextUtils.copySpansFrom((Spanned) text, 0, text.length(), Object.class, sp, 0);
                return sp;
            } else {
                return text + mSTring;
            }
        }
    }
}
```

```java
使用方法演示
multiAutoCompleteTextView.setTokenizer(new SemicolonTokenizer(';'));
```

## ToggleButton开关按钮

```xml
<ToggleButton
        android:id="@+id/toggleButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="71dp"
        android:textOff="关"
        android:textOn="开"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

```

```java
public class Main2Activity extends AppCompatActivity  implements CompoundButton.OnCheckedChangeListener {
ImageView imageView;
ToggleButton toggleButton;

    @Override
    public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
/*buttonView   代表被点击控件的本身*/
/*isChecked    代表被点击控件的状态*/
        /*当点击这个控件的时候，更换img的背景  3目运算符*/
        imageView.setBackgroundResource(isChecked ? R.drawable.one01 : R.drawable.second02);
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);
        imageView=findViewById(R.id.imageView);
        toggleButton=findViewById(R.id.toggleButton);
        //给当前的ToggleButton控件设置监听器
        toggleButton.setOnCheckedChangeListener(this);
        
    }
}
```

## checkBox 多选框

```java

public class LinearLayout extends AppCompatActivity  implements CompoundButton.OnCheckedChangeListener {
    CheckBox c1;
    CheckBox c2;
    CheckBox c3;
    CheckBox c4;

    @Override
    public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
        if(isChecked){
            String text=buttonView.getText().toString();
            Log.i("TAG", text);

        }
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_linear_layout);
        c1=findViewById(R.id.checkbox1);
        c2=findViewById(R.id.checkbox2);
        c3=findViewById(R.id.checkbox3);
        c4=findViewById(R.id.checkbox4);

        c1.setOnCheckedChangeListener(this);
        c2.setOnCheckedChangeListener(this);
        c3.setOnCheckedChangeListener(this);
        c4.setOnCheckedChangeListener(this);

    }
}
```

```xml
   <LinearLayout android:orientation="horizontal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="爱好："/>
        <CheckBox
            android:id="@+id/checkbox1"
            android:text="足球"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />
        <CheckBox
            android:id="@+id/checkbox2"
            android:text="DNF"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />
        <CheckBox
            android:id="@+id/checkbox3"
            android:text="计算机"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />
        <CheckBox
            android:id="@+id/checkbox4"
            android:text="小姐姐"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />

    </LinearLayout>
```

## 单选按钮

```xml
  <RadioGroup
            android:id="@+id/radiogroup"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <RadioButton
                android:id="@+id/radio01"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="男" />

            <RadioButton
                android:id="@+id/radio02"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"

                android:text="女" />

        </RadioGroup>
```

```java
/*接口实现*/
 @Override
    public void onCheckedChanged(RadioGroup group, int checkedId) {
switch (checkedId){
    case R.id.radio01:
        Log.i("TAG", "男士: ");
     break;
    case R.id.radio02:
        Log.i("TAG", "女士: ");
        break;
        default:
            Log.i("TAG", "未选择: ");
            break;

}
    }


/*直接实现监听事件*/
  Rg=findViewById(R.id.radiogroup);
      /*  实现radiogroup的监听事件*/
        Rg.setOnCheckedChangeListener(this);


```

## 五大布局

## ①LinearLayout

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181219155609.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181219155633.png)

## ②相对布局

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181219160404.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181219193308.png)

## ③帧布局 FrameLayout

```xml
<FrameLayout

        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <TextView
            android:id="@+id/FrametextView01"

            android:layout_width="200dp"
            android:layout_height="200dp"
            android:layout_gravity="center"
            android:background="#785435"
            android:text="第一个页面" />

        <TextView
            android:id="@+id/FrametextView02"

            android:layout_width="150dp"

            android:layout_height="150dp"
            android:layout_gravity="center"
            android:background="#984512"
            android:text="第二个页面" />

        <TextView
            android:id="@+id/FrametextView03"
            android:layout_width="120dp"
            android:layout_height="120dp"
            android:layout_gravity="center"
            android:background="#564835"
            android:text="第三个页面" />

        <TextView
            android:id="@+id/FrametextView04"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_gravity="center"
            android:background="#697524"
            android:text="第四个页面" />

        <ProgressBar
            android:layout_width="40dp"
            android:layout_height="40dp"
            android:layout_gravity="center" />

        <TextView
            android:layout_width="30dp"
            android:layout_height="30dp"
            android:layout_gravity="center"
            android:text="80%" />
    </FrameLayout>
```

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181219213004.png)

## ④绝对布局AbsoluteLayout

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181219213247.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181219213308.png)

## ⑤表格布局TableLayout

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181219213924.png)

```
android:stretchColumns="*"    //这个可以平均占满空间
```

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181219214209.png)

## 跳转Intent

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181220091019.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181220091133.png)

```java
IntentFirst.java
package com.gavin.www.numerator;

import android.content.Intent;
import android.support.annotation.Nullable;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class IntentFirst extends AppCompatActivity {
    Button Bt1;
    Button Bt2;
    TextView T1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_intent_first);
        T1 = findViewById(R.id.intentText01);

        Bt1 = findViewById(R.id.intentBt01);
        /*通过startActivity方式实现跳转*/

        //注册点击事件
        Bt1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                /**初始化Intent
                 * 第一个参数：上下文对象
                 * 第二个参数：目标文件
                 */
                Intent intent = new Intent(IntentFirst.this, IntentSecond.class);
                startActivity(intent);

            }
        });

        /*通过startActivityForResult*/
        Bt2 = findViewById(R.id.intentBt02);
        Bt2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(IntentFirst.this, IntentSecond.class);
                /**
                 * 第一个参数：intent对象
                 * 第二个参数：请求标识
                 */
                startActivityForResult(intent, 1);

            }
        });

    }

    @Override

    /*requestCode:请求标志
     *resultCode  第二个页面返回的标志
     * data  第二个页面回传的数据
     * 这时候需要在第二个页面写标志
     *
     * */
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == 1 && resultCode == 2) {
            //取key
            String test = data.getStringExtra("data");
            T1.setText(test);
        }
    }
}




```

```java
IntentSecond.java
package com.gavin.www.numerator;

import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

public class IntentSecond extends AppCompatActivity {
Button bt1;
private  String test="helloworld";
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_intent_second);

        /* 第二个页面什么时候给第一个页面回传数据
        * 回传给第一个页面的实际上是一个intent对象*/

        bt1=findViewById(R.id.intentSecondBt01);
        bt1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent data=new Intent();

                //key   value形式存放
             data.putExtra("data",test);

             /*这个结果码需要匹配*/
             setResult(2,data);
             finish();//销毁当前页面

            }
        });
    }
}



```

## APP签名打包

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181220115307.png)

## 组件配置说明

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181221160854.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181221161122.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181221161148.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181221161156.png)





## ListView

### 数据适配器

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181221162945.png)

# 数据存储

## ①SharedPreferences

> 1、是一种轻型的数据存储方式
>
> 2、本质是基于XML文件存储key-balue键值对数据
>
> 3、通常用来存储一些简单的配置信息
>
>

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181225085417.png)

```java
package com.gavin.www.numerator;

import android.content.SharedPreferences;
import android.os.SystemClock;
import android.preference.PreferenceManager;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.Toast;

import static android.widget.Toast.LENGTH_SHORT;

public class SharedpreferencesDemo extends AppCompatActivity {
    EditText account_edit, password_edit;
    CheckBox checkBox;
    Button bt1, bt2;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_sharedpreferences_demo);
        account_edit = findViewById(R.id.pref_account_edit);
        password_edit = findViewById(R.id.pref_password_edit);
        checkBox = findViewById(R.id.pref_check);
        bt1 = findViewById(R.id.pref_bt1);
        bt2 = findViewById(R.id.pref_bt2);
        SharedPreferences pref = getSharedPreferences("data", MODE_PRIVATE);
        final SharedPreferences.Editor editor = pref.edit();

        //   SharedPreferences pref=PreferenceManager.getDefaultSharedPreferences(this);
      bt1.setOnClickListener(new View.OnClickListener() {
          @Override
          public void onClick(View v) {

                      String name = account_edit.getText().toString().trim();
                      String pwd = password_edit.getText().toString().trim();
                      if ("admin".equals(name) && "123456".equals(pwd)) {
                          if (checkBox.isChecked()) {
                              editor.putString("name", name);
                              editor.putString("password", pwd);
                              editor.commit();
                              Toast.makeText(SharedpreferencesDemo.this, "登录成功", LENGTH_SHORT).show();
                          }else {
                              editor.remove("name");
                              editor.commit();
                          }

                      }else {
                          Toast.makeText(SharedpreferencesDemo.this, "登录失败", LENGTH_SHORT).show();
                      }


//


          }
      });




       /* editor.putString("name","gavin");
        editor.putInt("age",18);
        editor.putLong("time",System.currentTimeMillis());
        editor.putBoolean("default",false);
        editor.commit();
        editor.remove("default");
        editor.commit();
        //测试
        String str=pref.getString("name"," ");
        Log.i("test", str);*/
 /*       String name=pref.getString("name"," ");
      if (name==null||name.equals("")){
          checkBox.setChecked(false);
      }else {
          checkBox.setChecked(true);
          account_edit.setText(name);
      }*/
    }

/*    public void doClick(View v) {

        switch (v.getId()) {
            case R.id.pref_bt1:
                String name = account_edit.getText().toString().trim();
                String pwd = password_edit.getText().toString().trim();
                if ("admin".equals(name) && "123456".equals(pwd)) {
                    if (checkBox.isChecked()) {
                        editor.putString("name", name);
                        editor.putString("password", pwd);
                        editor.commit();
                        Toast.makeText(this, "登录成功", Toast.LENGTH_SHORT).show();
                    }else {
                        editor.remove("name");
                        editor.commit();
                    }

                }else {
                    Toast.makeText(this, "登录失败", Toast.LENGTH_SHORT).show();
                }
           break;

//            case     R.id.pref_bt2:
                 default:
                     break;

        }


    }*/
}

```



## SQlite

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181225134548.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181225134817.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181225134928.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181225135107.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181225135329.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181225135519.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181225135604.png)



![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181225145424.png)





![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181225150643.png)

![](https://raw.githubusercontent.com/xunyegege/picgo_repo/master/G%3A%5Cgithub%5Cpicgo_repo20181225160202.png)



### 1

```java1
package com.gavin.www.numerator;

import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;

public class SQLiteDemo extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_sqlite_demo);
        //每个程序的数据库都是唯一的，默认是互相不干扰
        //创建数据库，并打开

        /**参数
         * 1、数据库名字
         * 2、数据库权限
         * 3、实例化工厂类
         * */
        SQLiteDatabase db = openOrCreateDatabase("user.db", MODE_PRIVATE, null);
        /*执行sql语句
         * */
        db.execSQL("create table if not exists usertb(_id Integer primary key autoincrement ,name text not null,age integer not null,sex text not null )");
        db.execSQL("insert into usertb(name,sex,age) values('gavin1','female','18')");
        db.execSQL("insert into usertb(name,sex,age) values('gavin2','female','18')");
        db.execSQL("insert into usertb(name,sex,age) values('gavin3','male','18')");
        db.execSQL("insert into usertb(name,sex,age) values('gavin4','male','18')");
        //参数  1、sql语句   2、查询条件cousor(游标)
        Cursor c = db.rawQuery("select *from usertb", null);
        if (c != null) {
            while (c.moveToNext()) {
                Log.i("database", "_id:" + c.getInt(c.getColumnIndex("_id")));
                Log.i("database", "name:" + c.getString(c.getColumnIndex("name")));
                Log.i("database", "sex:" + c.getString(c.getColumnIndex("sex")));
                Log.i("database", "age:" + c.getInt(c.getColumnIndex("age")));
                Log.i("count", "******************************************** ");
            }
//释放游标
            c.close();
        }
//释放数据库
        db.close();
    }
}

```

### 2

```java
package com.gavin.www.numerator;

import android.content.ContentValues;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;

public class SQLiteDemo02 extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_sqlite_demo02);
        SQLiteDatabase db = openOrCreateDatabase("stu.db", MODE_PRIVATE, null);
        db.execSQL("create table if not exists stutb(_id Integer primary key autoincrement ,name text not null,age integer not null,sex text not null )");
        /*ContentValues  这边的key-value组合*/
        ContentValues values = new ContentValues();
        values.put("name", "gavin01");
        values.put("age", 18);
        values.put("sex", "male");
        long rowId = db.insert("stutb", null, values);  //这个有返回值，就是行数
        values.clear();  //这边清空，然后再次执行插入操作
        values.put("name", "gavin02");
        values.put("age", 19);
        values.put("sex", "female");
        db.insert("stutb", null, values);//这个返回值也可以不要
        values.clear();
        values.put("name", "gavin03");
        values.put("age", 20);
        values.put("sex", "male");
        db.insert("stutb", null, values);
        values.clear();

        //更新
        values.put("sex","女");
        db.update("stutb",values,"_id==?",new String[]{"3"});  //将id等于3的人的性别改成女
        db.update("stutb",values,"_id>?",new String[]{"3"});  //将id大于3的人的性别改成女
        db.delete("stutb","name like ?",new String[]{"%02%"});//删除名字中带有02的人
      Cursor c= db.query("stutb",null,"_id>?",new String[]{"0"},null,null,"name");
        if(c!=null){
            String []columns=c.getColumnNames();
            while(c.moveToNext()){
                         for(String columnsName: columns){

                             Log.i("name", c.getString(c.getColumnIndex(columnsName)));


                         }

            }
            c.close();
        }
        db.close();
    }
}

```

### 3

```java
package com.gavin.www.numerator;

import android.content.Context;
import android.database.DatabaseErrorHandler;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;
import android.os.Build;
import android.support.annotation.RequiresApi;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class SQLiteDemo03 extends SQLiteOpenHelper {
    public SQLiteDemo03(Context context, String name) {
        super(context, name, null, 1);
    }

    public SQLiteDemo03(Context context, String name, SQLiteDatabase.CursorFactory factory, int version, DatabaseErrorHandler errorHandler) {
        super(context, name, factory, version, errorHandler);
    }

    @RequiresApi(api = Build.VERSION_CODES.P)
    public SQLiteDemo03(Context context, String name, int version, SQLiteDatabase.OpenParams openParams) {
        super(context, name, version, openParams);
    }

    //首次创建数据库的时候调用，一般可以把建表的操作放在这
    @Override
    public void onCreate(SQLiteDatabase db) {
        db.execSQL("create table if not exists teatb(_id Integer primary key autoincrement ,name text not null,age integer not null,sex text not null )");
db.execSQL("insert into teatb(name,age,sex)values('zhangsan',10,'nv')");
    }
//当数据的版本发生变化的时候，会自动执行
    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {

    }


}

```

```java
package com.gavin.www.numerator;

import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.support.v7.widget.ThemedSpinnerAdapter;
import android.util.Log;

public class SQLiteDemo03Main extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_sqlite_demo03_main);

        SQLiteDemo03  openhelper=new SQLiteDemo03(this,"teatb");
        SQLiteDatabase db=openhelper.getWritableDatabase();  //获取一个数据库，且返回为SQLiteDatabase对象
         Cursor c= db.rawQuery("select *from teatb",null);
          if(c!=null){
              String []cols=c.getColumnNames();
              while (c.moveToNext()){
                  for(String columnsName: cols){

                      Log.i("info", columnsName+"  "+c.getString(c.getColumnIndex(columnsName)));
                  }
              }
c.close();
          }
          db.close();
    }
}

```





## 记事本

```java
package com.gavin.www.numerator;

import android.content.ContentValues;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class NotePad extends AppCompatActivity {
    private Button bt_notepad_query, bt_notepad_commit;
    private EditText notepad_id_query, notepad_id, notepad_query_show, notepad_edit;
    SQLiteDatabase db;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_note_pad);
        bt_notepad_commit = findViewById(R.id.bt_notepad_commit);
        bt_notepad_query = findViewById(R.id.bt_notepad_query);
        notepad_edit = findViewById(R.id.notepad_edit);
        notepad_id = findViewById(R.id.notepad_id);
        notepad_id_query = findViewById(R.id.notepad_id_query);
        notepad_query_show = findViewById(R.id.notepad_query_show);
        //建立数据库
         db = openOrCreateDatabase("note.db", MODE_PRIVATE, null);
        db.execSQL("create table if not exists notetb(_id Integer primary key autoincrement ,content text not null,label text not null )");



        //点击保存按钮，这时候我们判断上面内容以及标签是否写了东西
        bt_notepad_commit.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String content = notepad_edit.getText().toString().trim();
                String label = notepad_id.getText().toString().trim();
                if ((!content.equals("") && content != null) && (!label.equals("") && label != null)) {
                    /*建立   ContentValues  这边为key-value组合*/
                     ContentValues values = new ContentValues();
                    //当判断里面有数据的时候，存储该数据
                    values.put("label", label);
                    values.put("content", content);

                    db.insert("notetb", null, values);
                    values.clear();
                    Toast.makeText(NotePad.this, "笔记保存成功", Toast.LENGTH_SHORT).show();
                } else {
                    Toast.makeText(NotePad.this, "您上面有内容未输入", Toast.LENGTH_SHORT).show();
                }

            }
        });
        //下面就是查询操作
        bt_notepad_query.setOnClickListener(
                new View.OnClickListener() {
                    @Override
                    public void onClick(View v) {
                        String label = notepad_id_query.getText().toString().trim();

                        //这边是否可以加个动态提示
                        if (!label.equals("") && label != null) {
                            Cursor c = db.query("notetb", null, "label=?", new String[]{label}, null, null, null);
                            if (c != null) {

                                //这边一定要加 while
                                while (c.moveToNext()) {
                                    String content = c.getString(c.getColumnIndex("content")).trim();
                                    notepad_query_show.setText(content);
                                }
                               c.close();
                            } else {
                                Toast.makeText(NotePad.this, "没有查询到您要的笔记呢", Toast.LENGTH_SHORT).show();
                            }


                        } else {
                            Toast.makeText(NotePad.this, "请输入您想要查询的标签哦", Toast.LENGTH_SHORT).show();
                        }


                    }
                }
        );


    }
}

```

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".NotePad">

    <LinearLayout
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Gavin记事本"
            android:textSize="40sp"
            android:gravity="center_horizontal"
            />
            <EditText
                android:layout_width="match_parent"
                android:layout_height="120sp"
                android:hint="请在此输入您想要记录的文字"
                android:id="@+id/notepad_edit"
                android:textSize="25sp"/>
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="horizontal">
            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="请输入标签 : "
                android:textSize="30sp"/>
            <EditText
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:hint="例 test/shoppong"
                android:id="@+id/notepad_id"
                android:textSize="20sp"
                />
        </LinearLayout>
       <Button
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:id="@+id/bt_notepad_commit"
           android:text="保存笔记"
           android:textSize="30sp"/>
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="horizontal">
            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="请输入标签 : "
                android:textSize="30sp"/>
            <EditText
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:hint="请输入查询标签"
                android:id="@+id/notepad_id_query"
                android:textSize="20sp"
                />
        </LinearLayout>
        <Button
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/bt_notepad_query"
            android:text="查询笔记"
            android:textSize="30sp"/>

        <EditText
            android:layout_width="match_parent"
            android:layout_height="120sp"
            android:hint="查询展示"
            android:id="@+id/notepad_query_show"
            android:textSize="25sp"/>
    </LinearLayout>



</android.support.constraint.ConstraintLayout>

```



