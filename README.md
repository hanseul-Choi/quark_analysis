# Quark

An Obfuscation-Neglect Android Malware Scoring System <br>
(난독화를 무시하는 악성 코드 점수 채점 시스템)

<br>

## 목차

### Background
  
1. [난독화](#난독화)

### Quark

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
역공학을 하는 것이 악의적인 목적도 있지만 선의적인 목적도 가질 수 있다. 애초에 악의적으로 만든 앱을 배포할 경우, 악성 앱 탐지 프로그램에서는 역공학을 통해 소스코드를 분석해 악의적인 목적을 가지는지 확인하여 악성앱을 판단한다. Quark tool도 마찬가지이다. 디컴파일하여 소스코드를 읽는 과정에서 난독화가 이루어져 있으면, 소스코드 분석이 어려워 해당 앱이 악의적인 목적을 가지고 있는지 선의적인 목적을 가지고 있는지 확인하기가 어렵다. 그렇다면 Quark는 어떻게 난독화를 무시하는 것일까? 난독화 기술이 발전하면서, 난독화를 해독하는 deobfustation 기술도 늘어나고 있다.  deobfuscation tool을 이용함으로써 이를 어느정도 해결할 것으로 기대한다

* 난독화 이론 출처 : 코드 난독화를 이용한 악성 코드 분석 기법에 관한연구 (2005-11)

<br><br>

# Quark

## Installation
추천 운영체제는 devian linux이지만, 본 설치는 ubuntu linux를 통해 진행하였다. <br>

### vm install
먼저 가상머신인 VM 머신을 다운받는다. https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html
<br> 작성자는 vmware workstaion pro 16버전을 이용하였다. <br><br>

### ubuntu linux install
그 후, ubuntu linux 사이트에 접속하여 ubuntu 20.04LTS를 다운받는다. https://ubuntu.com/ <br>

<br>

![ubuntu](https://github.com/hanseul-Choi/quark_analysis/blob/main/img/ubuntu.PNG?raw=true)
우분투 접속화면
<br><br>

### docker install
docker는 CE 버전으로 다운받는다. (출처: https://docs.docker.com/engine/install/ubuntu/) <br>
<br>
우분투 터미널로 설치를 진행한다. <br>
먼저 apt를 update 해준다. <br>
* sudo는 관리자 명령으로 실행한다는 의미이다.
* terminal여는 단축키는 ctrl + alt + t이다.
* 해당 코드를 ctrl + c로 복사하고 terminal에서는 shift + insert를 통해 붙여넣기가 가능하다.

<pre>
<code>
sudo apt-get update
</code>
</pre>

docker를 설치하기 위한 라이브러리들을 install한다. <br>

<pre>
<code>
sudo apt-get install \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg \
     lsb-release
</code>
</pre>

gpg를 등록하는데, 여기서 gpg는 암호화진행할 때 사용되는 키이다. <br>

<pre>
<code>
url -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
</code>
</pre>

docker repository를 추가해준다.<br>

<pre>
<code>
echo \
   "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
</code>
</pre>

한번더 update를 진행하고, <br>

<pre>
<code>
sudo apt-get update
</code>
</pre>

docker ce를 설치한다. <br>

<pre>
<code>
sudo apt-get install -y docker-ce
</code>
</pre>

마지막으로 docker의 설치여부를 확인하기 위해 hello-world를 run 시킨다. <br>

<pre>
<code>
sudo docker run hello-world
</code>
</pre>

<br>
다음과 같이 나온다면 정상적인 설치가 완료된 것이다. 
<br><br>

![hello-world](https://github.com/hanseul-Choi/quark_analysis/blob/main/img/docker_hello_world.PNG?raw=true)
<br>docker hello-world 실행
<br><br>

### quark installation and execution with terminal
먼저 quark의 실행환경을 위해 jre와 jdk를 설치한다.<br>

<pre>
<code>
sudo apt-get install openjdk-8-jre
sudo apt-get install openjdk-8-jdk
</code>
</pre>

그 후 pip를 통해 quark를 설치하기위해 pip를 설치하고 quark engine을 설치한다.<br>

<pre>
<code>
sudo apt install python3-pip
pip3 install -U quark-engine
</code>
</pre>

이제 quark를 git code에서 받아온다. <br>

<pre>
<code>
git clone https://github.com/quark-engine/quark-engine.git
</code>
</pre>

pipenv shell을 설치하기 위해 pipenv와 --skip-lock을 설치한다.<br>

<pre>
<code>
sudo apt install pipenv
pipenv install --skip-lock
</code>
</pre>

Terminal 환경에서 quark를 실행할 수 있다. <br>

<pre>
<code>
pipenv shell
quark --help
</code>
</pre>

다음과 같은 화면이 나온다면 quark가 정상적으로 설치된 것이다. <br>

![terminal_quark](https://github.com/hanseul-Choi/quark_analysis/blob/main/img/terminal_quark.PNG?raw=true)

<br><br>

### quark installation and execution with docker

docker에서는 docker환경에서 설치하면 실행이 가능하다. <br>

<pre>
<code>
sudo docker build . -t quark
</code>
</pre>

다음과 같이 quark 정상 설치 여부를 확인할 수 있다. <br>
* 여기서 ${pwd}는 자신의 우분투 password를 넣으면 된다.

<pre>
<code>
sudo docker run -v $(pwd):/tmp -it quark bash
cd /tmp
quark -a Ahmyth.apk -s
</code>
</pre>

다음과 같은 화면이 나오면 정상적으로 quark가 설치된 것이다. <br>

![docker_quark](https://github.com/hanseul-Choi/quark_analysis/blob/main/img/docker_quark.png?raw=true)
