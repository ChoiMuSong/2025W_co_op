Remote Keyless Entry: 원격 차량 잠금을 할 수 있는 시스템
    - LF (vehicle transmission): 유효범위 확인을 위해 차량해서 발신하는 주파수
    - RF (Digital key transmission): 차량 제어를 위해 디지털 키에서 발신하는 주파수
    - cf. Passive Keyless Entry: 거리를 감지하여 차량을 자동 잠금 해제하는 시스템

RKE 방식
- Near-Field Communication: 13.56MHz, 10cm 이내에서 전자기 유도 방식 Tag 감지
- Bluetooth Low Energy (Bluetooth 4.0): 2.4GHz, 저전력, 저용량 기반 Bluetooth 통신
    - RRSI(Received signal strength indication) 기반 10m 거리 대략적 인식
- UWB(UltraWide Band): 3.1~10.6GHz (초광대역) 이용
    - Time-of-Flight을 활용한 매우 정밀한 거리/위치 측정 가능 (서로 간의 통신에 걸린 시간을 기반으로 계산)
    - STS(Scrambled Timestamp Sequence)를 이용하여 보호된 정보 제공

공격 방식
- 단순 Replay Attack: 도청을 통해 기존에 확보한 신호를 재전송하는 공격, Rolling code(동기화 카운터)를 도입하여 해결 (ex- Keeloq)
- Rolljam Attack: Jamming을 통해 사용자로 하여금 두 번 신호를 보내게 한 후 사용할 수 있는 신호를 확보하는 공격
    - Jamming + Capture (첫 번째 FOB 신호 무효화 및 캡쳐) 
    - Jamming + Replay (두 번째 FOB 신호 무효화 및 첫 번째 신호 대신 사용, 공격자는 자동차가 앞으로 사용할 것이라고 믿는 두 번째 신호를 획득)
- Rollback attack: 카운터 재동기화 과정에서의 취약점을 이용하는 공격
    - Jamming + Capture (첫 번째 FOB 신호 무효화 및 캡쳐) 
    - Capture (두 번째 FOB 신호 캡쳐)
    - 연속된 두 신호를 이용하여 자동차의 카운터를 롤백할 수 있다.
- Replay Attack: 신호를 증폭하여 차량과 사용자 간을 중계하여 사용자의 거리를 속이는 공격 (UWB 이전)
- Distance reduction attack: UWB에 대해 거리를 속이는 공격
    - Early detect/late commit (ED/LC) Attack: Early detect from user and sends commit signal to car (이전 신호를 예측하여 짧은 거리인 것처럼 전송)
    - Cicada attack: Creates distance error by sending repeated signals (Backsearch 알고리즘을 악용하여 공격자의 신호를 direct path로 오인시킴)
    - Ghost peak attack: Occurs signal overshadowing and reduces ToA (STS가 신호가 '언제 시작되었는지' 에 대해서는 보안 불가능하기 때문에 Ghost Peak를 만들어 거리를 속임)
