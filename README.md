# 웹 서비스 배포 연습 레포

AWS, Spring boot를 활용한 웹 서비스 구현 및 CI/CD 연습용 저장소<br>


## 기술 스택

| 계층 | 사용 기술 |
|------|-----------|
| **Backend** | Spring Boot · Spring Security · Spring Data JPA · JUnit |
| **Auth** | OAuth 2.0 (Naver, Google) |
| **CI/CD** | GitHub → Jenkins (Gradle 빌드) → Amazon S3 (아티팩트) → AWS CodeDeploy |
| **Infra** | Amazon EC2 · Amazon RDS (MariaDB) |
---
## 구현 기능
- **회원 인증/인가**  
  - OAuth 2.0 Login (Naver, Google)  
  - Spring Security 기반 세션 관리
- **게시글 CRUD** (`/posts`)  
  - JPA · Spring Data 리포지터리  
  - 엔티티, DTO, Service, Controller 계층 분리
- **테스트 코드**  
  - JUnit5 단위 테스트  
  - 통합 테스트 (H2 In-Memory DB)
    
## 아키텍처 상세

1. **개발자**가 GitHub에 코드를 Push  
2. **Jenkins**가 Webhook 이벤트(선택)를 받아 파이프라인 실행 (Jenkins에서 수동 실행도 가능)  
   - `clean build` 로 JAR 생성  
   - 테스트(JUnit) 수행  
3. 완성된 JAR을 **Amazon S3**(Artifacts Bucket)로 업로드  
4. **AWS CodeDeploy**가 S3 아티팩트를 받아 대상 **EC2** 인스턴스에 배포  
5. **EC2** 애플리케이션은 **Spring Boot**로 동작하며, **Amazon RDS(MariaDB)** 와 연결  
6. 사용자는 OAuth 2.0(네이버·구글)로 로그인 후 서비스를 이용  

---


## 아키텍처

![아키텍처](https://github.com/user-attachments/assets/50618884-62fc-43bd-b528-f9441172f987)
