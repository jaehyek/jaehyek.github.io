---
layout: post
title:  "BOOK-TCP/IP 쉽게 더 쉽게-03"
categories: CCNA
comments: true
tags:  TCP-IP
author: Jaehyek
---

# 보안 프로토콜 적용하기
- HTTPS : HTTP + SSL/TLS을 적용한 것
- VPN : 통신 거점간의 통신을 통째로 암호화하는 방식하므로 app별로 암호화하지 않아도 된다.


#### 공유키 : 하나의 키로 암호화/복호화가 가능한 방법
- 키를 공유할 모든 사람에게 공유해야 하므로 부담이 되는 방법

#### 공개키 : 암호화키와 복호화키를 세트로 관리
- 개인키(비밀키) : 자신이 가지는 키
- 공개키 : 상대방에게 전달하는 키.
- 공개키와 개인키의 사용절차
![001](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/001.JPG)

#### 전자인증서 : 사용자가 본인이라는 것을 증명
![002](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/002.JPG)
![003](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/003.JPG)
![004](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/004.JPG)

- PKI ( Public Key Infrastructure ) 
- CA ( Certification Authority ) : 한국정보인증, 코스콤, 한국전자인증, 한국무역정보통신, 금융결재원

#### 전자서명  : 데이터가 위변조 되지 않았다는 것을 증명
- 반드시 개인키로 암호화 한다.
- 개인키로 암호화한 데이터는 공개키로 복호화할 수 있다
![005](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/005.JPG)
![006](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/006.JPG)

#### 이메일을 안전하게 전달 : S/MIME
- secure /Multipurpose Internet Mail Extenstion 
- 이메일을 암복호화 할때는 공개키와 공유키를 조합 사용한다. 
![007](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/007.JPG)


- 공유키 방식을 조합하는 이유 : 
- 이메일 본문을 공개키 방식으로 암복호화하는 것보다 공유키 방식으로 암복호화하는 것이 연산처리에서 부담이 적다

#### SSL / TLS
- SSL ( Secure Sockets Layer), TLS(Transport Layer Secure)
![008](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/008.JPG)

- HTTPS : SSL/TLS을 사용한다.
![009](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/009.JPG)

- SSL은 넷스케이프 커뮤니케이션즈가 개발하였고, IETF(Internet Engineering Task Force)는 이것을 TLS 로 퓨준화 후에 기존의 SSL을 대체하였다.
- TSL 대신 SSL이라고 부르는 경우가 많다.

#### SSH ( Secure Shell )
- 원격지의 컴퓨터를 제어하기 위해 
- 공개키와 공유키를 조합하여 사용.
- 전자인증서를 사용하지 않는다.
![010](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/010.JPG)
![011](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/011.JPG)

#### 방화벽
![012](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/012.JPG)

#### 무선랜 보안
- WEP(Wired Equipment Privacy), WPA(Wi-fi Protected Access)
![013](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/013.JPG)

- 암복호화 하기 위해 공유키를 사용한다.
- WPA2에서는 블록 암호화 방식을 사용한다
![014](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/014.JPG)

##### 패스프레이즈
- 키 = 패스프레이즈(사용자가 지정한 문자열) + 초기화벡터(조금씩 변화는 값)
- 암호화는 쉽고, 복호화는 어렵다
![015](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/015.JPG)
![016](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/016.JPG)

### VPN
- Virtual Private Network 
![017](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/017.JPG)
-IPSec(Security Architecture for Internet Protocol)
- PPTP(Point to Point Tunneling Protocol)

![018](/img/2017-01-14-CCNA-book-TCP-IP-easy-and-easy-03/018.JPG)


