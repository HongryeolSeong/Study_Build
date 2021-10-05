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
