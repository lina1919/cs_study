
## IEEE 802.11 wireless LANs("Wi-Fi")

802.11b
- 2.45GHz unlicensed spectrum
	- 누구든지 가서 쓸 수 있다.
- direct sequence spread spectrum(DSSS) in physical layer
	- 모든 host들이 동일한 chipping code를 가짐
	
802.11a, 802.11g, 802.11n 등 종류 다양
- 모두 다중 접속에 **CSMA/CA** 사용
- 모두 base station과 ad-hoc 네트워크 버전이 있음

### 802.11 LAN architecture
- wireless host는 base station으로 소통
	- base station = access point(AP)
	- AP 공유기 같은거
- Basic Service Set(BSS)

### 802.11 : Channels, association
- host : AP와 반드시 associate 해야함
	- SSID와 MAC address
	- DHCP 프로토콜 AP의 ip address를 얻는다.

### 802.11 : passive/active scanning
- passive scanning : 수동적, host는 가만히 있고 AP에서 beacon 신호를 주기적으로 보냄
- active scanning : host 자체가 능동적으로 신호를 보냄(Probe Request), AP는 Probe Response가 옴


### IEEE 802.11: multiple access
- avoid collision
	- wired는 collision detection 가능
	- wireless는 detection 불가능 -> avoid 해야함
- 충돌 방지를 하려면 detection X -> aviod!!
	- CSMA/CA

### IEEE 802.11 MAC Protocol: CSMA/CA
802.11 sender
1. channel idle 감지하면(DIFS 동안) 그러면 보냄
2. busy 하면 backoff algorithm을 돌려서 일정시간 기다린 다음 다시 보냄

802.11 receiver
1. ACK를 SIFS 이후에 보냄

-> 이 방식으로 **aviod collision**

### Avoiding collisions (more)
- Collision avoidance를 100프로 보장
- **channel reservation**
	- RTS(request-to-send) base station에 보내고 기다림
	-  BS는 CTS(clear-to-send) 보내서 확인
	- Data send
	- BS에서 ACK 보내서 끝난 거 확인
![Pasted image 20230531152237](https://github.com/lina1919/cs_study/assets/63230463/13b26bb1-0cc5-4c14-be6c-810e378d53fd)


### 802.11: mobility within same subnet
- 동일한 네트워크라면 부여받은 IP address를 가지고 그대로 옮겨감
- self learning을 통해서
- 즉, 이동성을 지원한다.

### 802.11: advanced capabilities
Power Management , 즉 energy management
배터리 문제
1. 에너지 효율을 높이는 것(화공과)
2. 있는 배터리를 어떻게 더 잘쓸까(컴공과)
	1. 사용하지 않을 때는 sleep mode
	2. 사용하지 않을 때는 active mode

### 802.15: personal area network
- 802.15 = Buletooth
- 반경 10m 이하에서 wireless 통신
- leader가 있고 follower 가 있다.


## Cellular Internet Access

### Components of cellular network architecture
1. Cell
	- 일정 거리 이상만 띄워져 있으면 같은 주파수 사용 가능
	- 문제는 사람들이 움직인다면? -> hand off mobility issue
	- 낮은 파워로 같은 주파수 사용
2. MSC
	- Mobile switching Center
	- call connection & mobility 담당
-> first hop을 wireless, 그 이후는 wired로 함

### Cellular networks: the first hop
1. CDMA
2. TDMA/FDMA
	1. 2개를 섞어서 보냄

### 2G (voice) network architecture

### 3G (voice+data) network architecture
- 둘이 분리 시킴

### 3G versus 4G LTE network architecture
- 4세대 에서는 동일한 core 망을 사용
- MME HSS

## Principles: addressing and routing to mobile users

### What is mobility?

![Pasted image 20230531155944](https://github.com/lina1919/cs_study/assets/63230463/8c148e72-5c9e-4ab4-ae6c-7d2ff82797bc)


### Mobility: approaches
- 라우터에게 handle 하게 함
	- 택도 없는 소리
- end-systems 에게 handle 하게 함
	- edge node에 있는 애들에게 담당하게 함
		1. indirect routing
			1. home network에 연결해서 home network가 연결하게 함
			2. triangle routing
		2. direct routing

### Mobility: registration
indirect routing
특정한 permanet address 가지는 애가 저기에 가있다고 알림.
#### Mobility via indirect routing
![Pasted image 20230531160655](https://github.com/lina1919/cs_study/assets/63230463/6aee856f-39db-46b1-9da5-90de1b601442)


### Indirect Routing: comments
- mobile는 2개의 address를 씀
	- permanent address
		- transparent 보장(layering approach할때처럼) : permanent address만 가지면 그걸로 통신할 수 있다. 안에서 무슨 일이 일어나는지 몰라도.
	 - care-of -address
 - 단점 : 비효율

### Mobility via direct routing
![Pasted image 20230531160717](https://github.com/lina1919/cs_study/assets/63230463/c3bd9f17-fbc0-4275-be9d-68ad97583b23)

하지만 단점.
그새 못참고 옮기면??
![Pasted image 20230531160753](https://github.com/lina1919/cs_study/assets/63230463/6b71fcee-3c0d-478a-8a77-e7ed982a7862)

- 맨 처음 방문한 foreign agent를 anchor agent라고 정의
- anchor 가 서로 연결해줌

- non transparent to correspondent
	- 그 안의 정보를 빼와서 care-of-address로 접속

## Mobile IP
- three components to standard
	- indirect routing of datagrams
	- agent discovery
	- registration with home agent
![Pasted image 20230531161314](https://github.com/lina1919/cs_study/assets/63230463/e2fca538-2874-4217-981d-00992f1293cc)

