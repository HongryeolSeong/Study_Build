# 빌드의 유형
소스코드 작업 후 빌드 시 작업 진행 상태에 따라 적용시켜야하는 모드가 달라진다.   
1. 아직 개발이 진행중이어서 디버깅이 계속 필요한 소스코드 -> Debug mod
2. 디버깅이 완료되어 릴리즈가 가능한 소스코드 -> Release mod

###### + 라이브러리 링킹시 빌드하고자하는 환경(32bit or 64bit)에 따라 맞게 링킹할 것

## 1. Debug
1. 디버깅 정보를 넣기 때문에 실행 파일 크기가 크다.
2. 컴파일 속도가 빠르다.
3. 코드 실행 속도가 느리다.
<br>

### 리눅스 환경에서 Debug 모드 설정 과정은 다음과 같다.
1. 빌드할 소스코드를 생성한다.   
![1](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/n1.png)
<br>

2. 컴파일러를 이용하여 실행 파일을 생성한다.   
![2](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/n2.png)   
위와 같이 컴파일시 -g 옵션을 추가하여 실행 파일에 디버깅 정보를 삽입한다.
<br>

app_01은 다음과 같이 gdb 디버거를 통해 디버깅이 가능하다.   
![5](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/n5.png)

<br>

## 2. Release
1. 디버깅 정보가 없고 코드를 최적화하기 때문에 실행 파일 크기가 작다.
2. 최적화 과정이 있으므로 컴파일 속도가 느리다.
3. 코드 실행 속도가 빠르다.
<br>

### 리눅스 환경에서 Release 모드 설정 과정은 다음과 같다.
1. 빌드할 소스코드를 생성한다(Debug 소스코드와 동일).   

<br>

2. 컴파일러를 이용하여 실행 파일을 생성한다.   
![3](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/n3.png)   
위와 같이 -O 옵션을 추가하여 코드를 최적화함으로써 Release 파일을 생성한다.   
<br>

다음처럼 파일 크기가 차이나는 것을 볼 수 있다(app_01: 디버그 모드, app_02: 릴리즈 모드).   
![4](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/n4.png)

<br>

## 3. 출력파일 정리
일반적으로 출력파일(.exe, .lib)은 다음과 같이 정리한다.   
<br>

![1](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/o1.png)   
   ㅣ   
![2](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/o2.png)   
   ㅣ   
![3](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/o3.png) ![3](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/o3.png) 
<br>
<br>

## Visual Studio 컴파일러와 비교한 gcc 컴파일러
리눅스에서의 빌드와 동일하게 Visual Studio에서의 빌드 역시 여러 옵션을 이용하여 진행된다.

#### 최적화
리눅스에서는 $ gcc -O 형식으로 빌드시 최적화를 하게되는데,   
Visual Studio에서는 프로젝트속성 - 구성속성 - C/C++ - 최적화 탭에 보면   
/Od, /O1, /O2, /Ox 옵션을 볼 수 있다. 뒤로 갈 수록 최적화 수준이 높아진다.

#### 경고 메세지 수준
리눅스에서의 $ gcc -Wall 을 이용한 경고 수준 설정은   
Visual Studio에서 프로젝트속성 - 구성속성 - C/C++ - 일반 에 경고 수준 탭에서 설정 가능하다.   
/W0, /W1, /W2, /W3, /W4, /Wall이 있고, 뒤로 갈 수록 경고 메시지의 수준이 높아진다.

#### 옵션 확인
프로젝트속성 - 구성속성 - C/C++ - 명령줄 을 확인해보면   
빌드시 적용되는 전체 옵션들을 확인할 수 있다.
