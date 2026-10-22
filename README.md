# notbad

해야 할 일을 등록하고, 정해진 시간에 울리는 알림으로 끈기 있게 실천할 수 있도록 돕는 Android 앱입니다.

## 기술 스택

| 영역 | 기술 |
| --- | --- |
| Android 앱 | Kotlin, Jetpack Compose |
| 로컬 저장 | Room, DataStore |
| 알림 | AlarmManager, Android Notification API |
| 백엔드 | Java, Spring Boot |
| 데이터베이스 | MySQL |
| 배포 | Railway |
| 협업·버전 관리 | Git, GitHub |

## 저장소 구성

이 저장소는 Android 앱과 백엔드를 함께 관리하는 모노레포로 구성합니다.

```text
notbad/
├── android/   # Kotlin, Jetpack Compose 앱
├── backend/   # Java, Spring Boot API
└── docs/      # 설계 및 프로젝트 문서
```

## 주요 설계 기준

- 할 일과 알림 일정은 Android 앱에서 Room으로 관리합니다.
- 앱 설정과 작은 키-값 데이터는 DataStore에 저장합니다.
- 정해진 시간의 알림은 AlarmManager로 예약하고 Notification API로 표시합니다.
- 백엔드 API와 MySQL은 Railway에 배포합니다.
- 소스 변경은 Git으로 관리하고 GitHub에서 협업합니다.
