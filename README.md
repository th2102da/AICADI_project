# **AI Cadi 로봇 서비스 소개**

AI Cadi는 XYZ사의 스토리지 로봇 플랫폼을 기반으로 구현된 스마트 캐디 로봇 서비스입니다. 이 로봇은 고객 행동 인식, 고객 추적, 안내, 그리고 충돌 방지 기능을 통해 효율적인 서비스와 안전한 이동을 지원합니다. 특히, AI 2D/3D pose estimation 기술로 고객의 스윙자세를 분석해주고, SAM2 모델과 융합한 로봇 네비게이션 기술로 실내/실외 골프장에서 고객 경험을 혁신적으로 향상시킵니다.

---

> **소개영상**
> 

https://www.youtube.com/watch?v=jCcdT3CDg8U

**1. 행동 인식 및 자세 분석**

- 고객의 행동을 실시간으로 인식하고 준비된 Task를 수행합니다.
- 골프 스윙 영상 분석을 통해 8가지 주요 동작 프레임을 반환하며, 자세 교정과 피드백에 활용됩니다.
- 골프 스윙에 대한 **3D Human Pose Estimation(HPE)**을 생성하여 고객의 자세를 세밀하게 분석합니다.

**2. 고객 추적**

- 실외 필드 환경에서 고객을 효과적으로 추적합니다.
- 한 번 등록된 고객을 서비스 종료 시까지 기억하며, 원활한 서비스를 제공합니다.
- 바운딩 박스 길이를 활용하여 고객의 위치를 추정하고, 로봇의 이동 명령을 생성합니다.

**3. 고객 안내**

- 등록된 고객을 안내 데스크에서 클럽 하우스나 출입구로 안내합니다.
- **네비게이션 패키지**를 활용하여 목적지까지 효율적으로 이동합니다.

**4. 충돌 방지**

- **LiDAR 데이터**를 이용한 실시간 장애물 인식 및 회피 알고리즘이 탑재되어 안전한 이동을 보장합니다.
- **Depth Estimation** 기술을 활용하여 후방 충돌을 예방합니다.

---

**주요 기술 구성 요소**

- **LiDAR SLAM**: 실내 및 실외 자율주행 구현
- **ROS2**: 로봇 운영 시스템 및 데이터 처리
- **Simulation**: LiDAR 및 Depth 데이터 기반 알고리즘 테스트
- **Depth-Anything V2**: 깊이 인식 및 충돌 방지
- **Action Recognition**: 행동 인식 및 자세 분석
- **Tello Drone Control**: 드론 제어 및 실시간 데이터 통합
- **Embedded SW**: 임베디드 시스템 개발
- **ArUco Markers**: 주차 및 물체 위치 검출

---

**프로젝트 팀 구성**

| 이름 | 역할 |
| --- | --- |
| 김현우 | 고객 추적 및 HPE(Human Pose Estimation) 구현, FastAPI를 활용한 시스템 통합 및 이벤트 감지 로직 구현 |
| 김태현 | 행동 인식 및 2D HPE 알고리즘 개발, Navigation 시스템을 활용한 실내 자율 추적 구현 |
| 라환철 | Visual SLAM 기술 및 드론 제어 연구, 웹페이지 개발 및 통합 |
| 박성우 | 실내 자율주행 시스템 구현, LiDAR를를 활용한 장애물 회피 및 충돌 방지 알고리즘 개발 |
| 이지헌 | Depth Estimation을 활용한 충돌 방지, ArUco Marker를 활용한 주차 기능 개발, Arduino 기반 드론 제작 |

---

**배운 점**

1. **라이더 센서 활용법**
    - 라이더 센서가 어떻게 작동하는지 알게 되었고, 자율 주행에서 주변 상황을 인지 할때 중요한 역할을 한다는것을 깨달았다. 특히 라이더 센서의 index를 사용해 레이저를 하나씩 센서를 받고 주변 장애물을 인식하는데 활용할수 있었다.
2. **팀워크**
    - 구성원들이 상호 작용 하면서 기술과 속성이 효과적인 방식으로 결합될수 있었고, 모르는 문제에 직면 했을때 서로가 소통하면서 해결해 나갈수 있었다.
3. **시스템 통합의 복잡성**
    - 각 기능은 개별적으로 잘 작동했지만, 전체 시스템으로 통합 시 환경 충돌, 실시간 동작 구현, 기존 코드 수정 등이 많은 난관이었다.

---

**문제 해결**

**장애물 회피 기능**

**상황**:

- 프로젝트 진행중, 지도화된 장소 이외에서 장애물을 회피할수 있는 방법을 고안해 내야 했습니다

**해결 방법**:

- **라이더 센서**를 사용하여 50cm 범위에서 장애물이 감지가 되면 회피기능을 기동하는 방법을 선택 했습니다. 이 기능은 Navigation 패키지가 필요 없을뿐더라 맵핑이 안된 지역에서도 사용할수 있는 이점이 있습니다

**카메라 연결**

**상황**:

- 스토리지 로봇에 있는 카메라를 직접써서 computer vision을 사용해보려고 했으나, 로봇에 입력값이 많고 FPS가 낮아졌습니다

**해결 방법**:

- 라즈베리 파이를 이용해서 카메라를 직접 부착해야 했습니다. 이로 인해서, 더 높은 화질과 FPS를 볼수 있었고 computer vision을 더 수월하게 이용할수 있었습니다.

**ROS 통신**

- 프로젝트 진행 중, 팀 내에 ROS에 대한 경험자가 없어 팀원들이 쉽게 따라올 수 있도록 ROS2 Humble 설치부터 카메라 토픽 구독까지의 과정을 문서화해 공유했습니다. 또한, Future Work로 Issac Sim을 이용해 시뮬레이션을 진행하던 중, Issac Sim 역시 ROS로 토픽을 발행하는 구조임을 알게 되었습니다. 이를 바탕으로, 모든 PC에 Issac Sim을 설치하지 않아도 한 PC에서 Issac Sim을 실행해 토픽을 발행하면, 다른 PC에서 해당 시뮬레이션 내 로봇을 조종할 수 있다는 점을 확인하고 실습해 보았습니다.

---

**문제 해결 접근법**

1. **문제 해결 습관**
    - 오류를 만났을 때 최소 30분간 스스로 해결하려고 노력했습니다.
    - 이를 통해 문제 이해도가 높아지고, 해결한 경우 다른 사람에게 쉽게 설명할 수 있었으며, 유사 문제 발생 시 스스로 해결할 수 있었습니다.
2. **개발자 노트**
    - 오류, 명령어, 해결 방법 등을 체계적으로 기록하여 문제 해결 속도를 크게 향상시켰습니다.
    - 팀원들과 노트를 공유하면 협업의 효율이 배가되었습니다.
