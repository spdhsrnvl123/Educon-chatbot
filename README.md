# 건설산업교육원 FAQ 챗봇

> 건설산업교육원의 전화 문의를 줄이기 위해 개발한 FAQ 챗봇 서비스입니다.

![React](https://img.shields.io/badge/React-19.x-61DAFB?logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4.x-06B6D4?logo=tailwindcss)
![Vite](https://img.shields.io/badge/Vite-7.x-646CFF?logo=vite)

## 프로젝트 소개

건설산업교육원에서는 수강신청, 교육비, 수료증 발급 등 반복되는 문의 전화가 많았습니다.  
이를 해결하기 위해 **FAQ 기반 챗봇**을 개발하여 사용자가 빠르게 답변을 찾을 수 있도록 했습니다.

### 개발 목표
- 반복되는 전화 문의 감소
- 24시간 자동 응답 제공
- 직관적인 카테고리 기반 탐색
- 키워드 검색으로 빠른 답변 찾기

## 데모

**Live Demo**: [https://chatbot-taupe-two-95.vercel.app](https://chatbot-taupe-two-95.vercel.app)

## 주요 기능

### 1. 카테고리 기반 탐색
- 6개 대분류: 수강신청, 수강·수료, 회원정보, 교육비, 결제·환불, 온라인강의
- 중분류 → 질문 선택 → 답변 확인의 직관적인 흐름

### 2. 키워드 검색 & 자동완성
- 질문/답변 내용에서 키워드 검색
- 입력 중 추천 검색어 자동완성
- 카테고리/서브카테고리 키워드 매칭

### 3. 반응형 디자인
- 모바일/태블릿/PC 대응
- 최대 너비 제한으로 가독성 확보

### 4. 상담 연결
- 카카오톡 상담 버튼
- 전화 연결 버튼

## 기술 스택

| 분류 | 기술 |
|------|------|
| **Frontend** | React 19, TypeScript |
| **상태관리** | Zustand |
| **스타일링** | Tailwind CSS |
| **빌드 도구** | Vite |
| **배포** | Vercel |
| **아이콘** | Lucide React |

## 프로젝트 구조
```
src/
├── components/
│   ├── chat/                 # 채팅 관련 컴포넌트
│   │   ├── category-buttons.tsx
│   │   ├── subcategory-buttons.tsx
│   │   ├── question-buttons.tsx
│   │   ├── navigation-buttons.tsx
│   │   ├── search-results.tsx
│   │   ├── subcategory-results.tsx
│   │   └── chat-input.tsx
│   ├── layout/
│   │   └── chat-header.tsx
│   ├── chat-message.tsx
│   └── typing-indicator.tsx
│
├── stores/                   # Zustand 스토어
│   ├── message-store.ts      # 메시지 상태
│   ├── navigation-store.ts   # 네비게이션 상태
│   └── search-store.ts       # 검색 결과 상태
│
├── hooks/
│   └── use-chat-search.ts    # 검색 커스텀 훅
│
├── types/                    # 타입 정의
│   ├── index.ts
│   ├── chat.ts               # Message, DisplayType
│   ├── faq.ts                # Category, SubCategory, Question
│   └── search.ts             # SearchResult, Suggestion
│
├── db/                       # FAQ 데이터
│   ├── index.ts
│   ├── enrollment.ts         # 수강신청
│   ├── completion.ts         # 수강·수료
│   ├── member.ts             # 회원정보
│   ├── tuition.ts            # 교육비
│   ├── payment.ts            # 결제·환불
│   └── online.ts             # 온라인강의
│
├── data/
│   ├── keywords.ts           # 검색 키워드 매핑
│   └── suggestions.ts        # 추천 검색어
│
└── pages/
    └── chatbot-page.tsx      # 메인 페이지
```

## UI/UX 특징

- **타이핑 인디케이터**: 봇 응답 전 로딩 애니메이션
- **메시지 애니메이션**: 새 메시지 페이드인 효과
- **이미지 모달**: 답변 내 이미지 클릭 시 확대 보기
- **네비게이션**: 이전으로/처음으로 버튼으로 쉬운 탐색
- **한글 입력 지원**: IME 조합 중 중복 전송 방지

## 개발자

- **이름**: 이태형
- **이메일**: spdhsrnvl456@gmail.com

## 참고사항

**본 프로젝트는 건설산업교육원에서 서비스 중인 프로젝트입니다.**
