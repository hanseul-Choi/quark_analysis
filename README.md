# Quark

An Obfuscation-Neglect Android Malware Scoring System <br>
(난독화를 무시하는 악성 코드 점수 채점 시스템)

<br>

## 목차

### Background
  
1. [난독화](#난독화)

### Theory

1. [Installation](#Installation)

<br>

# background

## 난독화

코드 난독화는 프로그래밍 언어로 작성된 코드에 대해 읽기 어렵게 만드는 작업이다. <br>(출처: 위키백과 https://ko.wikipedia.org/wiki/%EB%82%9C%EB%8F%85%ED%99%94) 

### 난독화의 이유
일반적인 실행 파일은 컴파일이 된 후 기계어 명령어 형태로 변환되기 때문에 소스코드의 정보를 잃게 된다. 따라서, 컴파일 하는 과정으로 실행파일을 만드는 것 자체로 중요한 정보를 보호하기가 쉽다. 하지만, 자바의 경우 (안드로이드의 경우 자바기반 가상머신에서 컴파일이 됨(코틀린도 물론 자바 기반)) 중간 언어로 컴파일하여 가상기계에서 실행되는 경우, 디컴파일 시 소스 코드를 거의 대부분 보존하고 있다. 해커들은 이를 악용하여 취약점을 찾아내 코드 삽입 및 변조를 통해 해킹을 시도한다. 따라서, 코드 난독화를 하는 이유는 실행 파일에 대한 역공학(reverse engineering)을 막기 위한 방식이다. <br>
* 현존하는 소프트웨어는 대부분 바이너리 형태로 배포되고 있기 때문에, 소프트웨어의 보호를 위해서는 난독화 기술이 필수불가결하게 적용되어야 한다.
<br>  
  
### 코드 난독화
코드 난독화(Obfuscation)은 프로그램의 역공학 분석을 어렵게 하기 위해서 사용되는 기법이다. 프로그램의 의미(semantics)를 유지하면서 배치(layout), 논리(logic), 자료(data) 그리고 구조(organization) 를 변화시켜 역공학자가 읽기 힘들게 만들고, 자동화된 분석 도구가 분석하기 어렵게 하는 것을 의미한다. <br>
위에서 언급했듯이 중간 언어를 사용하는 실행파일(자바, 닷넷)은 소스 코드의 정보를 대부분 포함하고 있으며, 이 디컴파일을 막는 과정은 사실상 불가능하다. 따라서, 디컴파일을 하더라도 소스코드의 가독성을 떨어뜨리는 방식으로 코드 난독화를 진행한다.
<br>  

### 난독화 종류

#### 배치 난독화(layout obfuscation)
배치 난독화는 실행 파일에 포함되어 있는 문자열의 내용을 바꾸는 것으로 난독화를 수행한다. 즉, 문자열을 통해 호출하게 되는 메소드 이름과 필드 이름을 바꿈으로써 추측할 수 있는 의미를 제거한다. 메소드나 어떠한 변수 값은 모두 심볼 테이블(symbol table)에 의해 관리되는데, 해당 symbold table을 변경함으로써 역공학을 어렵게 한다.<br>

#### 자료 난독화(data obfuscation)
자료 난독화는 프로그램 내부의 자료구조를 바꾸어 자료를 암호화하는 방식이다.<br>
  
#### 제어 난독화(control obfuscation)
제어 난독화는 if문과 같은 제어 흐름을 바꾸는 것을 통해 역공학 과정을 어렵게 하는 방식이다.<br>
  
#### 방지 난독화(preventive obfuscation)
방지 난독화는 역공학 도구로 사용되는 도구를 무력화시키는 방법으로 본 내용에서는 중요하지 않아 넘어가겠다.<br>

### 난독화가 악성 코드 채점에 미치는 영향?
역공학을 하는 것이 악의적인 목적도 있지만 선의적인 목적도 가질 수 있다. 애초에 악의적으로 만든 앱을 배포할 경우, 악성 앱 탐지 프로그램에서는 역공학을 통해 소스코드를 분석해 악의적인 목적을 가지는지 확인하여 악성앱을 판단한다. Quark tool도 마찬가지이다. 디컴파일하여 소스코드를 읽는 과정에서 난독화가 이루어져 있으면, 소스코드 분석이 어려워 해당 앱이 악의적인 목적을 가지고 있는지 선의적인 목적을 가지고 있는지 확인하기가 어렵다. 그렇다면 Quark는 어떻게 난독화를 무시하는 것일까? 난독화 기술이 발전하면서, 난독화를 해독하는 deobfustation 기술도 늘어나고 있다. 해당 deobfuscation tool을 이용함으로써 이를 어느정도 해결할 것으로 기대한다.

* 난독화 이론 출처 : 코드 난독화를 이용한 악성 코드 분석 기법에 관한연구 (2005-11)

<br><br>

# Theory

## Installation
추천 운영체제는 devian linux이지만, 본 설치는 ubuntu linux를 통해 진행하였다. <br>
먼저 가상머신인 VM 머신을 다운받는다. https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html
<br> 작성자는 vmware workstaion pro 16버전을 이용하였다. <br>
그 후, ubuntu linux 사이트에 접속하여 ubuntu 20.04LTS를 다운받는다. https://ubuntu.com/ <br>


  
