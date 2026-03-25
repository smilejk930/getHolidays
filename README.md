# getHolidays

## claude.ai를 이용해서 생성

### 생성 프롬프트

공휴일 api를 이용해서 내가 입력한 연도의 1년치 공휴일을 json 형식으로 리턴해주는 프로그램 만들어줘.
```
- apiuri: https://apis.data.go.kr/B090041/openapi/service/SpcdeInfoService/getHoliDeInfo
- parameter
    - ServiceKey=`servicekey`
    - solYear=`2026`
    - solMonth=`09`
    - _type=`json`
    - numOfRows=`20`
- httpmethod: GET
```

- return
```json
{"response":{"header":{"resultCode":"00","resultMsg":"NORMAL SERVICE."},"body":{"items":{"item":[{"dateKind":"01","dateName":"추석","isHoliday":"Y","locdate":20260924,"seq":1},{"dateKind":"01","dateName":"추석","isHoliday":"Y","locdate":20260925,"seq":1},{"dateKind":"01","dateName":"추석","isHoliday":"Y","locdate":20260926,"seq":1}]},"numOfRows":20,"pageNo":1,"totalCount":3}}}
```

- 기능 요청
    1. 리턴 데이터 항목은 아래와 같이 구성
        `dateName`, `startDate`, `endDate`
    2. 해당월의 apiuri의 결과값 datename이 동일한 것들은 묶어서 하나의 datename에 startDate와 endDate으로 구성(dateName:"추석", startDate:'20260924', endDate:"20260926")

## config.js 설정 예시 (로컬 환경 CORS 우회)

루트 디렉토리에 `config.js` 파일을 생성하여 공공데이터포털 API 서비스 키를 미리 설정할 수 있습니다. 
키가 설정되어 있으면 브라우저에서 파일을 직접 열었을 때도(`file:///`) 자동으로 조회가 실행됩니다.

```javascript
window.CONFIG = {
  serviceKey: "발급받은_서비스키를_여기에_입력하세요"
};
```