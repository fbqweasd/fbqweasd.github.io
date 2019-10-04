---
layout: post
title: talloc 라이브러리 (1)
author:     UKC
tags: 프로그래밍 C/C++ 리눅스 
subtitle: talloc으로 메모리 할당하기
category: 리눅스
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
