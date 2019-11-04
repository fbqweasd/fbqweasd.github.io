---
layout: post
title: talloc 라이브러리 (1)
author:     UKC
tags: 프로그래밍 C/C++ 리눅스 
subtitle: talloc으로 메모리 할당하기
category: talloc
---

이번에는 talloc으로 메모리를 heap 영역에 할당하고 talloc에 장점인 트리구조를 이용하여 메모리 해제 해보도록 하겠습니다.

# context 생성

talloc은 트리구조로 구성을 할 수 있기 때문에 최상단 노드 역할을 하는 친구를 만들어 관리를 하는 것이 편합니다.

{% highlight C %}
#include <talloc.h>

int main(){
	
	--- 코드 ---	

}
{% endhighlight %}

위 코드는 talloc 에서 튜토리얼용으로 만든 코드 입니다. 이 코드로 talloc의 계층구조를 설명하려고 합니다. 

![talloc](/img/2019-10-04/talloc.png)

포스팅을 하는 도중에 talloc 메인페이지가 고장 나서 복구되는 동안 포스팅을 잠시 준비 하겠습니다...ㅜ
