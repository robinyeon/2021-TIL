## 프로그래밍 언어 & 운영체제(OS)
### 컴파일러
- 컴퓨터와 인간 중간에 컴파일러라는 프로그램을 만듦
- 의사소통이 안되는 인간과 컴퓨터 사이에서 인간의 요구를 컴퓨터에 전달

### IDE(Integrated Development Environment)
- 통합 개발 환경: 개발을 하기 위한 모든 것들을 제공해주는 환경
- 문서 작업을 위해 한컴이나 워드 사용하는 것처럼 코딩에 필요한 다양한 기능들이 들어있고, 그 기능들을 통해 쉽게 코드를 만들 수 있음
- e.g. 안드로이드 스튜디오 for Android, 엑스코드 for iOS 등


### 프로그래밍 언어
- 개발자들은 기존의 것을 발전시키거나 새로운 것을 만들기 좋아하기에 
  - e.g. C언어가 발전(개선)해서 Objective-C, C++, 파이썬
- 저수준(컴퓨터 친화적 언어) vs 고수준(인간 친화적 언어)
  - 저수준: 인간은 배우기 어렵겠지만 컴퓨터 입장에서는 구체적으로 적혀있으니 일하기 쉬우니 낮은 사양에서도 원활히 작동
  - 고수준: 인간이 학습하긴 쉽지만 그만큼 컴퓨터가 더 많이 고민해야하니 저수준 언어보다 작동이 느림
  - 사실 요즘 우리가 쓰는 컴퓨터들은 사양이 아주 좋아서 고수준 언어로 쓰인 문서도 충분히 돌아감
  - 그럼 저수준 언어는 어디서 쓰이는가?: 컴퓨터 사양을 낮춰 가격이 저렴해지면 이득인 경우 e.g. IPTV 셋톱박스 내 컴퓨터

### 컴퓨터의 구성요소
- CPU: 머리
- RAM(메모리): CPU의 개인 작업 공간
- HDD, SDD(보조기억장치): 창고. 전원이 꺼져도 이 안의 데이터는 남아있음. 느림
  - 이 부품들을 메인보드에 끼워서 조립 컴퓨터를 만들 수 있는 것
- 보조기억장치에서 '실행에 필요한 데이터'를 메모리에 올려주고, 이덕분에 CPU가 메모리 위에서 빠르게 작업수행 가능

### 운영체제(OS)
- CPU, RAM 등 이 모든것이 낯선이유: 운영체제(Operating System)가 모든 과정을 대신해주기 때문
- 윈도우: C#, Visual Basic, C++, JavaScript, ...
- 맥OS, iOS: Objective-C -> Swift
- 안드로이드: JAVA, Kotlin

## JAVA
- 과거엔 운영체제의 종류가 훨씬 다양해서 개발자가 배워야하는 프로그래밍 언어도 굉장히 많았음
- 10개의 운영체제에서 하나의 버그를 수정하려면 같은 작업을 각 언어로 10번씩 해야만 함
- 이 문제를 자바라는 프로그래밍 언어가 해결: 운영체제에 독립적인 언어
- JVM(Java Virtual Machine)
  - 자바를 만든 팀은 각 운영체제 위애 JVM이라는 소프트웨어를 만듦
  - 사용자가 자신의 컴퓨터에 JVM을 설치하면 운영체제별로 여러개의 프로그램을 만들 필요없이 자바로만 만들면 됨
- 자바 이외에도 다양한 언어(e.g. 파이썬)가 이러한 방식을 취하고 있음
- 단점: 속도가 느리다. 운영체제 위에 프로그램을 올리고, 그 위에 또 프로그램을 돌리는 것이기 때문.
- **모바일의 경우는 PC와 다름**
  1. 현재 모바일 운영체제는 iOS와 안드로이드가 시장 양분. 이 때문에 JVM같은 컨셉에 대한 니즈가 적음(프로그래밍 언어 2개만 알면 되니까)
  2. 모바일의 크기는 PC보다 작기에 용량이나 성능에 제한이 있음. JVM 같이 프로그램 위에 프로그램을 돌린다면 속도 저하
  3. 애플과 구글의 시장 영향력 유지위한 행보


## 네트워크, 클라이언트, 서버

## Ubuntu
