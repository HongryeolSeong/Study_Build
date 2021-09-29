# 프로그램 동작 순서
![순서](https://t1.daumcdn.net/cfile/tistory/99E473355EC0FF5A07)

### 전처리
#include, #define, typedef, extern 과 같은 것들이 정의되어 실행되는 단계.   
main함수 위에 등록 된다.

### 컴파일
실제로 호출되고 사용되는 부분만 번역.   
어셈블리어(기계어)로 번역한다.

### 어셈블
다음 단계인 링킹에서 링커가 여러개의 바이너리 파일을 하나의 실행 파일로 묶게 되는데,   
각 바이너리의 정보를 효과적으로 파악하기 위해   
일정한 규칙을 갖게 형식화하여 목적파일을 생성한다.

### 링킹
만들어진 목적 파일들을 하나로 묶어 실행 파일을 만든다.   
링커는 목적 파일들과 프로그램에서 사용된 표준 C 라이브러리, 사용자 라이브러리들을 링크한다.

<br>

# 라이브러리
자주 사용되는 특정한 기능을 main 함수에서 분리시켜 놓음으로써,   
프로그램을 유지, 디버깅을 쉽게하고 컴파일 시간을 좀더 빠르게 할 수 있다.

<br>

## 1. 정적 라이브러리 Windows - .lib, Linux - .a
컴파일시 적재돼서 실행 파일에 라이브러리의 내용이 모두 들어간다.   

#### 장점
1. 런타임시 외부를 참조할 필요가 없어 속도가 빠르고 성능이 좋다.
2. 라이브러리를 따로 배포할 필요가 없다.

#### 단점
1. 같은 코드를 가진 여러 프로그램 실행시 메모리가 낭비된다.
2. 라이브러리 수정시 적용된 프로그램을 다시 재배포해야한다.

<br>

### 라이브러리 생성 및 적용
#### 1. Windows
1. 라이브러리의 헤더파일과 소스 코드를 작성한다.   
![1](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/1.png) ![2](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/2.png)
2. 빌드하여 .lib을 생성한다.   
![28](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/28.png)
3. 라이브러리를 적용할 프로젝트를 만들고, 디렉터리를 추가한다.   
속성 -> C/C++ -> 일반 -> 추가 포함 디렉터리 에 헤더파일 경로 입력   
속성 -> 링커 -> 일반 -> 추가 라이브러리 디렉터리 에 라이브러리 경로 입력   
속성 -> 링커 -> 입력 -> 추가 종속성 에 라이브러리 파일명 입력
4. 해당 프로젝트를 빌드 및 실행한다.   
![4](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/4.png)   
![5](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/5.png)

<br>

#### 2. Linux
1. 라이브러리의 헤더파일과 소스 코드를 작성한다.   
![6](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/6.png) ![7](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/7.png)
2. 목적 파일을 생성한다.   
![8](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/8.png)   
![9](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/9.png)
3. 정적 라이브러리 파일을 생성한다.   
![10](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/10.png)   
![11](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/11.png)
4. 라이브러리를 적용할 소스 코드를 만들고, 컴파일을 거쳐 실행 파일을 만들고 실행한다.   
![12](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/12.png)   
![13](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/13.png)   
![15](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/15.png)

<br>

## 2. 동적 라이브러리 Windows - .dll, Linux - .so
여러 프로그램이 공통적으로 필요로 하는 기능들을 프로그램과 분리하여 필요할 때에만 불러내어 쓸 수 있게 만들어 놓은 것.

#### 장점
1. 메모리가 절약된다.
2. 쉽게 수정이 가능하다. -> 출시 후 지원이 가능하다.

#### 단점
1. 필요할 때마다 라이브러리가 메모리에 로드되어서 속도가 느리고 성능이 낮아질 수 있다.
2. 실행 파일 배포시 라이브러리도 함께 배포해야 한다.

<br>

### 라이브러리 생성 및 적용
#### 1. Windows
1. 라이브러리의 소스 코드를 작성한다.   
![16](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/16.png)
2. 빌드하여 .dll과 .lib(정적 라이브러리의 .lib과 다르다)을 생성한다.   
![17](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/17.png)
3. 라이브러리를 적용할 프로젝트를 만들고, 디렉터리를 추가한다.   
속성 -> 디버깅 -> 환경 에 .dll 경로 입력   
속성 -> 링커 -> 일반 -> 추가 라이브러리 디렉터리 에 .lib 경로 입력   
속성 -> 링커 -> 입력 -> 추가 종속성 에 .lib 파일명 입력
4. 해당 프로젝트를 빌드 및 실행한다.   
![18](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/18.png)   
![19](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/19.png)

<br>

#### 2. Linux
1. 라이브러리의 소스 코드를 작성한다.   
![20](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/20.png)
2. 목적 파일을 생성한다.   
![21](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/21.png)   
![22](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/22.png)
3. 동적 라이브러리 파일을 생성한다.   
![23](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/23.png)   
![24](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/24.png)
4. 라이브러리 경로에 라이브러리를 추가한다.
![25](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/25.png)   
위 처럼 해도 되고, /usr/lib 디렉토리에 .so를 복사해도 된다(안될시 둘 다 할 것).
5. 라이브러리를 적용할 소스 코드를 만들고, 컴파일을 거쳐 실행 파일을 만들고 실행한다.   
![26](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/26.png)   
![27](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/27.png)   
![14](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/14.png)

<br>
