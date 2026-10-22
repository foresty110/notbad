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

이 저장소는 Android 앱과 백엔드를 함께 관리합니다.

```text
notbad/
├── android/                 # Kotlin, Jetpack Compose 앱
├── backend/                 # Java, Spring Boot 앱
├── docker-compose.yml       # 로컬 MySQL
├── .env.example             # 로컬 DB 기본 환경 변수
├── railway.json             # Railway 배포 설정
└── gradlew                  # Android와 백엔드가 공유하는 Gradle Wrapper
```

## 개발 환경 준비

현재는 빌드 확인을 위한 시작 뼈대입니다. Android 앱은 `notbad` 시작 화면을 표시하고, 백엔드는 Actuator 상태 확인 경로만 제공합니다. 할 일, 로그인, 알림 기능과 Google OAuth 연결은 아직 포함하지 않습니다.

주요 빌드 버전은 Gradle Version Catalog에 고정되어 있습니다: Gradle 8.14.3, Android Gradle Plugin 8.13.2, Kotlin 2.2.21, Compose BOM 2026.06.00, Spring Boot 4.1.1, Java 21.

### 필요한 도구

- Android Studio와 Android SDK Platform 36
- JDK 21 이상
- Docker Desktop 및 Docker Compose

Gradle Wrapper가 빌드 도구 버전을 관리하므로 별도 Gradle 설치는 필요하지 않습니다.

### Android

Android Studio에서 저장소 루트를 열고 Gradle 동기화를 진행합니다. CLI로는 저장소 루트에서 다음 명령을 실행합니다.

```bash
./gradlew :android:app:assembleDebug
```

### 백엔드와 로컬 MySQL

```bash
cp .env.example .env
docker compose up -d mysql
./gradlew :backend:bootRun
```

상태 확인 주소: <http://localhost:8080/actuator/health>

로컬 DB 기본값은 `.env.example`에 있습니다. `.env` 파일은 Git에 포함되지 않습니다. 애플리케이션은 환경 변수 `SPRING_DATASOURCE_URL`, `SPRING_DATASOURCE_USERNAME`, `SPRING_DATASOURCE_PASSWORD`, `PORT`로 설정을 덮어쓸 수 있습니다.

### Railway

저장소를 Railway에 연결하면 `railway.json`이 `backend/Dockerfile`을 사용하도록 지정합니다. Railway 프로젝트에 MySQL 서비스를 추가하고 백엔드 서비스의 `SPRING_DATASOURCE_URL`, `SPRING_DATASOURCE_USERNAME`, `SPRING_DATASOURCE_PASSWORD` 변수를 MySQL 서비스 값으로 연결해야 합니다. `PORT`는 Railway가 제공하는 값을 사용합니다.

Google OAuth 클라이언트 설정과 실제 앱 기능은 기능 구현 단계에서 추가합니다.
