# Python Environment Setup
Miniconda로python 가상 환경 설치 방법에 대해 다룬다.
# 설치 사양
## OS
* **LINUX**: UBUNTU 18.04 LTS, 20.04 LTS
* **MacOS**: Mojave version 10.14 이상

> **주의:**
> MacOS는 CPU 모드만 지원한다.

# Miniconda 설치
> **참고:**
> 본 문서는 miniconda를 이용하여 python을 설치하는 방법에 대해 다룬다.
> miniconda는 설치가 간편하며 작고 가볍다. pip 패키지 관리자와도 궁합이 잘 맞아 쉽게 혼용할 수 있는 장점이 있다.
> 본 문서는 모든 명령어를 터미널에서 실행한다.

miniconda installer를 다운로드 받는다.
```shell
$ curl -o miniconda.sh \
https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```
> **참고:**
> Python 3.xx가 기본 사양 버전이므로 반드시 Miniconda3를 다운로드 받아야 한다. 그외에는 항상 최신 버전(`latest`)을 받으면 된다. 실제 사용하는 python의 버전은 miniconda가 생성한 환경(environemnt)과 관련 있고 miniconda와 관련 없다.

다운로드 받은 파일의 이름은 `miniconda.sh`이다. 파일 실행 속성을 활성화하고 수행한다.
```shell
$ chmod +x miniconda.sh
$ ./miniconda.sh         # ./을 생략하면 실행되지 않는다.
```
인스톨러 실행 후 화면에 나오는 질문 아래와 같이 적절히 답변을 하면 설치가 진행된다.
* `Review license agreement`에 대해 엔터를 누르고 `q`를 누르면 `Do you accept the license terms?`라는 질문을 하는데 `yes`라고 입력한다.
* 홈 디렉토리 밑에 설치할지 여부를 묻는데 엔터를 누르면 기본 설정이 선택된다.
* `conda init`을 수행할지 여부를 묻는데 `yes`를 입력한다.

```shell
$ ./miniconda.sh
(base) $
```
설치가 완료되면 쉘 프롬프트 맨 앞에 `(base)`가 붙어 있음을 확인할 수 있다. `base`는 `miniconda`의 default environment이다.  
사용자 environment를 생성한다. `-n`은 environment의 이름이고 `python=`은 environment에 설치될 python 버전이다. Python 버전은 반드시 2.XX가 아닌 3.XX를 설치해야 한다.
> **참조:**
> Python 버전은 [여기](https://www.python.org/doc/versions/)에서 확인할 수 있다.
```shell
(base) $ conda create -n omg python=3.9
```

> **참조:**
> `base` environment에 패키지를 설치하지 않도록 한다. 대신 직접 생성한 environment에 패키지를 설치한다. 위의 경우 python 3.9 버전의 `omg`라는 environment가 생성되었다. 이처럼 사용자는 다수 개의 environment를 만들 수 있으며 environment마다 서로 다른 버전의 python과 패키지를 설치할 수 있다.
# Miniconda Commands
## conda env list
현재 생성된 모든 environment의 리스트를 출력한다.
```shell
$ conda env list
```
```shell
# conda environments:
#
base                  *  /home/hmyang/miniconda3
omg                      /home/hmyang/miniconda3/envs/omg
```
> **참조:**
> `base`와 `omg`는 각각 environment의 이름이다.  
> Environment마다 경로가 도시되어 있다.  
> 예를 들어 `omg`의 경로는 `/home/hmyang/miniconda3/envs/omg`이다. Environment별로 이 경로 아래 python 패키지가 설치된다.  
> `*`는 현재 활성화된 environment를 나타낸다.
## conda activate *env*
디렉토리 변경의 개념처럼 현재 environment를 변경한다.
```shell
(base) $ conda activate omg

(omg) $ which python
  /home/hmyang/miniconda3/envs/omg/bin/python

(omg) $ conda activate base

(base) $ which python
  /home/hmyang/miniconda3/bin/python
```
## conda deactivate
현재 environment가 `base`가 아닐 경우 `base`로 바꾼다.  
현재 environment가 `base`일 경우, `miniconda`에서 빠져 나간다. 
```shell
(omg) $ conda deactivate
(base) $ conda deactivate
```
## conda list
현재 environment에 설치된 python package 리스트를 출력한다.
```shell
(omg) $ conda list
```
## conda install *pkg*
현재 environment에 python package를 설치한다.
```shell
(omg) $ conda install numpy
```
## conda remove *pkg*
현재 environment에 설치된 python package를 제거한다.
```shell
(omg) $ conda remove numpy
```
# 터미널 수행 시 자동으로 환경 선택
쉘 초기화 파일에 입력하여 처음 로그인하면 자동으로 환경이 설정되게 할 수 있다.
Mac OS일 경우 `~/.zshrc`, Linux일 경우 '~/.bashrc`를 편집한다.

```
$ vi ~/.zshrc # 또는 vi ~/.bashrc
```

파일 맨 끝에 아래 문장을 삽입한다. `omg`는 내가 만든 환경의 이름이다. `omg` 대신 자기가 만든 환경의 이름을 넣으면 된다.
```
conda activate omg 
```

아래 명령을 실행한다.
```
$ source ~/.zshrc # 또는 source ~/.bashrc
```

# Python Package 설치
`pip install` 명령어를 사용하여 설치할 수도 있으며 `conda install` 명령어를 사용하여 설치할 수도 있으나 `pip install`을 권장한다. `pip install`로 간혹가다 설치가 안 되는 경우에 `conda install`을 실행해 볼 수도 있다.

모든 python package는 `pip` 명령어가 인식할 수 있는 고유의 이름이 있다. 이 고유의 이름을 잘 찾기만 하면 그후 package 설치는 쉽다. 대부분의 경우 고유 이름은 `import` 문의 package명과 일치하나 다를 경우도 있다. 이 경우 고유 이름을 찾을 수 없으면 구글링을 하거나 ChatGPT에게 물어본다.
```
(omg) $ pip install pandas    # pandas package를 설치한다
(omg) $ pip remove pandas    # pandas package를 제거한다
(omg) $ pip list  # 설치된 모든 package를 리스트로 보여준다
(omg) $ pip list | grep pandas  # pandas package가 설치되었는지 확인한다
```
