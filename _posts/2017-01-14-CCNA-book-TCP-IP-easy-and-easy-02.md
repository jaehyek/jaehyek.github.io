---
layout: post
title:  "BOOK-TCP/IP 쉽게 더 쉽게-02"
categories: CCNA
comments: true
tags:  TCP-IP
author: Jaehyek
---

# 네트워크 인터페이스 
![001](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/001.JPG)

PPP : 전화회선을 사용해서 원격지와 접속
이더넷: UTP 케이블을 사용
ARP : IP address 를 이용하여 목적지의 MAC address 찾기

### MAC address
- Media Access Control 

![002](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/002.JPG)
![003](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/003.JPG)
![004](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/004.JPG)

### 이더넷
- 유선 LAN 규격
![005](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/005.JPG)

### 프리엠블 (preamble )
![006](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/006.JPG)

### 케이블 종류
![007](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/007.JPG)

### L2  스워치 : 접속된 상대만 인식
![008](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/008.JPG)

- broadcast 도메인 : broadcast address가 data가 도달할 수 있는 범위
 
### L3  스워치 : 인터넷계층까지 기능수행
- VLAN : 가상의 네트워크를 분할해서  지역을 나눈다. 통신효율을 높인다.
![009](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/009.JPG)

### 무선통신 규격
![010](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/010.JPG)

- 무선LAN  Frame 구조
![011](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/011.JPG)
![012](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/012.JPG)

### ARP ( Address Resolustion Protocol )
- 송신측은 수신 IP을 요청 패킷에 설정하고 브로드캐스트한다. 
- 명령어로 "ARP -a " : 캐시에 있는 것도 표시할 때.
![013](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/013.JPG)

- ARP Header
 - 헤더 내의 오퍼래이션 코드가 1:요청,  2:응답 
![014](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-02/014.JPG)

- 프락시 ARP : 호스트 대신, router가 ARP 기능을 하는 것.

### FTTx : 광섬유 케이블을 사용
### xDSL : 금속 케이블을 사용
### PPP : 컴퓨터와 1대1 로 통신



