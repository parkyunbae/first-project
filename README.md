# ![CCTV AIoT Project](https://example.com/your_image.png) <!-- 여기에 실제 이미지 URL을 넣으세요 -->

## AI 스마트 CCTV 시스템 프로젝트 (8월 22일 ~ 8월 30일)

---

### 프로젝트 개요
AI 기반의 스마트 CCTV 시스템을 구축하는 것을 목표로 합니다. 다양한 기능을 통해 사용자에게 편리하고 안전한 환경을 제공합니다.

### 사용 기술
- **Android Studio**
- - **Firebase Authentication**
- **IntelliJ IDEA**
- **Arduino**
- **Python**

---

### 프로젝트 계획

1. **리모콘 기능 (UDP 통신: 서버(PC), 클라이언트(안드로이드))**: 1~2일
2. **음성 인식 기능 (SpeechToText: text -> 서버(PC, ChatGPT 파이썬 연동))**: 2일
3. **통화 기능 (SIP 프로토콜)**: 2일
4. **Webcam IP Streaming (Java OpenCV 라이브러리 이용)**: 1일

---

### 프로젝트 목표
- 사용자 친화적인 인터페이스 제공
- 실시간 모니터링 및 통화 기능 구현
- AI 기술을 활용한 고급 기능 추가


## 로그인 XML

로그인 화면의 배경을 그라데이션으로 꾸미며 제작하였습니다.

![로그인 화면](https://github.com/user-attachments/assets/1cbaf535-1cb5-42de-a000-0ca1e01425d5)

### 그라데이션 배경 설정

아래의 XML 코드를 사용하여 그라데이션 배경을 설정합니다.

```xml
<!-- res/drawable/background_gradient.xml -->
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <gradient
        android:startColor="#BBDEFB"
        android:endColor="#E1F5FE"
        android:angle="90"/>
</shape>
```
## 로그인 기능

### LoginActivity.java

```java
package kr.co.example.myapplication;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;

public class LoginActivity extends AppCompatActivity {

    private EditText emailEditText;
    private EditText passwordEditText;
    private Button loginButton;
    private Button registerButton;
    private FirebaseAuth mAuth;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);

        mAuth = FirebaseAuth.getInstance();

        emailEditText = findViewById(R.id.emailEditText);
        passwordEditText = findViewById(R.id.passwordEditText);
        loginButton = findViewById(R.id.loginButton);
        registerButton = findViewById(R.id.registerButton);

        loginButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String email = emailEditText.getText().toString().trim();
                String password = passwordEditText.getText().toString().trim();

                if (email.isEmpty() || password.isEmpty()) {
                    Toast.makeText(LoginActivity.this, "이메일과 비밀번호를 입력해주세요.", Toast.LENGTH_SHORT).show();
                    return;
                }

                mAuth.signInWithEmailAndPassword(email, password)
                        .addOnCompleteListener(LoginActivity.this, new OnCompleteListener<AuthResult>() {
                            @Override
                            public void onComplete(@NonNull Task<AuthResult> task) {
                                if (task.isSuccessful()) {
                                    Toast.makeText(LoginActivity.this, "로그인 성공!", Toast.LENGTH_SHORT).show();
                                    Intent intent = new Intent(LoginActivity.this, MainActivity.class);
                                    startActivity(intent);
                                    finish();
                                } else {
                                    Toast.makeText(LoginActivity.this, "로그인 실패: " + task.getException().getMessage(), Toast.LENGTH_SHORT).show();
                                }
                            }
                        });
            }
        });

        registerButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(LoginActivity.this, RegisterActivity.class);
                startActivity(intent);
            }
        });
    }
}
```
