# moomin-cve

매일 아침 Claude 예약 작업이 정리하는 CVE 브리핑 기록. GitHub Pages로 서빙하는 PWA라 폰 홈 화면에 추가해서 볼 수 있다.

## 구조

```
index.html             앱 (등급 필터, 검색, 날짜별 보기)
sw.js                  서비스 워커 (오프라인 캐시)
manifest.webmanifest
icons/
data/cves.json         CVE 기록 배열
data/runs.json         날짜별 실행 기록 배열
```

## 데이터 스키마

`data/cves.json`: CVE ID 오름차순 배열

| 필드 | 타입 | 설명 |
|---|---|---|
| cve | string | CVE ID |
| date | string | 처음 기록한 날짜 (KST, YYYY-MM-DD) |
| grade | "red" \| "orange" \| "green" \| "gray" | 즉시 확인 / 주의 / 흥미 / 과장 체크 |
| title | string | 짧은 제목 |
| product | string | 영향 제품 |
| summary | string | 2~3문장 요약 |
| cvss | number \| null | |
| kev | boolean | CISA KEV 등재 여부 |
| poc | boolean | 공개 PoC 존재 여부 |
| tags | string[] | |
| links | {label, url}[] | 원본 소스 |
| history | {date, note}[] | 상태 변화 이력 |
| deepDive | string \| null | 심층 설명한 날짜 |

`data/runs.json`: 날짜 오름차순 배열 `{date, note, count, deepDive}`

## 규칙

- 앱 UI와 data/*.json 어디에도 이모지를 쓰지 않는다. 등급은 색 점(CSS)과 텍스트로 표시한다.
