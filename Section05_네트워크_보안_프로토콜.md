# 1. 가상 사설망(VPN:Virtual Private Network)
### 1) 개요
1. 가상 사설망이란 인터넷과 같은 공중망을 이용하여 사설망이 요구하는 서비스를 제공할 수 있도록 구축하는 망으로 공중망 내에서 마치 단일 회사만 사용하는 전용선처럼 사용하는 기술을 말한다.
2. 공중망을 공유하기 때문에 낮은 비용으로 전용선과 같은 수준의 서비스를 제공하므로 많은 기업에서 사용하고 있다.
3. VPN은 터널링 프로토콜과 보안 과정을 거쳐 내부 기밀을 유지하여 보안성이 우수하고 외부로부터 안전하도록 주소 및 라우터 체계의 비공개와 데이터 암호화, 사용자 인증, 사용자 액세스 권한 및 제한의 기능을 제공한다.
   * 터널링 : 송신자와 수신자 사이의 전송로에 외부로부터의 침입을 막기 위해 일종의 파이프를 구성하는 것으로 파이프는 터널링을 지원하는 프로토콜을 사용하여 구현하고 있으며, 사설망과 같은 보안 기능을 지원한다.
   * 터널링되는 데이터를 페이로드라고 하며 터널링 구간에서 터널링 프로토콜을 통해 페이로드는 캡슐화되어 전송된다.

### 2) VPN 프로토콜 종류
#### (가) PPTP(Point to Point Tunnel Protocol)
1. 지원계층 : 2계층(Data Link Layer)
2. 특징
   * 마이크로소프트사가 설계한 프로토콜
   * Windows NT4.0에서 처음으로 제공
   * PPP(Point-to-Protocol Protocol)의 Packet을 IP Packet으로 캡슐화하여 IP 네트워크에서 전송하기 위한 터널링 기법
   * 하나의 터널에 하나의 연결만을 지원하여 일대일 통신만 가능

#### (나) L2F(Layer 2 Forwarding)
1. 지원계층 : 2계층(Data Link Layer)
2. 특징
   * 시스코사에서 제안한 프로토콜
   * 원격지의 ISP 장비에서 접근 서버 측의 터널 서버로 L2F 터널을 생성시키며, 이 가상 터널은 Direct-dial PPP/RAS 세션을 생성함
   * 원격지 사용자의 home site에서 주소를 할당하며 home site의 게이트웨이에서 사용자 인증함
   * 하나의 터널에 여러 개의 연결을 지원하여 다자간 통신을 가능하게 함
   * PPP(Point-to-Point Protocol)를 사용하며, 인증으로 RADIUS와 TACACS+를 이용함

#### (다) L2TP(Layer 2 Tunnelling Protocol)
1. 지원계층 : 2계층(Data Link Layer)
2. 특징
   * 마이크로소프트와 시스코에서 제안한 프로토콜
   * L2F에 기반을 두고 PPTP와의 호환성을 고려하여 만들어진 터널링 프로토콜
   * IP, IPX, AppleTalk 프로토콜에 대해 지원되며 X.24, ATM, FrameRelay 등의 WAN 기술도 지원한다.

#### (라) IPSec(IP Security)
1. 지원계층 : 3계층(Network Layer)
2. 특징
   * IP망에서 안전한 전송을 위한 표준화된 3계층 터널링 프로토콜로 IP 계층의 보안을 위해 IETF에 의해 제안되어 VPN 구현에 가장 널리 사용되고 있다.
   * 네트워크상의 IP 계층에서의 보안에 중점을 두었으며, 사설 및 공중망을 사용하는 TCP/IP 통신을 보다 안전하게 유지하기 위한 IP 데이터그램의 인증, 무결설과 기밀성 등을 제공한다.\
   * IP 계층에서 직접 서비스를 제공하기 떄문에 상위계층 프로그램의 변경이 필요 없다.
   * 암호화된 패킷은 보통의 IP 패킷과 동일한 형태를 갖기 때문에 네트워크 장비의 내부 변경 없이 네트워크를 통해 쉽게 라우팅이 가능하다.

# 2.IP 보안 - IPSec(IP Security)
### 1) 개요
1. IETF(국제 인터넷 기술 위원회)에서 IP 보안을 위하여 개방형 구조로 설계한 표준으로 IP 계층 보안에 대해서 안전정이고 표준화된 기초를 제공한다.
2. 종단 노드 구간 또는 보안/터널 게이트웨이 구간에 IP 패킷 보안 서비스를 제공해주는 네트워크 계층 보안 프로토콜
3. IP 계층에서 직접 보안 서비스를 제공함에 따라 상위계층 프로그램의 변경이 필요하지 않다.
4. 차세대 인터넷 프로토콜인 IPv6에서 IPSec을 기본적으로 포함하고 있다.

### 2) 보안 서비스 제공(RFC2401 표준 정의)
1. **기밀성(Confidentiality)** 
   * 메시지가 제3자에 의해 도청되어도 그 내용을 알 수 없음을 보장해준다.
   * 대칭 암호화를 통해 기밀성을 제공해준다. 단, **AH 프로토콜은 암호화를 지원하지 않으며 ESP 프로토콜만 암호화를 지원**한다.
2. **비연결형 무결성(Connectionless Integrity)**
   * 메시지가 위변조되지 않았음을 보장해준다.
   * 메시지 인증 코드(MAC:Message Authentication Code)를 통해 각 IP 패킷별로 무결성을 보장해준다.
   * 송신측에서 인증 데이터/MAC 값을 계산하여 전송하고 수신 측에서 이를 검증한다.
3. **데이터 원천 인증/송신처 인증(Data Origin Authentication)**
   * 수신한 메시지가 올바른 송신처로부터 온 것임을 보장해준다.
   * 메시지 인증 코드를 통해 IP 패킷이 올바른 송신처로부터 온 것임을 보장해준다.
4. **재전송 공격 방지(Protection Against Replays)**
   * 송신 측에서 IP 패킷별로 순서번호를 전송하고 수신 측에서 해당 보안연관(SA:Security Association)에 순서번호를 유지하고 이를 검증함으로써 재전송 공격을 방지한다.
5. **접근 제어(Access Control)**
   * 보안정책(SP:Security Policy)을 통해 송수신 IP 패킷에 대한 시스템 접근을 제어한다.
   * 접근 제어 방식은 IP 패킷의 허용, 폐기, 보호 등이 있다.
6. **제한된 트래픽 흐름의 기밀성(Limited Traffic Flow Confidentiality)**
   * 트래픽 흐름이란 해당 패킷이 어디에서 출발해서 어디를 목적지로 향해 가는지에 대한 정보를 말한다.
   * ESP/터널모드의 경우 New IP 헤더를 통해 터널/보안 게이트웨이 구간의 트래픽 흐름 정보는 노출되지만, 원본 IP 헤더는 암호화되어 있기 때문에 터널/보안 게이트웨이와 종단 노드 구간의 트래픽 흐름의 기밀성은 보장된다.
  
### 3) IPSec 동작 모드
#### (가) 전송 모드(Transport Mode)
1. 보호 범위
   * **IP 패킷의 페이로드를 보호**하는 모드, 즉 IP의 상위 프로토콜 데이터를 보호하는 모드이다.
   * IP 패킷의 페이로드만 IPSec으로 캡슐화하고 IP 헤더는 그대로 유지하므로 네트워크상 패킷 전송에 문제가 발생하지 않는다.
   * IP 헤더를 보호하지 않기 때문에 트래픽 흐름(최초 출발지 및 최종 목적지)이 분석될 수 있다.
2. 보호 구간
   * 일반적으로 **종단 노드 구간의 IP 패킷 보호**를 위해 사용한다.
3. 정리하면 IP 헤더를 제외하고 페이로드만 보호하고, 페이로드만 IPSec으로 캡슐화하고 IP 헤더는 그대로 유지하므로 네트워크상 패킷 전송에 문제가 발생하지 않는다. IP 헤더를 보호하지 않기 때문에 트래픽 흐름(최초 출발지 및 최종 목적지)가 분석될 수 있다. 보호 구간은 종단 노드 구간의 IP 패킷 보호를 위해 사용한다. (예. 사용자PC -> Server까지)

#### (나) 터널 모드(Tunnel Mode)
1. 보호 범위
   * **IP 패킷 전체를 보호**하는 모드
   * IP 패킷 전체를 IPSec으로 캡슐화하여 IP헤더를 식별할 수 없기 때문에 네트워크상 패킷 전송이 불가능하다. 따라서 전송구간 주소 정보를 담은 New IP 헤더를 추가한다.
   * 원본 IP 헤더를 보호하기 때문에 최초 출발지 및 최종 목적지에 대한 트래픽 정보의 기밀성을 보장해준다. 단, 새로운 IP 헤더를 통해 보안/터널 게이트웨이 구간 정보는 노출될 수 있기 때문에 "제한적 트래픽 흐름의 기밀성을 보장해준다"라고 한다.
2. 보호 구간
   * 일반적으로 **터널/보안 게이트웨이 구간 또는 종단 노드와 터널/보안 게이트웨이 구간의 IP 패킷 보호를 위해 사용**
   * 터널/보안 게이트웨이 구간 IP 패킷 보호는 물리적으로 떨어진 위치의 본지점 사이에 다수의 사용자 호스트와 서버로 구성된 VPN 환경을 예를 들 수 있다.
   * 종단 노드와 터널/보안 게이트웨이 구간 IP 패킷 보호는 외부 사용자 호스트와 본지점 사이의 VPN 환경 구성을 예를 들 수 있다. 이 경우 외부 사용자 호스트는 IPSec을 위한 VPN 클라이언트 프로그램이 필요하다.
3. 정리하면 IP 헤더와 IP Payload 전체를 IPSec으로 캡슐화하여 보호하기 때문에 IP 헤더를 식별할 수 없기(최초 출발지 및 최종 목적지) 때문에 전송구간 주소를 담은 New IP 헤더를 추가한다. 원본 IP 헤더를 보호하기 때문에 최초 출발지 및 최종 목적지에 대한 트래픽 정보의 기밀성을 보장해주지만, 새로운 IP 헤더를 통해 보안/터널 게이트웨이 구간 정보는 노출될 수 있기 때문에 "제한적 트래픽 흐름의 기밀성 보장"이라 한다. 보호 구간은 두 가지인데 종단 노드에서 보안 게이트웨이까지 보호하거나, 보안 게이트웨이들 사이를 보호한다. 보안 게이트웨이 사이 구간 IP 패킷 보호는 VPN 환경을 예를 들 수 있고, 종단 노드에서 보안 게이트웨이 구간 IP 패킷 보호는 외부 사용자 호스트와 본지점 사이의 VPN 환경 구성을 예로 들고 VPN 클라이언트 프로그램 필요

### 4) IPSec 세부 프로토콜
#### (가) AH(Authentication Header) 프로토콜
1. 개요
   * AH 프로토콜은 메시지 인증 코드(MAC)를 이용하여 **인증(무결성(Integrity)과 송신처 인증(Authentication))을 제공해주는 프로토콜로 기밀성(암호화)은 제공하지 않는다.**
   * 송신 측에서 MAC 알고리즘과 인증키를 통해 인증 데이터(Authentication Data)를 계산하여 전송하고 수신 측에서 이를 검증한다. 인증 데이터 계산에는 IP 헤더의 변경 가능한 필드를 제외한 IP 패킷 전체를 대상으로 한다.
   * 동적으로 변경되는 필드를 인증 데이터 계산에 포함할 경우 수신 측 검증 시 인증 데이터가 일치하지 않아 인증에 실패하므로 변경되는 필드를 제외하고 인증 데이터를 계산한다.
   * IP 헤더의 전송 중 변경 가능한 필드는 **TTL(Time To Live), Header Checksum, NAT 환경에서의 Source IP** 등이 있다.
2. 주요 헤더 필드
   * SPI(Security Parameter Index) : 현재 연결에 대한 보안연관(SA) 식별자
   * 순서번호(Sequence Number) : 재전송 공격을 방지하기 위한 필드로 정상적인 환경에서는 패킷 재전송이 발생해도 일련번호는 항상 1씩 증가하기 때문에 재전송 공격을 방지할 수 있다.
   * 인증 데이터(Authentication Data) : IP 헤더의 변경 가능한 필드를 제외한 IP 패킷 전체에 대한 MAC값(또는 ICV(Integrity Check Value)라고도 함)을 설정한다.
3. AH 프로토콜 동작모드
   * 전송 모드는 **IP 헤더의 전송 중 변경 가능한 필드를 제외한 IP 패킷 전체를 인증**한다.
   * 터널 모드는 **New IP 헤더의 전송 중 변경 가능한 필드를 제외한 New IP 패킷 전체를 인증**한다.
4. AH/전송모드 캡처
   * AH 헤더의 ICV(Integrity Check Value)가 인증 데이터를 의미한다.
   * AH 프로토콜은 암호화를 지원하지 않기 때문에 ICMP 메시지가 평문으로 전송된다.
5. 정리하면 AH 프로토콜은 IP 헤더의 변경 가능한 필드를 제외(TTL, Header checksum, NAT 환경에서의 Source IP)한 IP 패킷 전체를 대상으로 MAC으로 인증한다. 주요 헤더 필드는 SPI는 현재 연결에 대한 보안연관(SA) 식별자, 순서번호, 인증 데이터(MAC 값 또는 ICV(Integrity Check Value))가 있고, 전송 모드에서는 IP-H, AH-H, IP-Payload에서 IP 헤더의 변경 가능한 필드를 제외한 패킷 전체를 인증하고, 터널 모드에서는 NewIP-H, AH-H OriIP-H, IP-Payload에서 IP 헤더의 변경 가능한 필드를 제외한 패킷 전체를 인증한다. 그리고 MAC을 통해 무결성과 인증만 지원하고 기밀성(암호화)는 지원하지 않는다.

#### (나) ESP(Encapsulation Security Payload) 프로토콜
1. 개요
   * ESP 프로토콜은 메시지 인증 코드(MAC)와 암호화를 이용하여 **인증(무결성(Integrity)과 송신처 인증(Authentication))과 기밀성(Confidentiality)을 제공**한다.
   * 인증과 암호화를 선택적으로 적용할 수 있다. 즉, 인증만 적용하거나 인증+암호화를 적용할 수 있다.
   * 인증에 있어서 AH 프로토콜과의 차이점은 AH는 변경 가능한 IP 헤더 필드를 제외한 IP 패킷 전체를 인증하지만, ESP는 IP 헤더를 인증하지 않는다.
2. ESP 헤더 필드
   * SPI(Security Parameter Index) : 현재 연결에 대한 보안연관(SA) 식별자
   * 일련변호(Sequence Number) : 재전송 공격을 방지하기 위한 필드로 정상적인 환경에서는 패킷 재전송이 발생해도 일련번호는 항상 1씩 증가하기 때문에 재전송 공격을 방지할 수 있다.
3. ESP 트레일러 필드
   * 블록 암호를 위한 패딩 정보와 전송하는 페이로드의 프로토콜 타입 정보를 담고 있다.
4. ESP Auth 필드
   * 인증 데이터 정보를 저장한다.
5. ESP 프로토콜 동작모드
   * 전송 모드는 **IP 페이로드와 ESP 트레일러를 암호화하고 암호화된 데이터와 ESP 헤더를 인증**한다.
   * 터널 모드는 **원본 IP 패킷 전체와 ESP 트레일러를 암호화하고 암호화된 데이터와 ESP 헤더를 인증**한다.
6. ESP/터널모드 캡처
   * ESP 프로토콜은 암호화를 지원하기 때문에 ICMP 메시지가 암호화되어 전송된다.
7. 정리하면 ESP 프로토콜은 MAC과 암호화를 통해 인증, 무결성, 기밀성을 제공한다. 주요 헤더 필드는 SPI는 현재 연결에 대한 보안연관(SA) 식별자, 순서번호가 있고 ESP 트레일러 필드는 블록 암호를 위한 패딩 정보와 페이로드의 프로토콜 타입 정보를 담고 있다. ESP Auth 필드는 인증 데이터 정보를 저장한다. 전송 모드에서는 IP-H ESP-H IP-Payload ESP-T ESP Auth에서 ESP-H에서 ESP-T 까지 인증을 하고 ESP-H 다음부터 ESP-T 까지 암호화를 하고, 터널 모드에서는 NewIP-H ESP-H OriIP-H IP-Payload ESP-T ESP Auth에서 ESP-H에서 ESP-T까지 인증을 하고 ESP-H 다음부터 ESP-T까지 암호화를 한다. 결국 전송 모드에서는 IP 페이로드와 ESP-T을 암호화를 하고 터널 모드에서는 IP 헤더 전체와 ESP-T을 암호화한다.

### 5) SA(Security Association)와 SP(Security Policy)
#### (가) 보안연관(SA: Security Association)
1. 둘 사이에 논리적인 연결 상태를 유지하는 동안 적용할 보안 설정 정보를 "보안연관(SA)"이라 한다.
2. 보안연관은 단방향성/일방향성을 갖기 때문에 대상 호스트와 송수신을 모두하려면 2개의 보안연관이 필요하다. 가령 A 호스트와 B 호스트가 송수신한다면 A->B를 위한 보안연관과 B->A를 위한 보안연관 2개가 필요하다.
3. 여러 보안연관을 저장해놓은 데이터베이스를 보안연관 데이터베이스(SAD: Security Association Database)라 한다.
4. 보안연관(SA) 주요 항목
   * SPI(Security Parameter Index) : 보안연관 식별자
   * Sequence Number Counter : 패킷의 순서번호 카운터
   * Anti-Replay Window : Replay-Attack을 방지하기 위한 윈도우값
   * AH/ESP 정보 : AH 및 ESP 프로토콜 정보(MAC 알고리즘, 대칭키 알고리즘, 관련 키 정보 등)
   * Lifetime : 세션 만료 기간
   * Mode : IPSec 동작 모드(전송 모드, 터널 모드)
   * Path MTU : 경로의 MTU값
5. 정리하면 보안연관은 둘 사이에 논리적인 연결 상태를 유지하는 동안 적용할 보안 설정 정보라고 하며 보안연관 데이터베이스(SAD)에 저장하여 관리한다. 단방향성/일방향성을 갖기 때문에 송수신을 하려면 2개의 보안연관이 필요하다.

#### (나) 보안정책(SP: Security Policy)
1. 패킷을 송신하거나 수신했을 때 적용할 보안의 종류를 정의하는 것을 보안정책(SP)이라 한다.
2. 일반적인 보안정책에는 IP 패킷을 허용하거나, 폐기하거나, IPSec 적용 등이 있다.
3. 이러한 보안 정책들을 저장해놓은 데이터베이스를 보안 정책 데이터베이스(SPD: Security Policy Database)라 한다.
4. 정리하면 보안정책(SP)는 IP 패킷을 허용, 폐기, 보호(IPSec 처리)등 정책을 보안 정책 데이터베이스(SPD)에 저장하여 정책을 처리하는 것

### 6) IPSec 패킷 송수신 절차
#### (가) 송신 절차
1. 전송할 패킷에 대해서 보안정책데이터베이스(SPD)를 검색한다.
2. SPD에 일치하는 엔트리가 없으면 패킷을 삭제한다.
3. SPD에 일치하는 엔트리가 있으면 첫 번째 엔트리의 정책에 따라 처리한다.
   * 정책이 폐기라면 해당 패킷을 삭제
   * 정책이 허용이라면 해당 패킷을 송신
   * 정책이 보호라면 보안 연관 데이터베이스(SAD)를 검색한다.
4. 보안 연관 데이터베이스(SAD)에 일치하는 엔트리가 있으면 IPSec 처리를 수행한 후 전송하고 일치하는 엔트리가 없으면 인터넷 키 교환(IKE)과정을 수행하여 SA를 생성하는 과정을 수행한다.
5. 정리하면 전송 패킷에 대해 보안정책 데이터베이스 검색하여 일치하지 않으면 삭제 일치하면 정책에 맞게 처리 보호라면 보안연관 데이터베이스를 검색하여 일치하면 IPSec 처리 수행 후 전송하고 없으면 키 교환(IKE) 과정 수행하여 SA 생성 과정 수행한다.

#### (나) 수신 절차
1. IP 프로토콜의 protocol 필드를 조사하여 보호되지 않는 IP 패킷인지 IPSec(AH/ESP) 패킷인지 확인한다.
2. 보호되지 않는 IP 패킷이라면 보안 정책 데이터베이스(SPD)를 검색하여 첫 번째 일치하는 엔트리가 허용 정책이면 상위 계층으로 전달하고, 폐기 또는 보호라면 패킷을 삭제
3. IPSec 패킷이라면 보안 연관 데이터베이스(SAD)를 검색하여 일치하는 엔트리가 없으면 패킷을 삭제하고 일치하는 엔트리가 있으면 IPSec 처리를 수행한 후 상위계층으로 전달한다.
4. 정리하면 IP 프로토콜의 protocol 필드를 조사하여 IPSec인지 아닌지 확인하고 IPSec이 아니면 보안정책 데이터베이스를 검색하여 허용이면 상위 계층 전달하고, 폐기 또는 보호라면 패킷을 삭제한다. IPSec 패킷이라면 보안연관 데이터베이스를 검색하여 일치하지 않으면 패킷을 삭제하고 일치하면 IPSec 처리를 수행한 후 상위 계층으로 전달

### 7) 인터넷 키 교환(IKE: Interney Key Exchange) 프로토콜
#### (가) 개요
1. 보안 관련 설정을 생성, 협상 및 관리하는 프로토콜로 500/udp 포트 사용
2. IPSec에서 양 당사자 간의 논리적인 연결정보 및 보안 설정을 보안연관(SA)이라고 한다.
3. 정리하면 IKE는 보안 관련 설정을 생성, 협상 및 관리하는 프로토콜이고 500/udp 포트를 사용

#### (나) IKE 1단계(phase 1)
1. IKE 2단계(phase 2)에서 사용할 메시지들을 어떻게 보호할 것인지를 협상하는 단계로 이 과정을 통해 IKE용 마스터키를 생성한다.
2. 이 단계를 통해 생성된 보안연관(SA)을 "IKE SA"라고 하고, 양방향성(송수신 모두 이용)을 가진다. 다음 2가지 중 1가지 모드로 구현한다.
   * Main Mode : 3쌍의 메시지(6개의 메시지)를 교환하는 방식으로(기본 모드) aggressive Mode에 비해 단계가 많지만, 세션 ID를 암호화하기 때문에 보안성이 높다.
   * Aggressive Mode : Main Mode보다 빠른 버전으로 3쌍의 메시지가 아닌 3개의 메시지를 교환하는 방식이다. 협상을 빠르게 할 수 있지만 세션 ID를 암호화하지 않기 때문에 보안성이 낮다.
3. 정리하면 IKE 1단계는 사용할 메시지들을 어떻게 보호할 것인지를 협상 단계로 이 과정을 통해 IKE용 마스터키 생성하고 이 단계를 통해 생성된 보안연관을 "IKE SA"라고 하고, 양방향성을 가지고, Main Mode(3쌍(6개 메시지 교환 방식으로 aggressive Mode보다 단계가 많지만, 세션 ID 암호화하기 때문에 보안성이 높다), Aggressive Mode(Main Mode보다 빠른 버전으로 3개의 메시지를 교환 방식, 세션 ID 암호화하지 않기 때문에 보안성이 낮다) 둘 중 하나의 모드로 구현된다.
   
#### (다) IKE 2단계(phase 2)
1. 2단계는 실질적인 데이터를 어떤 방식으로 보호할 것인지를 협상하는 단계로 이단계를 통해 생성된 보안연관을 "IPSec SA"라고 한다.
2. 1단계를 통해 생성된 키를 이용해 메시지가 보호되며 Quick Mode를 통해 구현한다.
   * 3번의 메시지 교환을 통해 IPSec 통신을 위한 보안연관(SA) 및 키 협상이 이루어진다.
   * 이때 생성된 보안연관(SA)은 단방향성을 가진다. 따라서 수신용 SA와 송신용 SA가 생성된다.
3. 정리하면 IKE 2단계는 실질적인 데이터를 어떤 방식으로 보호할 것인지를 협상 단계로 이 단계를 통해 생성된 보안연관을 "IPSec SA"라고 하고, 1단계를 통해 생성된 키를 이용해 메세지 보호하고 Quick Mode를 통해 구현되고 3번의 메시지 교환을 통해 보안연관 및 키 협상 이루어지고 이때 생성된 보안연관은 단방향성을 가지며 수신용 SA와 송신용 SA가 생성된다.

# 3. 전송 계층 보안 - SSL/TLS
### 1) 개요
1. SSL(Secure Socket Layer)은 1994년 Netscape사의 웹 브라우저를 위한 프로토콜로 처음 제안되어 1996년 SSL3.0 버전까지 발표
2. 1999년 IETF(국제 인터넷 표준화 기구)에서 SSL3.0을 기반으로 표준화시킨 TLS1.0 버전을 발표, 현재 TLS1.2 버전까지 널리 사용되고 있다.
3. SSL/TLS는 클라이언트/서버 환경에서 TCP 기반의 Application에 대한 종단 간(End-To-End) 보안 서비스를 제공하기 위해 만들어진 전송계층 보안 프로토콜이다.
   * 전송계층(TCP)과 애플리케이션 계층 사이에서 동작, 다양한 TCP 기반의 애플리케이션 프로토콜에 보안 서비스를 제공
   * 각 애플리케이션 프로토콜이 SSL을 이용할 경우 이를 구분하기 위해 고유한 well-known 포트를 할당 예) https(443/tcp), smtps(465/tcp), ftps(990/tcp), telnets(992/tcp) 등

### 2) 보안서비스 제공
1. **기밀성(Confidentiality)**
   * 대칭 암호를 이용한 송수신 메시지 암호화를 통해 기밀성을 제공한다.
2. **무결성(Integrity)**
   * 메시지 인증 코드(MAC:Message Authentication Code)를 통해 송수신 메시지의 위변조 여부를 확인할 수 있는 무결성을 제공한다.
3. **인증(Authentication)**
   * 공개키 인증서를 이용한 서버/클라이언트 간 상호 인증을 수행

### 3) SSL/TLS 프로토콜 구조
#### (가) SSL/TLS는 크게 2계층으로 이루어진 프로토콜이다.
1. 상위계층 : Handshake, Change Chipher Spec, Alert, Application Data 프로토콜로 구성
2. 하위계층 : Record 프로토콜

#### (나) 세부 프로토콜의 기능
1. **Handshake** 프로토콜
   * 종단 간에 보안 파라미터를 협상하기 위한 프로토콜
2. **Change Cipher Spec** 프로토콜
   * 종단 간에 협상된 보안 파라미터를 이후부터 적용/변경함을 알리기 위한 프로토콜
3. **Alert** 프로토콜
   * SSL/TLS 통신 과정에서 발생하는 오류를 통보하기 위한 프로토콜
4. **Application Data** 프로토콜
   * Application 계층의 데이터를 전달하기 위한 프로토콜
5. **Record** 프로토콜
   * 적용/변경된 보안 파라미터를 이용하여 실제 암호화/복호화, 무결성 보호, 압축/압축해제 등의 기능을 제공하는 프로토콜

#### (다) 상태 유지 프로토콜
1. 세션과 연결 기반의 상태 유지 프로토콜이다.
   * 완전 협상을 통해 세션을 생성하고, 이 세션 정보를 공유하는 다수의 연결을 단축협상을 통해 생성한다.
2. 세션 상태정보
   * 양 종단 간에 완전 협상을 통해 생성되는 상태정보로 세션이 유지되는 동안에 지속적으로 다수의 연결에 의해 사용되는 보안 파라미터 정보가 관리된다.
   * 대표적인 상태정보로 다수 연결이 사용할 "대칭 암호 알고리즘", "HMAC용 해시 알고리즘" 등이 있다.

|필드|설명|
|:-:|:-|
|session ID|둘 사이의 세션 식별자, 32바이트로 구성된다.|
|peer certificate|상대방의 인증서(X.509v3)|
|cipher spec (암호 명세)|암호 명세로 다음과 같은 정보를 담고 있다. </br>* 대칭 암호 알고리즘, 키 길이, 블럭 암호 모드 등 </br>* HMAC용 해시 알고리즘|
|compression method|압축 방식, 현재는 null만 정의|
|master secret|* 키 블럭을 생성하기 위해 서버와 클라이언트가 공유하는 48 바이트 비밀값 </br>* 완전 협상을 통해 생성한 premaster secret, server random, client random을 조합/해시하여 master secret를 생성한다. </br>* server random, client random은 master secret를 생성하기 위한 salt 역할을 수행한다.|
|is resumable|현재 세션이 재사용 될 수 있는지 여부 플래그, 재사용 된다는 의미는 여러 연결에 의해 다시 사용될 수 있는가 하는 의미이다.|

3. SSL/TLS 연결 상태정보
   * 실제 통신이 이루어지는 단위로 단축 협상을 통해 생성되며 세션 상태를 공유하면서 통신을 수행한다.
   * 대표적인 상태정보로 암호키, 인증키 등이 있다.

|필드|설명|
|:-:|:-|
|server/client random|* 단축 협상을 통해 서버/클라이언트가 생성한 32 바이트 난수 값 </br>* 세션에 저장된 master secret와 단축 협상을 통해 생성된 client random, server random을 조합/해시하여 키 블럭을 생성한 후 이를 이용하여 다양한 키를 만들어낸다. </br>* server random, client random은 키 블럭을 생성하기 위한 salt 역할을 수행한다.|
|server/client write key|서버/클라이언트가 암호화에 사용하는 비밀키|
|server/client write MAC secret|서버/클라이언트가 메시지 인증 코드(MAC) 생성 시 사용하는 인증키|
|server/client write IV|서버/클라이언트가 블록 암호 모드에 사용하는 IV(Initialize Vector)|
|sequence number|전송 메시지 순번|

4. 세션 상태정보와 연결 상태정보를 이용한 키 생성 과정
   * 완전 협상을 통해 주고받은 사전 마스터 비밀, Client Random, Server Random을 조합하여 해시한 결과로 마스터 비밀을 생성한다.
   * 생성한 Master Secret는 다수 연결이 이용할 수 있도록 세션 상태에 저장된다.
   * 단축 협상을 통해 주고받은 Client Random, Server Random과 세션에 저장된 Master Secret를 조합하여 해시한 결과로 키블럭을 생성한다.
   * Key Block으로부터 서버/클라이언트 각각의 암호용 비밀키, MAC용 인증키, 블럭 암호 모드용 IV를 계산해낸다.
   * Premaster Secret, Server Random, Client Random을 조합하여 Master Secret을 생성한다. Master Secret, Server Random, Client Random을 조합하여 키블럭을 생성한다. Key Block으로부터 서버/클라이언트의 각각의 암호용 비밀키, MAC용 인증키, 블럭 암호 모드용 IV를 계산해낸다.
  
### 4) 완전 협상 과정(Handshake 프로토콜)
#### (가) (Client -> Server) Client Hello 메시지
1. 클라이언트가 지원 가능한 SSL/TLS 버전, 암호 도구 목록, 압축 방식 등을 서버에 전달하는 메시지
2. 클라이언트 랜덤
   * 클라이언트가 생성하는 32바이트 난수값(임의 난수 28바이트+현재 날짜 및 시간 4바이트)으로 "master secret" 및 "키블럭" 생성 시 솔트 역할을 한다.
3. 세션 ID
   * 서버 세션을 식별하기 위한 ID로 클라이언트가 처음 세션을 생성할 때에는(완전 협상) 빈값을 전달하고 이미 생성된 세션을 재사용할 때는 세션ID를 담아서 전달한다.
4. 암호 도구 목록(cipher suites)
   * 클라이언트에서 지원 가능한 암호 도구들에 대한 정보를 담아서 보낸다.
   * 암호 도구는 "키 교환 및 인증 알고리즘", "암호 명세"로 구성되어 있다. (형식) **SSL/TLS\_(A)\_WITH\_(B)** : A는 키 교환 및 인증 알고리즘, B는 Cipher spec
   * 암호 명세는 대칭 암호 알고리즘, 암호키 길이, 블럭 암호 모드, HMAC용 해시 알고리즘 등으로 구성된다.
   * 예) **TLS_RSA_WITH_AES_256_CBC_SHA256** : 키교환 및 인증 알고리즘으로 RSA를 사용하고, 대칭 암호 알고리즘으로 AES를 사용하며 암호키 길이는 256 비트, 블록 암호 모드는 CBC이고, HMAC용 해시 알고리즘은 SHA-256을 사용하는 cipher suite
   * 예) **TLS_DHE_DSS_WITH_AES_256_GCM_SHA256** : 키교환 알고리즘으로 DHE(Ephemeral Diifie-Hellman), 인증/서명 알고리즘으로 DSS를 사용하고, 대칭 암호 알고리즘으로 AES를 사용하며 암호키 길이는 256비트, 블럭 암호 모드는 GCM이고, HMAC용 해시 알고리즘은 SHA-256을 사용
5. 정리하면 Client Hello는 Client가 Server에게 Client Random(임의 난수 28+현재 날짜 및 시간 4=32byte), 암호 도구 목록(TLS_RSA_WITH_AES_256_CBC_SHA256, 등으로 대칭 암호 알고리즘, 암호키 길이, 블럭 암호 모드, HMAC용 해시 알고리즘 등으로 구성되는 목록)을 보낸다.

#### (나) (Server -> Client) Server Hello 메시지
1. 사용할 SSL/TLS 버전, 암호 도구, 압축 방식 등을 클라이언트에 전달하는 메시지
2. 서버 랜덤
   * 서버가 생성하는 32바이트 난수값(임의 난수 28바이트+현재 날짜 및 시간 4바이트)으로 "master secret" 및 "키블럭" 생성 시 솔트 역할을 한다.
3. 세션 ID
   * 새롭게 생성하거나 존재하는 세션 ID 정보
4. 정리하면 Server Hello는 Server가 Client에게 Server Random(임의 난수 28+현재 날짜 및 시간 4=32byte), 세션 ID 등을 보낸다.

#### (다) (Server -> Client) Server Certificate 메시지
1. 필요시 서버 인증서 목록(서버 인증서 및 인증서에 서명한 인증기관들의 인증서 목록)을 클라이언트에 전달하는 메시지
2. 정리하면 Server Certificate는 Server가 Client에게 서버 인증서 목록(인증서 및 인증서에 서명한 인증기관들의 인증서 목록)을 전달한다.

#### (라) (Server -> Client) Server Key Exchange 메시지
1. 필요시 키 교환에 필요한 정보를 전달하는 메시지
   * 키 교환 알고리즘으로 Ephemeral Diffie-Hellman을 사용한다면 공개 Diffie-Hellman 매개변수(소수 p, 원시근 g, 서버 Diffie-Hellman 공개키)를 서명 알고리즘으로 서명하여 서명값과 함께 전달한다.
2. 정리하면 Server Key Exchange는 Server가 Client에게 임시 디피-헬만을 사용하면 Diffie-Hellman 매개변수를 서명 알고리즘으로 서명하여 서명값과 전달한다.

#### (마) (Server -> Client) Certificate Request 메시지
1. 필요시 클라이언트 인증을 위한 인증서를 요청하는 메시지
   * 요청 시에는 서버 측에서 인증 가능한 인증기관 목록을 제공한다.
2. 정리하면 Certificate Request는 Server가 Client에게 클라이언트 인증서를 요청한다.

#### (바) (Server -> Client) Server Hello Done 메시지
1. Server Hello 과정 종료를 알리는 메시지

#### (사) (Client -> Server) Client Certificate 메시지
1. 필요시(서버의 Certificate Request 메시지) 클라이언트 인증서 목록을 전달하는 메시지
2. 정리하면 Client Certificate는 Client가 Server에게 클라이언트 인증서 목록을 전달한다.

#### (아) (Client -> Server) Client Key Exchange 메시지
1. 키 교환에 필요한 **"사전 마스터 비밀(Premaster Secret)"**를 생성하여 서버에 전달하는 메시지로 교환 알고리즘에 따라 사전 마스터 비밀을 생성하는 방식이 다르다.
   * RSA 방식 : premaster secret(난수값) 생성 후 수신한 서버 인증서의 공개키를 이용하여 암호화 전송
   * Diffie-Hellman 방식 : 클라이언트 Diffie-Hellman 공개키를 생성하여 서버에 전달, 클라이언트와 서버는 각각 Diffie-Hellman 연산을 통해 공통의 premaster secret를 생성한다.
2. 정리하면 Client Key Exchange는 Client가 Server에게 RSA 사용 시 premaster secret 난수값을 생성 후 서버 인증서의 공개키를 이용하여 암호화 전송하고 Diffie-Hellman 사용 시 클라이언트 Diffie-Hellman 공개키를 생성하여 서버에 전달, 클라이언트와 서버는 각각 DH 연산을 통해 공통의 premaster secret을 생성한다.
  
#### (자) (Client -> Server) Certificate Verify 메시지
1. 필요시(서버의 Certificate Request 메시지) 클라이언트가 보낸 인증서에 대한 개인키를 클라이언트가 가지고 있음을 증명하는 메시지
   * 지금까지 핸드셰이크 과정에서 주고받은 메시지와 master secret을 조합한 해시값에 클라이언트 개인키로 서명하여 전달
2. 정리하면 핸드셰이크 과정에서 주고받은 메세지와 master secret을 조합한 해시값에 클라이언트 개인키로 서명하여 전달함으로 써 인증서에 대한 개인키를 클라이언트가 가지고 있음을 증명한다.
#### (차) (Client -> Server) [Change Cipher Spec] 메시지
1. 협상한 암호 명세(Cipher spec)를 이후부터 적용/변경함을 알리는 메시지

#### (카) (Client -> Server) Finished 메시지
1. 협상 완료를 서버에 알리는 메시지

#### (타) (Server -> Client) [Change Cipher Spec] 메시지
1. 협상한 암호 명세(cipher spec)를 이후부터 적용/변경함을 알리는 메시지

#### (파) (Server -> Client) Finished 메시지
1. 협상 완료를 클라이언트에 알리는 메시지

### 5) 완전 협상 과정 패킷 분석
1. (Client -> Server) Client Hello 메시지
   * Client Hello 메시지를 통해 client random, cipher suites, compression methods 등의 정보가 전달되는 것을 볼 수 있다.
   * session id 정보는 서버 측에서 부여하는 ID로 빈값으로 전달되고 있다.
2. (Server -> Client) Server Hello 메시지
   * Server Hello 메시지를 통해 server random, 사용할 cipher suite, 서버에서 부여한 session id 등의 정보가 전달되는 것을 볼 수 있다.
3. (Server -> Client) Certificate/Server Hello Done 메시지
   * Certificate(Server Certificate) 메시지를 통해 서버 측 인증서 목록이 전달되고 있으며 Server Hello Done 메시지를 통해 Server Hello 과정을 종료하고 있다.
4. (Client -> Server) Client Key Exchange/Change Cipher Spec/Finished 메시지
   * Client Key Exchange 메시지를 통해 암호화된 premaster secret를 전달하고 있으며 Change Cipher Spec 메시지를 통해 협상한 암호 명세를 이후부터 적용/변경함을 상대방에게 알린다.
5. (Server -> Client) Change Cipher Spec/Finished 메시지
   * Change Cipher Spec 메시지를 통해 협상한 암호 명세를 이후부터 적용/변경함을 상대방에게 알리고 Finished 메시지를 통해 서버 측 협상을 종료한다.
  
### 6) 단축 협상 과정
#### (가) (Client -> Server) Client Hello 메시지
1. 사용할 session id와 client random을 전달하는 메시지

#### (나) (Server -> Client) Server Hello 메시지
1. server random을 전달하는 메시지

### 7) 단축 협상 과정 패킷 분석
1. (Client -> Server) Client Hello 메시지
   * Client Hello 메시지를 통해 사용할 session id 정보를 전달한다.
   * 서버 측에서는 해당 session id가 존재할 경우 기존 세션을 재사용하고 없다면 새로운 session id를 부여하여 Server Hello 메시지를 통해 전달한다. 새로운 session id를 부여받은 클라이언트는 기존 세션이 종료한 것으로 판단하고 완전 협상을 진행한다.
   * 해당 연결 동안 사용할 키 블럭을 생성하기 위한 client random 값을 전달한다.(세션의 master secret와 조합하여 키 블럭 생성)
2. (Server -> Client) Server Hello/Change Cipher Spec/Finished 메시지
   * 클라이언트가 요청한 session id가 서버에 존재하기 때문에 Server Hello 메시지를 통해 동일한 session id 정보를 전달하고 있다.
   * Change Cipher Spec 메시지를 통해 협상한 암호 명세를 이후부터 적용/변경함을 클라이언트에 알리고 Finished 메시지를 통해 서버 측 협상을 종료한다.
   * 일정 시간 클라이언트의 요청이 없으면 서버 측 세션 정보는 만료된다. 만료된 세션을 클라이언트가 요청하게 되면 위 예처럼 새로운 세션 ID를 생성하여 클라이언트에 전달한 후 완전 협상 과정을 수행한다.
3. (Client -> Server) Change Cipher Spec/Finished 메시지
   * Change Cipher Spec 메시지를 통해 협상한 암호 명세를 이후부터 적용/변경함을 서버에 알리고 Finished 메시지를 통해 클라이언트 측 협상을 종료한다.
4. 정리하면 단축 협상 과정은 Client Hello 메시지를 전송하여 session id와 client random 값을 전송한다. session id가 없다면 부여하고 완전 협상을 진행한다. Server Hello 메시지를 전송하여 server random 값을 전달하고, change cipher spec 메시지를 전송하여 협상한 암호 명세를 이후부터 적용/변경함을 알리고 finished로 서버 측 협상 종료. Client에서 Change Cipher Spec 메세지를 통해 협상한 암호 명세를 이후부터 적용/변경함을 알리고 finished로 클라이언트 측 협상 종료한다.

### 8) Record 프로토콜 동작방식
1. 단편화
   * 애플리케이션 데이터를 일정 크기로 단편화한다.
2. 압축
   * 단편화된 데이터를 협상을 통해 적용된 압축 알고리즘으로 압축한 후 MAC값을 계산하여 추가한다.
3. 암호화
   * 압축된 데이터와 MAC값을 협상을 통해 적용된 암호 알고리즘으로 암호화한다.
4. Record 헤더 추가
   * 암호화된 데이터에 Record 헤더를 추가하여 전송한다.

### 9) SSL/TLS와 완전 순방향 비밀성(PFS: Perfect Forward Secrecy)
#### (가) SSL/TLS 통신의 서버 개인키 노출 시 문제점
1. 서버의 공개키와 개인키를 이용하여 키 교환을 수행할 경우(RSA 방식) 공격자는 중간자 공격(MITM)을 통해 트래픽을 가로채고 서버 개인키를 이용해 세션키/비밀키 및 송수신 데이터를 복호화할 수 있다.
2. 희생자는 유출된 서버 인증서를 폐기해도(CRL 또는 OCSP 프로토콜을 통해) 유출된 서버 개인키로 보호되는 이전 트래픽 정보를 공격자가 보관하고 있다면 이들 모두 복호화되는 문제점이 있다.
3. 이러한 문제점을 해결하기 위해 등장한 암호학적 성질을 순방향 비밀성 또는 완전 순방향 비밀성이라 한다.
4. 정리하면 RSA 방식을 사용할 경우 MITM을 통해 트래픽을 가로채고 서버 개인키를 이용해 세션키/비밀키 및 송수신 데이터를 복호화할 수 있다. 인증서를 폐기해도(CRL, OCSP) 유출된 서버 개인키로 모두 복호화되는 문제점이 있는데 이 문제점을 해결하기 위해 등장한 완전 순방향 비밀성(PFS:Perfect Forward Secrecy)

#### (나) 완전 순방향 비밀성(PFS)
1. 서버 개인키가 노출되어도 이전 트래픽 정보의 기밀성은 그대로 유지되는(과거의 세션키가 노출되지 않는) 암호학적 성질을 말한다.
2. 좀 더 구체적으로 정의해보면, **클라이언트 서버 간에 키 교환에 사용되는 서버 개인키가 노출되어도 이전 트래픽의 세션키/비밀키 기밀성은 그대로 유지되어 통신 내용을 알 수 없는 암호학적 성질**을 말한다.
3. 정리하면 완전 순방향 비밀성(PFS)는 서버의 개인키가 노출되어도 트래픽의 세션키/비밀키 기밀성은 그대로 유지되어 통신 내용을 알 수 없다.

#### (다) SSL/TLS 통신의 완전 순방향 비밀성 지원
1. 키 교환 시마다 클라이언트/서버가 새로운 Diffie-Hellman 개인키를 생성하는 임시 디피-헬만 키 교환을 통해 클라이언트/서버간 공통의 비밀값을 생성하고 서버 개인키는 서버 Diffie-Hellman 파라미터를 인증하는 목적으로만 사용함으로써 서버 개인키가 노출되어도 통신 내용을 알 수 없는 완전 순방향 비밀성을 지원한다.
2. 정리하면 임시 Diffie-Hellman 키 교환을 통해 클라이언트/서버간 공통의 비밀값을 생성하고 서버 개인키는 Diffie-Hellman 파라미터를 인증하는 목적으로만 사욤함으로써 개인키 노출에도 통신 내용 유출이 안된다.

#### (라) 완전 순방향 비밀성만 적용하기 어려운 이유
1. 디피-헬만 키 교환의 경우 RSA에 비해 처리 속도가 느리다. 따라서 성능상의 이유로 DHE, ECDHE 관련 cipher suite을 비활성화하는 경우가 있다.
2. 모든 웹 브라우저에서 다양한 DHE, ECDHE 관련 cipher suite을 모두 지원하지 않기 때문에 브라우저 호환을 위해 RSA 방식의 키 교환을 함께 사용하는 경우가 있다.
3. 정리하면 완전 순방향 비밀성만 적용하기 어려운 이유는 DH는 RSA에 비해 속도가 느리고, 모든 웹브라우저에서 DHE, ECDHE를 지원하지 않는 경우가 많아 적용하기 어렵다.
