DATABASE.Q.1)
XML code:
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout 
xmlns:android="http://schemas.android.com/apk/res/andro
id"
 xmlns:app="http://schemas.android.com/apk/res-auto"
 xmlns:tools="http://schemas.android.com/tools"
 android:layout_width="match_parent"
 android:layout_height="match_parent"
 tools:context=".MainActivity">
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="Student Details"
 android:layout_marginTop="10dp"
 android:layout_marginLeft="120dp"
 android:textSize="25sp"
 android:textStyle="bold"
 android:textColor="@color/black"
 android:id="@+id/title"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t1"
 android:text="Enter Roll No. :"
 android:layout_below="@id/title"
 android:layout_marginTop="20dp"
 android:layout_marginLeft="15dp"
 android:textColor="@color/black"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_alignParentRight="true"
 android:layout_below="@id/title"
 android:layout_marginRight="80dp"
 android:id="@+id/e1"
 android:inputType="number"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t2"
 android:text="Enter Name :"
 android:layout_below="@id/t1"
 android:layout_marginTop="25dp"
android:layout_marginLeft="15dp"
 android:textColor="@color/black"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_alignParentRight="true"
 android:layout_below="@id/e1"
 android:layout_marginRight="80dp"
 android:id="@+id/e2"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t3"
 android:text="Enter Class :"
 android:layout_below="@id/t2"
 android:layout_marginTop="25dp"
 android:layout_marginLeft="15dp"
 android:textColor="@color/black"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_alignParentRight="true"
 android:layout_below="@id/e2"
 android:layout_marginRight="80dp"
 android:id="@+id/e3"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t4"
 android:text="Enter Contact :"
 android:layout_below="@id/t3"
 android:layout_marginTop="25dp"
 android:layout_marginLeft="15dp"
 android:textColor="@color/black"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_alignParentRight="true"
 android:layout_below="@id/e3"
 android:layout_marginRight="80dp"
 android:id="@+id/e4"
 android:inputType="phone"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
android:id="@+id/b1"
 android:text="Insert"
 android:layout_below="@id/t4"
 android:layout_marginTop="25dp"
 android:layout_marginLeft="150dp"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/b2"
 android:text="Display"
 android:layout_below="@id/b1"
 android:layout_marginTop="25dp"
 android:layout_marginLeft="150dp"/>
</RelativeLayout>
Java code:
package com.example.myapplication;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.app.AlertDialog.Builder;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.EditText;
import android.app.Activity;
public class MainActivity extends AppCompatActivity 
implements OnClickListener {
 EditText Rollno, Name, Class, Contact;
 Button Insert, ViewAll;
 SQLiteDatabase db;
 @Override
 protected void onCreate(Bundle savedInstanceState) 
{
 super.onCreate(savedInstanceState);
 setContentView(R.layout.activity_main);
 Rollno = (EditText) findViewById(R.id.e1);
 Name = (EditText) findViewById(R.id.e2);
 Class = (EditText) findViewById(R.id.e3);
 Contact = (EditText) findViewById(R.id.e4);
Insert = (Button) findViewById(R.id.b1);
 ViewAll = (Button) findViewById(R.id.b2);
 Insert.setOnClickListener(this);
 ViewAll.setOnClickListener(this);
 db = openOrCreateDatabase("StudentDatabase", 
Context.MODE_PRIVATE, null);
 db.execSQL("CREATE TABLE IF NOT EXISTS 
students(rollno VARCHAR,name VARCHAR,class 
VARCHAR,contact VARCHAR);");
 }
 public void onClick(View view)
 {
 if (view == Insert)
 {
 if 
(Rollno.getText().toString().trim().length() == 0 || 
Name.getText().toString().trim().length() == 0 || 
Class.getText().toString().trim().length() == 0||
Contact.getText().toString().trim().length() == 0)
 {
 showMessage("Error", "Please enter all 
values");
 return;
 }
 db.execSQL("INSERT INTO students VALUES('" 
+ Rollno.getText() + "','" + Name.getText() + "','" + 
Class.getText() + "','"+Contact.getText()+"');");
 showMessage("Success", "Record added");
 clearText();
 }
 if (view == ViewAll)
 {
 Cursor c = db.rawQuery("SELECT * FROM 
students", null);
 if (c.getCount() == 0)
 {
 showMessage("Error", "No records 
found");
 return;
 }
 StringBuffer buffer = new StringBuffer();
 while (c.moveToNext())
{
 buffer.append("Rollno:" + 
c.getString(0) + "\n");
 buffer.append("Name:" + c.getString(1) 
+ "\n");
 buffer.append("Class:" + c.getString(2)
+ "\n");
 buffer.append("Contact:" + 
c.getString(3) + "\n\n");
 }
 showMessage("Student Details:", 
buffer.toString());
 }
 }
 public void showMessage(String title, String 
message) {
 Builder builder = new Builder(this);
 builder.setCancelable(true);
 builder.setTitle(title);
 builder.setMessage(message);
 builder.show();
 }
 public void clearText() {
 Rollno.setText("");
 Name.setText("");
 Class.setText("");
 Contact.setText("");
 Rollno.requestFocus();
 }
}









DATABASE Q.2)
XML code:
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout 
xmlns:android="http://schemas.android.com/apk/res/andro
id"
 xmlns:app="http://schemas.android.com/apk/res-auto"
 xmlns:tools="http://schemas.android.com/tools"
 android:layout_width="match_parent"
 android:layout_height="match_parent"
 tools:context=".MainActivity">
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="Car Details"
 android:layout_marginLeft="120dp"
 android:layout_marginTop="30dp"
 android:id="@+id/title"
 android:textColor="@color/black"
 android:textSize="25sp"
 android:textStyle="bold"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t1"
 android:text="Car No. :"
 android:layout_marginTop="105dp"
 android:textSize="20sp"
 android:textColor="@color/black"
 android:layout_marginLeft="15dp"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:id="@+id/e1"
 android:inputType="number"
 android:layout_alignParentRight="true"
 android:layout_marginRight="90dp"
 android:layout_marginTop="90dp"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t2"
 android:text="Car Name :"
 android:layout_marginTop="25dp"
 android:textSize="20sp"
android:textColor="@color/black"
 android:layout_marginLeft="15dp"
 android:layout_below="@id/t1"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:id="@+id/e2"
 android:layout_alignParentRight="true"
 android:layout_marginRight="80dp"
 android:layout_marginTop="10dp"
 android:layout_below="@id/e1"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t3"
 android:text="Car Model :"
 android:layout_marginTop="25dp"
 android:textSize="20sp"
 android:textColor="@color/black"
 android:layout_marginLeft="15dp"
 android:layout_below="@id/t2"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:id="@+id/e3"
 android:layout_alignParentRight="true"
 android:layout_marginRight="80dp"
 android:layout_marginTop="10dp"
 android:layout_below="@id/e2"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t4"
 android:text="Car Colour :"
 android:layout_marginTop="25dp"
 android:textSize="20sp"
 android:textColor="@color/black"
 android:layout_marginLeft="15dp"
 android:layout_below="@id/t3"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:id="@+id/e4"
 android:layout_alignParentRight="true"
 android:layout_marginRight="70dp"
android:layout_marginTop="10dp"
 android:layout_below="@id/e3"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/b1"
 android:text="Insert"
 android:layout_below="@id/t4"
 android:layout_marginTop="30dp"
 android:layout_marginLeft="15dp"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/b2"
 android:text="Update"
 android:layout_below="@id/e4"
 android:layout_marginTop="20dp"
 android:layout_marginLeft="150dp"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/b3"
 android:text="Display"
 android:layout_below="@id/b1"
 android:layout_marginTop="25dp"
 android:layout_marginLeft="60dp"/>
</RelativeLayout>
Java code:
package com.example.myapplication;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.app.AlertDialog.Builder;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.EditText;
import android.app.Activity;
public class MainActivity extends AppCompatActivity 
implements OnClickListener{
 EditText Carno,Name,Model,Colour;
 Button Insert,Update,ViewAll;
 SQLiteDatabase db;
 @Override
 protected void onCreate(Bundle savedInstanceState) 
{
 super.onCreate(savedInstanceState);
 setContentView(R.layout.activity_main);
 Carno=(EditText) findViewById(R.id.e1);
 Name=(EditText) findViewById(R.id.e2);
 Model=(EditText) findViewById(R.id.e3);
 Colour=(EditText) findViewById(R.id.e4);
 Insert=(Button) findViewById(R.id.b1);
 Update=(Button) findViewById(R.id.b2);
 ViewAll=(Button) findViewById(R.id.b3);
 Insert.setOnClickListener(this);
 Update.setOnClickListener(this);
 ViewAll.setOnClickListener(this);
 
db=openOrCreateDatabase("CarDB",Context.MODE_PRIVATE,nu
ll);
 db.execSQL("CREATE TABLE IF NOT EXISTS 
car(carno VARCHAR,name VARCHAR,model VARCHAR,colour 
VARCHAR);");
 }
 public void onClick(View view)
 {
 if(view==Insert)
 {
 
if(Carno.getText().toString().trim().length()==0||
Name.getText().toString().trim().length()==0||
Model.getText().toString().trim().length()==0||
Colour.getText().toString().trim().length()==0)
 {
 showMessage("Error","Please enter all 
values");
 return;
 }
 db.execSQL("INSERT INTO car 
VALUES('"+Carno.getText()+"','"+Name.getText()
+"','"+Model.getText()+"','"+Colour.getText()+"');");
showMessage("Success","Record added");
 clearText();
 }
 if(view==ViewAll)
 {
 Cursor c=db.rawQuery("SELECT * FROM 
car",null);
 if(c.getCount()==0)
 {
 showMessage("Error","No records 
found");
 return;
 }
 StringBuffer buffer=new StringBuffer();
 while(c.moveToNext())
 {
 
buffer.append("Car_no:"+c.getString(0)+"\n");
 buffer.append("Name:"+c.getString(1)+"\
n");
 
buffer.append("Model:"+c.getString(2)+"\n");
 
buffer.append("Colour:"+c.getString(3)+"\n\n");
 }
 showMessage("Car 
Details:",buffer.toString());
 }
 if(view==Update)
 {
 
if(Colour.getText().toString().trim().length()==0)
 {
 showMessage("Error","Please enter 
colour");
 return;
 }
 Cursor c=db.rawQuery("SELECT * FROM car 
WHERE colour='"+Colour.getText()+"'",null);
 if(c.moveToFirst())
 {
 db.execSQL("UPDATE car SET 
name='"+Name.getText()+"',model='"+Model.getText()
+"',carno='"+Carno.getText()+"' WHERE
colour='"+Colour.getText()+"'");
 showMessage("Success","Record 
modified");
 }
 else
 {
 showMessage("Error","Invalid Colour");
 }
 clearText();
 }
 }
 public void showMessage(String title,String 
message)
 {
 Builder builder=new Builder(this);
 builder.setCancelable(true);
 builder.setTitle(title);
 builder.setMessage(message);
 builder.show();
 }
 public void clearText()
 {
 Carno.setText("");
 Name.setText("");
 Model.setText("");
 Colour.setText("");
 Carno.requestFocus();
 }
}






DATABASE Q.3)
XML code:
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout 
xmlns:android="http://schemas.android.com/apk/res/andro
id"
 xmlns:app="http://schemas.android.com/apk/res-auto"
 xmlns:tools="http://schemas.android.com/tools"
 android:layout_width="match_parent"
 android:layout_height="match_parent"
 tools:context=".MainActivity">
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="Student Details"
 android:layout_marginTop="10dp"
 android:layout_marginLeft="120dp"
 android:textSize="25sp"
 android:textStyle="bold"
 android:textColor="@color/black"
 android:id="@+id/title"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t1"
 android:text="Enter Student ID :"
 android:layout_below="@id/title"
 android:layout_marginTop="20dp"
 android:layout_marginLeft="15dp"
 android:textColor="@color/black"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_alignParentRight="true"
 android:layout_below="@id/title"
 android:layout_marginRight="30dp"
 android:id="@+id/e1"
 android:inputType="number"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t2"
 android:text="Enter Student Name :"
 android:layout_below="@id/t1"
 android:layout_marginTop="25dp"
android:layout_marginLeft="15dp"
 android:textColor="@color/black"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_alignParentRight="true"
 android:layout_below="@id/e1"
 android:layout_marginRight="30dp"
 android:id="@+id/e2"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t3"
 android:text="Enter Student Address :"
 android:layout_below="@id/t2"
 android:layout_marginTop="25dp"
 android:layout_marginLeft="15dp"
 android:textColor="@color/black"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_alignParentRight="true"
 android:layout_below="@id/e2"
 android:layout_marginRight="30dp"
 android:id="@+id/e3"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t4"
 android:text="Enter Student Phno :"
 android:layout_below="@id/t3"
 android:layout_marginTop="25dp"
 android:layout_marginLeft="15dp"
 android:textColor="@color/black"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_alignParentRight="true"
 android:layout_below="@id/e3"
 android:layout_marginRight="30dp"
 android:id="@+id/e4"
 android:inputType="phone"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
android:id="@+id/b1"
 android:text="Insert"
 android:layout_below="@id/t4"
 android:layout_marginTop="25dp"
 android:layout_marginLeft="150dp"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/b2"
 android:text="Display"
 android:layout_below="@id/b1"
 android:layout_marginTop="25dp"
 android:layout_marginLeft="150dp"/>
</RelativeLayout>
Java code:
package com.example.myapplication;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.app.AlertDialog.Builder;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.EditText;
import android.app.Activity;
public class MainActivity extends AppCompatActivity 
implements OnClickListener {
 EditText Id, Name,Address, Phno;
 Button Insert, ViewAll;
 SQLiteDatabase db;
 @Override
 protected void onCreate(Bundle savedInstanceState) 
{
 super.onCreate(savedInstanceState);
 setContentView(R.layout.activity_main);
 Id = (EditText) findViewById(R.id.e1);
 Name = (EditText) findViewById(R.id.e2);
 Address = (EditText) findViewById(R.id.e3);
Phno = (EditText) findViewById(R.id.e4);
 Insert = (Button) findViewById(R.id.b1);
 ViewAll = (Button) findViewById(R.id.b2);
 Insert.setOnClickListener(this);
 ViewAll.setOnClickListener(this);
 db = openOrCreateDatabase("StudentDatabase1", 
Context.MODE_PRIVATE, null);
 db.execSQL("CREATE TABLE IF NOT EXISTS 
students1(id VARCHAR,name VARCHAR,address VARCHAR,phno 
VARCHAR);");
 }
 public void onClick(View view)
 {
 if (view == Insert)
 {
 if (Id.getText().toString().trim().length()
== 0 || Name.getText().toString().trim().length() == 0 
|| Address.getText().toString().trim().length() == 0||
Phno.getText().toString().trim().length() == 0)
 {
 showMessage("Error", "Please enter all 
values");
 return;
 }
 db.execSQL("INSERT INTO students1 VALUES('"
+ Id.getText() + "','" + Name.getText() + "','" + 
Address.getText() + "','"+Phno.getText()+"');");
 showMessage("Success", "Record added");
 clearText();
 }
 if (view == ViewAll)
 {
 Cursor c = db.rawQuery("SELECT * FROM 
students1", null);
 if (c.getCount() == 0)
 {
 showMessage("Error", "No records 
found");
 return;
 }
 StringBuffer buffer = new StringBuffer();
 while (c.moveToNext())
{
 buffer.append("ID:" + c.getString(0) + 
"\n");
 buffer.append("Name:" + c.getString(1) 
+ "\n");
 buffer.append("Address:" + 
c.getString(2) + "\n");
 buffer.append("Phno:" + c.getString(3) 
+ "\n\n");
 }
 showMessage("Student Details:", 
buffer.toString());
 }
 }
 public void showMessage(String title, String 
message) {
 Builder builder = new Builder(this);
 builder.setCancelable(true);
 builder.setTitle(title);
 builder.setMessage(message);
 builder.show();
 }
 public void clearText() {
 Id.setText("");
 Name.setText("");
 Address.setText("");
 Phno.setText("");
 Id.requestFocus();
 }
}








DATABASE Q.4)

XML code:
<?xml version="1.0" encoding="utf-8"?>
<GridLayout 
xmlns:android="http://schemas.android.com/apk/res/andro
id"
 xmlns:app="http://schemas.android.com/apk/res-auto"
 xmlns:tools="http://schemas.android.com/tools"
 android:layout_width="match_parent"
 android:layout_height="match_parent"
 tools:context=".MainActivity"
 android:columnCount="2"
 android:rowCount="6">
 <LinearLayout
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:orientation="vertical"
 android:layout_marginTop="10dp"
 android:layout_marginLeft="30dp">
 <TextView
 android:id="@+id/pno"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="Pno :"
 android:textSize="20sp"/>
 <TextView
 android:id="@+id/pname"
 android:layout_marginTop="15dp"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="Pname :"
 android:textSize="20sp"
 />
 <TextView
 android:id="@+id/ptype"
 android:layout_marginTop="15dp"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="Ptype :"
 android:textSize="20sp"/>
 <TextView
 android:id="@+id/duration"
 android:layout_marginTop="15dp"
 android:layout_width="wrap_content"
android:layout_height="wrap_content"
 android:text="Duration :"
 android:textSize="20sp"/>
 </LinearLayout>
 <LinearLayout
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:orientation="vertical">
 <EditText
 android:id="@+id/ed_pno"
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:hint="Enter project number"
 android:textSize="15sp"/>
 <EditText
 android:id="@+id/ed_pname"
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:hint="Enter project name"
 android:textSize="15sp"/>
 <EditText
 android:id="@+id/ed_type"
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:hint="Enter project type"
 android:textSize="15sp"/>
 <EditText
 android:id="@+id/ed_duration"
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:hint="Enter project duration"
 android:textSize="15sp"/>
 </LinearLayout>
 <LinearLayout
 android:layout_height="wrap_content"
 android:layout_width="wrap_content"
 android:layout_marginLeft="80dp"
 android:orientation="vertical"
 android:layout_marginTop="40dp">
 <Button
android:id="@+id/addbtn"
 android:layout_width="wrap_content"
 android:layout_height="50dp"
 android:text="ADD"
 android:textSize="10sp"/>
 </LinearLayout>
 <LinearLayout
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_marginTop="40dp"
 android:layout_marginLeft="110dp">
 <Button
 android:id="@+id/viewbtn"
 android:layout_width="wrap_content"
 android:layout_height="50dp"
 android:text="VIEW"
 android:textSize="10sp"/>
 </LinearLayout>
 <LinearLayout
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:orientation="vertical"
 android:layout_marginTop="10dp"
 android:layout_marginLeft="30dp">
 <TextView
 android:id="@+id/eid"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="EID :"
 android:textSize="20sp"/>
 <TextView
 android:id="@+id/ename"
 android:layout_marginTop="15dp"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="Ename :"
 android:textSize="20sp"
 />
 <TextView
 android:id="@+id/qualification"
android:layout_marginTop="15dp"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="QUALIFICATION :"
 android:textSize="20sp"/>
 <TextView
 android:id="@+id/joindate"
 android:layout_marginTop="15dp"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="JOIN DATE :"
 android:textSize="20sp"/>
 </LinearLayout>
 <LinearLayout
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:orientation="vertical">
 <EditText
 android:id="@+id/ed_eid"
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:hint="Enter employee number"
 android:textSize="15sp"/>
 <EditText
 android:id="@+id/ed_ename"
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:hint="Enter employee name"
 android:textSize="15sp"/>
 <EditText
 android:id="@+id/ed_qualification"
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:hint="Enter qualification"
 android:textSize="15sp"/>
 <EditText
 android:id="@+id/ed_joindate"
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:hint="Enter join date"
 android:textSize="15sp"/>
 </LinearLayout>
<LinearLayout>
 <Button
 android:layout_marginTop="20dp"
 android:layout_marginLeft="80dp"
 android:id="@+id/addemp"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="ADD"/>
 </LinearLayout>
 <LinearLayout>
 <Button
 android:layout_marginTop="20dp"
 android:layout_marginLeft="80dp"
 android:id="@+id/viewemp"
 android:layout_width="wrap_content"
 android:text="view"
 android:layout_height="wrap_content"/>
 </LinearLayout>
 <LinearLayout>
 <Button
 android:id="@+id/thirdtableadd"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_marginLeft="80dp"
 android:layout_marginTop="20dp"
 android:text="Insert"/>
 </LinearLayout>
 <LinearLayout>
 <Button
 android:layout_marginTop="20dp"
 android:layout_marginLeft="80dp"
 android:id="@+id/thirdtableview"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="View"/>
 </LinearLayout>
 <LinearLayout
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_marginTop="40dp"
android:layout_marginLeft="30dp"
 android:orientation="horizontal">
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="Employee search :"
 android:textSize="18sp"
 />
 </LinearLayout>
 <LinearLayout
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_marginLeft="0dp"
 android:layout_marginTop="20dp">
 <EditText
 android:id="@+id/ed_pesearch"
 android:layout_width="180dp"
 android:layout_height="wrap_content"
 android:hint="Enter project number"/>
 </LinearLayout>
 <Button
 android:id="@+id/pseasrch"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_marginTop="10dp"
 android:layout_marginLeft="100dp"
 android:text="Search"/>
</GridLayout>
Java code:
package com.example.myapplication;
import androidx.appcompat.app.AppCompatActivity;
import android.annotation.SuppressLint;
import android.app.AlertDialog;
import android.content.Context;
import android.content.DialogInterface;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.view.View.OnClickListener;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
public class MainActivity extends AppCompatActivity 
implements OnClickListener {
 SQLiteDatabase db;
 EditText 
pno,pname,ptype,duration,eid,ename,qualification,joinda
te,psearch;
 Button b1,b2,b3,b4,b5,b6,b7;
 @Override
 protected void onCreate(Bundle savedInstanceState) 
{
 super.onCreate(savedInstanceState);
 setContentView(R.layout.activity_main);
 pno = (EditText) findViewById(R.id.ed_pno);
 pname = (EditText) findViewById(R.id.ed_pname);
 ptype = (EditText) findViewById(R.id.ed_type);
 duration = (EditText) 
findViewById(R.id.ed_duration);
 eid = (EditText) findViewById(R.id.ed_eid);
 ename = (EditText) findViewById(R.id.ed_ename);
 qualification = (EditText) 
findViewById(R.id.ed_qualification);
 joindate = (EditText) 
findViewById(R.id.ed_joindate);
 psearch = (EditText) 
findViewById(R.id.ed_pesearch);
 b1 = (Button) findViewById(R.id.addbtn);
 b2 = (Button) findViewById(R.id.viewbtn);
 b3 = (Button) findViewById(R.id.addemp);
 b4 = (Button) findViewById(R.id.viewemp);
 b5 = (Button) findViewById(R.id.pseasrch);
 b6 = (Button) findViewById(R.id.thirdtableadd);
 b7 = (Button) 
findViewById(R.id.thirdtableview);
 db = openOrCreateDatabase("assignment2", 
Context.MODE_PRIVATE, null);
 db.execSQL("CREATE TABLE IF NOT EXISTS 
project(pno number primary key, pname VARCHAR, ptype 
VARCHAR,duration number);");
 db.execSQL("CREATE TABLE IF NOT EXISTS 
employee(eid number primary key, ename VARCHAR,
qualification VARCHAR,joindate number);");
 //db.execSQL("CREATE TABLE IF NOT EXISTS 
pro_emp(p_no number foreign key references 
project(pno),e_id number foreign key references 
employee(eid));");
 db.execSQL("CREATE TABLE IF NOT EXISTS 
pro_emp(p_no number REFERENCES project(pno), e_id 
number REFERENCES employee(eid))");
 b1.setOnClickListener(this);
 b2.setOnClickListener(this);
 b3.setOnClickListener(this);
 b4.setOnClickListener(this);
 b5.setOnClickListener(this);
 b6.setOnClickListener(this);
 b7.setOnClickListener(this);
 }
 public void showMessage(String title,String 
message)
 {
 AlertDialog.Builder builder=new 
AlertDialog.Builder(this);
 builder.setCancelable(true); 
builder.setTitle(title);
 builder.setMessage(message);
 builder.show();
 }//show
 public void clearText()
 {
 pno.setText("");
 pname.setText("");
 ptype.setText("");
 duration.setText("");
 //e_pid.setText("");
 //e_jdate.setText("");
 //e_quali.setText("");
 //e_name.setText("");
 pno.requestFocus();
 }//clear
 public void onClick(View view){
 if (view == b1) {
 if 
(pno.getText().toString().trim().length() == 0 || 
pname.getText().toString().trim().length() == 0 || 
ptype.getText().toString().trim().length() == 0||
duration.getText().toString().trim().length()==0) {
Toast.makeText(this, "\"please enter 
the values", Toast.LENGTH_SHORT).show();
 return;
 }
 db.execSQL("INSERT INTO project VALUES('" +
pno.getText() + "','" + pname.getText() + "','" + 
ptype.getText() + "','" + duration.getText() + "');");
 //db.execSQL("INSERT INTO emp VALUES('" + 
e_id.getText() + "','" + e_name.getText() + "','" + 
e_quali.getText() + "','" + e_jdate.getText() + "');");
 //db.execSQL("INSERT INTO pro_emp VALUES('"
+ e_pid.getText() + "','" + e_id.getText() + "');");
 showMessage("Success", "Record added");
 //11clearText();
 }//b1
 if(view==b2)
 {
 Cursor c = db.rawQuery("SELECT * FROM 
project",null );
 if(c.getCount() == 0){
 Toast.makeText(MainActivity.this," No 
Records found",Toast.LENGTH_SHORT).show();
 return;
 }
 StringBuilder b = new StringBuilder();
 while(c.moveToNext()){
 b.append("Project 
no :").append(c.getString(0)).append("\n");
 b.append("Project 
name :").append(c.getString(1)).append("\n");
 b.append("Project 
type:").append(c.getString(2)).append("\n");
 
b.append("Duration :").append(c.getString(3)).append("\
n");
 }
 Toast.makeText(MainActivity.this, 
b.toString(), Toast.LENGTH_LONG).show();
 }////b2
 if(view==b3)
 {
 try {
 if
(eid.getText().toString().trim().length() == 0 || 
ename.getText().toString().trim().length() == 0 || 
qualification.getText().toString().trim().length() == 0
|| joindate.getText().toString().trim().length() == 0) 
{
 Toast.makeText(MainActivity.this, 
"Some fields are empty!!", Toast.LENGTH_SHORT).show();
 return;
 }
 db.execSQL("INSERT INTO employee 
VALUES('" + eid.getText() + "','" + ename.getText() + 
"','" + qualification.getText()+ "','" + 
joindate.getText()+ "');");
 Toast.makeText(MainActivity.this, 
"Record Inserted successfully!!", 
Toast.LENGTH_SHORT).show();
 }
 catch (Exception e){
 Toast.makeText(MainActivity.this, 
e.toString(), Toast.LENGTH_SHORT).show();
 return;
 }
 }//b3
 if(view==b4)
 {
 Cursor c = db.rawQuery("SELECT * FROM 
employee",null );
 if(c.getCount() == 0){
 Toast.makeText(MainActivity.this," No 
Records found",Toast.LENGTH_SHORT).show();
 return;
 }
 StringBuilder b = new StringBuilder();
 while(c.moveToNext()){
 b.append("Employee 
id:").append(c.getString(0)).append("\n");
 b.append("Employee 
name :").append(c.getString(1)).append("\n");
 
b.append("Qualification:").append(c.getString(2)).appen
d("\n");
 b.append("Join 
Date:").append(c.getString(3)).append("\n");
}
 Toast.makeText(MainActivity.this, 
b.toString(), Toast.LENGTH_LONG).show();
 }//b4
 if(view==b5)
 {
 Cursor c=db.rawQuery("SELECT eid,ename FROM
employee,project,pro_emp where 
employee.eid=pro_emp.e_id and project.pno=pro_emp.p_no 
and pno='"+psearch.getText()+"'",null);
 if(c.getCount()==0)
 {
 showMessage("Error","No Records 
Found");
 return;
 }//getcount
 StringBuffer b=new StringBuffer();
 while(c.moveToNext())
 {
 b.append("e_id:"+c.getString(0)+"\n");
 b.append("e_name:"+c.getString(1)+"\
n");
 ;
 }//while
 showMessage("Employee 
Details",b.toString());
 }//b5
 if(view==b6) {
 try {
 db.execSQL("INSERT into pro_emp 
values('" + pno.getText() + "','" + eid.getText()+ 
"');");
 Toast.makeText(MainActivity.this, 
"Record inserted successfully!!", 
Toast.LENGTH_SHORT).show();
 } catch (Exception e) {
 Toast.makeText(MainActivity.this, 
e.toString(), Toast.LENGTH_SHORT).show();
 }
 }//b6
 if(view==b7)
{
 Cursor c = db.rawQuery("SELECT * FROM 
pro_emp",null );
 if(c.getCount() == 0){
 Toast.makeText(MainActivity.this," No 
Records found",Toast.LENGTH_SHORT).show();
 return;
 }
 StringBuilder b = new StringBuilder();
 while(c.moveToNext()){
 b.append("Project 
no :").append(c.getString(0)).append("\n");
 b.append("Employee 
id :").append(c.getString(1)).append("\n");
 }
 Toast.makeText(MainActivity.this, 
b.toString(), Toast.LENGTH_LONG).show();
 }
 }//click
}//class







DATABASE Q.5)

XML code:
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout 
xmlns:android="http://schemas.android.com/apk/res/andro
id"
 xmlns:app="http://schemas.android.com/apk/res-auto"
 xmlns:tools="http://schemas.android.com/tools"
 android:layout_width="match_parent"
 android:layout_height="match_parent"
 tools:context=".MainActivity">
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t1"
 android:text="ID :"
 android:textSize="20sp"
 android:layout_marginTop="30dp"
 android:layout_marginLeft="20dp"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_marginTop="18dp"
 android:layout_marginLeft="80dp"
 android:id="@+id/eid"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t2"
 android:text="Name:"
 android:textSize="20sp"
 android:layout_marginTop="20dp"
 android:layout_marginLeft="20dp"
 android:layout_below="@id/t1"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_marginTop="60dp"
 android:layout_marginLeft="90dp"
 android:id="@+id/ename"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t3"
 android:text="Duration:"
android:textSize="20sp"
 android:layout_marginTop="20dp"
 android:layout_marginLeft="20dp"
 android:layout_below="@id/t2"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_marginTop="110dp"
 android:layout_marginLeft="110dp"
 android:id="@+id/eduration"/>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/t4"
 android:text="Description:"
 android:textSize="20sp"
 android:layout_marginTop="20dp"
 android:layout_marginLeft="20dp"
 android:layout_below="@id/t3"/>
 <EditText
 android:layout_width="200dp"
 android:layout_height="wrap_content"
 android:layout_marginTop="160dp"
 android:layout_marginLeft="140dp"
 android:id="@+id/edescription"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/badd"
 android:text="Add"
 android:layout_below="@id/t4"
 android:layout_marginTop="15dp"
 android:layout_marginLeft="20dp"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/bdel"
 android:text="Delete"
 android:layout_below="@id/badd"
 android:layout_marginTop="15dp"
 android:layout_marginLeft="20dp"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/bup"
android:text="Update"
 android:layout_below="@id/bdel"
 android:layout_marginTop="15dp"
 android:layout_marginLeft="20dp"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/bview"
 android:text="View all"
 android:layout_below="@id/bup"
 android:layout_marginTop="15dp"
 android:layout_marginLeft="20dp"/>
</RelativeLayout>
Java code:
package com.example.myapplication;
import androidx.appcompat.app.AppCompatActivity;
import android.annotation.SuppressLint;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.content.Context;
import android.database.sqlite.SQLiteDatabase;
import android.database.Cursor;
import android.view.View;
import android.view.View.OnClickListener;
import android.app.AlertDialog.Builder;
import android.widget.Toast;
public class MainActivity extends AppCompatActivity 
implements OnClickListener
{
 EditText id,name, dur,des;
 Button b1,b4,b2,b3;
 SQLiteDatabase db;
 String title,message;
 @SuppressLint("MissingInflatedId")
 @Override
 protected void onCreate(Bundle savedInstanceState) 
{
super.onCreate(savedInstanceState);
 setContentView(R.layout.activity_main);
 id=(EditText) findViewById (R.id.eid);
 name=(EditText) findViewById(R.id.ename);
 dur = (EditText) findViewById(R.id.eduration);
 des=(EditText) findViewById(R.id.edescription);
 b1=(Button) findViewById(R.id.badd);
 b4=(Button) findViewById(R.id.bview);
 b2=(Button) findViewById(R.id.bdel);
 b3=(Button) findViewById(R.id.bup);
 b1.setOnClickListener(this);
 b2.setOnClickListener(this);
 b3.setOnClickListener(this);
 b4.setOnClickListener(this);
 
db=openOrCreateDatabase("Course",Context.MODE_PRIVATE, 
null);
 db.execSQL("CREATE TABLE IF NOT EXISTS 
course(id VARCHAR,name VARCHAR,dur VARCHAR,des 
VARCHAR);");
 showMessage("Success","Table Created");
 }
 public void showMessage(String title,String 
message)
 {
 Builder builder=new Builder(this);
 builder.setCancelable(true);
 builder.setTitle(title);
 builder.setMessage(message);
 builder.show();
 }
 public void clearText()
 {
 id.setText("");
 name.setText("");
 dur.setText("");
 des.setText("");
 id.requestFocus();
 }
 @Override
 public void onClick(View view){
 if(view==b1)
 {
 
if(id.getText().toString().trim().length()==0||
name.getText().toString().trim().length()==0|| 
dur.getText().toString().trim().length()==0||
des.getText().toString().trim().length()==0)
 {
 Toast.makeText(this,"please enter the 
value",Toast.LENGTH_SHORT).show();
 return;
 }
 db.execSQL("insert into course 
values('"+id.getText()+"','"+name.getText()
+"','"+dur.getText()+"','"+des.getText()+"');");
 showMessage("Success","Record added");
 clearText();
 }
 if (view==b4)
 {
 Cursor c=db.rawQuery("select * from 
course",null);
 if(c.getCount()==0)
 {
 showMessage("Error","No Record Found");
 return;
 }
 StringBuffer b=new StringBuffer();
 while(c.moveToNext())
 {
 b.append("Course id:"+c.getString(0)+"\
n");
 b.append("Course 
name:"+c.getString(1)+"\n");
 b.append("Course 
duration:"+c.getString(2)+"\n");
 b.append("Course 
description:"+c.getString(3)+"\n");
 }
 showMessage("Course Details",b.toString());
 }
 if(view==b2)
 {
 
if(id.getText().toString().trim().length()==0)
 {
 showMessage("Error","Please Enter the 
Employee ID");
return;
 }
 Cursor c=db.rawQuery("select * from course 
where id='"+id.getText()+"'",null);
 if(c.moveToFirst())
 {
 db.execSQL("delete from course where 
id='"+id.getText()+"'");
 showMessage("Success","Record 
Deleted");
 }
 else
 {
 showMessage("Error","Invalid Course 
ID");
 }
 clearText();
 }
 if(view==b3)
 {
 
if(id.getText().toString().trim().length()==0)
 {
 showMessage("Error", "Please enter the 
course id");
 return;
 }
 Cursor c=db.rawQuery("select * from course 
where id='"+id.getText()+"'",null);
 if(c.moveToFirst())
 {
 db.execSQL("update course set 
name='"+name.getText()+"',dur='"+dur.getText()+"'where 
id='"+id.getText()+"'");
 showMessage("Success","Record 
Modified");
 }
 else
 {
 showMessage("Error","Invalid Course 
ID");
 return;
 }
 }
clearText();
 }
}
