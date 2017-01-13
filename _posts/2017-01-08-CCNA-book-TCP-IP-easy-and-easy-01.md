---
layout: post
title:  "BOOK-TCP/IP 쉽게 더 쉽게-01"
categories: CCNA
comments: true
tags:  TCP-IP
author: Jaehyek
---


# 대표적인 프로토콜 
![001](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/001.JPG)

# HTTP 응답과 상태코드 
![002](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/002.JPG)
![003](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/003.JPG)

# TCP Port 번호의 범위와 주요 port 번호
![004](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/004.JPG)
![005](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/005.JPG)

# TCP Header 구조 와 컨트롤 비트 
![006](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/006.JPG)
![007](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/007.JPG)

# UCP Header 구조  
![008](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/008.JPG)

# IPv4 Header 구조  
![009](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/009.JPG)

# 좁은 길을 지나갈 때는 작게 분할해서 지나간다.
- 한번에 지나갈 수 있는 데이터 크기를 MTU(Maximum Transmissin Unit )
- 데이터를 분할하고 복원하는 방법
![010](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/010.JPG)

# IPv6 및 IPv6로 갈아타기.
![011](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/011.JPG)
![012](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/012.JPG)

# IPv6 = network + host 
![013](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/013.JPG)
![014](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/014.JPG)

# IPv6 할당하기
![015](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/015.JPG)

# 퍼블릭 IP 관리
- ICANN ( Internet Corporation for Assigned Names and Numbers )
- KRNIC ( Korea Network Informatin Center )
![016](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/016.JPG)

# routing protocol
- BGP, OSPF, RIP
- 라우터는 서로 누구와 연결이 되어 있는지 정보 교환
![016](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/016.JPG)

- default router : 라우팅 테이블에 목적지의 address가 없는 경우, 사용하는 기본 라우터

### Dynamic Routing Algorithm

1. Distance Vector Type 
  - RIP (Routing Information Protocol )을 이용, 짧은 경로 선택
  - 비교적 간단한 설정.
2. Link Status Type
  - OSPF ( Open Shortest Path First ) 을  이용하여 네트워크의 통신 상태를 map으로 관리하고  상태가 좋은 경로 선택.
  - 복잡하고 변화가 잦은 네트워크에 적합.
3. AS(자율시스템)내에서 OSPF을 사용
   - 네트워크를 몇개의 영역으로 나누어 OSPF을 사용.
4. AS 내에서 BGP을 사용
   - BGP ( Border Gateway Protocol )을 AS내에서 사용. 경로 벡터형.
   - 경로 벡터형은 경로의 정보와 AS의 정보를 함께  사용하여 정보를 만든다

AS 번호 : IP address 처럼, 16bit 혹은 32bit 으로 활당하고, 전세계적으로 중복되지 않게 관리.

# 네트워크의 오류를 통보하는 프로토콜 : ICMP ( Internet Control Message Protocol )
데이터 전송중에 문제가 생길 경우 장애 상태를 통보하기 위해 사용.

### 주요 ICMP의 메세지
![017](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/017.JPG)

# 어드레스 변환
가정이나 사무실에서 사용하는 프라이빗 IP은 퍼블릭IP와 통신을 하지 못한다. 
이 때, 어드레스의 변환이 필요한데 NAT( Network Address Translation )을 사용한다. 
NAT은 IP4와 IP6의 변환에도 사용한다.

![018](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/018.JPG)

### NAT에서 발생가능한 제약 사항
- 내부의 호스트가 공교롭게도 같은 port 번호를 사용할 경우 라우터는 구별하지 못한다.

![019](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/019.JPG)

- 외부에서 온 데이터를 전달하지 못 한다.

![020](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/020.JPG)

- NAPT ( Network Address Port Translation )을 사용한다.
- 이는 address와 port을 함께 사용하여 변환한다.

### 외부에서 접속이 가능하게 하려면
- 대부분 내부에서 메세지 도착여부를 정기적으로 확인하는 방법으로 구현된다.

### 포트 포워딩 ( port forwarding )
- LAN안에 웹서버나 FTP 처럼 외부에 서비스를 공개해야 할 때가 있다. 이 때, 라이터의 특정 port로 들어오면
 내부의 특정 서버로 전달하게 한다.
 
# 도메인명 
![021](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/021.JPG)

- DNS 서버에 질의하기
![022](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/022.JPG)

### DNS 서버의 계층 구조
![023](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/023.JPG)

### 도메인 등록하기
![024](/img/2017-01-08-CCNA-book-TCP-IP-easy-and-easy/024.JPG)

# PING 으로 수신자의 통신상태 확인.
ping은 지정한 IP address으로 ICMP의 8번 메세지를 보내는 것이다. 
수신자는 ICMP 0번 메세지로 응답을 한다. 

# tracert 명령은 통신경로 확인하기 ( unix 에서는 traceroute )
ping 명령어와 비슷하게 ICMP 8번 메세지를 보낸다. 이 때, 생존기간을 1 부터 시작해서 1씩 증가시키면서
ICMP의 메세지를 확인하고 경로를 추적한다. 

# snlookup 명령으로 IP address을 알아내기
nslookup 명령은 DNS 서버에게 도메인명을 주고 IP 어드레스를 물어 보거나 거꾸로 IP 어드레스를 주고 도메인명을 물어 볼 때 사용한다.

