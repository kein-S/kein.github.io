# Swift design patterns

## Massive ViewController

iOS project 에서 ViewController 가 비대해지는건 고질적인 문제다.
MVC 패턴에서 Controller 가 비지니스 로직을 담당 해야하는데, ViewController 는 View 와 Controller 가 강하게 붙어 있어서, 보통 View의 구현과 비지니스 로직의 구현을 같이 하게 되기 때문이다. ViewController가 비대해지면 몇가지 단점이 있는데

* 코드 가독성이 떨어진다.
* 의존성 문제가 복잡해질 가능성이 크다.
* 이로 인해 test 를 복잡하고 불가능하게 만든다.
* Model / UI / Business logic (사실상 모든 코드)의 변경에 취약하다.

이를 해결하기 위해서 다양한 디자인 패턴들이 제안되었고 (MVVM, VIPER, VIP 등)
발전하고 있다. 이 글에서는 여러 패턴들의 장단점을 파악해 보고, 이 중 MVVM 패턴을 깊게 파보려고 한다.

## Good design patterns

Massive ViewController 의 문제를 해결하기 위한 나름의 현실적인 기준을 세워보았다.

### 계층간 의존성을 명확히 분리 할 수 있는가?

Model 과 View 그리고 비지니스 로직을 명확히 분리해서 구현하는것은 매우 중요하다. 계층간의 경계가 모호하면 하나의 계층의 변경이 다른 계층에 테러를 하게 된다.

예를 들면 어떤 View 를 외부에서 움직이는 속성이 4개 있다고 가정을 해보자.
```swift
progressView.backgroundColor = .white
progressView.innerBorderColor = .red
progressView.borderColor = .gray
progressView.alpha = 0.5
```
그런데 UI 요구사항이 변경되어 다른 속성을 3개 추가하게 되었다면, progressView가 있는 모든 코드를 찾아서 속성을 3가지 추가 해야한다.
대박. 심지어 이런 단순한 코드가 아니고 model 의 변경이 UI 까지 반영되는 코드라고 가정하면 상황은 더 복잡해진다. 그런데 만약 계층간의 연결이 단순화 되고 역할이 명확히 구분된다면 어떨까?
```swift
progressView.configure(setting: progressViewSetting)

```
더 자세한 얘기는 의존성 주입(DI) 에 대해 다룰때 해야겠다. 여기서 말하고 싶은것은 계층간의 연결통로를 1개 또는 2개 로 단순화 하고 역할을 명확히 해서, view 의 변경만 필요할땐 view 만 변경 할 수 있도록 하는 것이다.

### 기존 프로젝트를 Refectoring 하는데 어려움이 없는가?

*MVC 를 다른 패턴으로 바꾸는데서 오는 어려움에 대해 설명.*

### 코드 생산성을 오히려 떨어뜨리지 않는가?

*디자인 패턴을 만들기 위한 추가 코드의 오버헤드와 학습난이도에 대해 설명.*

## MVP, MVVM, VIPER, VIP

*각 패턴에 대해 장단점 서술*

## MVVM-Coordinator

*MVVM-C 에 대해 설명, 아쉬운점 설명, 이를 개선하기 위한 방법 설명, 예제코드*
