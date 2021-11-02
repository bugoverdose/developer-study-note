# Deployment

### Deployment는 배포 과정을 관리하는 역할

- Pod의 배포, 업데이트, 롤백 등의 과정을 담당하는 RC를 생성하고 관리하는 등 다양한 기능을 포괄적으로 수행하는 상위 개념

- RC와 RS의 상위 추상화 개념으로 기존에는 개발자의 수작업이 필요했던 작업들을 자동화

### 핵심

- Deployment의 오브젝트 스펙은 Pod에 지정된 라벨을 활용하여, 라벨 셀렉터 등으로 desired state에 대해 명시해주는 구조.

- 정의된 Deployment는 `desired state의 유지`를 목표로 함. 특정한 action을 취하도록 지정되지 않음.

- current state를 측정하고 Pod의 재배포, 롤백 등 적절한 action을 자동으로 취함으로써 desired state에 도달하는 것을 목표로 함.

### 부록: RC와 RS

- Replication Controller(RC) : 지정된 숫자만큼 Pod의 복제품을 실행시키고, 실시간으로 관리하는 역할을 수행함.

- ReplicaSet(RS) : RC의 새로운 버전.

- 차이점: 리소스를 선택하는 방법의 차이
  - RC : Equality based selector(같냐/다르냐와 같은 등가 조건을 이용하여 리소스를 선택하는 방법)
  - RS는 Set based selector(집합의 개념을 사용하여 리소스를 선택하는 방법)을 사용
