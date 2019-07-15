Minikube 환경 설치
=====================

### 1. 사전 요구 사항
Intel VT-x 또는 AMD AMD-v 활성화 및 지원 여부 확인

#### Linux
> egrep --color 'vmx|svm' /proc/cpuinfo

#### macOS
> sysctl -a | grep machdep.cpu.features | grep VMX

#### Windows
> systeminfo  

다음과 같은 출력이 확인되어야 함  

>> Hyper-V Requirements:  
>> &nbsp;&nbsp;&nbsp;&nbsp;VM Monitor Mode Extensions: Yes  
>> &nbsp;&nbsp;&nbsp;&nbsp;Virtualization Enabled In Firmware: Yes  
>> &nbsp;&nbsp;&nbsp;&nbsp;Second Level Address Translation: Yes  
>> &nbsp;&nbsp;&nbsp;&nbsp;Data Execution Prevention Available: Yes  

### 2. 지원되는 하이파바이저

#### Linux
VirtualBox, KVM(권장)

#### macOS
VirtualBox, VMware Fusion, HyperKit(권장)

#### Windows
VirtualBox(권장), Hyper-V

### (옵션) 3. 패키지 관리자 설치

#### macOS - homebrew 설치
> /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

#### Windows - Chocolatey 설치
- cmd.exe 
> @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

- PowerShell.exe
> Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

### (옵션) 4. VirtualBox 설치

#### 수동 설치
https://www.virtualbox.org/wiki/Downloads

#### Linux
https://www.virtualbox.org/wiki/Linux_Downloads

#### macOS
> brew cask install virtualbox virtualbox-extension-pack

#### Windows
> choco install virtualbox virtualbox.extensionpack

### 5. minikube 설치

#### Linux
> curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube
> sudo cp minikube /usr/local/bin && rm minikube

#### macOS
> brew cask install minikube
> brew install kubernetes-cli docker

또는

> curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64 && chmod +x minikube
> sudo mv minikube /usr/local/bin

#### Windows
> choco install minikube kubernetes-cli docker

또는

[minikube-installer.exe](https://github.com/kubernetes/minikube/releases/latest)

### 6. minikube 실행

#### minikube 최초 실행
> minikube start --cpus 2 --memory 2048 --disk-size 20g --vm-driver virtualbox -p minikube

[실습내용추가]

minikube start --memory 4096

minikube docker-env

@FOR /f "tokens=*" %i IN ('minikube docker-env') DO @%i



--cpus: CPU 개수 (기본 2)  
--memory: 메모리 크기 (기본 2048)  
--disk-size: 디스크 크기 (기본 20g)  
--vm-driver: virtualbox parallels vmwarefusion kvm xhyve hyperv hyperkit kvm2 vmware none (기본 virtualbox)  
-p: 프로파일(K8s 클러스터 이름) (기본 minikube)  

#### minikube 중지
> minikube stop

#### minikube 실행
> minikube start

#### minikube 삭제
> minikube delete (-p \<프로파일\>)

#### minikube 구성 파일 초기화
> rm -rf ~/.minikube

### (옵션) 7. Virtual Studio Code (Text Editor)
[VSCODE](https://code.visualstudio.com)

#### macOS
> brew cask install visual-studio-code

#### Windows
> choco install vscode
