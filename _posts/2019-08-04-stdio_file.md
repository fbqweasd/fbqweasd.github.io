---
layout: post
title: 파일 표준 입출력
author:     UKC
tags: 프로그래밍 C/C++
subtitle: stdio로 파일 입출력 
category: C/C++
---

시스템 프로그램밍을 공부하면서 처음 배울땐 엄청 쉽게만 생각했던 <stdio.h> 라이브러리에 쉬우면서 강력한 기능이 있는 것을 알고 감동하여 배우고 있는 것을 정리해 보려고 합니다.

먼저 stdio에서 파일관련 부분에서 강력함을 느껴서 이번 글에서는 파일 포인터와 스트림, 읽고 쓰는 방법을 적어보려고 합니다.

## 파일 포인터 

표준 입출력 함수를 사용하지 않을 경우에는 파일 디스크립터 라는 개념으로 파일에 접근을 하지만 표준 입출력에서는 파일 포인터라는 개념으로 접근 합니다. 

파일 포인터는 __시스템 프로그래밍__ 에서 말하는 파일 디스크립터를 직접적으로 다루지 않고 라이브러리 내부적으로 파일 디스크립터를 제어할 수 있게 만들어진 개념입니다.

`FILE` 이라는 자료형(구조체)을 사용해서 선언을 할 수 있으며, 포인터 형식으로 선언을 하고 뒤에 나오는 여러 함수를 사용하여 파일 스트림을 만들고 다양한 쓰기, 읽기, 잘라내기 등의 작업을 할 수 있습니다.

{% highlight C %}
FILE *input;
{% endhighlight %}

## fopen()

fopen이라는 함수는 앞서 이야기한 파일 포인터에 직접적으로 파일을 연결하는 역할을 합니다.

{% highlight C %}
FILE *input;
fopen("test.txt","r");
{% endhighlight %}

위의 예제 처럼 각 인자 값은 __경로, 파일 모드__ 를 입력 받습니다.

파일 모드는 

인자 값 | 모드
|:----------|:---------:|
r   | 읽기 목적 | 
r+   | 읽기 + 쓰기 | 
w   | 쓰기 | 
w+   | 쓰기 + 읽기 | 
a    | 덧붙이기 상태에서 쓰기 모드 |
a+  | 덧붙이기 상태에서 쓰기 모드 +읽기 |

쓰기 모드로 선언이 된 경우에 파일이 없을 시 자동으로 생성이 됩니다.

## fclose()

스트림을 열고 파일에 작업을 다 하고 난 뒤 스트림을 닫아주는 역할을 하는 함수가 `fclose()` 함수 입니다.

{% highlight C %}
int fclose(FILE *stream)
{% endhighlight %}

이 함수를 사용하여 파일 작업이 끝난 후 스트림을 닫아 아직 버퍼에 남아있는 데이터를 처리 하는 역할을 합니다.

예제는 아래 코드에서 확인해 주세요

### fcloseall()

이 함수는 현재 프로세스에서 사용되고 있는 모든 입출력 스트림을 닫는 역할을 합니다. 

* 단) 리눅스에서만 사용가능

# 파일에 쓰고 읽기

표준 입출력을 사용하여 파일에 읽고 쓰는 작업을 하면 사용자 버퍼를 사용하여 입출력을 하기 때문에 큰 노력 없이도 효과적으로 입출력을 할 수 있습니다.

물론 사용자 버퍼가 의도치 않게 사용하기 때문에 중요한 데이터를 쓰고 나면 동기화 시켜주는 작업을 하는 것도 신경을 써야 합니다.

## 읽기
* fgetc()
 
 이 함수는 스트림에서 한 글자를 읽어오는 함수 입니다. 

{% highlight C %}
// fgetc() 함수 예제
#include <stdio.h>

int main()
{
	int c;
	FILE* stream = fopen("text.txt", "r");

	c = fgetc(stream);
	if (c == EOF) {
		// Error
	}
	else {
		printf("%c \n", (char)c);
	}
}
{% endhighlight %}

이 함수에서 에러나 파일 끝을 알 수 있도록 EOF를 반환 하기 때문에 int 형으로 입력을 받아야 합니다.

* fgets()

{% highlight C %}
#include <stdio.h>

int main()
{
	char buf[50];
	FILE* stream = fopen("text.txt", "r");

	if (!fgets(buf, 50, stream)) {
		// Error
	}

	printf("%s",buf);
}
{% endhighlight %}

fgets() 함수는 buf에 최대값 -1 만큼의 값을 저장하는 함수 입니다. 값을 읽는 도중에 마지막 비트를 읽으면 버퍼 마지막에 NULL 문자를 저장하고
개행 문자를 만나면 개행문자 ("\n")을 저장하고 함수를 종료합니다. 

