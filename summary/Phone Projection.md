Phone Projection: 휴대전화의 화면을 IVI(In-vehicle Infotainment) display에 맞게 사용자에게 제공하는 것 (미러링에 가까움)
- Apple Carplay, Android Auto 등이 있음
    - Android Automotive는 차랑 자체에 OS가 있음
- USB 케이블 혹은 블루투스나 Wi-Fi로 연결
- GPS Navigation, Phone Call, Message, Music Player 제공
- Minimized driver distraction
    - Voice command integration, simple UI, no media play when driving

MirrorLink: 안드로이드에서 사용되던 Phone Projection, 2023년에 종료됨
- Frame 내부의 DAP가 신뢰할 수 없는 장치를 제한하지 않음
- Heap Overflow에 관한 취약점이 존재하며, 이를 통해 CAN bus에 접근할 수 있는 함수가 허용됨

Apple Carplay components
- Apple Device (iPhone, adapter)
- Carplay Accessory (IVI)
- MFi(Made for iPhone/iPad/iPod) chip

Connection between iPhone and IVI Systems
- USB connection (recognition)
- USB role switch
- iAP2(Inter-Accessory Protocol 2) session
    - Parameter negotiation
    - NCM configuration
    - IVI system Authentication (Authorize accessories with Mfi chip)    
    - IVI system Identification
- CarPlay Session
    - IP Networking and Bonjour Discovery
    - CarPlay Session Authentication
    - Content Transfer and Application Launch

Vulnerability for Apple Carplay
- 아이폰 중심 인증 방식: 아이폰 자체는 인증받지 않기 때문에 ID만 조작한다면 안드로이드 기기도 연결 가능

Vulnerability for Android Auto
- Android Auto는 원칙상 Playstore에 등록된 앱만 사용가능하다, 그러나 일부 앱에서 보안 원칙을 위반하는 경우가 있었다.
- 대표적인 케이스는 Webview 사용으로 인한 XSS, javascript injection 가능성, 운전 도중 Media autoplay가 허용될 여지가 있는 점 등이 있다.

Comments
- 블루투스 같은 기술도 보안에 크게 중점을 두지 않는 것을 보면 Phone Projection도 편의성과 인접성을 바탕에 두기 때문에'사용자만 차량 IVI에 접근할 수 있다'는 전제를 달고 개발된 것으로 보인다.
- Driver Distraction과 관련된 부분은 규제에 포함되어 있지 않음에도 큰 문제가 발생할 여지가 크기 때문에 이와 관련된 보안 기준이 필요할 것으로 보인다. (기존 논문처럼 Static Analysis 활용)