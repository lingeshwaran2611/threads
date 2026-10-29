# 13. Develop an Android Application Demonstrating Threads and Handlers for Background Processing

## Project Name: `ThreadHandlerDemo`

## Aim
To develop an Android application that demonstrates the use of Threads and Handlers for background processing and updating the user interface after the background task is completed.

## Technologies Used
- **Programming Language:** Java
- **IDE:** Android Studio
- **UI Design:** XML
- **Threading:** Java Thread
- **Handler:** Android Handler and Looper

## Project Structure

```text
ThreadHandlerDemo/
├── app/
│   └── src/
│       └── main/
│           ├── java/
│           │   └── com/
│           │       └── example/
│           │           └── threadhandlerdemo/
│           │               └── MainActivity.java
│           ├── res/
│           │   └── layout/
│           │       └── activity_main.xml
│           └── AndroidManifest.xml
└── README.md
```

---

## 1. `activity_main.xml`

**Location:** `app/src/main/res/layout/activity_main.xml`

This XML file defines a Button to start the background task and a TextView to display the result.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="20dp">

    <Button
        android:id="@+id/btnStart"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Start Background Task" />

    <TextView
        android:id="@+id/txtResult"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="22sp"
        android:paddingTop="20dp" />

</LinearLayout>
```

---

## 2. `MainActivity.java`

**Location:** `app/src/main/java/com/example/threadhandlerdemo/MainActivity.java`

This Java class creates a background Thread, simulates work for three seconds, and uses a Handler to update the TextView on the main UI thread.

```java
package com.example.threadhandlerdemo;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.widget.Button;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    Button btnStart;
    TextView txtResult;

    Handler handler = new Handler(Looper.getMainLooper());

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btnStart = findViewById(R.id.btnStart);
        txtResult = findViewById(R.id.txtResult);

        btnStart.setOnClickListener(v -> {

            // Background Thread
            Thread thread = new Thread(() -> {

                try {
                    // Simulate Background Work
                    Thread.sleep(3000);

                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                    return;
                }

                // Update UI using Handler
                handler.post(() -> {
                    txtResult.setText(
                        "Background Task Completed"
                    );
                });
            });

            thread.start();
        });
    }
}
```

---

## 3. `AndroidManifest.xml`

**Location:** `app/src/main/AndroidManifest.xml`

The manifest declares the main activity. No Internet permission is required for this practical.

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <application
        android:allowBackup="true"
        android:label="ThreadHandlerDemo"
        android:supportsRtl="true"
        android:theme="@style/Theme.ThreadHandlerDemo">

        <activity
            android:name=".MainActivity"
            android:exported="true">

            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>

        </activity>

    </application>

</manifest>
```

**Note:** The theme name must match the theme defined in your Android Studio project. If it differs, keep your existing theme reference.

---

## 4. How to Run the Application

1. Open Android Studio.
2. Create a new Android project named `ThreadHandlerDemo`.
3. Select **Java** as the programming language.
4. Set the package name to `com.example.threadhandlerdemo`.
5. Replace the code in `activity_main.xml` with the XML code provided above.
6. Replace the code in `MainActivity.java` with the Java code provided above.
7. Check that the theme reference in `AndroidManifest.xml` matches your project.
8. Run the application on an emulator or Android device.
9. Click the **Start Background Task** button.
10. After approximately three seconds, the message `Background Task Completed` appears.

---

## 5. Expected Output

### Initial Screen

```text
+----------------------------------+
|                                  |
|                                  |
|    [ Start Background Task ]     |
|                                  |
|                                  |
+----------------------------------+
```

### After Clicking the Button

After approximately three seconds, the TextView displays:

```text
Background Task Completed
```

---

## 6. Working of the Application

1. The application starts and displays the button and TextView.
2. When the user clicks the button, a new background Thread is created.
3. The Thread simulates a long-running task using `Thread.sleep(3000)`.
4. After the background task finishes, the Handler posts a Runnable to the main UI thread.
5. The TextView is updated with the completion message.

### Flowchart

```text
        Start Application
                |
                v
        Display Main Screen
                |
                v
       Click Start Task Button
                |
                v
       Create Background Thread
                |
                v
       Perform Background Work
          (3 Second Delay)
                |
                v
         Handler.post()
                |
                v
       Update TextView on UI
                |
                v
               End
```

---

## 7. Key Concepts

- **Thread:** Executes work separately from the main UI thread.
- **Background Processing:** Performs work without blocking the user interface.
- **Handler:** Sends tasks to a message queue associated with a Looper.
- **Looper.getMainLooper():** Obtains the main thread's Looper.
- **handler.post():** Schedules a Runnable to execute on the main thread.
- **Thread.sleep(3000):** Simulates a three-second background task.
- **runOnUiThread alternative:** Another way to schedule UI updates from a background thread.

---

## 8. Result

Thus, an Android application demonstrating Threads and Handlers for background processing was developed successfully. The background task runs on a separate Thread, and the Handler updates the TextView on the main UI thread after the task is completed.
