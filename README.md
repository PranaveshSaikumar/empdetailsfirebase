
# Ex.No:1 To create a employee details fields and to display the employee details using Firebase Database in Android Studio.


## AIM:

To create and display the employee details using Firebase Database in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as HelloWorld and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display the employee details in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the DatabaseTable using the firebasedatabase”.
Developed by: Pranavesh Saikumar
Registeration Number : 212223040149
*/
```
## ACTIVITY MAIN:
```
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fillViewport="true">

    <LinearLayout
        android:orientation="vertical"
        android:padding="16dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <EditText
            android:id="@+id/etId"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="@string/hint_id"
            android:inputType="text"
            android:importantForAutofill="no" />

        <EditText
            android:id="@+id/etName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="@string/hint_name"
            android:inputType="textPersonName"
            android:importantForAutofill="no" />

        <EditText
            android:id="@+id/etDept"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="@string/hint_dept"
            android:inputType="text"
            android:importantForAutofill="no" />

        <EditText
            android:id="@+id/etSalary"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="@string/hint_salary"
            android:inputType="number"
            android:importantForAutofill="no" />

        <Button
            android:id="@+id/btnSave"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="16dp"
            android:text="@string/save_employee" />

        <TextView
            android:id="@+id/tvDisplay"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="24dp"
            android:textSize="18sp"
            android:textColor="@android:color/black" />

    </LinearLayout>
</ScrollView>
```
## STRINGS.XML:
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">MyEx11</string>

    <string name="hint_id">Employee ID</string>
    <string name="hint_name">Employee Name</string>
    <string name="hint_dept">Department</string>
    <string name="hint_salary">Salary</string>
    <string name="save_employee">Save Employee</string>
</resources>
```
## EMPLOYEE.JAVA:
```
package com.example.myex11;

public class Employee {

    public String id;
    public String name;
    public String dept;
    public String salary;

    public Employee() {
        // Required empty constructor for Firebase
    }

    public Employee(String id, String name, String dept, String salary) {
        this.id = id;
        this.name = name;
        this.dept = dept;
        this.salary = salary;
    }
}
```
## MAIN ACTIVITY.JAVA:
```
package com.example.myex11;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;
import com.google.firebase.database.ValueEventListener;

public class MainActivity extends AppCompatActivity {

    EditText etId, etName, etDept, etSalary;
    Button btnSave;
    TextView tvDisplay;

    DatabaseReference databaseReference;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        etId = findViewById(R.id.etId);
        etName = findViewById(R.id.etName);
        etDept = findViewById(R.id.etDept);
        etSalary = findViewById(R.id.etSalary);
        btnSave = findViewById(R.id.btnSave);
        tvDisplay = findViewById(R.id.tvDisplay);

        databaseReference = FirebaseDatabase.getInstance().getReference("Employee");

        btnSave.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                String id = etId.getText().toString();
                String name = etName.getText().toString();
                String dept = etDept.getText().toString();
                String salary = etSalary.getText().toString();

                Employee emp = new Employee(id, name, dept, salary);

                databaseReference.child(id).setValue(emp);

                tvDisplay.setText("Employee Saved Successfully");
            }
        });

        // Display Data from Firebase
        databaseReference.addValueEventListener(new ValueEventListener() {
            @Override
            public void onDataChange(DataSnapshot snapshot) {

                String data = "";

                for (DataSnapshot ds : snapshot.getChildren()) {
                    Employee emp = ds.getValue(Employee.class);

                    if (emp != null) {
                        data += "ID: " + emp.id + "\n";
                        data += "Name: " + emp.name + "\n";
                        data += "Dept: " + emp.dept + "\n";
                        data += "Salary: " + emp.salary + "\n\n";
                    }
                }

                tvDisplay.setText(data);
            }

            @Override
            public void onCancelled(DatabaseError error) {
            }
        });
    }
}
```

## OUTPUT

<img width="1915" height="653" alt="image" src="https://github.com/user-attachments/assets/5a243f81-83c5-4ab0-a495-f455bbfabe0c" />




## RESULT
Thus a Simple Android Application create a firebase database and to display the employee details using Firbase Real Time Database in Android Studio is developed and executed successfully.
