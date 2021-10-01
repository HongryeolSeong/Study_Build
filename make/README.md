# Makefile을 이용한 빌드
리눅스 환경에서 실행 파일을 만들시(IDE없이) 대상 소스코드들이 많을 경우,   
컴파일 시간이 오래걸리고 매번 명령어 입력하기 힘들어진다.   
-> Makefile을 이용하여 make 명령어 한 번으로 컴파일을 가능하게 한다.

<br>

## Incremental build
명령어들을 모아 놓은 쉘 스크립트를 이용한 빌드와 다른 성격의 빌드.   
#### make 명령 시 목적 파일과 소스 코드의 마지막 수정 시간을 비교한다.
1. 목적 파일의 수정시간이 더 나중이다. -> 컴파일 하지 않는다.
2. 소스 코드의 수정시간이 더 나중이다. -> 컴파일 실행한다.   

소스코드 수정 시 빌드 과정에서 변경된 소스코드에 의존성이 있는 대상들만 추려서 빌드한다.   
-> 파일 하나만 바뀌어도 전체 파일을 컴파일하는 쉘 스크립트와 달리 빠르게 빌드가 가능하다.

<br>

## Makefile의 기본 형식
```
Target: Dependencies   
(탭)Recipe   
```
Target = 만들고자하는 파일   
Dependencies(prerequisites) = Target을 make할 때 필요한 파일 목록   
Recipe = Target을 make할 때 실행되는 명령어   

<br>

뒤에 소개할 규칙들을 적용한   
전체적인 통상 패턴은 다음과 같다.
```
CC=<컴파일러>
CFLAGS=<컴파일 옵션>
LDFLAGS=<링크 옵션>
LDLIBS=<링크 라이브러리 목록>
OBJS=<Object 파일 목록>
TARGET=<빌드 대상 이름>
 
all: $(TARGET)
 
clean:
    rm -f *.o
    rm -f $(TARGET)
 
$(TARGET): $(OBJS)
    $(CC) -o $@ $(OBJS)
```

<br>

## 내장 규칙
자주 사용되는 빌드 규칙들은 내장을 해서 굳이 기술하지 않아도 자동으로 처리된다.   
소스 파일(.c)을 컴파일해서 Object 파일(.o)로 만들어 주는 규칙이 여기에 해당.   

<br>

다음과 같이 적용 가능하다.   
![1](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m1.png)  ![2](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m2.png)

<br>

## 변수 사용
Makefile 내 변수 지정이 가능하다.   
```
CC = gcc
```
사용시
```
$(CC) -c foo.c //gcc -c foo.c
```

<br>

다음과 같이  가능하다.   
![1](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m1.png)  ![3](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m3n.png)   

<br>

## clean 및 PHONY
clean을 이용하여 상황에 따라 빌드업 결과 파일 삭제가 가능하다.
```
clean:
  rm -f *.o       // 모든 목적 파일 삭제
  rm -f $(TARGET) // 생성된 타겟 파일 
```
만약 디렉터리 내에 clean이라는 이름의 파일이 있는 경우, 위의 명령이 실행 되지 않는다.   
이 상황을 방지하기 위해 다음 코드를 넣는다.   
```
.PHONY: clean
```
<br>

makefile에 다음의 코드를 하단에 넣는다.
```
.PHONY: clean
clean:
  rm -f *.o
  rm -f $(TARGET)
```

<br>

## 패턴
실제 프로젝트에서 사용될 수십, 수백개의 소스코드를 다루기 위해서,   
특정 조건에 부합하는 파일들에 대해 자동 변수를 이용하여 간단하게 recipe를 작성하게 도와준다.   
<br>

예를들어
```
foo.o: foo.c foo.h
    $(CC) $(CFLAGS) -c foo.c
    
bar.o: bar.c bar.h
    $(CC) $(CFLAGS) -c bar.c
```
를
```
%.o: %.c %.h
    $(CC) $(CFLAGS) -c $<
```
로 바꿀 수 있다.
<br>

#### 자동 변수
- %.o : 모든 .o를 타겟으로 지정하는 것이다.   
- % : 타겟의 파일 이름에 대응된다. // 만약 foo.o가 타겟이라면 Dependencies 부분의 %.c와 %.h는 foo.c와 foo.h가 된다.   
- $< : Dependencies의 첫 번째 파일에 대응된다.   
- $@ : 타겟 이름에 해당된다.   
- $^ : Dependencies 전체 목록에 해당된다.
- $? : 타겟보다 최신인 Dependencies들에 해당된다.
- $+ : $^ + 중복된 이름들까지 다 포함한다.

<br>

## 예제
![ex](https://www.tuwlab.com/files/attach/images/2382/193/027/7e9501d245506aae63834478c8b28917.png)   

![6](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m6.png)  ![8](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m8.png)   
![5](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m5.png)  ![7](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m7.png)  ![4](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m4.png)   
위 파일들을 컴파일 및 링크하여 실행 파일 app.out을 만든다.   
<br>

이용할 Makefile은 다음과 같다.   
![9](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m12.png)   

<br>

make하고 실행 파일을 실행시킨 결과이다.   
![11](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m11.png)  ![10](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m10.png)

<br>
