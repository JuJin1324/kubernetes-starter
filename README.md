# kubernetes-starter

## Hypervisor
### Hypervisor 란?
> 가상화(Virtualization)는 실제 운영체제 위에 가상화 소프트웨어를 설치한 후에 소프트웨어를 통해 하드웨어(CPU, Memory, Disk, NIC 등)를 에뮬레이션한 후에 
> 이 위에 운영체제(Guest OS)를 설치하는 것을 의미합니다. 가상화를 해 주는 소프트웨어를 하이퍼바이저(Hypervisor) 라고 하며 종류로는 VirtualBox, 그리고 VMWare, Xen 등이 있습니다.  
> 참조사이트: [Vagrant 란](https://www.lesstif.com/laravelprog/vagrant-24445417.html)

## Vagrant
### Vagrant 란?
> 가상 머신에 운영체제를 설치하고 웹 서버, DBMS, PHP 를 설치하는 것은 개발 환경 구성 대상이 PC 에서 가상 머신으로 옮겨졌을 뿐이지 기존 작업과 
> 난이도 측면에서 차이가 없으며 오히려 가상 머신을 설치하고 관리해야 하는 부담이 더 늘었습니다.  
> Vagrant 는 이런 문제를 해결하기 위한 솔루션으로 설정 스크립트를 기반으로 특정 환경의 가상 머신을 만들어서 신속하게 개발 환경을 구축하고 공유할 수 있게 만들어진 솔루션입니다.  

### 설치
> 설치: `brew install vagrant`  
> 확인: `vagrant --version`  

## VirtualBox
### 설치
> 설치: [Download VirtualBox](https://www.virtualbox.org/wiki/Downloads)  
> Apple M1(ARM) 의 경우 brew 에서 VirtualBox 를 설치할 수 없고 다운로드 페이지를 통해서 Developer preview 를 다운받는다.(2022-11-18 기준)  

## Kubernetes
### 노드(Node)
> 쿠버네티스 리소스 중에서 가장 큰 개념은 노드(node)이다. 
> 노드는 클러스터의 관리 대상으로 등록된 도커 호스트로, 도커 컨테이너가 배치되는 대상이다.   
> 그리고 쿠버네티스 클러스터 전체를 관리하는 서버인 마스터가 적어도 하나 이상 있어야한다. 
> 여기서 하나 이상이라는 말은 클러스터가 작동하기 위한 최소 조건이지만 실제 프러덕 환경에서는 절대 하나로 클러스터를 구성하지 않는다. 
> 최소 3개 이상의 마스터 노드를 갖는 것이 좋다.  

### 파드(Pod)
> 파드는 컨테이너가 모인 집합체의 단위로, 적어도 하나 이상의 컨테이너로 이루어진다. 여기서 말하는 컨테이너는 도커 컨테이너를 이야기한다. 
> 쿠버네티스를 도커와 함께 사용한다면 파드는 컨테이너 하나 혹은 컨테이너의 집합체가 된다.  
> 쿠버네티스에서는 결합이 강한 컨테이너를 파드로 묶어 일괄 배포한다.(ex spring web app + nginx)  
> 한 팟 안의 컨테이너는 모두 같은 노드에 배치된다. 다시 말해, 팟 하나가 여러 노드에 걸쳐 배치될 수는 없다.  
> 그렇다면 가장 먼저 고민되는 부분은 '팟의 적절한 크기는 어느 정도인가'가 될 것이다. 보통 리버스 프록시 역할을 할 Nginx와 그 뒤에 위치할 
> 애플리케이션 컨테이너를 함께 팟으로 묶는 구성이 일반적이다. 또한 예거와 같은 로그와 관련된 서버는 애플리케이션 컨테이너의 사이드카로 많이 팟을 구성한다.  

### 매니페스트(Manifest) 파일
> 파드 생성은 kubectl 만 사용해도 가능하지만, 버전 관리 관점에서도 yaml 파일로 정의하는 것이 좋다. 
> 쿠버네티스의 여러 가지 리소스를 정의하는 파일을 매니페스트 파일이라고 한다.

### 레플리카셋(ReplicaSet)
> 파드를 정의한 매니페스트 파일로는 파드를 하나밖에 생성할 수 없다. 
> 그러나 어느 정도 규모가 되는 애플리케이션을 구축하려면 같은 파드를 여러 개 실행해 가용성을 확보해야 하는 경우가 생긴다. 
> 이런 경우 사용하는 것이 레플리카세트이다.   
> 레플리카세트는 똑같은 정의를 갖는 파드 여러개를 생성하고 관리하기 위한 리소스이다.

### 디플로이먼트(Deployment)
> 레플리카셋보다 상위에 해당하는 리소스로 디플로이먼트가 있다. 보통 디플로이먼트가 애플리케이션 배포의 기본 단위가 되는 리소스이다. 
> 레플리카셋은 똑같은 팟의 레플리카를 관리 및 제어하는 리소스인데 반해, 디플로이먼트는 레플리카셋을 관리하고 다루기 위한 리소스이다.

### 참조사이트
> [Kubernetes - Kubernetes란? (클러스터,노드,파드(pod), 리플리카셋, 디플로이먼트)](https://coding-start.tistory.com/308)
