# 2장 애플리케이션 기본 구조

## <span style="background-color:#F5F5F5">1. 안드로이드 애플리케이션의 구성</span>

- 애플리케이션은 **컴포넌트**로 이루어진다. 
    - 컴포넌트 : 앱 내에서 <u>독립적인 실행 단위</u>이다. 
        - 인텐트(intent)를 매개로 정보를 주고 받음.
        
#### 📱 안드로이드의 4대 컴포넌트
    - **액티비티**(Activity)
        - UI 화면을 가지는 하나의 작업을 표시하는 컴포넌트
        - 사용자가 앱과 직접 상호작용할 수 있게 해준다.

    - **서비스** (Service)
        - 백그라운드에서 실행되는 컴포넌트
        - 사용자 인터페이스(UI)는 없으며, 액티비티 등 다른 컴포넌트에 의해 시작됨.

    - **방송 수신자** (Broadcast Receiver)
        - 서비스와 같이 UI를 가지지 않고 주로 이벤트 모델로 수행함.
        - 즉, 이벤트 발생 시 이를 수신하고 처리하는 컴포넌트

    - **컨텐츠 제공자** (Content Provider)
        - 데이터를 관리하고 다른 Application에게 제공하는 컴포넌트 등이 존재함.


* 자바와의 차이점
    - 컴포넌트를 class로 구현하지만, 해당 클래스의 생명주기는 *안드로이드*가 관리해준다.
       즉, 직접 객체를 생성하거나 소멸하는 것이 아닌, 시스템이 필요할 때 생성 및 제거를 한다.

---

#### <span style="background-color:#fff5b1">액티비티</span> (컴포넌트 중 하나)
- <u>사용자 인터페이스(UI) 화면을 가지는 하나의 작업을 표시</u>하는 컴포넌트임.
- 하나의 앱은 당연히 여러 액티비티를 가질 수 있음.
- 액티비티들이 모이면 **애플리케이션**이 된다.

> 액티비티 3개가 있다면, 각각 별도의 화면을 가진다.

<br>

#### <span style="background-color:#fff5b1">서비스</span> (컴포넌트 중 하나)
- **백그라운드에서 실행되는 컴포넌트**이다.
- 액티비티와 같은 다른 컴포넌트에 의해 시작이 됨. 
> ex. 음악 앱
- 사용자 인터페이스(UI)를 가지지 않음.
> 백그라운드 실행이므로


<br>

#### <span style="background-color:#fff5b1">방송 수신자</span> (컴포넌트 중 하나)
- **방송을 받고 반응**하는 컴포넌트 // 필수는 아님
> 주로 이벤트 모델로 수행한다.
- 서비스와 마찬가지로 사용자 인터페이스(UI)를 가지지 않음.
> ex. 배터리 상태(배터리가 10% 미만 -> 배터리가 부족합니다 알림), 통신 연결 등

<br>

#### <span style="background-color:#fff5b1">컨텐츠 제공자</span> (컴포넌트 중 하나)
- **애플리케이션 간 데이터를 공유**하기 위한 표준화된 인터페이스를 제공한다.
- 데이터를 관리, 다른 애플리케이션에게 제공하는 컴포넌트
> 데이터는 파일 시스템, SQLite 데이터베이스, 웹 등에 저장함.

  <br>

##### 앱을 개발할 때 4가지 컴포넌트를 전부 사용해야 할까?
> 당연히 아니며, 개발자가 필요로 하는 것을 사용하면 된다.
대개 액티비티가 핵심으로 작동한다.

---

#### <span style="background-color:#fff5b1">인텐트(Intent)</span>
앞에서 컴포넌트는 인텐트(Intent)를 매개로 정보를 주고 받는다고 했었음.
-> 인텐트란 무엇일까?  <br>
- 인텐트는 Intent 클래스의 객체로, 컴포넌트가 필요로 하는 요청 내용을 가짐.
    - 다른 앱에 무슨 컴포넌트가 있는지 모르니 Intent 를 사용해 가져오는 것.
> 앱 컴포넌트 간의 **의사소통 메시지**라고 생각하면 된다.

<br>


## <span style="background-color:#F5F5F5">2. 안드로이드 애플리케이션 작성 절차</span>
> 자바 파일은 **앱의 로직**을 나타냄
> XML 파일은 **앱의 사용자 인터페이스(UI)**를 나타냄

여기에 사운드와 이미 같은 <u>리소스(자원)</u>들이 추가된다.  <br>
1. 프로젝트 생성
2. 사용자 인터페이스 작성 (XML)
3. 자바 코드 작성(JAVA)
4. 매니페이스 파일 작성(XML)    → AndroidManifest.xml
5. ADV를 사용한 실행
  
**매니페스트 파일**
- 애플리케이션 안에 있는 컴포넌트들을 기술하고, 권한을 지정한다.
- 앱이 필요한 최소한의 API레벨을 선언하고 필요로 하는 하드웨어 사양을 선언한다.
  
**프로젝트 빌드 과정**
1. 프로젝트 구성 (Android Studio 이용)
2. 소스 컴파일
3. 패키징

> 빈 프로젝트를 만들면 아래와 같은 화면이 나온다.
![프로젝트생성이미지](img/Ch2/2-1appTest.PNG)
  
<br>

**MainActivity.java 소스 분석**
``` java
package com.example.myfirstapplication;  // 패키지 지정 문자

import androidx.appcompat.app.AppCompatActivity;    // 필요한 클래스를 포함시 켜는 import 문장들
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {   // MainActivity 클래스 정의, AppCompatActivity로부터 상속 받음

    @Override   // 어노테이션의 하나로 컴파일러에게 부모 클래스의 메소드를 재정의 했다는 것을 나타냄.
    protected void onCreate(Bundle savedInstanceState) { // 액티비티 생성될 때 딱 한번 호출. 모든 초기화와 UI 설정이 들어감.
        super.onCreate(savedInstanceState); // 상속 받은 클래스의 onCreate()를 호출하는 문장
        setContentView(R.layout.activity_main); // activity_main.xml을 화면에 보여주는 메서드
    }
}
```
  
**안드로이드에는 main()이 없다.**
    - 액티비티 별로 독립적으로 실행됨. → 어디서든 실행될 수 있다.
    - 액티비티 중에선 <u>onCreate() 메소드가 가장 먼저 실행됨.</u>

  <br>
---

## <span style="background-color:#F5F5F5">4. 리소스</span>
<u>3장은 프로젝트 생성이라 생략함.</u>  <br>
안드로이드에서 <u>레이아웃, 이미지, 문자열</u> 등은 리소스로 취급함.  <br>
    - 리소스들은 모두 XML을 이용해 정의됨.
    - app > res 폴더에 존재함.

안드로이드는 코드와 리소스를 분리하는 <u>이원적 구성</u>으로 되어있다.
    - **UI를 구현**하기 위해 XML기반 뷰를 사용하고
    - **세부적인 행위와 로직을 구성**하기 위해 자바를 사용한다.

  
#### <span style="background-color:#fff5b1">이원적 구성</span>은 개발자에게 이점을 제공함.
    1. 코드 분리 덕분에 디자이너와 개발자의 **분담 작업이 용이**
    2. 조건에 따라 레이아웃 통째 교체가 가능해 **호환성 확보 및 국제화에 유리**
        - 코드 하나로 여러 나라의 언어를 표현 가능
    3. 레이아웃만 수정할 땐 코드 컴파일이 필요 없어 **개발 속도가 빠름**
    4. 구조와 속성을 함축적으로 기술할 수 있으며, **레이아웃 재활용도 가능**

#### <span style="background-color:#fff5b1">레이아웃(layout)과 XML</span>
    - 레이아웃 : 화면을 어떻게 구성할 것이냐
    - XML의 구조는 기본적으로 **요소(Element)와 속성(Attribute)로 나누어 짐.

    - XML 문서에는 요소가 **반드시** 존재하여야 함.
    - 속성은 요소에 대한 추가 정보이다.

``` xml
<string name="hello">Hello World, Hello Android!</string>
```

##### 코드 설명
    <string name="hello"> : 시작태그
        - string : **요소**
        - name : **속성**
        - "hello" : **속성값**

    Hello World, Hello Android! : **요소 값**

    </string> : 종료태그

---

#### XML 속성
xmlns:android → XML 파일에서 항상 최외각 태그는 이 속성을 정의해야 함.  <br>
android:id → 유일한 아이디를 할당해서 참조할 수 있도록 한다.  <br>
android:layout_width → 화면에서 차지할 폭  <br>
android:layout_height → 화면에서 차지할 높이  <br>
android:text → 화면에 표시하는 텍스트를 설정  <br>

#### <span style="background-color:#fff5b1">안드로이드 네임스페이스</span>
    - XML namespace를 사용하는 이유
        1. 특정 태그가 **어떤 XML스키마 또는 라이브러리에 속하는지 구분**하기 위해서
        2. XML 문서에서 **이름 충돌을 방지**하기 위해서
    
    - 안드로이드는 ns를 사용하여 XML의 요소와 속성을 자바의 클래스와 메소드처럼 정의하였다.
  
``` xml
xmlns:android="http://..." <!-- 안드로이드 SDK에서 제공하는 기본 속성을 포함, 필수로 사용 -->
xmlns:app="http://..." <!-- 라이브러리 및 사용자 정의 속성을 위한 네임스페이스 -->
xmlns:tools="http://..." <!-- UI 미리보기에서 가독성을 높이거나 샘플 데이터 적용하는 용도로 사용 -->
```
  
#### 안드로이드 NS에서 적용하고 있는 <span style="background-color:#FFE6E6">XML 규칙</span>
    1. XML 요소는 반드시 안드로이드 클래스와 연관된 요소를 사용해야 함. 
        - 사전 정의된 <TextView> 같은 클래스. 새로운 버튼을 만든다 = 새로운 클래스를 정의한다.

    2. XML에서 사용하는 속성은 클래스의 메서드 또는 필드와 대응된다.
    
    3. 자바와 연관된 XML 속성은 'android:'라는 접두사로 시작해야함.

    4. XML 요소의 속성은 XML 계층 구조 내 부모 요소의 속성에 따라 결정됨.
        - 부모 속성에 따라 제한될 수 있는 것.
        - 부모 공간이 100x100이라면, 그 이상은 될 수 없다.


#### <span style="background-color:#fff5b1">문자열 리소스</span>
    - 문자열도 strings.xml에 기술하는 것이 바람직함.
        - 사용할 땐, android:text="@string/message"처럼 사용.
    
    이렇게 기술하면 레이아웃 수정이 간단해짐.


#### <span style="background-color:#FFE6E6">코드에서 리소스를 참조하는 방법</span>
    자바  프로그램에서 XML 문장을 사용하려면, 이를 **인스턴스화** 해주어야 함.

    요소별로 고유한 아이디를 부여해 개별적으로 구분해주어야 함.

---

## <span style="background-color:#F5F5F5">5. 그레이들</span>
- **그레이들(Gradle)**은 안드로이드의 <u>앱의 **빌드**(build) 및 종속성 관리를 담당하는 빌드 도구</u>임.
    - 빌드는 크게 신경쓸 필요가 없으나 SDK 버전에 따라 오류가 나기도 함.

#### 프로젝트 VS 모듈
    1. 프로젝트(My Application)
        - 안드로이드 개발의 최상위 단위이며, 여러 개의 모듈을 포함할 수 있음
        - 전반적인 설정 파일을 가짐
    
    2. 앱 모듈
        - 실제 애플리케이션의 코드, 리소스 및 프로젝트의 구성요소
        - SDK 버전, 의존성, 빌드 타입 등을 설정 가능
        - 모듈 간 의존성을 설정해 라이브러리 및 기능을 공유 가능

---

## <span style="background-color:#F5F5F5">6. 매니페스트 파일</span>
    - AndroidManifest.xml
    - 앱의 기본정보, 컴포넌트, 권한, 하드웨어 요구사항 등을 정의함.
    - 다른 액티비티 호출할 때 의미를 담아 보내는 것
    - 6장에서 사용할 예정



