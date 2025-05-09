# wh06-1st-6team-yorijori

# 🍳 개인 맞춤형 레시피 추천 서비스 - 요리조리

**LG U+ Why Not SW Camp 6기**  
**팀명**: 요리조리  
**기간**: 2025.05.07 ~ 2025.05.09

---
<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/4a852ead-e34e-48ba-a308-b9002c91835b" width="200px;" alt="유승환"/><br />
      <strong>유승환</strong><br />
     사업기획, 데이터 분석, 모델링<br />
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/0cd3f662-d873-4c96-b4a3-85c05449f70c" width="200px;" alt="이지헌(팀장)"/><br />
      <strong>이지헌(팀장)</strong><br />
     사업기획, 데이터 분석, 모델링<br />
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/f1267652-550c-4340-98ca-4a8d6c041889" width="250px;" alt="주수진"/><br />
      <strong>주수진</strong><br />
      사업기획, 데이터 분석, 모델링<br />
    </td>
  </tr>
</table>

---

## 🧠 프로젝트 소개

요리조리는 **사용자 정보 + AI 챗봇 대화**를 기반으로 개인의 식습관, 취향, 건강 조건에 맞는 **맞춤형 레시피**를 추천하는 서비스입니다.  
다양한 출처(유튜브, 블로그, 공공 레시피북 등)의 콘텐츠를 통합 검색해, **특정 식단**이나 **기호**에 맞는 레시피를 손쉽게 찾을 수 있습니다.

---

## 🗓 프로젝트 일정

| 기간       | 내용 |
|------------|------|
| 1~2주차    | 서비스 기획, 기술 스택 선정, 데이터 출처 조사 |
|            | 유튜브/블로그/레시피 사이트 크롤링, PDF 텍스트 추출 |
| 3~4주차    | FAISS 구축 및 벡터 임베딩 처리, 유사 레시피 추출 |
|            | 생성형 응답 모델 연동 (LangChain + CLOVA X) |
| 5~6주차    | 사용자 입력 → 검색 → 응답 흐름 연결, UI 기획 |
| 7~8주차    | 기능 테스트, 데이터 보완, 최종 배포 |

---

## 🎯 프로젝트 목적

- AI 챗봇 + 사용자 정보 기반 **맞춤형 레시피 추천 서비스** 구현
- 특이식단 사용자(비건, 저염식 등)도 포함한 **개인 최적화 추천**
- 유튜브, 블로그 등 **다채널 통합 검색** 제공
- 대화 기반 UX를 통해 **친숙하고 재미있는 요리 경험** 제공

---

## 📱 서비스 플로우 및 서비스 화면 기획

**주요 플로우:**

1. 시작화면  
2. 접속화면: 로그인 / 회원가입 / 비밀번호 찾기  
3. 메인화면  
   - 캐릭터 노출
   - 하단 메뉴: 챗봇, 북마크, 칼로리 계산기, 마이페이지  
4. 추천 방식
   - 유튜브/블로그 링크 추천
   - 이미지+텍스트 형태의 레시피북 뷰 지원

![Image](https://github.com/user-attachments/assets/71e684e1-9aa2-4241-ada6-194b92b8a6a2)

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/52a7aca4-7c86-4c7d-b1f7-541f020aaaef" width="300" /></td>
    <td><img src="https://github.com/user-attachments/assets/e72aca1b-bfcb-4731-9684-f0a63bc8e508" width="300" /></td>
    <td><img src="https://github.com/user-attachments/assets/7c1160f5-fafe-41a0-93dd-f9535a447f94" width="300" /></td>
  </tr>
</table>


---

## 🧾 사용 데이터

- **공공 레시피북**: 식약처, 농촌진흥청 배포 PDF 자료
- **온라인 콘텐츠**: 유튜브, 네이버 블로그, 틱톡, 만개의레시피
- **식품 성분 데이터**: 국가표준식품성분표 (10개정판)

---

## 🧬 ERD (개요)

- 사용자 정보 테이블
- 레시피 정보 테이블 (재료, 태그, 출처, 이미지 등 포함)
- 추천 기록 및 북마크 저장 테이블
- 챗봇 대화 로그 및 칼로리 계산 기록 테이블 등
![Image](https://github.com/user-attachments/assets/2581585e-0a93-497f-9839-297d7920d544)

---

## 📊 데이터 활용 및 분석 방법

![Image](https://github.com/user-attachments/assets/2c5d6328-0f5b-4069-aa8b-7092067a2671)


**크롤링**  
- YouTube Data API, Selenium, aiohttp, BeautifulSoup, PyMuPDF  
- 비동기 방식으로 빠른 병렬 처리 구현

**하이브리드 검색 엔진**  
- KoBERT 기반 벡터 임베딩 → FAISS 사용  
- BM25 기반 키워드 검색 → Elasticsearch 사용  
- `final_score = α * vector_score + (1 - α) * keyword_score` 방식 결합

**생성형 AI 챗봇**  
- CLOVA X + LangChain 구조  
- 한국어 자연어 최적화  
- 대화 문맥 유지 기능 지원 (ConversationChain)

**SQL 활용**  
- 사용자별 추천 기록, 검색 조건 저장 및 통계 분석  
- 크롤링 데이터 저장 및 필터링 기반 조회

---

## 🧭 SWOT 분석

| 강점 (Strength)           | 약점 (Weakness)            |
|---------------------------|-----------------------------|
| AI + 개인화로 차별성 확보 | 초기 데이터 품질 편차 존재 |
| 한국어 최적화 모델 활용   | 클라우드 비용 부담         |

| 기회 (Opportunity)        | 위협 (Threat)              |
|---------------------------|-----------------------------|
| 건강 관심 증가 추세 반영 | 경쟁 서비스의 기술 도입 속도 |
| B2B 시장 확장 가능성      | 레시피 콘텐츠 라이선스 문제 |

---

## 💡 서비스 활용 방안

- **일반 사용자용**: 다이어트, 비건 등 특이식단에 맞춘 추천
- **육아 부모용**: 이유식, 유아식 등 레시피 제공
- **요리 초보자**: 도구 기반 쉬운 레시피 탐색
- **브랜드 제휴**: 식재료/가전 마켓 연동
- **B2B 모델**: 단체 급식, 식단관리 업체 대상 레시피 API 제공

---

## 💰 비용 (월 기준)

| 사용자 수 | 예상 비용 (원) |
|-----------|----------------|
| 10,000    | 약 547,500     |
| 50,000    | 약 2,147,500   |
| 100,000   | 약 4,230,000   |

**주요 항목:**

- AWS EC2 + OpenSearch + EBS + 전송
- CLOVA X API 사용료 (HCX-005 기준)
- iOS 앱 개발자 등록 비용: $99/년

---

## 🛠 사용기술스택

### 📦 프레임워크 및 라이브러리
<p align="left">
  <img src="https://img.shields.io/badge/LangChain-000000?style=for-the-badge&logo=OpenAI&logoColor=white"/>  
  <img src="https://img.shields.io/badge/aiohttp-005571?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/BeautifulSoup-4B8BBE?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Selenium-43B02A?style=for-the-badge&logo=selenium&logoColor=white"/>
  <img src="https://img.shields.io/badge/PyMuPDF-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white"/>
</p>

### 🔍 검색 및 추천 엔진
<p align="left">
  <img src="https://img.shields.io/badge/FAISS-000000?style=for-the-badge&logo=Meta&logoColor=white"/>
  <img src="https://img.shields.io/badge/KoBERT-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white"/>
  <img src="https://img.shields.io/badge/Elasticsearch-005571?style=for-the-badge&logo=elasticsearch&logoColor=white"/>
  <img src="https://img.shields.io/badge/BM25-7D4698?style=for-the-badge&logo=search&logoColor=white"/>
</p>

### 🧠 생성형 AI 및 대화형 모델
<p align="left">
  <img src="https://img.shields.io/badge/HyperCLOVA%20X-00C73C?style=for-the-badge&logo=naver&logoColor=white"/>
  <img src="https://img.shields.io/badge/LangChain-000000?style=for-the-badge&logo=openai&logoColor=white"/>
</p>

### 🗃 데이터베이스 및 저장소
<p align="left">
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white"/>
  <img src="https://img.shields.io/badge/FAISS-000000?style=for-the-badge&logo=Meta&logoColor=white"/>
</p>

### ☁️ 인프라 및 클라우드
<p align="left">
  <img src="https://img.shields.io/badge/AWS%20EC2-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white"/>
  <img src="https://img.shields.io/badge/AWS%20S3-569A31?style=for-the-badge&logo=amazon-aws&logoColor=white"/>
  <img src="https://img.shields.io/badge/OpenSearch-005571?style=for-the-badge&logo=elasticsearch&logoColor=white"/>
  <img src="https://img.shields.io/badge/CloudWatch-FF4F00?style=for-the-badge&logo=amazonaws&logoColor=white"/>
  <img src="https://img.shields.io/badge/iOS%20Dev%20Program-000000?style=for-the-badge&logo=apple&logoColor=white"/>
</p>

---
