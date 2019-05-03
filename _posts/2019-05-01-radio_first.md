---
layout: post
title: 송신기 발진회로 구상
author:     UKC
tags: 전자회로 라디오 무선통신
subtitle: NE555 칩 집중 공부
category: 라디오
---

학교 `프로젝트 실무` 시간에 공중파 라디오 신호를 잡을 수 있는 라디오 만드는 것을 기획해서 여러가지를 공부하면서 준비를 하였습니다. 하지만 휴대폰 FM라디오에 아무런 신호가 잡히지 않는 것을 보고 주제를 살짝 틀어 FM라디오에 신호를 보낼 수 있는 라디오 송신기를 만들기로 하였습니다.

## 발진 회로

휴대폰에서 잡을 수 있는 라디오의 신호가 85Mh에서 108Mh 정도의 신호를 잡을 수 있기 때문에 소리를 변조할 고주파의 신호가 필요한 것을 알았습니다.

제가 알고 있는 발진회로는

* 멀티바이브레터
* RC 발진회로 
* Transistor Oscillator

이 정도만 알고 만들기 힘들거나 너무 낮아 사용이 불가능한 회로가 많아서 NE555라는 타이머 칩을 사용하여 RF회로를 만들기로 하였습니다.

## NE555 타이머 

NE555 타이머는 일정한 시간 마다 주기를 만들어 출력을 할 수 있는 타이머 칩입니다. 

아직 실제로 사용을 하지는 않았지만 데이터시트와 블로그 글을 보고 타이머 회로를 설계 해보았습니다.

![NE555 회로](/img/2019_05_01/NE555.png)

*아직 회로를 만들어서 실험 해보지 않아서 제대로 동작하지 않을 수 있습니다*

저 회로에 있는 NE555의 칩은 핀번호대로 아래의 기능을 가지고 있습니다.

	1. GND
	2. TR (TRIGGER) : 단자가 접지(-신호)가 물리면 타이머의 작동이 시작
	3. Q (OUTPUT) : 타이머에서 신호가 나오는 핀
	4. R (RESET) : 접지 시키고 전압을 걸면 타이머가 RESET됨
	5. CV (CONTROL VOLTAGE) : 타이머 동작을 안정화 시키는 핀(일반적인 상황에선 사용안해도됨) 
	6. THR (THRESHOLD) : 출력 전압에 저항을 연결하고 핀에 물려서 입력전압에 2/3이 넘으면 타이머 종료 - 펄스 폭 제어용
	7. DIS (DISCHARGE) : 커패시터 방전용 핀 - 가끔씩 듀티사이클을 다르게 설정할때 사용함
	8. VCC

이 타이머는 저항과 커패시터의 용량으로 주기를 결정하는데 제가 만든 회로에서는 반주기당

**T = 0.69 x R x C** 의 공식을 가지고 있어서 한 주기는 **T =2 x 0.69 x R x C**이라는 공식이 성립할 거라고 생각합니다. 

*실제 회로로 실험 해보는 것은 나중에 부품이 도착하면 제대로 진행을 해보겠습니다.*

### 참고 링크

공부하면서 참고를 한 여러 사이트의 링크입니다.

http://urin79.com/blog/19227658

https://murcielrago.tistory.com/8

https://tapito.tistory.com/160