# 건설산업교육원 FAQ 챗봇

> 건설산업교육원의 반복적인 전화 문의를 줄이기 위해 개발한 FAQ 기반 챗봇 서비스입니다.

![React](https://img.shields.io/badge/React-19.x-61DAFB?logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4.x-06B6D4?logo=tailwindcss)
![Nginx](https://img.shields.io/badge/Nginx-1.20-009639?logo=nginx)
![Rocky Linux](https://img.shields.io/badge/Rocky_Linux-9.5-10B981?logo=rockylinux)

---

## 프로젝트 소개

건설산업교육원에서는 수강신청, 교육비, 수료증 발급 등 반복적인 문의 전화가 하루 수백 건씩 발생하고 있습니다.  
이를 해결하기 위해 사용자가 스스로 질문에 대한 답변을 찾을 수 있는 **FAQ 기반 챗봇 서비스**를 기획·개발했습니다.

본 프로젝트는 단순 챗봇 도입이 아닌,  
**운영 부서의 실제 문의 유형과 응대 흐름을 기반으로 FAQ 구조를 설계**하고  
실서비스 환경에서 안정적으로 운영할 수 있도록 배포 및 서버 환경까지 직접 구성한 프로젝트입니다.

### 개발 목표
- 반복되는 전화 문의 감소
- 24시간 자동 응답 제공
- 직관적인 카테고리 기반 탐색
- 키워드 검색을 통한 빠른 정보 접근


## 서비스 링크

- **Live**: https://chatbot.con.or.kr  
- **Test**: https://vsquare.con.or.kr  


## 주요 기능

### 1. 카테고리 기반 FAQ 탐색
- 수강신청 / 수강·수료 / 회원정보 / 교육비 / 결제·환불 / 온라인강의
- 대분류 → 중분류 → 질문 선택 흐름의 직관적인 UI

### 2. 키워드 검색 & 자동완성
- 질문 및 답변 데이터 기반 키워드 검색
- 입력 중 추천 검색어 자동완성
- 카테고리·서브카테고리 키워드 매칭

### 3. 반응형 UI
- 모바일 / 태블릿 / PC 대응
- 최대 너비 제한을 통한 가독성 확보

### 4. 상담 연결
- 카카오톡 상담 연결 버튼
- 전화 연결 버튼 제공


## 기술 스택

| 분류 | 기술 |
|------|------|
| **Frontend** | React 19, TypeScript, Zustand |
| **스타일링** | Tailwind CSS |
| **빌드 도구** | Vite |
| **서버/운영** | Nginx, Rocky Linux 9.5 |
| **배포** | 로컬 기반 배포 자동화 스크립트 |
| **보안** | SSL 인증서 적용 (HTTPS) |


## 아키텍처
```
[로컬 개발]
코드 수정 → npm run build → dist 폴더 생성

[배포]
./deploy.sh 실행
  ├── 빌드 (npm run build)
  ├── SCP로 서버 업로드
  └── 권한 설정 (chmod, chown, chcon)

[서버 구성]
Nginx (443 포트)
  ├── SSL 인증서 적용
  ├── 정적 파일 서빙 (/var/www/chatbot)
  └── React SPA 라우팅 (try_files)
```

## 프로젝트 구조
```
src/
├── components/
│   ├── chat/                 # 채팅 관련 컴포넌트
│   │   ├── category-buttons.tsx
│   │   ├── subcategory-buttons.tsx
│   │   ├── question-buttons.tsx
│   │   ├── navigation-buttons.tsx
│   │   ├── kakao-contact.tsx
│   │   ├── start-button.tsx
│   │   ├── search-results.tsx
│   │   └── chat-input.tsx
│   ├── layout/
│   │   └── chat-header.tsx
│   ├── chat-message.tsx
│   └── typing-indicator.tsx
│
├── config/                   # 설정 파일
│   ├── companies.ts          # 회사별 설정
│   └── contact.ts            # 연락처 정보
│
├── stores/                   # Zustand 스토어
│   ├── message-store.ts
│   ├── navigation-store.ts
│   └── search-store.ts
│
├── hooks/                    # 커스텀 훅
│   ├── use-chat-handlers.ts
│   ├── use-chat-search.ts
│   └── use-company.ts
│
├── types/                    # 타입 정의
│   ├── chat.ts
│   ├── faq.ts
│   └── search.ts
│
├── db/                       # FAQ 데이터
│   ├── enrollment.ts
│   ├── completion.ts
│   ├── member.ts
│   ├── tuition.ts
│   ├── payment.ts
│   └── online.ts
│
└── pages/
    └── chatbot-page.tsx
```

## 배포 방법
```bash
# 배포 스크립트 실행 (빌드 + 업로드 + 권한 설정)
./deploy.sh
```



## 트러블슈팅 & 문제 해결 방식

문제를 감으로 수정하지 않고,  
**재현 → 원인 범위 축소 → 검증 → 문서화**의 기준으로 대응했습니다.

- **한글 입력 시 메시지 중복 전송**
  - IME 조합 과정과 전송 이벤트가 동시에 처리되는 문제 확인
  - 조합 중 입력과 전송 이벤트 분리 처리

- **Nginx 배포 후 403 오류**
  - 정적 파일 접근 권한 문제 확인
  - 파일 소유자 및 권한 재설정으로 해결

- **500 서버 오류**
  - SELinux 보안 컨텍스트 설정 이슈 확인
  - 정책 수정으로 정상 서비스 복구

- **CI/CD 환경 제약**
  - 서버 접근 제한으로 자동 배포 불가
  - 로컬 빌드 기반 배포 스크립트로 대안 구축


## UI/UX 특징

- **타이핑 인디케이터**: 봇 응답 전 로딩 애니메이션
- **메시지 애니메이션**: 새 메시지 페이드인 효과
- **이미지 모달**: 답변 내 이미지 클릭 시 확대 보기
- **네비게이션**: 이전으로/처음으로 버튼으로 쉬운 탐색
- **한글 입력 지원**: IME 조합 중 중복 전송 방지

## 개선 예정 사항

- [x] Nginx 서버 배포
- [x] SSL 인증서 적용
- [x] 배포 자동화 스크립트 구축
- [ ] Supabase 연동으로 FAQ 데이터 관리
- [ ] 관리자 페이지 개발

## 개발자
- **이름**: 이태형
- **이메일**: spdhsrnvl456@gmail.com
