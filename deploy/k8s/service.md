# Service

- [공식문서](https://kubernetes.io/docs/concepts/services-networking/service/)

### Service는 복수의 Pod로 배포된 동일한 앱을 하나로 묶어서 관리.

- 하나의 서버 어플리케이션은 복수의 Pod들에서 개별적으로 실행될 수 있음.
- 각 Pod에서 실행 중인 어플리케이션들을 서로 별개로 보지 않고, 전부 `하나의 네트워크 요소로 간주되도록 외부에 노출`시켜주는 것이 서비스의 역할
- 복수의 Pod를 로드밸런서를 이용하여 하나의 IP 주소와 Port로 묶어서 하나의 서비스로 제공하는 구조.

### Service 정의 방법

1. Pod를 생성할 때 오브젝트 스펙의 metadata 정보로 라벨을 지정.

2. 서비스를 정의할 때 라벨 셀렉터(spec.selector)의 값으로 Pod의 라벨을 선택하면 해당 라벨을 지닌 Pod를 대상으로 서비스가 생성됨.

3. ports 정보에서는 컨테이너의 어떤 포트번호(targetPort)를 외부로 어떠한 포트번호(port)로 노출시킬 것인지 지정.

### 부록: Label과 Label Selector

- 핵심: 로드밸런싱할 Pod들의 목록을 지정하기 위해 각 Pod가 지니는 고유한 IP 주소를 그대로 사용하면 안됨.

  - 오토 스케일링(Auto Scaling)으로 인해 Pod는 동적으로 꾸준히 새롭게 생성되고 삭제되며, 생성되는 Pod는 매번 별개의 IP 주소를 지니게 되기 때문임.

- 꾸준히 변하는 Pod 목록을 로드밸런서가 유연하게 선택하기 위해서 `같은 종류의 Pod들에 공통적으로 지정된 라벨(label) 값`을 라벨 셀렉터(label selector)가 선택하도록 하는 것.
