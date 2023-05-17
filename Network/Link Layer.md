## 6.3 multiple access protocols

### Multiple access links, protocols
link에는 2가지 type 이 있다.
1. point-to-point
	- 독점적
	- 비효율적
2. broadcast
	- 공유하는 medium을 share 한다.
	- ex) 옛날 Ethernet, 802.11 wireless LAN

 - Broadcast channel을 한개만 쓰고 이를 공유하면 간섭(interference) 가 발생한다.
 - collision은 node가 2개 이상의 시그널을 같이 receive 하면 발생한다.
 - 이를 피하기 위해 **multiple access protocol** 이 나왔다.
	 - distributed algorithm(packet을 보낼 지 말지에 대해서 분산적으로 처리)
	 - out-of-band channel을 사용하지 않는다.

### 이상적인 Multiple Access Protocol
1. 하나의 노드가 데이터를 보내고 싶을 때 R bps의 처리율을 갖는다.
2. M개의 노드가 데이터를 보내고 싶을 때, R/M rate로 보낸다.
3. 완벽하게 분산(distributed)
	- master node가 없다.
	- synchronization 처리 X

### MAC(multiple access control) Protocols
1. channel partitioning(채널 분할)
	- 채널을 다른 pieces로 나눈다.(time slots, frequency, code)
2.  random access
	-  collision이 나면, recover 한다.
3. taking turns
	- 위 2개의 중간!
	- Bluetooth 에서 이거 사용


### TDMA
TDMA : time division multiple access
- 시간을 time frame으로 나누고 각 time frame을 N개의 time slot으로 나눈다.
- 노드는 전송할 packet이 있을 때마다 TDM 프레임에서 자신에게 할당된 시간 슬롯동안 전송될 수 있게 선택
- 사용되지 않는 slot들은 idle 해진다.
![Pasted image 20230517164936](https://github.com/lina1919/cs_study/assets/63230463/93d86bdf-6f05-454f-8d06-d283b8667f0a)

6 station 6 slot : 바보
6 station 2~3 slot : 충분

### FDMA
FDMA : frequency division multiple access
- R bps의 채널을 다른 주파수로 나눠서 N개의 노드 중 하나에게 할당
- 사용되지 않는 frequency band는 idle 해진다.
![Pasted image 20230517165154](https://github.com/lina1919/cs_study/assets/63230463/93f52b3b-e432-4942-a39b-e8a72b96ccfc)

### Random Access Protocols
- 항상 채널의 최대 전송률인 R bps로 전송
- collision이 나면 -> recover 한다.
- ex) slotted ALOHA, ALOHA, CSMA, CSMA/CD, CSMA/CA

### Slotted ALOHA
가장 단순한 랜덤 접속 protocol
- 모든 frame은 같은 size
- 시간은 equal size로 divided 되어 있음.
- 싱크로아니즈 된 nodes
- slot의 시작점에서만 node들이 transmit 됨.
- 2개 이상의 node가 같은 slot에 transmit, collison detect됨
- *if no collision :* 다음 slot에서 frame 보낼 수 있음.
- *if collision :*  충돌 없이 전송될 때까지 p의 확률로 재전송.
	- ex) 재전송 : p , 이번 slot은 건너뛰고 다음 slot에서 다시 : 1-p
![Pasted image 20230517165656](https://github.com/lina1919/cs_study/assets/63230463/0b8af775-250e-487a-8a45-e5f94b0fe65c)
장점 : 
- 하나의 활성 node로 하여금 채널의 전속력으로 계속해서 전송 가능
- decentralized
단점 : 
- collision, wasting slots
- idle slots
- 싱크 안맞춰주면 동작 X

**Slotted ALOHA efficiency**
max 37%!

Pure ALOHA efficiency
18%!


### CSMA
CSMA : carrier sense multiple access
- 말하기 전에 듣는다.
- 캐리어를 감지해서 보냄

- 모든 노드들이 충돌을 감지하지만, collison은 그래도 발생한다.
	- 왜냐하면 **propagation delay**

### CSMA/CD
CD : collision detection
- collision을 detect 하고, 발생하면 즉시 중지하자.
- wired LAN 에서는 detect 쉬움.
- 하지만 wireless에서는? 불가능

**CSMA/CD 알고리즘**
1. NIC가 채널이 idle한 걸 감지하면 frame 보내고, 아니면 기다린다.
2. 만일 collision이 발생하면, binary (exponential) backoff 알고리즘 실행.
	1. mth collision 이후에 NIC는 K를 {0,1,2,...,2^m-1}에서 고름.
	2. 그 다음 NIC는 K*512bits만큼 기다린다.
	3. 즉 충돌이 많아지면, K값이 커져서 오래 기다릴 확률이 올라감.

**CSMA/CD efficiency**
![Pasted image 20230517170601](https://github.com/lina1919/cs_study/assets/63230463/6376a168-08fd-4b48-b3ba-347350b0be7d)
- Tprop = max prop delay between 2 nodes in LAN
- ttrans = time to transmit max-size frame


### Taking Turns MAC Protocol
- channel partitioning과 random access, 2가지의 장점 추출

1. polling
	1. 노드 중 하나를 master node로 지정
	2. 각 노드를 round robin 방식으로 polling
	- 단점 : polling overhead, 지연, master node가 고장나면 동작 X
2. token
	1. token으로 알려진 작은 frame을 노드 간 전달.
	 - 단점 : token overhead, latency, token이 전달 안되면 동작 X

### Summary
1. channel partitioning, by time, frequency or code
	•Time Division, Frequency Division

2. random access (dynamic)
	- ALOHA, S-ALOHA, CSMA, CSMA/CD
	- carrier sensing: easy in some technologies (wire), hard in others (wireless)
	- **CSMA/CD used in Ethernet**
	- **CSMA/CA used in 802.11**

3. taking turns
  - polling from central site, token passing
	- Bluetooth, FDDI,  token ring
