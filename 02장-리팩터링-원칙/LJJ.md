## 목차

- [2.1 리펙터링 정의](#21-리펙터링-정의)
- [2.2 두 개의 모자](#22-두-개의-모자)
- [2.3 리팩터링하는 이유](#23-리팩터링하는-이유)
- [2.4 언제 리팩터링해야 할까?](#24-언제-리팩터링해야-할까)
- [2.5 리팩터링 시 고려할 문제](#25-리팩터링-시-고려할-문제)
- [2.6 리팩터링, 아키텍처, 에그니(YAGNI)](#26-리팩터링-아키텍처-에그니yagni)
- [2.7 리팩터링과 소프트웨어 개발 프로세스](#27-리팩터링과-소프트웨어-개발-프로세스)
- [2.8 리팩터링과 성능](#28-리팩터링과-성능)
- [2.9 리팩터링의 유래](#29-리팩터링의-유래)
- [2.10 리팩터링 자동화](#210-리팩터링-자동화)

## 2.1 리펙터링 정의

- 리팩터링은 코드를 정리하는 모든 작업을 말한다.
- 동작을 보존하는 작은 단계들을 거쳐 코드를 수정하고
- 이러한 단계들을 순차적으로 연결하여 큰 변화를 만들어내는 일
  > 리팩터링하는 동안에는 코드가 항상 정상 작동하기 때문에 전체 작업이 끝나지 않더라도 언제든 멈출 수 있다.

```
지금까지 내가 리팩터링이라고 부르던 친구들은 사실 리팩터링이 아니었던 것 같다...리팩터링을 진행하면 항상 코드가 깨져서 고생하는데, 여기서는 그걸 리팩터링이라고 부르지 않는다.
```

코드 베이스를 정리하거나, 구조를 바꾸는 모든 작업을 `재구성` 이라는 포괄적인 의미로 표현한다.

| 이름       | 목적                                                                            |
| ---------- | ------------------------------------------------------------------------------- |
| 리팩터링   | 기능은 유지하고, 코드를 이해하고 수정하기 쉽게 만드는 것이 목적                 |
| 성능최적화 | 속도 개선에 초점을 둔 코드 변경, 이 과정에서 코드가 오히려 더 복잡해질 수 있다. |

## 2.2 두 개의 모자

`기능추가`모자를 썼다면, 기능추가만하고, 수정을 하지 않는다.
`리팩터링`모자를 썼다면, 기능추가는 하지 않고, 코드를 재구성하는 일에만 집중한다.

글쓴이는 `기능추가`중간에 `구조개선`이 필요하다고 느끼면, `리팩터링`모자를 잠깐 써서, 코드의 구조를 바꾸고, 다시 `기능추가`모자로 돌아와 작업을 한다고 한다.

## 2.3 리팩터링하는 이유

> 리팩터링하면 소프트웨어 설계가 좋아진다.

중복 코드 제거는 설계 개선 작업의 중요한 축을 차지한다.
코드량을 줄인다고 해서 시스템이 빨라지는 것은 아니지만, 수정하는데 드는 노력은 크게 달라질 수 있다.
또한, 모든 코드가 언제나 고유한 일을 수행함을 보장할 수 있다.

> 리팩터링하면 소프트웨어 이해하기 쉬워진다.

미래의 내가, 혹은 내가 아닌 다른사람이 코드를 확인할 때, 코드를 쉽게 이해할 수 있다.

> 버그를 찾기 쉽다.

> 프로그래밍 속도를 높일 수 있다.

처음 리팩터링을 진행할때는 오히려 시간이 더 걸린다고 생각할 수 있지만, 지속적인 기능 추가로 인해서 변경점이 발생할 때, 잘 짜여진 설계를 바탕으로한 구조는 쉽게 기능추가가 가능하기 때문에, 결과적으로 프로그래밍 속도가 증간한다.

## 2.4 언제 리팩터링해야 할까?

| 리팩터링                               | 내용                                                                                                                                                                       |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 준비를 위한 리팩터링                   | 리팩터링하기 가장 좋은 시점은 기능을 추가할 때 이다. 기능을 추가하기 전에 구조를 살짝 바꾸면 다른 작업을 하기 훨씬 쉬워질 만한 부분을 찾아서 바꿔준다.                     |
| 이해를 위한 리팩터링                   | 자신 혹은 다른 사람이 코드를 파악할 때 코드의 의도가 명확하게 들어나도록 리팩토링                                                                                          |
| 쓰레기 줍기 리팩터링                   | 비효율 적인 코드를 발견했을 때, 즉시 수정할 수 있는건 수정하고, 시간이 걸리는 일은 두고두고 조금씩 리팩터링을 진행한다. 조금씩 개선하다보면 문제가 해결되어 있다.          |
| 계획된 리팩터링과 수시로 하는 리팩터링 | 리팩터링 시간을 따로 두지 않고, 다른 일을 하는 중에 처리한다. 미뤘던 코드 개선을 하기 위한 계획된 리팩터링은 나쁜게 아니지만, 수시로 조금씩 개선하는게 좋다. (글쓴이 의견) |
| 오래 걸리는 리팩터링                   | 대부분의 리팩터링은 짧은 시간에 끝나는데, 긴 시간이 걸리는 리팩터링을 하면 좋지 않다. 조금씩 시간을 두고 해결하는 편이 효과적일 때가 많음                                  |
| 코드 리뷰에 리팩터링 활용하기          | 리팩터링에 대한 아이디어를 수집해, 한 차원 더 높은 리팩터링이 가능할 수 있다. -> 프로그래밍 과정 안에 지속적인 코드 리뷰가 녹아들어간 짝 프로그램이 된다                   |
| 리팩터링을 하지 말아야 할 때           | 지저분한 코드를 발견해도 굳이 수정할 필요가 없다면 하지 않는다. (외부 API를 다루 경우), 혹은 리팩터링보다 다시 만드는게 빠르다고 판단될 경우(상급자 코스)                  |

## 2.5 리팩터링 시 고려할 문제

결국 리팩토링은 새 기능 개발의 속도를 증가시킨다.(계속 반복해서 하는 말)

> 리팩터링의 궁극적인 목적은 개발 속도를 높여서, 더 적은 노력으로 더 많은 가치를 창출하는 것

- 코드 소유권

  팀의 누구든 소유한 코드를 수정할 수 있도록 해야한다. 그리고 수정된 코드를 잘 관리하는게 해당 영역을 책임지는 사람의 임묵다.
  오픈소스에서 사용하는 개발 모델은 대규모 시스템 개발에 적합하다.

- 브랜치

  보통 브랜치 작업을 진행할 때, 기능 브랜치로 나눠서 작업 지행 후 통합 브랜치로 통합하는 개발 방식을 진행하는데, 해당 방식에서 큰 문제점이 있다.
  브랜치에서 개발하는 기간이 늘어날 수 록, 통합브랜치로부터 받아와야할 데이터가 많아져 복잡도가 증가한다는 것 이다.
  이를 해결하기 위해서는 짧은 주기의 통합(머지) 를 가져가야 한다.

  다른 방법으로는 CI를 활용해서 리팩터링을 함께 진행하는 것이다. 겐트 백이 제안한 XP(eXtreme Programming)기법이 존재한다.

- 테스트

  테스트는 리팩터링을 할 수 있게 해줄 뿐 아니라, 새로운 기능 추가도 훨씬 안전하게 가능하다.
  그리고 이 과정은 배포를 더 쉽게 만들어준다. (CICD)

- 레거시 코드

  레거시 코드를 파악할 때 리팩터링이 도움이 많이 된다.
  대규모 레거시 시스템을 리팩터링하기 위해서 테스트 보강을 해야한다. (복잡하고, 시간이 많이 소요되는 과정)
  단번에 리팩터링을 진행하는 것 보단, 조금씩 나눠서 진행

## 2.6 리팩터링, 아키텍처, 에그니(YAGNI)

리팩터링을 통해서 기존의 수년동안 운영하던 아키텍쳐를 바꾸는데 유용하다.

> 유연성 메커니즘

다양한 예상 시나리오에 대응하기 위한 `매개변수`를 추가한다. 이것이 유연성 매커니즘인데, 이 `매개변수`를 무지성으로 사용하면 `함수`의 `복잡도`가 `증가` 하기 때문에 모든 상황에서 사용되는 것은 아니다.
모든 상황을 고려하다보면 유연성 매커니즘이 오히려 대응 능력을 떨어뜨릴 때가 있다.

리팩터링을 활용하면, 미래를 예측할 필요없이, 그저 현재까지 파악한 요구사항만을 해결하는 소프트웨어를 구축할 수 있다.
사용자 요구사항을 더 잘 이해하게 되면 아키텍처도 그에 맞게 리팩터링하면 된다.

이런식으로 설계하는 방식을

- 간결한 설계
- 점진적 설계
- YAGNI(you aren't going to need it)

처음부터 미래를 예측한 아키텍처를 변경하는게 아닌, 현재 상황을 이해(리팩터링)하고 이해가 완료되었을 때, 아키텍처를 그에 맞게 처리하는 방식이 훨씬 좋다고 생각하는 것이다.

## 2.7 리팩터링과 소프트웨어 개발 프로세스

- 팀에서 실행하는 프로세스에 따라서 리팩터링의 효과가 크게 달라질 수 있다.

- 최초의 애자일 방법론중 하나인 `XP`는 수년에 걸쳐 부흥을 이끌었고, 현재도 상당수의 프로젝트에서 이 `애자일 프로세스`가 이용된다.
  애자일을 제대로 적용하려면, 리팩터링에 대한 팀의 역량과 열정이 뒷받침 되어야 한다.

> 프로세스 전반에 걸쳐 자연스럽게 리팩터링이 스며들게 해야한다.

자가 테스트 코드와 리팩터링을 묶어서 `테스트 주도 개발 TDD`라 부른다.

## 2.8 리팩터링과 성능

> 리팩터링 vs 성능

리팩터링을 하면 성능이 떨어지는건 사실이지만, 리팩터리을 통해서 더욱 쉽게 성능을 개선시킬 수 있다.

성능개선의 세 가지 방법

- 시간 예산 분배: 엄격한 시간 엄수가 강조된 방법으로 시간에 민감한 데이터를 다룰때 유용하게 작용한다.
- 끊임없이 관심을 기울이기 : 프로그램 특정 동작 뿐 아니라, 컴파일러, 런타임, 하드웨어 동작에 대해서도 잘 이해해야 한다.
- 90%의 시간 낭비 : 대부분의 프로그램은 극히 일부분의 동작에서 많은 시간을 소비한다. 그 말은 리팩터링 없이 성능최적화만한다면 `90%의 시간`만 낭비한 다는 것 이다.
  그렇기 때문에 리팩터링을 진행하고, 그 사이에 발견되는 성능 문제를 최적화 시키는게 좋다.

## 2.9 리팩터링의 유래

리팩터링의 유래는 어디인지 모르지만, 프로그램을 개발하다 복잡하고, 수정하기 어려운 코드를 보고 사람들은 개선의 필요성을 느껴서 `리팩터링`이라는 개념이 나오게 되었고, 실제 프로젝트에 도입되면서 쓰이게 되었다.

## 2.10 리팩터링 자동화

> 프로그래밍 도구의 자동 리팩터링 기능의 추가

- 소스코드의 텍스트를 직접 조작하는 경우에는 허점이 많기 때문에 테스트를 해 봐야한다.

현재 여러 도구가 존재하고, 각 언어에 맞는 여러 방법이 있지만, 자동으로 해주는 리팩터링은 항상 문제를 염두해 두어야한다. (테스트를 꼭 진행해야 함)

## 2.11 더 알고 싶다면

- 윌리엄 웨이크 [ 리팩터링 워크북 ] : 리팩터링 연습 주력
- 조슈아 케리에프스키 [ 패턴을 활용한 리팩터링 ] : 디자인 패턴을 통한 리팩터링
- 예로 스캇 엠블러, 프라모드 사달게 [ 리팩토링 데이터베이스 ] : 범용 프로그래밍
- 엘리엇 러스트 해롤드 [ 리팩토링 HTML ] : 범용 프로그패밍
- 마이클 페더스 [ 레거시 코드 활용 전략 ] : 오래된 코드 베이스
