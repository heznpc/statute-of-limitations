# 시효제도(Statute of Limitations)의 역사적 기원과 진화: "제도적 망각"의 계보학

> 연구 목적: AI 에이전트 메모리 시스템 설계를 위한 역사적 유비(analogy) 자료
> 작성일: 2026-03-29
> 검색 범위: 영어/한국어 양방향 웹 검색 기반

---

## 1. 고대 기원: 시효 개념은 언제, 어디서 처음 등장했는가?

### 1.1 고대 그리스 (기원전 5~4세기) --- 현존하는 가장 오래된 기록

고대 아테네는 현재까지 확인 가능한 가장 오래된 시효제도를 운용했다. 핵심 내용:

- **5년 시효 원칙**: 살인을 제외한 거의 모든 범죄에 대해 5년의 공소시효를 적용했다.
- **살인죄 예외**: 살인(phonos)은 시효의 적용을 받지 않았다. 이미 이 시기에 "어떤 범죄는 시간이 지나도 잊혀서는 안 된다"는 직관이 법에 반영되어 있었다.
- **용어**: 그리스어로 시효 기간을 의미하는 용어는 **prothesmia**(프로테스미아)였다.
- **graphe paranomon의 1년 시효**: 위헌 법률 소추(graphe paranomon)에는 별도로 1년의 시효가 적용되었다.

**제도의 목적 --- "sycophant" 통제**

데모스테네스(Demosthenes)는 시효제도가 **시코판트(sycophant, 직업적 고발자)**를 통제하기 위해 도입되었다고 기록했다. 시코판트는 고소 협박을 통해 금전적 이득을 취하고, 허위 고발을 일삼으며, 민주적 법적 절차를 개인 이익을 위해 남용하는 자들이었다.

> **[AI 메모리 시스템 시사점]**: 시효의 최초 목적은 "정의의 완화"가 아니라 **시스템 남용 방지**였다. 과거 데이터를 무한히 보관하면, 그 데이터를 악용할 수 있는 공격 벡터도 무한히 열린다.

### 1.2 고대 로마법 --- 체계적 법제화의 시작

#### 12표법 (기원전 450년경): 취득시효(usucapio)

로마에서 시효의 최초 형태는 민사적 **취득시효(usucapio)**였다:

- **동산(movables)**: 1년간 점유하면 소유권 취득
- **부동산(immovables)**: 2년간 점유하면 소유권 취득
- **요건**: 선의(bona fides), 정당한 원인(iusta causa), 연속적 점유, 도품이 아닐 것

> 12표법의 취득시효는 "시간의 경과가 법적 상태를 확정한다"는 원칙의 출발점이다.

#### 법무관법(Praetorian Law): 1년 시효의 등장

초기 로마 시민법(ius civile)에서 소송은 대부분 **영구소권(actiones perpetuae)**이었다. 즉, 시효가 없었다. 그러나 법무관(praetor)은 자신이 고시(Edict)를 통해 새로 도입한 소권들에 대해 **annus utilis(유효연도)** --- 소권 발생 시점부터 1년 --- 의 기간 제한을 부과했다.

#### Lex Julia de Adulteriis (기원전 18년): 형사 시효의 초기 사례

아우구스투스 황제의 간통죄법은 로마 역사상 최초로 간통을 **공적 범죄(public offence)**로 규정하면서, 동시에 소추 기간을 설정했다:

- **남편/아버지**: 범죄 인지 후 60일 이내에 고소
- **외부인(extraneus)**: 남편/아버지가 60일 내 불기소 시, 이후 6개월 이내 고소 가능

> [주의: 일부 2차 문헌에서 Lex Julia에 "5년 시효"가 있었다고 언급하나, 1차 사료 검토 결과 60일/6개월 체계가 더 정확한 것으로 보인다. 5년 시효는 아테네법과의 혼동 가능성이 있다.]

#### 테오도시우스 2세 (서기 424년): 소멸시효의 체계화

**핵심 전환점**: 테오도시우스 2세는 424년, 모든 기존의 영구소권에 대해 시효(praescriptio)를 부과하여 30년(일부 40년) 이내에 소송을 제기하도록 했다. 이는 "소멸시효(extinctive prescription)"의 체계적 확립으로 평가된다.

- Codex Theodosianus 4, 14, 1, 3 (서기 424년)
- 목적: **certum tempus in protrahendis litibus** (소송의 장기화에 대한 확정적 기한 설정)

#### 유스티니아누스 대제 (6세기): 최종 통합

유스티니아누스는 다음을 통합했다:

- 기존의 취득시효(usucapio)와 장기점유시효(longi temporis praescriptio)를 융합
- **longissimi temporis praescriptio**(최장기시효, 원래 40년 -> 테오도시우스 2세가 30년으로 단축)를 기반으로 새로운 특별시효 체계 구축
- 선의점유 + 30년 = 소유권 취득이라는 통합 원칙 확립

### 1.3 고대 기원 요약 --- 불확실성 표시

| 시기 | 법체계 | 핵심 내용 | 사료 확실성 |
|------|--------|-----------|------------|
| 기원전 5세기 | 아테네법 | 살인 외 5년 시효, prothesmia | **중간** (데모스테네스 등 간접 사료) |
| 기원전 450년 | 로마 12표법 | usucapio (동산 1년, 부동산 2년) | **높음** (키케로 등 다수 확인) |
| 기원전 18년 | Lex Julia | 간통죄 60일/6개월 시효 | **높음** (법전 직접 기록) |
| 서기 424년 | 테오도시우스 2세 | 영구소권에 30년 시효 부과 | **높음** (Codex Theodosianus) |
| 6세기 | 유스티니아누스 | 시효제도 종합 통합 | **높음** (Corpus Juris Civilis) |

---

## 2. 시효의 정당화 논리: 왜 사회는 "잊기"를 제도화했는가?

### 2.1 역사적으로 제시된 주요 근거

시효제도의 정당성은 시대에 따라 다양한 논거로 뒷받침되어 왔다:

#### (1) 증거의 열화 (Evidentiary Decay)
가장 오래되고 가장 보편적인 논거. 시간이 지나면 증거가 소멸하고, 증인의 기억이 불확실해지며, 문서가 훼손된다. 이 상태에서 재판을 진행하면 **적정한 사실인정(accurate fact-finding)**이 불가능해진다.

> Santa Clara 법대 연구: "시효의 주된 목적은, 증거가 더 이상 신선하지 않고 증인이 더 이상 이용 가능하지 않은 상태에서 원고가 낡은 청구를 주장하는 것을 방지하는 데 있다."

#### (2) 법적 안정성과 피고인의 안식 (Repose and Finality)
피고인 또는 피의자가 무한한 기간 동안 소추의 위협 아래 놓이는 것은 부당하다. 일정 기간이 지나면 법적 분쟁은 **종결(finality)**되어야 하며, 이것이 법적 안정성의 요체다.

> 한국법에서의 표현: "범인이 범죄 후 일정한 기간 동안 기소되지 아니하고 사회생활을 영위하였다는 **상태를 보호**"하는 것.

#### (3) 가벌성의 감소 (Diminished Punishability)
시간의 경과에 따라 범죄에 대한 사회적 응보 감정이 냉각되고, 범인 자체도 변화한다. 20년 전의 범행에 대해 현재의 인간을 처벌하는 것이 정의에 부합하는가?

#### (4) 국가의 태만에 대한 책임 (State Accountability)
일정 기간 내에 범인을 검거하지 못한 것은 국가(검찰/수사기관)의 태만이다. 이 태만의 결과를 범인에게만 전가하는 것은 부당하다.

#### (5) 사법 효율성 (Judicial Efficiency)
법원의 자원은 유한하다. 수십 년 전의 사건을 재구성하려면 막대한 비용이 들며, 그 자원은 현재의 사건에 투입하는 것이 더 효율적이다.

### 2.2 논거의 역사적 진화

| 시대 | 지배적 논거 | 비고 |
|------|-----------|------|
| 고대 아테네 | 시스템 남용 방지 (시코판트 통제) | 가장 실용적 |
| 로마 법무관법 | 법적 안정성 (소권의 체계적 관리) | 법기술적 |
| 테오도시우스 2세 | 소송 장기화 방지 | 행정적 효율 |
| 중세 교회법 | 사회 평화 + 영혼의 안식 | 신학적 요소 가미 |
| 근대 대륙법 | 증거 열화 + 법적 안정성 | 복합 논거 |
| 현대 | 피의자 인권 + 적정 재판 보장 | 인권론 가미 |

> **[AI 메모리 시사점]**: 시효의 정당화 논리는 본질적으로 **정보 열화(information decay)**, **시스템 자원 관리**, **상태 보호(protecting current state over historical state)**라는 세 축으로 수렴한다. 이는 AI 메모리 시스템의 retention policy 설계에 직접 대응한다.

---

## 3. 문명 간 비교: 동일한 문제에 대한 상이한 접근

### 3.1 동아시아 전통법: "시효 없음"이 기본값

#### 전통 중국법 --- 유교적 법관념과 시효의 부재

**핵심 발견**: 전통 중국법에는 공소시효(追诉时效) 개념이 존재하지 않았다. 국가는 필요하고 적절하다고 판단될 때 언제든지 소추를 개시할 수 있었다.

이 배경에는 유교적 법관념이 있다:
- **법(法)은 도덕(德)의 연장**: 범죄는 도덕적 위반이며, 도덕적 위반은 시간이 지나도 소멸하지 않는다.
- **불효(不孝)의 극단적 처벌**: "3000개의 죄 중 가장 중한 것은 불효"라는 원칙 하에, 자녀가 부모를 꾸짖으면 교형(絞刑), 부모 생존 시 분가하면 체형이 부과되었다.
- **유교의 "법치화"**: 한나라 이후 "법의 유교화(Confucianization of law)"가 진행되면서, 범죄의 시간적 소멸이라는 관념 자체가 존재하기 어려웠다.

**시효제도의 최초 도입**: 청나라가 1911년 「대청신형률(New Criminal Code of Great Qing)」에서 처음으로 시효 개념을 채택했다. 이는 서양법(특히 독일법과 일본법)의 직접적 영향이었다.

> **[사료 확실성: 중간~높음]** 다수의 법사학 연구(Norman Ho 등)가 당률(唐律)에 시효 규정이 없었음을 확인한다.

#### 조선시대 한국 --- 대명률 체계

조선은 형사법의 기본 원칙으로 **대명률(大明律, 명나라 형법전)**을 적용했다. 경국대전의 형전(刑典) 제1조가 대명률의 일반 적용을 명시하고 있었고, 인명 관련 범죄(7종의 살인 유형)에 대해서는 대명률이 직접 적용되었다.

전통 중국법과 마찬가지로, 조선의 형사법에서도 명시적 공소시효 규정이 확인되지 않는다.

> **[사료 확실성: 중간]** 조선시대 시효제도의 유무에 대한 전문 학술 연구는 제한적이다. 대명률 자체에 시효 규정이 없다는 점에서 추론하되, 관습적 시효의 존재 가능성은 열어두어야 한다.

#### 일본 --- 메이지 시대의 서양법 계수

에도 시대(1603~1868)의 전통 일본법에도 서양식 시효제도는 없었다. 일본의 시효제도는 **메이지 시대 서양법 계수**의 산물이다:

- **1880년**: 프랑스법 모델 기반 형법 및 형사소송법 최초 공포
- **1922년**: 독일법 영향을 받은 새 형사소송법 제정, 공소시효(公訴時効) 포함
- **이후**: 한국법은 일본법을 통해 간접적으로 독일-프랑스의 시효 전통을 계수

### 3.2 이슬람법: 독자적 시효 관념 "무루르 알-자만"

이슬람법에서 시효에 해당하는 개념은 **무루르 알-자만(murur al-zaman, 시간의 경과)**이다.

#### 핵심 원리

무루르 알-자만은 "장기간 동안 아무런 청구가 이루어지지 않은 권리에 대해, 시간의 경과에 의해 해당 권리를 보호하는 원칙"으로, 소송 제기에 시간적 제한을 부과한다.

#### 학파별 차이

- **하나피 학파(Hanafi)**: 대부분의 하드(hadd) 범죄에 대해 **범행 후 1개월** 이내에만 처벌 가능. 그러나 **카드프(qadhf, 간통 무고)**는 시효 적용 제외 --- 이 범죄가 신(하나님)의 권리와 인간의 권리 모두를 침해하며, 후자는 시간의 경과로 소멸하지 않기 때문.
- **말리키 학파(Maliki)** 및 다른 학파들도 시간 제한의 개념을 발전시켰으나, 구체적 기간은 학파마다 상이.

#### 오스만 제국의 혁신 --- 메젤레(Mecelle)

오스만 제국은 고전적 하나피 교리에서 중요한 이탈을 보여주었다:

- **15년 시효**: 오스만 제국은 카드프를 포함한 **모든 범죄**에 15년의 공소시효를 적용했다.
- 이는 고전적 하나피법에서 카드프에는 시효가 없었던 것과 명백히 대비된다.
- 1869~1876년 편찬된 **메젤레(Majallah al-Ahkam al-Adliyya)**는 하나피법을 성문화한 최초의 이슬람 민법전으로, 시효(prescription) 관련 조항을 포함했다.

> **[AI 메모리 시사점]**: 이슬람법의 "신의 권리 vs 인간의 권리" 구분은 흥미로운 유비를 제공한다. AI 시스템에서도 **시스템 수준의 안전 규칙(신의 권리에 해당)**은 만료되지 않아야 하고, **개인 수준의 선호(인간의 권리에 해당)**는 시효를 가질 수 있다.

### 3.3 게르만법과 영국 보통법

#### 게르만 전통법

초기 게르만법(Leges Barbarorum, 5~9세기)은 기본적으로 관습법이었으며, 중앙 권위가 제정하는 것이 아니라 특정 민족의 관습에서 유래했다. 살리카법(Lex Salica, 508~511년경)이 가장 중요했다. 이 법전들은 재판 절차, 폭력 행위에 대한 금전 배상, 상속을 주로 다루었으나, 체계적 시효 규정은 미확인.

독일에서의 시효(Verjahrung) 체계는 로마법의 계수를 통해 형성되었으며, 1900년 독일민법전(BGB)에서 체계화되었다:

- 원래 일반 시효: 30년
- 2002년 채무법 현대화(Schuldrechtsmodernisierung): 일반 시효를 **3년**으로 대폭 단축
- 생명/신체/자유 침해: 30년 (최장 시효)

#### 영국 보통법 --- 독자적 경로

영국법은 로마법의 직접적 계수 없이 독자적으로 시효를 발전시켰다:

- **헨리 1세(1100~1135)**: 부동산 침탈 소송에 대한 기간 제한 도입
- **머턴 법(1237)**: 헨리 1세 사망(1135) 이전 사건에 대한 소송 제한
- **웨스트민스터 법(1275)**: 기준일을 리처드 1세 대관식(1189)으로 이동
- **1487년**: 부동산 소송에 대한 최초의 명시적 시효법
- **1540년**: 부동산 관련 60/50/30년 시효
- **1623년 시효법(Limitation Act 1623)**: **핵심 전환점**. 대인소권(in personam actions)에 대한 최초의 시효법:
  - 명예훼손: 2년
  - 인신 침해: 4년
  - 채무, 토지 침입 등: 6년

**6년의 미스터리**: 영국 법률위원회(Law Commission)는 "왜 6년이 적절하다고 생각되었는지에 대한 정보를 추적할 수 없었다"고 밝혔다.

1623년 법은 이후 미국의 대부분 시효법의 모델이 되었다.

### 3.4 교회법(Canon Law) --- 중세 유럽의 매개

교회법에서의 시효(prescription)는 로마법에서 기원하되, 교회법적으로 재해석되었다:

- **동산**: 선의점유 + 권원(title) = 3년
- **부동산**: 권원 없이 = 30년
- **교회 부동산**: 40년
- **로마 교회(교황청) 재산**: **100년**

교회법의 시효는 중세 유럽 전역의 세속법에 영향을 미쳤으며, 특히 취득시효와 소멸시효의 이론적 기반을 제공했다.

### 3.5 나폴레옹 법전 (1804)

프랑스 민법전은 시효를 두 유형으로 체계화했다:

- **취득시효(prescription acquisitive)**: 선의 + 권원 + 10~20년 점유 = 소유권 취득; 선의/권원 없이 = 30년
- **소멸시효(prescription extinctive)**: 30년간 미행사 시 권리 소멸

나폴레옹 법전은 19세기 유럽 대륙과 라틴아메리카 법전의 주요 모델이 되었으며, 이를 통해 시효제도가 전 세계로 확산되었다.

### 3.6 문명 간 비교 종합

| 법전통 | 시효 존재 여부 | 핵심 특징 | 기본 관념 |
|--------|-------------|-----------|----------|
| 동아시아 전통법 (중국/한국/일본) | **없음** | 도덕적 위반은 소멸하지 않음 | 범죄 = 도덕적 위반 |
| 고대 그리스 | **있음** (살인 제외) | 5년 시효, 시코판트 통제 | 시스템 남용 방지 |
| 로마법 | **발전적** | usucapio -> praescriptio | 법적 안정성 |
| 이슬람법 | **학파별 상이** | 하드 1개월 / 오스만 15년 | 신의 권리 vs 인간의 권리 |
| 영국 보통법 | **독자 발전** | 1623년 체계화 | 실용적/점진적 |
| 대륙법 (독일/프랑스) | **로마법 계수** | 30년 -> 현대 3년 | 체계적 법전화 |

---

## 4. 핵심 전환점들: 시효를 둘러싼 역사적 논쟁과 변곡점

### 4.1 독일의 나치 전범 시효 논쟁 (Verjahhrungsdebatte, 1965~1979)

20세기 법사에서 가장 치열했던 시효 논쟁.

**배경**: 서독 형법의 살인죄 공소시효는 20년이었다. 나치 전범에 대한 기소는 전후 지연이 있었고, 1960년대에 시효 만료가 임박했다.

**전개**:
- **1965년**: 격렬한 논쟁 끝에, 연방의회가 시효를 **1969년 말까지** 연장
- **1969년**: 모살(qualified murder)에 대한 시효를 20년에서 **30년**으로 연장 (1979년 말까지)
- **1979년 7월 3일**: 전일(全日) 생중계된 의회 토론 끝에, **255 대 222 표결**로 모살에 대한 공소시효를 **완전 폐지**

이 논쟁은 "시효의 기능적 정당성"과 "역사적 정의의 불가양도성" 사이의 긴장을 극적으로 보여주었다.

### 4.2 국제형사재판소 로마규정 (1998/2002)

1998년 채택, 2002년 발효된 로마규정 제29조:

> "재판소 관할 범죄에는 어떠한 공소시효도 적용되지 않는다."

적용 대상: 집단살해(genocide), 인도에 반한 죄(crimes against humanity), 전쟁범죄(war crimes), 침략범죄(crime of aggression).

이는 "시효 없음"이 국제법적 규범으로 확립된 결정적 순간이다.

### 4.3 일본 2010년 --- 살인죄 공소시효 폐지

**배경**: 일본의 형사소송법은 독일법의 영향 하에 공소시효를 두고 있었다. 살인죄의 시효는 15년이었다.

**전개**:
- **2004년**: 살인 등 사형에 해당하는 죄의 시효를 15년에서 25년으로 연장
- **2010년 4월 27일**: 국회(Diet)에서 법 개정. **사형에 해당하는 범죄(살인 등)의 공소시효 완전 폐지**. 무기징역에 해당하는 범죄의 시효는 15년에서 30년으로 2배 연장.

**주목할 점**: 법무대신 치바 게이코(千葉景子)는 법안 통과 **당일** 즉시 시행을 명령했다. 이유: 1995년 미해결 살인사건의 시효가 **자정에 만료**될 예정이었기 때문.

- 개정법은 **시효가 아직 만료되지 않은 사건**에 소급 적용되었다.

### 4.4 한국 2015년 --- "태완이법"

**배경**: 한국의 살인죄 공소시효는 원래 15년이었고, 2007년 25년으로 연장되었다.

**촉발 사건들**:
- 화성연쇄살인사건 10차 사건(2006.1), 이형호 군 유괴살해사건, 대구 성서초등학생 5인 살해사건이 2006년 1~4월 사이에 연이어 공소시효 만료
- **대구 황산 테러 사건**: 6세 소년 '태완'이가 황산 테러를 당해 49일 후 사망. 증인과 피해자 진술이 일치했으나 증거 부족으로 용의자 기소 불가, 이후 시효 만료

**결과**: 2015년 7월 24일, 국회가 살인죄 공소시효 폐지 법안(일명 "태완이법") 통과.

**적용 범위와 한계**:
- **적용 대상**: 법 시행 시점에 공소시효가 아직 만료되지 않은 미해결 1급 살인 사건
- **소급 불적용**: 이미 시효가 완성된 사건에는 적용되지 않음 (헌법 원칙)
- **2급 살인, 과실치사 등은 제외**

### 4.5 화성연쇄살인사건 --- 시효제도의 비극적 실패 사례

이 사건은 시효제도의 모순을 가장 극적으로 드러낸 사례다:

- **1986~1991년**: 이춘재가 경기도 화성 일대에서 여성 10여 명 강간 살해
- **2001~2006년**: 범행 후 15년이 지나 모든 사건의 공소시효 순차 만료
- **2019년 9월**: DNA 감정으로 이춘재가 진범으로 특정. 피해자 속옷의 DNA와 일치, 이후 4건의 추가 살인도 DNA로 연결
- **이춘재의 자백**: 원래 10건의 사건을 포함해 총 14건의 살인, 30건의 성폭행을 자백
- **처벌 불가**: 공소시효 만료로 화성연쇄살인에 대해서는 법적 처벌 불가능. (다만 1994년 처제 살해 사건으로 무기징역 복역 중)

**가장 비극적 부분 --- 윤성여 사건**:
- 8차 사건에서 경찰의 강압 수사로 소아마비 환자 윤성여(당시 22세)가 범인으로 지목
- 무기징역 선고 후 **20년 복역**
- 2020년 12월 17일 재심에서 **무죄 판결**
- 국가 배상: 18억 6,911만 원

> **[AI 메모리 시사점]**: 화성사건은 "정보의 비가역적 손실"이 초래하는 재앙을 보여준다. 시효가 만료된 시점에서는 진실이 밝혀져도 정의를 구현할 수 없다. 그러나 동시에, 시효가 없었다면 새로운 증거(DNA)가 나올 때까지의 기간 동안 윤성여 같은 무고한 사람이 더 오래 방치될 수도 있었다. 이것은 **false positive와 false negative 사이의 근본적 트레이드오프**다.

### 4.6 프랑스 2017년 개혁

- 중범죄(crimes/felonies) 시효: 10년 -> **20년**
- 경범죄(delits/misdemeanors) 시효: 3년 -> **6년**
- 집단살해, 인도에 반한 죄: **시효 없음**
- 미성년자 대상 성범죄: 피해자가 성인이 된 후부터 기산, 강간의 경우 피해자 **48세**(성인 18세 + 30년)까지 고소 가능
- 2023년: 미성년 대상 성폭력 시효 완전 폐지 권고안 제출

---

## 5. 현대적 긴장: 디지털 기록, DNA, 그리고 "잊힐 권리"

### 5.1 DNA 증거의 등장 --- 시효의 존재 근거를 흔들다

DNA 기술은 시효의 핵심 근거였던 "증거의 열화"를 정면으로 반박했다:

- **2000~2005년**: 미국 20개 주가 DNA 증거를 고려하여 시효법 개정, 10개 주가 추가 검토
- **John Doe 영장**: 용의자 미상이나 DNA가 확보된 경우, "John Doe" 명의로 영장을 발부하여 시효 진행을 정지시키는 기법 등장
- **한계**: DNA 증거가 존재하는 범죄는 전체의 10% 미만

> DNA는 "증거가 시간과 함께 소멸한다"는 전제를 무너뜨렸다. 그러나 모든 범죄에 DNA가 있는 것은 아니므로, 시효의 정당성이 완전히 소멸한 것은 아니다.

### 5.2 GDPR의 "잊힐 권리" --- 시효의 현대적 메아리

EU 일반데이터보호규정(GDPR) 제17조의 "잊힐 권리(Right to be Forgotten)"는 시효제도의 디지털 시대 버전으로 읽을 수 있다:

**핵심 원리**: 정보주체는 자신의 개인정보가 "부적절하거나, 관련성이 없거나, 더 이상 관련이 없거나, 수집 목적에 비해 과도한" 경우 삭제를 요구할 수 있다. 이는 "spent conviction(실효된 유죄판결)"과 유사하게, 데이터도 시간이 지나면 "spent(소진)"된 것으로 간주될 수 있다는 원리다.

**시효와의 구조적 유사성**:

| 시효제도 | GDPR 잊힐 권리 |
|---------|---------------|
| 일정 기간 경과 후 소추권 소멸 | 목적 달성/기간 경과 후 삭제 의무 |
| 증거 열화로 적정 재판 불가 | 데이터의 관련성 상실 |
| 법적 안정성/피고 안식 | 정보주체의 프라이버시 보호 |
| 중범죄(살인 등) 예외 | 공익적 필요 시 예외 |

**전 세계적 확산**: 아르헨티나, 필리핀, 캐나다(CPPA), 한국(개인정보보호법), 인도(DPDP Act 2023) 등이 유사 규정 도입.

### 5.3 AI와 "잊을 수 없는 기계" --- 시효의 기술적 불가능성?

현대 AI 시스템은 시효제도의 근본 전제를 기술적으로 무력화한다:

#### 핵심 문제: "디지털 영속성(digital permanence)"

> "21세기에 디지털 정보는 인류 역사상 유례없는 영속성을 획득했다. 모든 상호작용이 분산 서버에 저장되고 글로벌 네트워크에서 복제된다."

#### 머신 러닝의 "잊기" 문제

- AI 모델은 정보를 이산적 항목으로 저장하지 않는다. 개인정보가 모델 파라미터에 통합되면, 값비싼 재훈련이나 실험적 **머신 언러닝(machine unlearning)** 없이는 제거가 거의 불가능하다.
- 데이터베이스에서 기록을 삭제해도, 그 기록이 모델의 내부 표상(internal representations)에 미친 영향은 제거되지 않는다.

#### "잊힐 권리는 죽었다" --- 기술적 한계

ICLR 2025 논문에 따르면, 현재의 머신 언러닝 기법은 **데이터의 영향을 완전히 제거하는 데 실패**한다. 주요 기술적 장벽:

1. **검증 문제**: "잊기"가 실제로 발생했는지 증명할 방법이 없다
2. **데이터 접근 요건**: 언러닝에는 원본 데이터셋 접근이 필요하나, 상업용 LLM의 훈련 데이터는 재구성 불가능
3. **효용-망각 트레이드오프**: 공격적 정보 제거는 무관한 태스크의 성능도 저하시킨다
4. **스케일 문제**: 기존 기법은 소규모 분류기에서 테스트되었을 뿐, 수조 개 파라미터의 LLM에 확장되지 않았다

#### "설계에 의한 망각(Forgetting by Design)"

새로운 패러다임으로 **"설계에 의한 망각"**이 제안되고 있다:

> "이 패러다임은 망각을 우발적이거나 임시적인 것이 아니라, 형식적으로 명시되고, 측정 가능하고, 감사 가능한 능력으로 취급한다. 이는 명시적인 보안, 프라이버시, 효율성, 또는 효용 목표에 의해 지배된다."

**메모리 거버넌스(Memory Governance)**:

> "메모리 거버넌스는 AI 시스템의 메모리를 통제하는 정책과 메커니즘을 의미한다 --- 무엇을 유지하고, 무엇을 잊고, 어떤 정책 하에 그렇게 할 것인지를 결정하는 실천이다."

---

## 6. 시효 폐지 사례의 비교 분석: 전과 후

| 국가 | 폐지 시기 | 대상 범죄 | 소급 적용 | 주요 촉발 요인 | 사후 효과 |
|------|----------|-----------|----------|-------------|----------|
| 독일 | 1979 | 모살(qualified murder) | 미만료 건에 한해 | 나치 전범 시효 임박 | 100세 이상 전범 기소 사례 등장 |
| 일본 | 2010 | 사형 해당 범죄 | 미만료 건에 한해 (당일 시행) | 피해자 유족 운동 | 1995년 미해결 살인 등 구제 |
| 한국 | 2015 | 1급 살인 | **불소급** (이미 만료건 제외) | 화성사건, 태완이 사건 | 화성사건 진범 특정에도 처벌 불가 |
| 프랑스 | 2017+ | 집단살해, 인도에 반한 죄, (2023 미성년 성폭력 권고) | 해당 없음 | #MeToo, 아동학대 폭로 | 피해자 48세까지 고소 가능 |
| 국제(ICC) | 2002 | 집단살해, 전쟁범죄, 인도에 반한 죄 | 2002.7.1 이후 범행에 한해 | 르완다, 구유고슬라비아 경험 | 국제적 규범 확립 |

---

## 7. 종합 분석: AI 에이전트 메모리 시스템을 위한 교훈

### 7.1 시효제도에서 추출 가능한 설계 원칙

| 역사적 원리 | AI 메모리 시스템 대응 | 구현 방향 |
|-----------|-------------------|----------|
| **증거 열화(evidentiary decay)** | 정보 신뢰도의 시간적 감쇠 | 메모리 항목에 confidence decay function 적용 |
| **법적 안정성(legal certainty)** | 시스템 상태의 예측 가능성 | 오래된 메모리가 현재 행동을 지배하지 않도록 가중치 조정 |
| **중범죄 예외(murder exception)** | 안전 관련 메모리는 만료 없음 | safety-critical memory는 TTL 면제 |
| **소급 불적용** | 새 정책은 기존 데이터에 소급 적용하지 않음 | retention policy 변경 시 기존 메모리 보호 |
| **피해자 권리 vs 피고 안식** | 사용자 이익 vs 시스템 효율 | 사용자에게 메모리 만료 정책에 대한 통제권 부여 |
| **이슬람법의 이중 권리 구조** | 시스템 규칙 vs 사용자 선호 | 계층적 메모리 retention 정책 |
| **DNA의 시효 해체** | 새로운 기술이 기존 망각 정책을 무력화 | 메모리 정책의 동적 업데이트 메커니즘 |
| **GDPR 잊힐 권리** | 사용자의 명시적 삭제 요구 | 사용자 주도 메모리 삭제 기능 |
| **머신 언러닝의 한계** | 완전한 삭제의 기술적 불가능성 | 영향 무력화(nullification) vs 완전 삭제의 구분 |

### 7.2 "제도적 망각"의 핵심 통찰

역사적으로 시효제도는 단순한 "잊기"가 아니라 다음의 **복합적 기능**을 수행했다:

1. **시스템 남용 방지** (아테네의 시코판트 통제)
2. **자원 효율화** (사법 자원의 현재 집중)
3. **상태 보호** (현재의 사회적 안정 > 과거의 정의 실현)
4. **오류 비용 관리** (열화된 증거로 인한 오판 방지)
5. **도덕적 감쇠 반영** (가벌성의 시간적 감소)

그러나 동시에, 시효의 역사는 이 제도가 **끊임없이 도전받고 수정되어 왔음**을 보여준다. 아테네에서조차 살인은 예외였고, 20세기 이후 중대범죄에 대한 시효 폐지는 전 세계적 추세가 되었다.

> **최종 통찰**: "잊기"를 설계하는 것은 "기억하기"를 설계하는 것만큼이나 어렵고, 어쩌면 더 어렵다. 2,500년의 법사(法史)가 보여주는 것은, 완벽한 망각 정책은 존재하지 않으며, 망각의 규칙은 사회적 맥락과 기술적 조건에 따라 끊임없이 재협상되어야 한다는 것이다.

---

## Sources

### 고대 기원 및 로마법
- [Statute of limitations - Britannica](https://www.britannica.com/topic/statute-of-limitations)
- [Prescription - Encyclopedia (Theodora)](https://theodora.com/encyclopedia/p2/prescription.html)
- [Usucaption - Wikipedia](https://en.wikipedia.org/wiki/Usucaption)
- [LacusCurtius - Roman Law Usucapio (Smith's Dictionary)](https://penelope.uchicago.edu/Thayer/E/Roman/Texts/secondary/SMIGRA*/Usucapio.html)
- [A Brief History of the Origins of the Statute of Limitations](https://andrewwarland.wordpress.com/2010/01/28/the-really-brief-history-of-the-origins-of-the-statute-of-limitations/)
- [Praescriptio Longi Temporis - ResearchGate](https://www.researchgate.net/publication/386105854_PRAESCRIPTIO_LONGI_TEMPORIS)
- [Some Remarks on Extinctive Prescription in Legal History](https://www.civilprocedurereview.com/revista/article/download/276/232)
- [Lex Julia de adulteriis (18 B.C.) - CSUN](http://www.csun.edu/~hcfll004/Adulteriis.html)

### 영국법 및 보통법
- [Limitation Act 1623 - Wikipedia](https://en.wikipedia.org/wiki/Limitation_Act_1623)
- [A Brief History of Time Limits - Jacobson Lawyers](https://jacobsonlawyers.com/wordpress/wp-content/uploads/2013/04/A-Brief-History-of-Time-Limits.pdf)

### 이슬람법
- [Is There an Islamic Parallel to Statute of Limitations? - SeekersGuidance](https://seekersguidance.org/answers/hanafi-fiqh/is-there-an-islamic-parallel-to-the-western-legal-concept-of-a-statute-of-limitations/)
- [Mecelle - Wikipedia](https://en.wikipedia.org/wiki/Mecelle)
- [Application of Statutes of Limitations to Islamic Banking - JMIFR](https://jmifr.usim.edu.my/index.php/jmifr/article/download/260/282)
- [Prescription in Saudi Arabian Hanbali Law - Brunel University](https://bura.brunel.ac.uk/handle/2438/13801)

### 동아시아법
- [Traditional Chinese Law - Wikipedia](https://en.wikipedia.org/wiki/Traditional_Chinese_law)
- [Tang Code - Wikipedia](https://en.wikipedia.org/wiki/Tang_Code)
- [Understanding Traditional Chinese Law: Tang Dynasty - SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2568017)
- [Legal Codes of Historic Korea - TOTA](https://www.tota.world/article/147/)
- [공소시효 - 한국민족문화대백과사전](https://encykorea.aks.ac.kr/Article/E0067767)
- [공소시효 - 나무위키](https://namu.wiki/w/%EA%B3%B5%EC%86%8C%EC%8B%9C%ED%9A%A8)
- [Statutes of Limitations of the Criminal Code in Taiwan - DPCE Online](https://www.dpceonline.it/index.php/dpceonline/article/view/1460)

### 독일 시효 논쟁
- [W. Germany Drops Time Limit For Nazi Crimes - Washington Post](https://www.washingtonpost.com/archive/politics/1979/07/04/w-germany-drops-time-limit-for-prosecution-of-nazi-crimes/f262bbd3-4be7-40b1-8b2f-70c3fdf455ef/)
- [In Pursuit of Justice: Debating the Statute of Limitations for Nazi War Crimes](https://www.tandfonline.com/doi/abs/10.1080/17504902.2014.11435376)
- [Trial of 100-year-old man in Germany - The Conversation](https://theconversation.com/trial-of-100-year-old-man-in-germany-why-nazi-war-crimes-take-so-long-to-prosecute-166001)

### 일본/한국 시효 폐지
- [Japan: Statute of Limitations for Murder Abolished - Library of Congress](https://www.loc.gov/item/global-legal-monitor/2010-05-21/japan-statute-of-limitations-for-murder-abolished/)
- [Japan abolishes statute of limitations for murder - JURIST](https://www.jurist.org/news/2010/04/japan-abolishes-statute-of-limitations/)
- [South Korea Removes Statute of Limitation On Murder - Korean Law Blog](https://www.thekoreanlawblog.com/2015/07/defense-lawyer-korea-murder.html)
- [이춘재 연쇄살인 사건 - 위키백과](https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%B6%98%EC%9E%AC_%EC%97%B0%EC%87%84_%EC%82%B4%EC%9D%B8_%EC%82%AC%EA%B1%B4)
- [Korea's most-notorious serial killing cold case - CNN](https://www.cnn.com/2020/05/23/asia/south-korea-hwaseong-murder-injustices-intl-hnk)

### DNA 및 현대적 쟁점
- [Using DNA to Solve Cold Cases - NIJ](https://www.ojp.gov/pdffiles1/nij/194197.pdf)
- [DNA - Statute of Limitations - NIJ](https://nij.ojp.gov/nij-hosted-online-training-courses/dna-prosecutors-practice-notebook-inventory/special-case-circumstances/cold-hits-and-cold-cases/statute-limitations)

### GDPR 및 AI 망각
- [Right to be Forgotten - GDPR.eu](https://gdpr.eu/right-to-be-forgotten/)
- [The Right to Be Forgotten Is Dead: Data Lives Forever in AI - TechPolicy.Press](https://www.techpolicy.press/the-right-to-be-forgotten-is-dead-data-lives-forever-in-ai/)
- [Machine Unlearning in 2024 - Stanford](https://ai.stanford.edu/~kzliu/blog/unlearning/)
- [Machine Unlearning Fails to Remove - ICLR 2025](https://proceedings.iclr.cc/paper_files/paper/2025/file/7e810b2c75d69be186cadd2fe3febeab-Paper-Conference.pdf)
- [Beyond Permanent Memory: Digital Forgetting - IJFMR](https://www.ijfmr.com/papers/2025/5/58292.pdf)
- [Forgetting by Design: Engineered Memory Erasure](https://www.emergentmind.com/topics/forgetting-by-design)
- [Memory Governance and AI Security - Acuvity](https://acuvity.ai/what-is-memory-governance-why-important-for-ai-security/)
- [The AI Right to Unlearn - IAPP](https://iapp.org/news/a/the-ai-right-to-unlearn-reconciling-human-rights-with-generative-systems)

### 프랑스 개혁
- [Statute of Limitation Reform in Criminal Matters - Soulier Avocats](https://www.soulier-avocats.com/en/statute-of-limitation-reform-in-criminal-matters/)
- [France commission recommends removing statute of limitations - JURIST](https://www.jurist.org/news/2023/11/france-commission-recommends-removing-statute-of-limitations-for-sexual-violence-against-minors/)

### 국제형사재판소
- [Rome Statute - ICC](https://www.icc-cpi.int/publications/core-legal-texts/rome-statute-international-criminal-court)

### 시효 정당성 이론
- [The Puzzling Purposes of Statutes of Limitation - Santa Clara Law](https://digitalcommons.law.scu.edu/cgi/viewcontent.cgi?article=1107&context=facpubs)
- [공소시효, 도대체 무엇이고 왜 필요한가 - 시사저널](https://www.sisajournal.com/news/articleView.html?idxno=136886)

### 교회법
- [Catholic Encyclopedia: Prescription](https://www.newadvent.org/cathen/12395b.htm)
- [Prescription - Catholic Answers](https://www.catholic.com/encyclopedia/prescription)
