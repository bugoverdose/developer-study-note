# 쿠버네티스(Kubernetes)

## 기본 구조 (최신 표준)

- 도커 이미지들로 실행되는 도커 컨테이너들을 Pod 단위로 배포
- Pod의 배포는 Deployment에 의해 관리됨
- Service를 통해 Pod들을 묶고 외부에 하나의 IP 주소로 묶어서 노출시킴

1. [Pod](./pod.md)
2. [Deployment](./deployment.md)
3. [Service](./service.md)

## 심화

- [DB 연동](./database.md)
- [쿠버네티스 배포 원리](./update-rollback.md)
- Ingress
