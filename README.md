# SpartaArcade (UE5 Multiplayer Bomber Game)

![Unreal Engine](https://img.shields.io/badge/Unreal%20Engine-5.4+-0E1128?logo=unrealengine&logoColor=white)
![C++](https://img.shields.io/badge/C++-17%20/%2020-00599C?logo=c%2B%2B&logoColor=white)
![Epic Online Services](https://img.shields.io/badge/Epic%20Online%20Services-EOS-blue)

## 👤 내 역할 — 최정빈 (기획 · PM)

> 4인 팀 프로젝트 [NBcampUnrealTrack/8th-Team1-CH4-Project](https://github.com/NBcampUnrealTrack/8th-Team1-CH4-Project) 백업입니다. 제가 맡은 범위와 대표 커밋을 정리했습니다. · [기획 포트폴리오 (Notion)](https://www.notion.so/3fb5b2866264812a9bccc18ac9a6b783)

| 구분 | 범위 |
|---|---|
| 기획 · PM | 맵 생성 규칙(97×97, 8×8 방 슬롯, 스폰 주변 반경 3칸 비움), 아이템 · 스탯 성장(드롭 확률, 타입별 특화 스탯), 자기장 페이스, 레벨 디자인 |
| 직접 구현 | 압사 자기장 시스템, 스폰 보호 로직, 이동 속도 단계 조정, HUD · 미니맵 · 킬로그 UI (맵 생성 구현은 팀원) |

**대표 커밋**
- [`9e18716`](https://github.com/j1b2c3/SpartaArcade/commit/9e18716d457b78f5691de2b48c967ca4309fa786) 이동 속도 단계 격차 조정(기본 200 → 250, 단계당 100 → 50), 자기장 크기 · 시작 시간 조정
- [`15837e4`](https://github.com/j1b2c3/SpartaArcade/commit/15837e4b61cb30ca9ed0248f881d83b67c2cac01) 자기장 판정 수정
- [`b45604a`](https://github.com/j1b2c3/SpartaArcade/commit/b45604a6ada353a889ce6c251697882ab2048a94) 스폰 보호 로직 · 위젯 호출 버그 수정
- [`f419dbf`](https://github.com/j1b2c3/SpartaArcade/commit/f419dbfac5cc3e32838e1a8470776b20889f30b9) HUD 갱신 효율 개선, 생존자 수 산출 방식 수정
- [`f6d71c9`](https://github.com/j1b2c3/SpartaArcade/commit/f6d71c9fd31a6042cf8d3c70d4b8992cde2c1965) 미니맵 구현
- [`0b9d2e5`](https://github.com/j1b2c3/SpartaArcade/commit/0b9d2e5ba3c1fc88f2b7b5239b8fd87dd76880f3) 킬로그 추가


**SpartaArcade**는 Unreal Engine 5와 C++를 기반으로 개발된 **멀티플레이어 아케이드 봄버(Bomber) 게임**입니다. 클래식 봄버맨 스타일의 규칙에 현대적인 **GAS(Gameplay Ability System)** 아키텍처와 **EOS(Epic Online Services)** 멀티플레이어 매칭 환경을 결합하였습니다.


게임 다운로드 : https://drive.google.com/drive/my-drive

---

## 🎮 Key Features (핵심 기능)

1. **GAS 기반 능력 및 아이템 시스템**
   * 폭탄 설치, 구급상자 자가회복, 쉴드 방어막 활성화 등 다양한 액션을 Gameplay Ability System으로 유연하고 강력하게 처리합니다.
   * 복제(Replication)를 지원하는 `AttributeSet`을 통해 속도, 폭탄 범위, 보유 한도 등의 실시간 스탯 변화가 지연 없이 모든 클라이언트에 동기화됩니다.

2. **EOS(Epic Online Services) 멀티플레이 세션**
   * Dedicated Server/Listen Server 환경에서 세션 생성, 검색 및 가입을 원활히 지원합니다.
   * 심리스 트래블(Seamless Travel)을 적용하여 로비에서 인게임 맵으로 로딩 끊김 없이 전원이 동시에 안전하게 이동합니다.

3. **실시간 팀/솔로 랭킹 산정 및 매치 결과 시스템**
   * 서바이벌 방식의 탈락 연산을 실시간으로 처리합니다.
   * 플레이어가 죽을 때마다 실시간으로 살아있는 플레이어 수와 팀 수를 계산하여 최종 스코어 및 랭킹 결과를 리더보드에 업데이트합니다.

4. **실시간 관전(Spectate) 기능**
   * 게임에서 조기 탈락하더라도 다른 플레이어들을 관전할 수 있는 모드를 제공합니다.
   * 뷰타겟 전환 및 대상 플레이어의 체력/실드/스탯 정보를 내 HUD 화면에 실시간으로 바인딩하여 밀착도 높은 관전 경험을 제공합니다.

---

## 🛠️ Tech Stack (사용 기술 및 환경)

* **Game Engine**: Unreal Engine 5 (v5.4+)
* **Programming**: C++ 17/20, Blueprints
* **Framework**: Gameplay Ability System (GAS), Enhanced Input System
* **Network & Matchmaking**: Epic Online Services (EOS) SDK
* **UI**: UMG (Unreal Motion Graphics) C++ bindings

---

## 📁 Project Structure (프로젝트 주요 구조)

```text
Source/SpartaArcade/
├── Characters/         # 플레이어 캐릭터 및 입력/조작 처리를 위한 C++ 컨트롤러 클래스
│   ├── Public/Private/SpartaArcadeCharacter
│   └── Public/Private/SpartaArcadePlayerController
├── Framework/          # 게임 모드, 상태 관리 및 세션 전환 핵심 프레임워크
│   ├── InGame/         # 인게임 규칙 (SpartaGameMode, SpartaGameState, SpartaPlayerState)
│   └── Lobby/          # 로비 규칙 (LobbyGameMode, LobbyPlayerController)
├── Systems/            # GAS 어빌리티(폭탄 설치 등) 및 어트리뷰트 셋 구현
│   └── Public/Private/GA_PlaceBomb, BomberAttributeSet
└── UI/                 # HUD 메인 게이지 및 타이틀/로비/일시정지/결과창 UI 컨트롤러
    └── Public/Private/SpartaHUDWidget, SpartaMenuFlowWidget
```

---
