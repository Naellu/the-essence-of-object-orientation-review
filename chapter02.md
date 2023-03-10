# 02. 이상한 나라의 객체

|chapter|                                                     name                                                     |
|:---|:------------------------------------------------------------------------------------------------------------:|
| 1장 | [협력하는 객체들의 공동체](https://github.com/Naellu/the-essence-of-object-orientation-review/blob/master/chapter01.md) |
| **2장** |  [이상한 나라의 객체](https://github.com/Naellu/the-essence-of-object-orientation-review/blob/master/chapter02.md)   |

<br>

> 객체지향 패러다임은 지식을 추상화하고 추상화한 지식을 객체안에 캡슐화함으로써 실세계 문제에 내재된 복잡성을 관리하려고 한다.
> 객체를 발견하고 창조하는 것은 지식과 행동을 구조화하는 문제다. - 레베카 워프스브록(Rebecca Wirfs-Brock)

<br>

### 객체, 그리고 이상한 나라

'이상한 나라의 앨리스'의 이야기 초반부에서 앨리스는 작은 문을 통과하기 위해 자신의 키를 줄이거나 늘렸다  
문을 통과하기 위해 앨리스는 자신의 키를 적당한 `상태`로 변화시켰다  
또한 키를 변화시키기 위해 병 속의 음료를 마시거나 케이크를 먹는 것은 앨리스의 `행동`이었다

**앨리스의 상태를 결정하는 것은 행동이지만 행동의 결과를 결정하는 것은 상태이다**

`행동`간에는 **순서**도 중요한데, 문을 통과하기 위한 `행동1`을 하기전에  
먼저 키를 작게 변화시켜야 문을 통과할 수 있으니 키를 변화시키는 음료를 마시는 `행동2`가 선행되어야 하는 것이다

음료를 마시거나 케이크를 먹는 행동으로 상태가 변했지만  
우리는 여전히 앨리스를 앨리스로 부르는 것과 같이 앨리스가 어떤 상태에 있더라도 `식별 가능`하다

<br>

### 객체, 그리고 소프트웨어 나라

객체의 특성을 효과적으로 설명하기 위해서는 `상태(state)`, `행동(behavior)`, `식별자(identity)`를 지닌 실체롤 보는것이 효과적이다

#### 상태

`상태`를 이용하면 과거 모든 행동이력을 설명하지 않고도 행동의 결과를 예측할 수 있게된다  
앨리스가 무슨 행동을 했었던지간에 앨리스의 키와 문의 높이만 알게된다면 문을 통과한다는 행동의 결과를 알 수 있는 것처럼 말이다

앨리스나 음료, 케이크는 객체지만 앨리스의 `키`와 `위치`, 음료나 케이크의 `양`은 객체가 아니다  
이런 단순한 값들은 다른 객체의 상태를 표현하기 위해 사용된다

앨리스가 현재 음료를 들고 있는 상태를 표현하고 싶다면  
앨리스의 상태 일부를 음료 객체를 이용해 표현할 수 있다

1. 키는 130cm, 위치는 "통로" `---` `음료`의 양은 0.5l -> 음료를 가지고 있는 앨리스의 상태
2. 키는 40cm, 위치는 "정원" ` ` ` ` ` ` `음료`의 양은 0.5l -> 음료를 마시고 버린 앨리스의 상태

객체의 상태를 구성하는 모든 특징을 통틀어 객체의 `프로퍼티(property)` 라고 한다  
-> 앨리스의 키, 위치, 음료가 프로퍼티이며 고정되기 때문에 정적이다  
반면 `프로퍼티 값(property value)`은 시간이 흐름에 따라 변경되기 때문에 동적이다

1번에서는 앨리스가 음료를 알고있었지만, 2번에서는 음료에 대해 알지 못하는 상태로 변경되었다  
이처럼 객체와 객체 사이 의미있는 연결을 `링크(link)`라고 한다, 객체의 링크가 존재해야 메시지를 받을 수 있다  
링크와 달리 객체를 구성하는 단순한 값은 `속성(attribute)`이라고 한다 (앨리스의 키와 위치)

자율적인 객체는 스스로 자신의 상태를 책임져야한다  
외부의 객체가 직접적으로 객체의 상태를 조율할 수 없다면 간접적으로 객체의 상태를 변경하거나 조회할 수 있는 방법이 필요하다

<br>

#### 행동

객체가 취하는 행동은 객체 자신의 상태를 변경시킨다  
객체의 행동이 `부수 효과(side effect)`를 초래한다는 것을 의미한다

객체의 행동은 두 가지 관점의 부수효과를 명확하게 서술해야 한다
1. 객체 자신의 상태 변경
2. 행동 내에서 협력하는 다른 객체에 대한 `메시지 전송`

앨리스는 음료를 마신다는 행동을 하면 자신의 `상태를 변화`시킬 수 있다  
앨리스가 가진 상태 중 하나인 음료객체에도 자신이 마신 양만큼 음료의 양을 줄여달라고 `메시지를 전송`한다

앨리스가 음료의 양을 직접 바꾸는 것이 아니다  
그저 자신이 마신 양만큼 믿고 요청만 할 뿐이다  
앨리스는 `drinkBeverage()`이라는 메시지를 받고 음료에게 `drunken(quantity)`이라는 메시지를 보낸다  
여기서 앨리스가 음료의 상태 변경에 대해서는 예상할 수 없다

**메시지 송신자는 메시지 수신자의 상태 변경에 대해서는 전혀 알지 못한다는 것이다**

이것이 `캡슐화`의 의미이며, 객체가 외부로 노출하는 것은 **행동**뿐이고 외부에서 객체에 접근할 수 있는 유일한 방법 또한 **행동** 뿐이다    
송신자는 단지 요청을 메시지로 포장해서 전달할 뿐이지 메시지를 해석하고 상태를 변경할지 말지는 전적으로 수신자의 `자율적인 판단`에 따라야한다

상태를 잘 정의된 행동 뒤로 캡슐화하는 것은 **객체의 자율성을 높이고 협력을 단순하고 유연하게 만든다**  
이것이 상태를 캡슐화해야 하는 이유다

<br>

#### 식별자

식별 가능하다는 것은 서로 구별할 수 있는 특정한 프로퍼티가 객체안에 존재한다는 것을 의미한다  
이것을 `식별자`라고 한다

값은 숫자, 문자열, 날짜 시간 등 변하지 않는 양을 모델링하며 `불변 상태(immutable state)`를 가진다고 말한다  
값은 상태를 이용해 두 값이 같은지 판단할 수 있는 `동등성(equality)`의 성질이 있다  
때문에 인스턴스를 구별하기 위한 별도의 식별자를 필요로 하지 않는다

객체는 시간에 따라 변경되는 상태를 포함하며, 행동을 통해 상태를 변경하기에 `가변 상태(mutable state)`를 가진다고 말한다  
두 객체의 상태가 다르더라도 식별자가 같다면 같은 객체로 판단할 수 있다, 이 성질을 `동일성(identical)`이라고 한다  
객체는 가변상태를 가지기에 상태를 기반으로 동일성을 판단할 수 없다    
그렇기에 상태 변경에 독립적인 별도의 식별자를 이용할 수 밖에 없다

식별자를 지닌 객체는 `참조 객체(reference object)`, `엔티티(Entity)`라고 하며  
식별자를 가지지 않는 값은 `값 객체(value object)`라고 한다

<br>

### 행동이 상태를 결정한다

상태를 먼저 결정하고 행동을 나중에 결정하는 방법은 설계에 나쁜 영향을 끼친다

1. 상태를 먼저 결정할 경우 캡슐화가 저해된다
2. 객체를 협력자가 아닌 고립된 섬으로 만든다
3. 객체의 재사용성이 저하된다

객체지향 설계는 애플리케이션에 필요한 협력을 생각하고 협력에 참여하는데 필요한 행동을 생각한 후  
행동을 수행할 객체를 선택하는 방식으로 진행되어야한다  
그 후 행동에 필요한 정보가 무엇인지를 고려하게 되며 이 과정에서 필요한 상태가 결정된다

협력 안에서 객체의 행동은 결국 객체가 협력에 참여하면서 완수해야 하는 책임을 의미한다  
어떤 책임이 필요한가를 결정하는 과정이 전체 설계를 주도해야한다 `RDD(Responsebility-Driven Design)`

<br>

### 은유와 객체

현실속에서는 수동적인 존재가 소프트웨어 객체로 구현될 때는 능동적으로 변한다    
현실의 객체보다 더 많은 일을 할 수 있는 소프트웨어 객체의 특징을 `의인화(anthropomorphism)`라고 부른다  
스스로 전화를 걸고 끊는 전화기나 눈에 보이지 않는 공기나 바람도 소프트웨어 안에선 시각적인 형태를 가지도록 만들 수 있다

실제로 적용되지 않는 한 가지 개념을 이용해 다른 개념을 서술하는 `은유(metaphor)`가 있다  
현실 속의 객체의 의미 일부가 소프트웨어 객체로 전달되기 때문에 프로그램 내의 객체는 현실 속의 객체에 대한 은유이다

은유 관계에 있는 실제 객체의 이름을 소프트웨어 객체의 이름으로 사용하면 표현적 차이를 줄여 소프트웨어의 구조를 쉽게 예측할 수 있다  
이처럼 현실 객체의 은유를 효과적으로 사용할 경우 표현적 차이를 줄일 수 있어 이해하기 쉽고 유지보수가 용이한 소프트웨어를 만들 수 있다  

