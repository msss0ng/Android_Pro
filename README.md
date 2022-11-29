package com.example.touch_20221129;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.Rect;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.MotionEvent;
import android.view.SubMenu;
import android.view.View;

public class MainActivity extends AppCompatActivity {
    final static int LINE = 1, CIRCLE = 2, SQUARE = 3;
    static int curShape = LINE, curColor = Color.RED;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(new MyGraphicView(this));
        setTitle("글임판");
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        super.onCreateOptionsMenu(menu);
        menu.add(0,1,0,"선 그리기");
        menu.add(0,2,0,"원 그리기");
        menu.add(0,3,0,"사각형 그리기");
        SubMenu sMenu = menu.addSubMenu("색 변경");
        sMenu.add(0,4,0,"빨강");
        sMenu.add(0,5,0,"초록");
        sMenu.add(0,6,0,"파랑");
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        switch (item.getItemId()) {
            case 1:
                curShape = LINE;
                return true;
            case 2:
                curShape = CIRCLE;
                return true;
            case 3:
                curShape = SQUARE;
                return true;
            case 4:
                curColor = Color.RED;
                return true;
            case 5:
                curColor = Color.GREEN;
                return true;
            case 6:
                curColor = Color.BLUE;
                return true;
        }
        return super.onOptionsItemSelected(item);
    }

    private static class MyGraphicView extends View {
        int startX = -1, startY = -1, stopX = -1, stopY = -1;
        public MyGraphicView(Context context) {
            super(context);
        }

        @Override
        public boolean onTouchEvent(MotionEvent event) {
            switch (event.getAction()) {
                case MotionEvent.ACTION_DOWN:
                    startX = (int) event.getX();
                    startY = (int) event.getY();
                    break;
                case MotionEvent.ACTION_MOVE:
                case MotionEvent.ACTION_UP:
                    stopX = (int) event.getX();
                    stopY = (int) event.getY();
                    this.invalidate();
                    break;
            }
            return true;
        }

        @Override
        protected void onDraw(Canvas canvas) {
            super.onDraw(canvas);
            Paint paint = new Paint();
            paint.setAntiAlias(true);
            paint.setStrokeWidth(5);
            paint.setStyle(Paint.Style.STROKE);
            paint.setColor(curColor);

            switch (curShape) {
                case LINE:
                    canvas.drawLine(startX, startY, stopX, stopY, paint);
                    break;
                case CIRCLE:
                    int radius = (int) Math.sqrt(Math.pow(stopX - startX, 2)
                            + Math.pow(stopY - startY, 2));
                    canvas.drawCircle(startX, startY, radius, paint);
                    break;
                case SQUARE:
                    Rect rect = new Rect(startX, startY, stopX, stopY);
                    canvas.drawRect(rect, paint);
                    break;
            }
        }
    }

}

-----

package com.example.image_9_2_20221129;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.graphics.Canvas;
import android.os.Bundle;
import android.view.View;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(new MyGraphicView(this));
        setTitle("미니포토#");
    }

    private static class MyGraphicView extends View {
        public MyGraphicView(Context context) {
            super(context);
        }

        @Override
        protected void onDraw(Canvas canvas) {
            super.onDraw(canvas);
            Bitmap picture = BitmapFactory.decodeResource(getResources(),
                    R.drawable.jg);

            int cenX = this.getWidth() / 2;
            int cenY = this.getHeight() / 2;
            int picX = (this.getWidth() - picture.getWidth()) / 2;
            int picY = (this.getHeight() - picture.getHeight()) / 2;

            canvas.scale(0.5F,0.5F,cenX,cenY);
            canvas.drawBitmap(picture, picX, picY, null);
            picture.recycle();
        }
    }
}

-----

package com.example.p_6_6;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="여긴 서랍 밖입니다" />

    <SlidingDrawer
        android:id="@+id/slidingdrawer"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:content="@+id/content"
        android:handle="@+id/handle"
        android:orientation="vertical"
        >

        <Button
            android:id="@+id/handle"
            android:layout_width="wrap_content"
            android:layout_height="50dp"
            android:text="서랍 손잡이" />

        <LinearLayout
            android:id="@+id/content"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:background="#3ADF00"
            android:orientation="vertical" >

            <SlidingDrawer
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:content="@+id/content2"
                android:handle="@+id/handle2"
                android:orientation="vertical"
                android:topOffset= "200dp"
                >

                <Button
                    android:id="@+id/handle2"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:background="#3ADF00"
                    android:text="안 서랍 손잡이" />

                <LinearLayout
                    android:id="@+id/content2"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:orientation="vertical"
                    android:background="#8904B1"
                    android:gravity="center"
                    >

                    <TextView
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text="여긴 두번쨰 서랍입니다"

                        />
                </LinearLayout>
            </SlidingDrawer>
        </LinearLayout>
    </SlidingDrawer>

</LinearLayout>

-----

package com.example.p_7_5;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.Display;
import android.view.Gravity;
import android.view.View;
import android.view.WindowManager;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    Button btn;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        btn = (Button)findViewById(R.id.btn);

        btn.setOnClickListener(new View.OnClickListener()
        {
            @Override
            public void onClick(View v)
            {
                Toast msg = new Toast(getApplicationContext());
                ImageView img = new ImageView(getApplicationContext());
                img.setImageResource(R.drawable.ic_launcher_background);
                msg.setView(img);

                Display display = ((WindowManager) getSystemService(WINDOW_SERVICE)).getDefaultDisplay();
                int xOffset = (int) (Math.random()*display.getWidth());
                int yOffset = (int) (Math.random()*display.getHeight());

                msg.setGravity(Gravity.TOP|Gravity.LEFT,xOffset,yOffset);
                msg.show();
            }
        });
    }
}

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:gravity="center">

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="토스트 보내기"
        android:id="@+id/btn"
        />
</LinearLayout>

-----

package com.example.p_7_6;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

import android.app.Dialog;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.RadioGroup;

public class MainActivity extends AppCompatActivity {

    RadioGroup rg;
    Button btn;
    ImageView img;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btn = (Button) findViewById(R.id.btn);
        rg = (RadioGroup) findViewById(R.id.gr);


        btn.setOnClickListener(new View.OnClickListener()
        {
            @Override
            public void onClick(View v)
            {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.this);
                View dlgView = View.inflate(MainActivity.this,R.layout.dialog,null);

                img = (ImageView) dlgView.findViewById(R.id.imageView1);
                dlg.setView(dlgView);

                switch (rg.getCheckedRadioButtonId())
                {
                    case R.id.rd1:
                        dlg.setTitle("강아지");
                        img.setImageResource(R.mipmap.ic_launcher_round);
                        break;
                    case R.id.rd2:
                        dlg.setTitle("고양이");
                        img.setImageResource(R.mipmap.ic_launcher);
                        break;
                    case R.id.rd3:
                        dlg.setTitle("토끼");
                        img.setImageResource(R.drawable.ic_launcher_foreground);
                        break;
                    case R.id.rd4:
                        dlg.setTitle("말");
                        img.setImageResource(R.drawable.ic_launcher_background);
                        break;
                }

                dlg.setPositiveButton("닫기",null);
                dlg.show();
            }
        });
    }
}

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">


    <RadioGroup
        android:id="@+id/gr"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content">
        <RadioButton
            android:id="@+id/rd1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="강아지"/>
        <RadioButton
            android:id="@+id/rd2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="고양이"/>
        <RadioButton
            android:id="@+id/rd3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="토끼"/>
        <RadioButton
            android:id="@+id/rd4"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="말"/>

    </RadioGroup>

    <Button
        android:id="@+id/btn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="그림보기"/>

</LinearLayout>

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical" >

    <ImageView
        android:id="@+id/imageView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:src="@mipmap/ic_launcher"
        />
</LinearLayout>
