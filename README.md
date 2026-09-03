# study-os

개인 학습과 프로젝트 실행을 하나로 연결하는 로컬 우선(local-first) AI CLI 도구입니다.

공부한 자료를 쌓아두는 데서 끝나지 않고, 자료를 검색하고 질문하며 복습하고, 실제 프로젝트 작업과 Git 기록으로 연결하는 것을 목표로 합니다.

## 이 프로젝트는 무엇을 만드는가

`study-os`는 다음 흐름을 반복해서 사용할 수 있게 만드는 개인용 학습 운영체제입니다.

```text
자료 수집 → 개념 이해 → 복습 → 프로젝트 실행 → 결과 기록 → 포트폴리오 증거
```

사용자는 Markdown, PDF, 웹 자료, 프로젝트 문서를 등록합니다. CLI는 등록된 자료를 바탕으로 질문에 답하고, 부족한 개념을 찾아주며, 복습 문제와 다음 작업을 제안합니다. 프로젝트 작업이 끝나면 Git 커밋과 문서를 분석해 무엇을 배웠고 무엇을 만들었는지 정리합니다.

## 해결하려는 문제

- 공부 자료가 여러 폴더와 서비스에 흩어지는 문제
- 읽은 내용이 실제 코딩 작업으로 이어지지 않는 문제
- AI 답변을 믿을 만한 근거와 함께 확인하기 어려운 문제
- 매일 한 일을 기록하지 않아 나중에 학습 과정을 설명하기 어려운 문제
- AI가 생성한 계획과 답변의 품질을 측정하기 어려운 문제

## 기존 서비스와의 차이점

`study-os`의 기능 중 일부는 이미 다른 서비스에도 존재합니다. 자료 기반 질문은 NotebookLM, Readwise Reader, Khoj 등에서 제공하고, Markdown 지식 관리는 Obsidian과 플러그인으로 구성할 수 있습니다. 터미널에서 AI와 코드를 수정하는 기능은 Aider, GitHub Copilot CLI, Claude Code와 같은 도구가 제공합니다.

따라서 `study-os`는 “세상에 없던 AI 노트 앱”을 만드는 것을 목표로 하지 않습니다. 이미 존재하는 기능을 그대로 복제하는 대신, **학습한 내용을 실제 개발 작업과 Git 기록, 포트폴리오 증거로 연결하는 흐름**에 집중합니다.

```text
NotebookLM / Readwise / Khoj
  = 자료 이해와 지식 관리

Aider / Copilot CLI / Claude Code
  = 코드 작성과 프로젝트 작업

study-os
  = 학습 자료 → 구현 작업 → 코드 변경 → 테스트 → Git 증거 → 포트폴리오
```

### 차별화하려는 핵심 흐름

#### 1. 학습 자료를 코딩 작업으로 변환

```powershell
study ask "SQLite FTS5가 무엇인지 설명해줘"
study plan "방금 배운 FTS5로 검색 기능을 구현해줘"
```

단순히 개념을 요약하는 데서 끝내지 않고, 다음 단계로 연결합니다.

```text
학습 개념 → 구현 목표 → 작은 작업 → 완료 조건 → 테스트 방법
```

#### 2. 작업과 Git 증거 연결

```powershell
study tasks done task-001 --evidence tests/test_search.py
```

학습 기록을 실제 개발 증거와 연결합니다.

```text
개념: SQLite FTS5
구현: 검색 함수 작성
파일: src/study_os/search.py
테스트: tests/test_search.py
커밋: 실제 Git 커밋 ID
```

#### 3. 실제 증거 기반 포트폴리오 생성

포트폴리오를 AI의 추측으로 작성하지 않고 다음 자료를 바탕으로 생성합니다.

- 실제 Git 커밋
- 실제 변경 파일
- 실제 테스트 결과
- 실제 학습 기록
- 실제 프로젝트 문서

이를 통해 “공부했다”는 추상적인 표현을 “무엇을 이해했고, 어떤 코드를 작성했으며, 어떻게 검증했는가”로 바꿉니다.

#### 4. CLI 중심의 학습·개발 흐름

GUI 서비스처럼 자료를 보고 질문하는 데서 끝나지 않고, 학습과 개발의 다음 행동을 터미널에서 이어갑니다.

```powershell
study status
study review
study tasks list
study project status
study portfolio
```

이는 CLI와 바이브 코딩을 배우는 개발자가 자신의 프로젝트 안에서 바로 사용할 수 있도록 하기 위한 방향입니다.

### 차별화의 범위

이 프로젝트는 기존 서비스를 모두 대체하려는 제품이 아닙니다. NotebookLM처럼 완성도 높은 학습 도구를 새로 만들거나, Aider처럼 범용 코딩 에이전트를 재현하는 것이 목표가 아닙니다.

`study-os`의 MVP는 다음 세 명령으로 시작합니다.

```text
study ingest  # 학습 자료 등록
study ask     # 등록한 자료를 근거로 질문
study plan    # 학습 내용을 실제 코딩 작업으로 변환
```

이후 다음 기능을 추가합니다.

```text
study review      # 복습
study task done   # 작업 완료와 증거 연결
study portfolio   # 실제 기록 기반 포트폴리오 생성
```

최종적으로 `study-os`가 제공하려는 핵심 가치는 새로운 AI 기능 하나가 아니라, **공부 → 구현 → 검증 → 기록 → 회고**를 하나의 로컬 우선 CLI 흐름으로 반복하게 만드는 것입니다.

## 핵심 사용자 경험

```bash
# 학습 자료 등록
study ingest ./notes

# 내 자료를 근거로 질문
study ask "RAG와 fine-tuning의 차이를 내 노트 기준으로 설명해줘"

# 목표를 작업 단위로 분해
study plan "SQLite 기반 학습 검색 기능을 이번 주에 완성하기"

# 오늘 복습할 내용과 문제 생성
study review

# 프로젝트 상태와 다음 작업 확인
study project status

# 학습·개발 기록을 포트폴리오 초안으로 변환
study portfolio
```

AI가 파일을 수정하거나 Git 명령을 실행할 때는 변경 예정 내용을 먼저 보여주고 사용자의 승인을 받아야 합니다. 삭제, 커밋, 외부 서비스 호출은 자동으로 실행하지 않는 것을 기본 원칙으로 합니다.

## MVP 범위

첫 번째 버전은 아래 기능만 완성합니다.

1. Markdown 파일을 학습 자료로 등록한다.
2. 등록한 자료를 SQLite 전문 검색으로 찾는다.
3. 검색 결과를 AI에 문맥으로 전달해 근거가 포함된 답변을 만든다.
4. 답변에서 핵심 개념과 복습 문제를 구조화된 데이터로 저장한다.
5. 학습 목표를 작은 프로젝트 작업으로 분해한다.
6. 모든 질문과 결과를 로컬에 기록한다.

벡터 데이터베이스, 웹 대시보드, 다중 사용자 인증, 자동 Git 커밋은 MVP 이후로 미룹니다. 먼저 매일 실제로 사용할 수 있는 CLI 루프를 검증합니다.

## 예상 구조

```text
study-os/
├── README.md
├── pyproject.toml              # 패키지와 개발 도구 설정
├── src/
│   └── study_os/
│       ├── cli.py              # CLI 진입점과 명령어 등록
│       ├── config.py           # 환경 변수와 사용자 설정
│       ├── db.py               # SQLite 연결과 마이그레이션
│       ├── models.py           # 자료, 질문, 복습, 작업 모델
│       ├── ingest.py           # 파일 읽기와 자료 등록
│       ├── search.py           # SQLite FTS5 기반 검색
│       ├── ai.py               # 모델 호출과 구조화된 출력
│       ├── planner.py          # 목표를 작업으로 분해
│       ├── reviewer.py         # 복습 문제와 오답 기록
│       ├── git_context.py      # Git 로그와 diff 읽기
│       └── portfolio.py        # 학습·개발 기록 정리
├── tests/
│   ├── test_search.py
│   ├── test_planner.py
│   └── test_cli.py
├── evals/
│   ├── questions.jsonl         # 대표 질문 데이터셋
│   └── README.md               # AI 답변 평가 기준
├── data/                       # 로컬 데이터; Git에 올리지 않음
└── .env.example                # 필요한 환경 변수 예시
```

## 데이터 흐름

```text
파일/URL
  ↓
ingest
  ↓
정규화된 문서 + 메타데이터
  ↓
SQLite / FTS5
  ↓
질의 분석 및 관련 문서 검색
  ↓
AI 모델
  ↓
답변·출처·개념·복습 문제·작업
  ↓
SQLite + Markdown 기록
```

원본 자료와 사용자의 기록은 로컬에 보관합니다. AI 호출에 전송되는 범위는 검색된 문맥으로 제한하고, API 키는 환경 변수로만 관리합니다.

## 기술 선택

- **언어:** Python
- **CLI:** Typer, Rich
- **저장소:** SQLite
- **검색:** SQLite FTS5부터 시작하고 필요할 때 임베딩 검색을 추가
- **AI:** OpenAI SDK 또는 호환 API 클라이언트
- **테스트:** pytest
- **패키지 관리:** uv 또는 표준 Python 가상환경
- **버전 관리:** Git

처음부터 복잡한 에이전트 프레임워크를 도입하지 않습니다. 명확한 Python 함수와 승인 가능한 도구 인터페이스를 먼저 만들고, 실제 사용 흐름이 확인된 뒤 에이전트 기능을 추가합니다.

## 개발 로드맵

### Phase 0 — 실행 가능한 뼈대

- [ ] Python 패키지 초기화
- [ ] `study --help` 구현
- [ ] 설정 파일과 API 키 로딩
- [ ] SQLite 스키마 작성

### Phase 1 — 학습 자료와 질문

- [ ] `study ingest <path>` 구현
- [ ] Markdown 파싱 및 메타데이터 저장
- [ ] FTS5 검색 구현
- [ ] `study ask <question>` 구현
- [ ] 답변에 문서명과 위치 표시

### Phase 2 — 복습과 계획

- [ ] 개념 추출
- [ ] 복습 문제 생성
- [ ] 정답·오답 기록
- [ ] 학습 목표를 작업 목록으로 분해
- [ ] `study review`, `study plan` 구현

### Phase 3 — 프로젝트 연결

- [ ] Git 로그 및 diff 읽기
- [ ] 프로젝트별 작업 상태 요약
- [ ] 학습 기록과 커밋 연결
- [ ] 포트폴리오 초안 생성

### Phase 4 — 신뢰성과 배포

- [ ] 대표 질문 eval 데이터셋 작성
- [ ] 답변 근거성·정확성·형식 준수 평가
- [ ] 실패 로그와 비용 기록
- [ ] PyPI 또는 GitHub Release 배포

## 품질 기준

이 프로젝트의 성공은 기능 개수보다 실제 사용성으로 판단합니다.

- 새 자료를 30초 이내에 등록할 수 있는가?
- 답변마다 어떤 자료를 참고했는지 확인할 수 있는가?
- AI가 모르는 내용은 모른다고 표시하는가?
- 계획이 추상적인 조언이 아니라 실행 가능한 작업으로 나뉘는가?
- AI 호출 실패나 네트워크 오류가 발생해도 기존 기록이 보존되는가?
- 같은 질문 세트로 버전별 답변 품질을 비교할 수 있는가?
- 사용자가 승인하지 않은 파일 수정·커밋이 발생하지 않는가?

## 개발 원칙

1. **로컬 우선:** 원본 자료와 기록은 먼저 로컬에 저장합니다.
2. **근거 우선:** 답변보다 출처와 불확실성 표시를 중요하게 다룹니다.
3. **작은 명령:** 하나의 CLI 명령은 하나의 분명한 목적을 가집니다.
4. **승인 가능한 자동화:** 외부 변경은 미리 보여주고 승인받습니다.
5. **측정 가능한 AI:** 좋은 답변이라는 감각만으로 판단하지 않고 evals로 확인합니다.
6. **실사용 우선:** 기능을 추가하기 전에 본인의 공부 흐름에서 반복 사용합니다.

## 첫 번째 완료 조건

다음 시나리오가 처음부터 끝까지 동작하면 MVP 완료로 간주합니다.

1. 학습 Markdown 파일을 등록한다.
2. 등록된 자료를 기반으로 질문한다.
3. 답변과 참고 출처를 확인한다.
4. 답변에서 복습 문제를 생성한다.
5. 학습 목표를 프로젝트 작업으로 분해한다.
6. 작업을 수행하고 Git 커밋을 만든다.
7. `study portfolio`로 학습 과정과 결과를 설명하는 초안을 만든다.

## 현재 상태

프로젝트 설계 단계입니다. 다음 작업은 Python 패키지와 최소 CLI 진입점을 만드는 것입니다.

## 완성 후 사용 방법

아래 내용은 `study-os`가 완성되었을 때의 목표 사용 방법과 기능 명세입니다. 현재 모든 명령이 구현된 상태는 아니며, 개발하면서 이 명세를 기준으로 기능을 하나씩 완성합니다.

### 1. 최초 설정

프로젝트를 처음 받거나 새 컴퓨터에서 실행할 때는 다음 순서로 준비합니다.

```powershell
cd C:\Users\dongh\Desktop\study-os
py -3.14 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -e ".[dev]"
study init
```

`study init`은 다음 작업을 수행합니다.

- `data/` 폴더 생성
- SQLite 데이터베이스 생성
- 검색용 FTS5 테이블 생성
- 기본 설정 파일 생성
- 프로젝트 식별자 등록
- 현재 Git 저장소 연결 확인

API 키는 프로젝트 파일에 직접 작성하지 않고 환경 변수로 등록합니다.

```powershell
$env:OPENAI_API_KEY = "your-api-key"
```

영구 환경 변수로 등록할 때는 Windows 사용자 환경 변수 설정을 사용합니다. API 키가 포함된 `.env` 파일은 Git에 커밋하지 않습니다.

### 2. 도움말과 현재 상태 확인

모든 명령과 옵션은 도움말로 확인할 수 있습니다.

```powershell
study --help
study ingest --help
study ask --help
study review --help
```

현재 데이터베이스, 등록된 자료 수, 최근 질문, 오늘 할 일을 한 번에 확인합니다.

```powershell
study status
```

예상 출력:

```text
study-os status

자료              24개
저장된 개념        87개
오늘 복습           6개
진행 중인 작업      3개
최근 학습           42분 전
검색 인덱스         정상
Git 연결            study-os / main
```

### 3. 학습 자료 등록

#### Markdown 파일 등록

```powershell
study ingest .\notes\rag-basics.md
```

#### 폴더 전체 등록

```powershell
study ingest .\notes
```

하위 폴더까지 등록하려면 `--recursive` 옵션을 사용합니다.

```powershell
study ingest .\notes --recursive
```

#### 자료에 태그 추가

```powershell
study ingest .\notes\embeddings.md --tag ai --tag fundamentals
```

#### 이미 등록한 자료 갱신

```powershell
study ingest .\notes\embeddings.md --update
```

등록할 때 문서의 해시를 저장하므로 같은 파일을 다시 실행해도 중복 자료가 쌓이지 않습니다. 파일이 변경된 경우에만 필요한 내용을 다시 색인합니다.

#### 등록 자료 확인

```powershell
study sources list
study sources show embeddings
study sources remove old-note-id
```

삭제 명령은 원본 파일을 삭제하지 않고 `study-os`의 색인과 메타데이터만 제거합니다. 실제 파일 삭제는 지원하지 않는 것을 기본으로 합니다.

### 4. 학습 자료 검색

```powershell
study search "vector database"
```

태그와 자료 유형으로 범위를 좁힐 수 있습니다.

```powershell
study search "chunking" --tag rag
study search "Python" --source notes
study search "embedding" --limit 10
```

검색 결과에는 다음 정보가 표시됩니다.

- 문서 제목
- 일치한 문장 또는 문단
- 파일 경로
- 문서 내 위치
- 태그
- 관련도
- 마지막 갱신 시간

검색은 처음에는 SQLite FTS5를 사용하고, 이후 필요하면 임베딩 검색을 함께 사용할 수 있습니다. 사용자는 AI가 답변을 만들기 전 검색된 근거를 직접 확인할 수 있어야 합니다.

### 5. 자료를 근거로 AI에게 질문하기

```powershell
study ask "RAG와 fine-tuning의 차이를 설명해줘"
```

이 명령은 다음 순서로 동작합니다.

1. 질문에서 핵심 검색어를 추출합니다.
2. 등록된 자료에서 관련 문서를 검색합니다.
3. 검색된 문맥만 AI에 전달합니다.
4. 답변, 참고 자료, 불확실성을 구조화합니다.
5. 질문과 답변을 학습 기록에 저장합니다.

예상 출력:

```text
답변
RAG는 외부 자료를 검색한 뒤 그 내용을 문맥으로 사용해 답변하는 방식이고,
fine-tuning은 모델의 가중치를 특정 데이터에 맞게 추가 학습하는 방식입니다.

근거
[1] notes/rag-basics.md:12-28
[2] notes/model-training.md:41-55

확실하지 않은 부분
현재 등록된 자료에는 비용 비교에 대한 정보가 없습니다.
```

#### 답변 형식 지정

```powershell
study ask "이 개념을 초보자에게 설명해줘" --format beginner
study ask "이 내용을 면접 답변으로 정리해줘" --format interview
study ask "이 주제로 구현 작업을 제안해줘" --format implementation
```

#### 답변에 사용할 자료 범위 지정

```powershell
study ask "벡터 검색의 장단점은?" --tag search
study ask "이 프로젝트에서 다음에 뭘 해야 해?" --project study-os
```

등록된 자료에서 근거를 찾지 못하면 AI가 일반적인 지식으로 추측하지 않고, “등록된 자료에서 확인할 수 없다”고 표시하는 것을 기본 동작으로 합니다.

### 6. 개념과 복습 문제 만들기

특정 자료에서 핵심 개념을 추출합니다.

```powershell
study concepts extract .\notes\rag-basics.md
study concepts list
```

복습 문제를 생성합니다.

```powershell
study review generate --topic rag
study review generate --source embeddings
```

오늘 복습할 문제를 시작합니다.

```powershell
study review
```

문제를 직접 풀고 답을 입력하면 `study-os`는 다음을 기록합니다.

- 사용자가 입력한 답
- 정답 또는 모범 답안
- 부족한 부분
- 다시 복습할 날짜
- 관련 학습 자료

특정 문제만 다시 확인할 수도 있습니다.

```powershell
study review wrong
study review show review-2026-001
study review postpone review-2026-001 --days 2
```

복습 시스템의 목적은 문제를 많이 만드는 것이 아니라, 사용자가 답을 직접 떠올리고 부족한 개념을 다시 학습하도록 돕는 것입니다. AI가 정답을 먼저 보여주는 방식은 기본 동작으로 사용하지 않습니다.

### 7. 학습 목표를 프로젝트 작업으로 바꾸기

추상적인 목표를 실행 가능한 작업으로 분해합니다.

```powershell
study plan "SQLite FTS5로 학습 자료 검색 기능을 이번 주에 완성하기"
```

예상 출력:

```text
목표: SQLite FTS5로 학습 자료 검색 기능 완성

작업 1  SQLite 연결 모듈 만들기
작업 2  documents 테이블 설계하기
작업 3  FTS5 인덱스 생성하기
작업 4  검색 함수와 CLI 명령 연결하기
작업 5  빈 검색어·한글 검색 테스트하기
작업 6  README 사용 예시 추가하기

추천 첫 작업: 작업 1
완료 조건: 테스트에서 SQLite 연결과 테이블 생성을 확인할 수 있음
```

계획은 자동으로 실행되지 않고 작업 목록에 저장됩니다.

```powershell
study tasks list
study tasks show task-001
study tasks start task-001
study tasks done task-001
```

작업을 완료할 때는 완료 조건을 확인하고, 관련 커밋이나 파일을 연결할 수 있습니다.

```powershell
study tasks done task-001 --evidence "tests/test_db.py"
```

### 8. 프로젝트와 Git 연결

현재 프로젝트의 Git 상태를 확인합니다.

```powershell
study project status
```

예상 출력:

```text
프로젝트: study-os
브랜치: main
최근 커밋: docs: add project blueprint
변경 파일: 2개
열린 작업: 3개
```

최근 개발 기록을 학습 기록과 함께 요약합니다.

```powershell
study project summarize --since 7d
study project commits --limit 10
study project diff
```

AI에게 코드를 수정하게 하는 기능을 추가하더라도 다음 원칙을 지킵니다.

- 수정 전에 어떤 파일을 바꿀지 설명
- 수정 후 diff를 보여주기
- 테스트 실행 결과 표시
- 커밋은 기본적으로 자동 실행하지 않기
- 삭제·reset·push는 명시적인 사용자 승인 필요

### 9. 포트폴리오 기록 만들기

학습 기록, 완료한 작업, Git 커밋을 바탕으로 포트폴리오 초안을 생성합니다.

```powershell
study portfolio
```

기간을 지정할 수 있습니다.

```powershell
study portfolio --since 30d
study portfolio --project study-os
study portfolio --format markdown --output portfolio.md
```

생성되는 내용은 다음 구조를 가집니다.

```markdown
# 프로젝트: study-os

## 문제
학습 자료와 실제 프로젝트 작업이 분리되어 있었다.

## 해결 방법
로컬 Markdown 자료, SQLite 검색, 근거 기반 AI 질문 기능을 연결했다.

## 구현한 기능
- 자료 등록과 전문 검색
- 검색 문맥 기반 질문
- 복습 문제 생성

## 기술적으로 배운 점
- FTS5 인덱스 설계
- 구조화된 AI 출력 검증
- CLI 명령 설계

## 증거
- 관련 커밋
- 테스트 결과
- 사용 예시
```

AI가 성과를 과장하지 않도록 실제 파일, 테스트, 커밋과 연결된 내용만 증거로 사용합니다.

### 10. 일상적인 사용 흐름

#### 공부를 시작할 때

```powershell
study status
study review
study tasks list --open
```

오늘 복습할 내용과 현재 진행 중인 작업을 확인합니다.

#### 공부하면서

```powershell
study ingest .\notes\today.md
study ask "오늘 배운 내용을 세 문장으로 요약하고 모르는 부분을 알려줘"
study review generate --source today
```

새로 배운 내용을 바로 자료로 등록하고, 질문과 복습 문제로 변환합니다.

#### 코딩을 시작할 때

```powershell
study plan "학습 자료 검색 기능 구현하기"
study tasks list --open
study tasks start task-001
```

가장 작은 작업 하나만 선택해 구현합니다.

#### 코딩을 끝낼 때

```powershell
study project status
study project summarize --since 1d
study log "SQLite FTS5 인덱스 생성과 기본 검색을 구현했다"
```

작업 결과와 배운 점을 기록합니다. 기록은 나중에 복습과 포트폴리오 생성에 사용됩니다.

#### 주간 회고

```powershell
study weekly
study portfolio --since 7d
study review wrong
```

주간 회고에서는 다음을 확인합니다.

- 실제로 공부한 개념
- 완료한 프로젝트 작업
- 막힌 부분
- 반복해서 틀린 문제
- 다음 주에 할 가장 중요한 작업

### 11. 설정과 데이터 관리

설정값을 확인합니다.

```powershell
study config list
study config set default-format markdown
study config set max-context-docs 5
```

기본 데이터는 프로젝트의 `data/` 폴더에 저장됩니다.

```text
data/
├── study.sqlite3       # 자료, 질문, 복습, 작업 메타데이터
├── notes/               # 사용자가 선택적으로 보관하는 기록
├── exports/             # Markdown·JSON 내보내기
└── logs/                # 오류와 실행 기록
```

데이터를 백업합니다.

```powershell
study export --output .\backup\study-os-2026-01-01.json
```

데이터를 복원합니다.

```powershell
study import .\backup\study-os-2026-01-01.json
```

내보내기 파일에는 개인 학습 기록이 포함될 수 있으므로 공개 저장소에 올리기 전에 내용을 확인해야 합니다.

### 12. AI 사용 비용과 개인정보

`study-os`는 필요한 문맥만 AI에 보내는 것을 기본으로 합니다.

- 전체 문서 대신 검색된 문단만 전송
- 긴 문서의 중복 문맥 제거
- 동일한 질문 결과를 선택적으로 캐시
- 호출 횟수와 토큰 사용량 기록
- API 키를 소스 코드나 Git에 저장하지 않음
- 민감한 문서는 태그로 AI 전송 제외 가능

```powershell
study sources mark-private personal-notes
study ask "이 자료를 요약해줘" --no-external
```

`--no-external`은 외부 AI 호출 없이 로컬 검색 결과만 표시하는 모드입니다. 실제 지원 방식은 구현 단계에서 결정합니다.

### 13. 오류가 발생했을 때

AI API가 실패해도 등록된 자료와 기존 학습 기록은 삭제되지 않아야 합니다.

```powershell
study doctor
```

`study doctor`는 다음을 점검합니다.

- Python 환경
- 데이터베이스 연결
- FTS5 인덱스 상태
- API 키 존재 여부
- Git 저장소 연결
- 손상된 기록

문제 해결에 필요한 상세 로그를 확인합니다.

```powershell
study logs --last 50
study logs --level error
```

오류 보고에는 API 키나 개인 문서 내용이 포함되지 않도록 합니다.

### 14. 품질을 직접 평가하기

AI 기능은 “그럴듯해 보인다”만으로 완성 판단하지 않습니다. 대표 질문을 평가 데이터셋으로 저장합니다.

```powershell
study eval create
study eval run
study eval compare --baseline latest
```

평가 기준의 예시는 다음과 같습니다.

- 답변이 질문에 직접 답했는가?
- 등록된 자료를 실제로 근거로 사용했는가?
- 출처 위치가 정확한가?
- 자료에 없는 내용을 사실처럼 만들지 않았는가?
- 요청한 출력 형식을 지켰는가?
- 실행 가능한 작업을 제안했는가?

새 기능을 만들 때는 관련 질문을 하나 이상 eval 데이터셋에 추가합니다. 프롬프트나 모델을 바꾼 뒤 품질이 좋아졌는지 나빠졌는지 비교할 수 있어야 합니다.

### 15. 완성된 프로젝트의 대표 사용 시나리오

예를 들어 “RAG 기반 문서 검색 기능을 공부하고 구현하는 날”에는 다음처럼 사용합니다.

```powershell
# 1. 기존 자료와 오늘 할 일을 확인
study status
study review
study tasks list --open

# 2. 새 강의 노트 등록
study ingest .\notes\rag-retrieval.md --tag rag

# 3. 내 자료를 근거로 이해하기
study ask "retrieval 단계에서 chunk size가 결과에 어떤 영향을 주는가?"

# 4. 모르는 내용을 복습 문제로 만들기
study review generate --topic chunking

# 5. 구현 목표를 작은 작업으로 나누기
study plan "학습 노트 검색 CLI 만들기"

# 6. 한 작업을 구현하고 테스트
study tasks start task-001
pytest

# 7. 배운 내용과 결과 기록
study log "FTS5 검색 함수와 CLI 연결을 완료했다"
study project summarize --since 1d

# 8. 하루 결과 확인
study status
study portfolio --since 1d
```

이 흐름이 자연스럽게 반복되면 `study-os`는 단순한 AI 데모가 아니라, 공부한 내용을 실제 개발 결과와 연결하는 개인 도구가 됩니다.
