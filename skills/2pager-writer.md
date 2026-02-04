---
name: 2pager-writer
description: 2-pager 문서 작성 도우미. "2pager 작성해줘", "2페이저 만들어줘", "2-pager 써줘" 등의 요청에 트리거됩니다. 6단계 워크플로우를 통해 목표 설정, 레퍼런스 수집(Wiki, Amplitude, Jira), 아웃라인 작성, 문서 작성, Confluence 페이지 생성까지 지원합니다.
---

#2-Pager Writer

무신사 2-pager 문서 작성을 위한 단계별 가이드입니다.

## 워크플로우 개요

2-pager 작성은 6단계로 진행됩니다:

1. **목표 확인** → 해결할 문제와 전달한 스토리 파악
2. **레퍼런스 수집** → Wiki, Amplitude, Jira에서 데이터 수집
3. **아웃라인 작성** → 문서 구조 제안 및 확인
4.  **문서 작성** → 2-pager 템플릿으로 작성 (또는 수정 반복)
5. **Confluence 위치 확인** → 페이지 생성 위치 질문
5. **Confluence 생성** → 최종 페이지 생성

## Step 1: 목표 확인
사용자에게 다음을 질문합니다:
> **해결하고자 하는 문제**와 **전달하고 싶은 핵심 스토리**가 무엇인가요?
>
>예시:
> - 문제: "상품 등록 리드타임이 너무 길어 상품 판매 시작이 늦어짐"
> - 스토리: "상품 등록 리드타임을 줄여 빠른 판매 시작을 통한 매출 증대 달성"

---

## Step2: 레퍼런스 수집

모든 소스에서 관련 데이터를 수집합니다:

### 검색 도구
- **Confluence Wiki**:
'MCP_plugin_atlassian_atlassian_search' 또는 'MCP_plugin_atlassian_atlassian_searchConfluenceUsingCql'
 - **JIRA**:
'MCP_plugin_atlassian_atlassian_searchJIRAIssueUsingJql'
 - **Amplitude**:
'MCP_Amplitude_search', 'MCP_Amplitude_query_dataset', 'MCP_Amplitude_query_charts'
-   **Google Drive**: 'MCP_google_drive_search' (MCP 연결 필요)

*** 수집 대상
1. 현재 비즈니스 지표 (GMV, 전환율,  DAU 등)
2. 사용자 피드백 및 Pain points
3. 경쟁사 분석 자료
4. 관련 기존 문서 및 정책
5. 실험 결과 및 인사이트

### 출처 표기 규칙
모든 데이터에 'Source : [링크]' 형태로 출처를 명시합니다.

### 도구 호출 실패 시 대응

- **Confluence/JIRA 접근 실패**: 사용자에게 Atlassian 연결 상태 확인 요청
- **Amplitude 접근 실패**: 사용자에게 직접 데이터 제공 요청하거나, 해당 섹션 "데이터 미확보" 표기
- **Google Drive** 미연결: MCP 서버 설정 필요 안내, 또는 사용자가 직접 파일 공유

---
## Step 3: 아웃라인 작성

수집된 레퍼런스를 바탕으로 문서 아웃라인을 작성하고 사용자에게 확인을 요청합니다:

> 다음 아웃라인으로 진행해도 될까요?
>
> 1. Executive Summary: [핵심 요약]
> 2. Problem Definition: [문제 정의]
> 3. Solution Proposed: [가설 및 해결책]
> ...

---

## Step 4: 문서 작성

사용자가 아웃라인을 승인하면 템플릿에 맞춰 전체 문서를 작성합니다.
승인하지 않으면 구체적으로 질문합니다:

> 어떤 부분을 수정할까요?
> - 문제 정의가 다른가요?
> - 추가로 포함할 레퍼런스가 있나요?
> - 해결책의 방향성을 바꿔야 할까요?


수정 후 Step 2-3을 반복합니다.

**종료 조건: ** 사용자가 아웃라인을 승안하면 문서 작성을 완료하고 Step 5로 진행합니다.
최대 3회 반복 후에도 합의되지 않으면 현재 상태에서 진행 여부를 사용자에게 질문합니다.

---

## Step 5: Confluence 위치 확인

문서 작성이 완료되면:

> Confluence 페이지를 어느 Space에 생성할까요?
> - Space 이름 또는 URL을 알려주세요.
> - 상위 페이지가 있다면 함께 알려주세요.

---

## Step 6: Confluence 생성

'mcp_plugin_atlassian_atlassian_createConfluencePage' 도구를 사용하여 페이지를 생성합니다.

---

## 2-Pager 템플릿 구조

### 필수 섹션
1. **Executive Summary** - 핵심 요약 (두괄식)
2. **Problem Definition** - 문제 정의 (데이터 기반)
3. **Solution Proposed** - 해결책 (ASIS/TOBE 테이블)
4. **Financial Forecasting** - 재무 검토 (비용/수익 관련 시 필수)
5. **Metrics** - Success Criteria + Guardrail Metrics
6. **Negative Impact to Monitor** - 부정적 영향 모니터링
7. **특허출원 검토** - 신규 기술 구현 시 필수
8. **AB Test 진행 여부** - 26점 이상 시 실험 권고

### 부가 섹션
9. **Next Step** - 후속 과제
10. **Alternative Proposed** - 대안
11. **Appendix** - 참고 자료

### 작성 순서 권장
1. Executive Summary (마지막에 최종 수정)
2. Problem Definition → Solution Proposed (핵심)
3. Metrics** - Success Criteria + Guardrail Metrics
4. 나머지 필수 섹션
5. 부가 섹션 (필요시)

---

## 작성 원칙

1. **두괄식 작성**: Executive Summary만 읽어도 핵심 파악 가능
2. **데이터 기반**: 모든 주장에 출처 명시
3. **한국어 작성**: 모든 내용은 한국어로 작성
4. **테이블 활용**: Solution Proposed는 ASIS/TOBE 테이블 사용
5. **레퍼런스 링크**: Appendix에 모든 참고 자료 정리
