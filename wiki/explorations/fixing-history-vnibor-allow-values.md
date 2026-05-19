---
query: "fixing history 에 VNIBOR 은 allow values 에 없어서 에러나는데 따로직접등록하는 방법이 있나요?  "
---

이 질문에 답하려면 먼저 "fixing history" 관련 문서를 찾아보겠습니다.Fixing History 관련 내용을 찾았습니다. "Fixing History" 섹션(pages 348-351)에서 VNIBOR 같은 index fixings가 어떻게 등록되는지 확인하겠습니다.Fixing History에 대한 정보를 찾았습니다. VNIBOR는 Table 81의 IR Index 목록에 없습니다. 하지만 **Generic Indices**를 이용하면 직접 등록할 수 있습니다.

---

네, 가능합니다. VNIBOR는 **Allowable Values** 목록(Table 81)에 없는 커스텀 인덱스이지만, **Generic Index** 형식으로 직접 등록할 수 있습니다.

## 방법: Generic Index 사용

fixings.txt 파일에 다음과 같은 형식으로 등록하면 됩니다:

```
GENERIC-VNIBOR
```

즉, 아래와 같이 fixings.txt에 추가하면 됩니다:

```
20250203 GENERIC-VNIBOR 0.04500
20250204 GENERIC-VNIBOR 0.04550
```

**형식 규칙** (Table 85 기준):

| 구성요소 | 값 |
|---|---|
| Prefix | 반드시 `GENERIC` |
| 구분자 | `-` (하이픈) |
| NAME | 임의의 문자열 |

## 작동 방식

ORE에서 VNIBOR fixing이 필요할 때, `GENERIC-VNIBOR`라는 이름으로 fixings.txt에서 값을 조회하게 됩니다. `GENERIC-` prefix가 붙은 인덱스는 **어떤 문자열이든 허용**되므로 VNIBOR 외에도 다른 커스텀 인덱스들을 자유롭게 등록할 수 있습니다.

## 전체 fixings.txt 예시

```
# fixings.txt
20250203 GENERIC-VNIBOR 0.04500
20250204 GENERIC-VNIBOR 0.04550
20250203 EUR-EURIBOR-3M 0.00250
20250204 EUR-EURIBOR-3M 0.00255
```

> ⚠️ **참고**: 실제로 VNIBOR fixing 값을 ORE 내부에서 index curve 이름과 매핑하려면, `curveconfig.xml`이나 market data 설정에서 해당 인덱스 이름이 `GENERIC-VNIBOR`와 일치해야 합니다.
