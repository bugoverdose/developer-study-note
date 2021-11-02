# Pod

### Pod는 쿠버네티스에서 가장 기본적인 배포 단위

- 쿠버네티스는 개별 컨테이너를 하나씩 배포하는 것이 아니라 Pod 단위로 배포함.
- 하나의 Pod에 하나 이상의 도커 컨테이너가 포함되어 함께 실행됨.

### 주요 특성

같은 Pod에 속한 컨테이너들은 동일한 IP 주소와 디스크 볼륨을 공유함. 때문에 컨테이너 간 상호작용 용이.

1. 각 컨테이너의 포트번호를 통해 서로 localhost:8080, localhost:7001 등의 방식으로 간단하게 서로 통신 가능.

2. 하나의 Pod 내에서 컨테이너들끼리 디스크 볼륨을 공유 가능.

3. Side Car Pattern : 애플리케이션과 애플리케이션에서 사용하는 주변 프로그램을 하나의 Pod로 묶어서 함께 배포하는 패턴

### 부록: Volume

- Pod 단위로 배포되는 외장 디스크
- 같은 Pod에 속한 복수의 컨테이너들에서 특정 볼륨을 공유하여 사용하도록 설정 가능.
- 디폴트 설정: 영구적이지 않음.
  - 컨테이너가 재시작되거나 새로 배포될때마다 Pod 설정에 따라 로컬 디스크도 매번 새롭게 정의되서 배포됨.
  - 때문에 디스크에 기록된 내용은 매번 유실됨.
- 심화 학습 주제: PV(PersistentVolume), PVC(PersistentVolumeClaim)