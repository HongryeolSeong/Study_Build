# Makefile을 이용한 빌드
리눅스 환경에서 실행 파일을 만들시(IDE없이) 대상 소스코드들이 많을 경우,   
컴파일 시간이 오래걸리고 매번 명령어 입력하기 힘들어진다.   
-> Makefile을 이용하여 make 명령어 한 번으로 컴파일을 가능하게 한다.

<br>

## Incremental build
명령어들을 모아 놓은 쉘 스크립트를 이용한 빌드와 다른 성격의 빌드.   
1. make 명령 시 목적 파일과 소스 코드의 마지막 수정 시간을 비교한다.
2. 목적 파일의 수정시간이 더 나중이다. -> 컴파일 하지 않는다.
3. 소스 코드의 수정시간이 더 나중이다. -> 컴파일 실행한다.   

소스코드 수정 시 빌드 과정에서 변경된 소스코드에 의존성이 있는 대상들만 추려서 빌드한다.   
-> 파일 하나만 바뀌어도 전체 파일을 컴파일하는 쉘 스크립트와 달리 빠르게 빌드가 가능하다.

<br>

## Makefile의 기본 형식
```
Target: Dependencies   
(탭)Recipe   
```
Target = 만들고자하는 파일   
Dependencies = Target을 make할 때 필요한 파일 목록   
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
gcc -c foo.c => $(CC) -c foo.c
```

<br>

다음과 같이  가능하다.   
![2](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m2.png)  ![3](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m3.png)   

<br>

## clean 및 PHONY
clean을 이용하여 상황에 따라 목적 파일 및 실행 파일 삭제가 가능하다.
```
clean:
  rm -f *.o
  rm -f $(TARGET)
```
만약 디렉터리 내에 clean이라는 이름의 파일이 있는 경우, 위의 명령이 실행 되지 않는다.   
이 상황을 방지하기 위해 다음 코드를 넣는다.   
```
.PHONY: clean
```
적용시 다음과 같다.   
![3](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m3.png)  ![9](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m9.png)   

<br>

## 예제
![ex](https://www.tuwlab.com/files/attach/images/2382/193/027/7e9501d245506aae63834478c8b28917.png)   

![4](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m4.png)   
![5](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m5.png)  ![6](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m6.png)   
![7](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m7.png)  ![8](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m8.png)   

<br>

위 파일들을 컴파일 및 링크하여 실행 파일 app.out을 만든다.   
이용할 Makefile은 다음과 같다.   
![9](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m9.png)   

<br>

make하고 실행 파일을 실행시킨 결과이다.   
![11](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m11.png)  ![10](https://github.com/HongryeolSeong/Study_Build/blob/main/refimg/m10.png)

<br>
