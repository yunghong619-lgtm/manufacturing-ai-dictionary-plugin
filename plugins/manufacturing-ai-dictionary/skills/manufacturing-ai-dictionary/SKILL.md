---
name: manufacturing-ai-dictionary
description: "제조 AI / Industrial AI / 스마트팩토리 용어 사전. 사용자가 제조 관련 용어의 뜻, 개념, 차이점을 물어볼 때 사전 형식으로 설명해주는 스킬. 'MES가 뭐야', 'Digital Twin 설명해줘', 'PLC랑 DCS 차이', 'APC 뜻', '예지보전이 뭔지', 'SPC 개념 알려줘' 같은 질문에 반드시 이 스킬을 사용할 것. 제조, 공장, 스마트팩토리, 산업AI, SCM, 물류자동화, 품질관리 관련 용어 질문이면 모두 해당."
---

# 제조 AI 기초 학습 사전

PM/기획자가 제조 AI 도메인을 빠르게 이해할 수 있도록 돕는 용어 사전 스킬이다. 제조 현장 경험이 없는 사람도 "아, 그런 거구나" 하고 감을 잡을 수 있는 수준으로 설명한다.

## 핵심 원칙

- **쉬운 말 먼저**: 전문 용어를 풀어 설명하되, 정확성을 잃지 않는다
- **현장 예시 필수**: 추상적 정의만으로는 PM이 감을 못 잡는다. "자동차 공장에서~", "반도체 라인에서~" 같은 구체적 예시를 반드시 포함한다
- **관계 맥락 제공**: 이 기술이 왜 필요한지, 어떤 다른 기술과 연결되는지 맥락을 준다

## 출력 형식

사용자가 용어를 물어보면 아래 구조의 **HTML 파일**을 생성하여 저장한다. 파일명은 `dictionary_{용어영문명}.html` 형식으로 한다.

### HTML 템플릿 구조

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>제조AI 사전 - {용어명}</title>
  <style>
    /* 깔끔한 사전 스타일 */
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: 'Pretendard', -apple-system, 'Segoe UI', sans-serif;
      background: #f5f7fa; color: #1a1a2e; line-height: 1.7;
      padding: 40px 20px;
    }
    .container { max-width: 800px; margin: 0 auto; }
    .header {
      background: linear-gradient(135deg, #0f4c75, #3282b8);
      color: white; padding: 32px; border-radius: 16px 16px 0 0;
    }
    .header h1 { font-size: 28px; margin-bottom: 4px; }
    .header .en-name { font-size: 18px; opacity: 0.85; font-weight: 300; }
    .tags { margin-top: 16px; display: flex; gap: 8px; flex-wrap: wrap; }
    .tag {
      background: rgba(255,255,255,0.2); padding: 4px 12px;
      border-radius: 20px; font-size: 13px;
    }
    .tag.level-beginner { background: #27ae60; }
    .tag.level-intermediate { background: #f39c12; }
    .tag.level-advanced { background: #e74c3c; }
    .body { background: white; padding: 32px; border-radius: 0 0 16px 16px; box-shadow: 0 4px 20px rgba(0,0,0,0.08); }
    .section { margin-bottom: 28px; }
    .section h2 {
      font-size: 16px; color: #3282b8; text-transform: uppercase;
      letter-spacing: 1px; margin-bottom: 12px;
      padding-bottom: 8px; border-bottom: 2px solid #e8f0fe;
    }
    .one-liner {
      font-size: 20px; font-weight: 600; color: #1a1a2e;
      padding: 16px; background: #f0f7ff; border-radius: 8px;
      border-left: 4px solid #3282b8;
    }
    .example-box {
      background: #fafbfc; border: 1px solid #e1e8ed;
      border-radius: 8px; padding: 16px; margin-top: 8px;
    }
    .example-box .label {
      font-size: 12px; font-weight: 700; color: #3282b8;
      text-transform: uppercase; margin-bottom: 6px;
    }
    .related-terms { display: flex; gap: 8px; flex-wrap: wrap; }
    .related-term {
      background: #e8f0fe; color: #0f4c75; padding: 6px 14px;
      border-radius: 20px; font-size: 14px; text-decoration: none;
    }
    .checklist { list-style: none; }
    .checklist li { padding: 8px 0; padding-left: 28px; position: relative; }
    .checklist li::before {
      content: '✓'; position: absolute; left: 0;
      color: #27ae60; font-weight: bold; font-size: 18px;
    }
    .pm-tip {
      background: #fff8e1; border: 1px solid #ffecb3;
      border-radius: 8px; padding: 16px; margin-top: 12px;
    }
    .pm-tip .label { font-size: 12px; font-weight: 700; color: #f57f17; margin-bottom: 6px; }
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <h1>{한글 용어명}</h1>
      <div class="en-name">{영문 용어명} ({약어})</div>
      <div class="tags">
        <span class="tag level-{난이도}">{난이도: 초급/중급/고급}</span>
        <span class="tag">{카테고리}</span>
      </div>
    </div>
    <div class="body">
      <div class="section">
        <h2>한 줄 정의</h2>
        <div class="one-liner">{비전문가도 바로 이해할 수 있는 한 줄 설명}</div>
      </div>
      <div class="section">
        <h2>상세 설명</h2>
        <p>{2-3 문단으로 개념을 풀어 설명. 왜 이게 필요한지, 어떤 문제를 해결하는지 중심으로}</p>
      </div>
      <div class="section">
        <h2>현장 예시</h2>
        <div class="example-box">
          <div class="label">예시 1 — {산업/상황}</div>
          <p>{구체적인 현장 시나리오}</p>
        </div>
        <div class="example-box">
          <div class="label">예시 2 — {산업/상황}</div>
          <p>{다른 산업/상황의 예시}</p>
        </div>
      </div>
      <div class="section">
        <h2>PM이 알아야 할 포인트</h2>
        <div class="pm-tip">
          <div class="label">PM TIP</div>
          <ul class="checklist">
            <li>{이 기술 도입 시 PM이 체크해야 할 사항 1}</li>
            <li>{체크 사항 2}</li>
            <li>{체크 사항 3}</li>
          </ul>
        </div>
      </div>
      <div class="section">
        <h2>관련 용어</h2>
        <div class="related-terms">
          <span class="related-term">{관련 용어 1}</span>
          <span class="related-term">{관련 용어 2}</span>
          <span class="related-term">{관련 용어 3}</span>
        </div>
      </div>
    </div>
  </div>
</body>
</html>
```

## 용어 카테고리

다음 카테고리 중 해당하는 것을 태그로 표시한다:

| 카테고리 | 설명 | 대표 용어 예시 |
|---------|------|--------------|
| 제조 공정 | 공장 운영/제어 시스템 | MES, PLC, DCS, SCADA, HMI |
| 품질 관리 | 불량 검출, 공정 안정성 | SPC, AQL, Six Sigma, Vision Inspection |
| 산업 AI | AI/ML의 제조 적용 | PHM, APC, Digital Twin, Edge AI |
| 설비 관리 | 설비 유지보수/최적화 | CBM, RCM, OEE, MTBF, MTTR |
| SCM/물류 | 공급망 및 물류 | WMS, TMS, S&OP, ATP, 수요예측 |
| 데이터/인프라 | 데이터 수집/처리 기반 | OPC-UA, MQTT, Data Lake, Edge Computing |
| 경영/전략 | 디지털 전환 전략 | DX, AX, Industry 4.0, Smart Factory |

## 난이도 기준

- **초급**: 제조 도메인 입문자가 첫 주에 알아야 할 용어
- **중급**: 프로젝트 참여 시 실무에서 마주치는 용어
- **고급**: 아키텍처 설계나 전략 수립 시 필요한 심화 용어

## 복수 용어 비교 요청 시

사용자가 "A랑 B 차이가 뭐야?" 같은 비교 질문을 하면, 각 용어의 사전 항목을 나란히 보여주는 비교 테이블을 HTML에 추가한다:

```html
<div class="section">
  <h2>비교</h2>
  <table style="width:100%; border-collapse:collapse;">
    <tr style="background:#e8f0fe;">
      <th style="padding:12px; text-align:left;">구분</th>
      <th style="padding:12px; text-align:left;">{용어A}</th>
      <th style="padding:12px; text-align:left;">{용어B}</th>
    </tr>
    <tr><td>목적</td><td>...</td><td>...</td></tr>
    <tr><td>범위</td><td>...</td><td>...</td></tr>
    <tr><td>사용 시점</td><td>...</td><td>...</td></tr>
    <tr><td>PM 관점 핵심</td><td>...</td><td>...</td></tr>
  </table>
</div>
```

## 여러 용어 한꺼번에 요청 시

사용자가 "스마트팩토리 기본 용어 정리해줘" 같이 여러 용어를 한 번에 요청하면, 카테고리별로 묶어서 하나의 HTML 파일에 여러 용어를 사전 카드 형태로 나열한다.

## 주의사항

- 영어 약어만 쓰지 말고 반드시 한글 풀네임도 같이 쓸 것 (예: "MES (Manufacturing Execution System, 제조실행시스템)")
- 정의에 또 다른 전문 용어가 나오면 괄호 안에 짧게 풀어줄 것
- "~라고 할 수 있습니다" 같은 교과서체 대신 "~이다", "~한다" 체로 간결하게
- 잘못된 정보보다는 차라리 "이 개념은 산업/맥락에 따라 다르게 쓰인다"고 명시
