IEEE 802.11 Wireless LAN (Wi-Fi)
- 무선 랜을 위한 기술 표준
- 1997년부터 시작하여 현재까지도 계속 개선되오고 있다.
- Data Link Layer와 Physical Layer의 범위에 있다.

용어 정리
- Access Point: 라우터, EAPoL에서는 Authenticator에 해당한다.
- Station/Host: AP에 연결하는 무선 연결 단말, EAPoL에서는 Supplicant에 해당한다.
- RADIUS 서버: Host를 인증하는 서버, EAPoL에서는 Authenticaiton Server에 해당한다.
- EAP: 인증 프로토콜을 위한 프레임워크
- EAPOL: EAP Encapsulation over LAN
- MSK(Master Session Key): 키 교환 이전에 각자가 공유하는 키의 원형, 일부를 PMK로 사용한다.
- PMK (Pairwise Master Key): MSK의 일부를 이용하여 키 교환 이전에 각자가 공유하는 키
    - GMK (Group Master Key): AP가 여러 Host에 대해 통일하여 가질 경우에 사용된다.
- Anonce/Snonce: Authenticator/Supplicant의 난수 
- PTK(Pairwise Transient Key): AP와 Host간의 암호화된 통신에 사용되는 키이다.
    - PTK = PRF(PMK + Anonce + SNonce + Mac (AA)+ Mac (SA))
    - GTK는 AP가 여러 Host에 대해 통일하여 가질 경우에 사용된다.
- MIC(Message Integrity Check): CRC(단순 나눗셈)보다 진보한, 키를 이용한 무결성 체크 방법

AP-Host 연결 과정 1 (beacon frame, management frame)
- AP는 Beacon Frame을 발신한다.
    - Beacon frame: SSID(AP’s name) + MAC address
- Host는 자신이 요구하는 조건으로 Proning을 시도한다.
- AP와 Host 간의 Authentication을 확인한다. (기본 정보 교환, 통신 조건 등)
- AP와 Host 간의 Associatoin을 확인한다. (보안 규격, 4-way Handshake 관련 정보 교환 등)

AP-Host 연결 과정 2 (EAP 이용, data frame)
- 엔터프라이즈 모드인 경우, RADIUS 서버(Authentication Server)를 통해 Host를 인증한 후 MSK를 발급한다. (802.1X)
- 개인 모드인 경우, Pre-Shared Key를 MSK로 취급한다.
- AP와 Host 간의 4-way Handshake가 실행된다.
- 제어 Port가 열리고 PTK(GTK)로 암호화된 통신이 시작된다.
- Host는 AP로부터 동적 IP를 할당받는다. (DHCP)
- Disassociate 메시지로 통신이 종료된다.

4-way Handshake의 의의
- Authenticator와 Supplicant가 각각 생성한 난수를 사용하기 때문에 세션 키처럼 통신마다 사용되는 PTK가 달라진다.
- PMK를 직접 보내지 않으면서 서로를 인증할 수 있다.
- 또한 인증한 후에는 해당 과정에서 발급한 PTK로 암호화된 메시지를 주고받을 수 있다.

4-way Handshake의 취약점
- PMKID: Message 1에서 PMK에 대한 정보를 유추할 수 있는 PMKID가 담겨있기 때문에 개인 모드에서 단순한 Pre-Shared Key를 사용하는 경우 Dictionary Attack으로 쉽게 뚫을 수 있다.
- Key Reinstallation: Message 3를 재전송하면 난수가 고정된 상태에서 PTK를 새로 만들면서 Counter가 초기화되기 때문에 Block Cipher가 재기능을 할 수 없다. 따라서 공격자는 중간에서 PTK를 유추할 수 있고, 더 나아가서 암호화된 메시지에 접근할 수 있다. 이러한 공격을 KRACK이라고 부른다. (MitM Attack의 일종)

암호화 방식
- WEP(Wired Equivalent Privacy): static key를 사용한 RC4(Stream Cipher) 이용
- WPA(Wi-Fi Protected Access): non-static key를 사용한 TKIP(RC4 기반) 암호화
    - TKIP(Temporal Key Integrity Protocol) 
        - Temporal Key와 Sequence counter를 사용한 Key Mixing 도입
        - MIC key를 이용한 Message Integrity Check
- WPA2: AES based Counter mode with CBC-MAC 사용
- WPA3: SAE(Simultaneous Authentication of Equals) 도입 (Dragonblood Attack에서 후술)

공격 방식
- PMKID Offline Dictonary Attack
- KRACK
    - [vanhoefm/krackattacks-scripts](https://github.com/vanhoefm/krackattacks-scripts): It creates virtual AP on device. It can check its connected client's vulnerability by resending M3s in different situations
- Fragattacks: fragment 단위로 보내고 조립하는 Wi-Fi의 설계 상, 악성 프레임을 생성할 수 있다.
    - Aggregation attack: is aggregated flag는 평문 상태로 프레임 내에 존재하기 때문에 이를 인증하지 않는 경우 조작할 수 있다.
    - Mixed key attack: 서로 다른 키로 암호화된 정보를 임의로 조합하여 공격할 수 있다. (이론적인 공격에 가까움)
    - Fragment cache attack: 악성 Fragment를 미리 전송하여 이후에 전송될 Fragment와 조합시킬 수 있다. (연결을 종료하거나 재접속하는 경우 fragment를 초기화하는 것으로 해결할 수 있다.)
    - [vanhoefm/fragattacks](https://github.com/vanhoefm/fragattacks): Vulnerability Check by sending various fragmented pings to devices in different conditions.
- Dragonblood Attack: WPA3에서 사용되는 동시 인증 방식(SAE, Dragonfly Handshake)에 대한 공격이다.
    - Dragonfly Handshake의 특징
        - Convert password into group element (point on eliptic curve)
        - Iteration is affected by pw and mac address
    - Timing (side-channel Attack)
        - By spoofing mac addresses, we can filter out password with iteration (average time) 
        - Offline dictionary attack possible
    - DoS Attack
        - Hash-to-curve algorithm iterates 40 times to prevent side-channel attack
