<div align="center">

# 🦁 Likelion by Team Iris

**코드만 올리면 빌드·배포·장애 진단·수정 PR까지 — AI가 붙은 배포 자동화 플랫폼**

2026 SoftBank Hackathon 1차 예선 · Team Iris

[🎬 데모 영상]() · [🌐 라이브 서비스](https://likelion.uk/) · [📑 발표 자료](https://app.notion.com/p/3ed8bee9ada480b6a0e3d0c504de5730?source=copy_link)

</div>

---

## 💡 왜 만들었나

서비스 배포를 위해서는 Dockerfile, 인프라, CI/CD 파이프라인에 대한 이해가 필요하며, 배포에 실패하면 복잡한 로그 속에서 직접 원인을 찾아야 합니다.

**Likelion**은 이러한 배포 과정을 단순화합니다. **GitHub Repository를 연결하거나 프로젝트 폴더를 입력하는 것만으로 애플리케이션을 배포**할 수 있으며, 배포에 실패하면 **AI가 로그와 코드를 분석해 원인을 진단하고 수정 PR까지 생성합니다.**

또한 Kubernetes의 표준화된 오케스트레이션 환경과 **ArgoCD 기반 멀티 클러스터 GitOps 배포 구조**를 활용해 특정 클라우드에 대한 종속성을 낮췄습니다. 이를 통해 AWS를 비롯한 다양한 클라우드와 On-Premise 환경에서도 **동일한 방식으로 일관된 배포 환경을 제공합니다.**

## ✨ 핵심 기능

- **원클릭 배포** — GitHub 레포 연결 후 push 자동 배포, 또는 로컬 폴더를 CLI `likelion up` 한 번으로 배포. 빌드·배포·도메인(`*.likelion.uk`)까지 자동
- **AI 오류 진단** — 배포가 실패하면 자동으로 빌드·런타임 로그와 소스 스냅샷을 분석해 원인 후보·근거·해결안 제시
- **AI 원클릭 수정** — 버튼 한 번으로 수정안 생성 → 핫픽스 PR → CI 통과 후 main 머지 → 재배포까지 자동
- **GitOps 배포·롤백** — image digest 고정, Argo CD 동기화. 실패 시 직전 정상 release로 자동 롤백, 재빌드 없는 수동 롤백 지원
- **실시간 관측** — 배포 단계별 상태, 런타임 로그 스트리밍(SSE), CPU·메모리·네트워크·트래픽 메트릭
- **AI 코드 분석 (개발 중)** — 소스를 실행하지 않고 Node/Vite/Express/Dockerfile/Compose 구성을 분석해 배포 구성 추론

## 🏗 아키텍처

<img width="1443" height="780" alt="image" src="https://github.com/user-attachments/assets/d13be1d9-f855-4cdf-a0f7-20e60c92db94" />


인프라(VPC·EKS 2개·Argo CD·관측 스택)는 모두 [iris-infra](https://github.com/2026-softbank-1/iris-infra)의 Terraform·Helm 코드로 관리한다.

## 📦 레포지토리

| 영역 | 레포 | 설명 | 스택 |
|---|---|---|---|
| 플랫폼 | [iris-was](https://github.com/2026-softbank-1/iris-was) | Control API · Build/Deploy Worker | FastAPI, PostgreSQL |
| | [iris-web](https://github.com/2026-softbank-1/iris-web) | 대시보드 | React, TypeScript, Vite |
| | [iris-cli](https://github.com/2026-softbank-1/iris-cli) | `likelion` CLI (login · link · up · logs) | TypeScript, Node.js |
| AI 에이전트 | [iris-code-analyzer-agent](https://github.com/2026-softbank-1/iris-code-analyzer-agent) | 레포 정적 분석 · 배포 구성 추론 | Python, OpenCode |
| | [iris-error-check-agent](https://github.com/2026-softbank-1/iris-error-check-agent) | 배포 로그 기반 오류 진단 | Python, OpenCode, RDF/SHACL |
| | [iris-code-fix-agent](https://github.com/2026-softbank-1/iris-code-fix-agent) | 진단 결과 기반 수정안 · PR 생성 | Python |
| 인프라 | [iris-infra](https://github.com/2026-softbank-1/iris-infra) | AWS · EKS · Helm · Argo CD · 관측 스택 | Terraform, Helm |
| | [iris-gitops-environments](https://github.com/2026-softbank-1/iris-gitops-environments) | 사용자 서비스·플랫폼 배포 상태(values) | Argo CD |


## 🛠 Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?logo=react&logoColor=black)
![AWS](https://img.shields.io/badge/AWS-232F3E?logo=amazonwebservices&logoColor=white)
![Kubernetes](https://img.shields.io/badge/EKS-326CE5?logo=kubernetes&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-844FBA?logo=terraform&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?logo=helm&logoColor=white)
![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?logo=argo&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?logo=openai&logoColor=white)

## 👥 Team Iris

| | 이름 | 역할 | 담당 |
|---|---|---|---|
| <img src="https://github.com/kylo-dev.png" width="60"/> | [@kylo-dev](https://github.com/kylo-dev) | Infra · Backend | iris-infra, iris-gitops-environments, iris-was |
| <img src="https://github.com/timbergrizz.png" width="60"/> | [@timbergrizz](https://github.com/timbergrizz) | Infra | iris-infra |
| <img src="https://github.com/Saccharine1211.png" width="60"/> | [@Saccharine1211](https://github.com/Saccharine1211) | Backend · Frontend | iris-was, iris-web, iris-cli |
| <img src="https://github.com/monitor5.png" width="60"/> | [@monitor5](https://github.com/monitor5) | AI Agent · Backend | iris-code-analyzer-agent, iris-code-fix-agent, iris-was |
| <img src="https://github.com/kimhwan1103.png" width="60"/> | [@kimhwan1103](https://github.com/kimhwan1103) | AI Agent | iris-error-check-agent |
