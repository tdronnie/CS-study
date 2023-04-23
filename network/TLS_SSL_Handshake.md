# TLS_SSL_Handshake

## SSL과 TLS
### SSL
Secure Socket Layer, 넷스케이프사에서 개발한 인터넷 보안 프로토콜
<br>
컴퓨터 네트워크에 통신 보안을 제공하기 위해 설계된 암호 규약이다.

SSL의 흐름은 공개키 비밀키로 종단간 대칭키를 생성 및 공유하고, 그 이후에 대칭키로 암호화하여 전송한다. 


SSL의 취약성이 알려지고 IETF가 업데이트를 제안하면서 TLS로 바뀌었다.

### TLS
이전 암호화 프로토콜인 SSL에서 발전한 것이다.
<br>네트워크 레이어의 TCP/IP 네트워크를 사용하는 통신에 적용되고 통신과정에서 종단간 보안과 데이터 무결성을 확보해준다.


### handshake
SSL(TLS가 최신이지만 SSL이라고 많이 사용)은 두 통신 장치에 handshake를 수행해서 정보보호와 데이터 무결성을 제공한다.


![image](https://user-images.githubusercontent.com/69182630/233798028-d39610cb-dca1-41e7-83cf-88f205b8866f.png)


1. client는 "client hello"라는 메세지와 암호화된 정보(버전, 암호 알고리즘, 압축 방식 등)를 보낸다


2. server는 "server hello"라는 메세지와 cipher suite, CA 인증서(서버 공개키 담김)를 보낸다.
   
   cf. cipher suite -> 암호화 스위트, 프로토콜, 암호화 방식 등 통신에 이용할 여러가지 알고리즘 집합


3. client가 server의 CA 인증서를 확인한다.(CA목록을 통해 server의 공개키 얻기)


4. CA 인증서로 신뢰 확보 후 난수 바이트를 생성해 인증서로부터 얻은 서버의 공개키로 암호화하여 보낸다.
   (서버가 인증서 요구 시 클라이언트 인증서와 클라이언트 비밀키로 암호화된 임의의 바이트 문자열도 하나 보낸다.)


5. server는 client 인증서 확인 후 난수 바이트를 자신의 비밀키로 복호화한다. 그리고 대칭키 생성에 사용한다.


6. handshake 완료. client에서 "finished" 메세지와 지금까지 보낸 교환내역 해싱 후 대칭키로 암호화해서 보낸다.


7. server도 교환내역 해싱 후 비교, 일치하면 "finished" 메세지 대칭키로 암호화한 후 보낸다.


8. client는 메세지를 대칭키로 복호화해서 신뢰받은 사용자임을 인지, 그 후부터 대칭키로 데이터를 주고받는다.


### SSL/TLS의 약점

종단간 데이터 교환이 일어나므로 정보유출, DDos, APT, 악성코드들의 공격에는 무력화된다.



### 참고
https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/TLS%20HandShake.md