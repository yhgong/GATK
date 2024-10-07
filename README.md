![image](https://github.com/user-attachments/assets/47b4f470-5131-4ed5-8cd2-dd9174658443)# 카카오클라우드 VM 생성

## 1. kakaocloud 콘솔 로그인
![image](https://github.com/user-attachments/assets/58d15e7c-d0eb-4b02-b4c3-547ab0cd70a3)

## 2. Virtual Machine 에 인스턴스 선택
![image](https://github.com/user-attachments/assets/5623ee90-d57c-4e40-ba9a-4c9cfdac8b2a)

## 3. 인스턴스 생성
#### 1. 인스턴스 생성 버튼 클릭
![image](https://github.com/user-attachments/assets/ee570e6b-9045-4844-b6ef-cd53e0ca5587)
--
#### 2. 서버명 입력 : lab-svr
![image](https://github.com/user-attachments/assets/2c4f6e72-b282-4686-b5f1-4eb32f39add0)
---
#### 3. 이미지 선택 : Rocky_linux 9.4
![image](https://github.com/user-attachments/assets/deb41818-e72e-460a-82d0-5f8fc5cf7806)
---
#### 4. 인스턴스 유형 : 컴퓨팅 최적화 , c2a.xlarge
![image](https://github.com/user-attachments/assets/fcfbf0e7-cbce-4748-a8c4-6dfeebd49693)
---
#### 5. 루트 볼륨 : 100GB

![image](https://github.com/user-attachments/assets/8a707b8d-6a65-47b5-870f-7433f396c03c)
---
#### 6. 키페어 : 앞 시간에 생성한 키페어 선택
![image](https://github.com/user-attachments/assets/3a7aeaf6-0d93-45a4-8dfc-34b11df5b2d3)
---
#### 7. 네트워크

![image](https://github.com/user-attachments/assets/abeb2c6a-0197-49b1-80e4-35bfbe47f8e2)

- VPC : 앞전 실습에서 생성한 VPC 선택
- 서브넷 : main 서브넷 선택
- 보안그룹 : 아래와 같이 포트 오픈
  - 출발지 : www.naver.com 에서 "내 아이피 주소 확인" 으로 확인
  ![image](https://github.com/user-attachments/assets/9850df61-c501-4cc6-95ea-f9df88af79da)


![image](https://github.com/user-attachments/assets/d340f3d1-9c52-42ac-9c93-4ad8d4042742)
![image](https://github.com/user-attachments/assets/aeccbbe0-bd7b-4de2-bb2b-eb7f259750a1)
---
#### 8. 생성 버튼 클릭

![image](https://github.com/user-attachments/assets/fd9d16e7-7480-4992-99b3-24fa6880c41e)
---
#### 9. 공인 IP 생성 : VPC -> 퍼블릭 IP 선택
![image](https://github.com/user-attachments/assets/34b712ca-bd77-4434-8bd8-76781d1f1bf9)
---
#### 10. "+ 퍼블릭 IP 생성" 클릭

![image](https://github.com/user-attachments/assets/9686dcec-ac50-499c-a9a3-311bc2772181)
---
#### 11. 퍼블릭 IP 설명에 내용 입력(옵션)후  "생성" 버튼 클릭
![image](https://github.com/user-attachments/assets/e7ff0c5d-00d0-4ac0-b997-eaffe9ee5e9a)
---

#### 12. 퍼블릭 IP 서버 연결 : 리소스 연결 선택
![image](https://github.com/user-attachments/assets/c311e2e6-5f04-4fba-9e77-1264609833a6)
---

#### 13. 리소스 선택 : 앞에서 생성한 서버 선택 후 "저장" 버튼 클릭
![image](https://github.com/user-attachments/assets/5190b2ef-68d5-4af7-9c81-f169e5f44e9b)
---

<br>

# 주피터랩 설치 및 conda GATK3 연동

## 1. System Update
패키지 업그레이드를 강제로 실행하면서 기존 의존성 문제를 무시하고 최신 버전으로 업데이트하는 옵션입니다.

sudo는 관리자 권한을 일시적으로 얻어 명령어를 실행하는 데 사용되는 유닉스 계열 운영체제에서의 명령어입니다. 주로 시스템 관리나 보안 관련 작업을 수행할 때 사용됩니다.
```
sudo dnf -y upgrade –refresh
```
시간대를 미국에서 한국으로 변경
```
sudo timedatectl
```
![image](https://github.com/user-attachments/assets/b12064be-9e70-4bc5-962e-90a3016d22e1)
```
sudo timedatectl set-timezone Asia/Seoul
```
![image](https://github.com/user-attachments/assets/ca40206a-2226-42c0-8518-724267d2700f)

#### 기본 repository 확인

```
sudo dnf repolist
```
Linux에서 Repository는 프로그램을 다운로드하고 설치 할 수 있는 저장소 입니다.

![image](https://github.com/user-attachments/assets/c4232c04-1c3d-4b52-8d9b-20ae314dd186)

위와 같이 기본적으로는 3개의 저장소가 활성화 되어 제공 됩니다. 제공되는 3개의 저장소에서 필요한 프로그램이 설치 되지 않을 수 있어 다음과 같이 저장소를 활성화 하거나 추가 합니다.

#### 모든 repository 확인

```
sudo dnf repolist all
```
![image](https://github.com/user-attachments/assets/03e68906-30c3-40b7-a7f1-ad2a68e3ce5d)


#### dnf config-manager 명령어는 CentOS Linux 8 이상 버전에서 제공되는 DNF(Dandified Yum) 패키지 매니저에서 사용되는 명령어이며 crb 패키지가 활성화되고, 
#### 이후 dnf update 또는 dnf upgrade 명령을 실행하면 crb 패키지가 설치됩니다.
```
sudo dnf config-manager --set-enabled crb
```
추가된 crb 레파지토리 확인
```
sudo dnf repolist
```
![image](https://github.com/user-attachments/assets/8cf154ba-3f50-4633-97ab-fdf4ef768bed)

![image](https://github.com/user-attachments/assets/3814184e-1ae3-401a-b5c8-be82fbfaca64)

#### RPM 추가 epel-next-release, epel-release
RPM(Red Hat Package Manager)은 레드햇 리눅스 계열 운영체제에서 사용되는 패키지 관리 도구입니다. 
RPM은 소프트웨어 패키지를 설치, 삭제, 업그레이드 및 유지보수하는데 사용됩니다.
```
sudo dnf -y install \
    https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm \
    https://dl.fedoraproject.org/pub/epel/epel-next-release-latest-9.noarch.rpm
```
#### noarch : 아키텍처 무관, CPU가 인텔이건 AMD건 관계 없이 설치 가능하다는 의미

추가된 레파지토리 확인
```
sudo dnf repolist
```
![image](https://github.com/user-attachments/assets/ced4eebf-2c39-4b83-8da7-7afe94ef4d96)

![image](https://github.com/user-attachments/assets/165b69a5-0568-4de1-81b4-688f479d5e47)

#### dnf -y update 명령은
- 기존에 설치된 패키지들의 최신 버전을 확인하고, 필요한 경우 최신 버전으로 업데이트합니다.
- 패키지 목록 데이터베이스를 갱신하여 최신 상태로 유지합니다.
1. dnf는 먼저 패키지 목록 데이터베이스를 조회하여 현재 설치된 패키지들의 최신 버전을 확인합니다.
2. 만약 최신 버전이 이미 설치되어 있다면 아무 작업도 하지 않고 종료됩니다.
3. 그렇지 않은 경우, 최신 버전의 패키지를 다운로드하고 설치합니다.
4. 이 과정에서 일부 패키지는 의존성 문제로 인해 설치되지 않을 수도 있습니다.
```
sudo dnf -y update
```

## 2. System Extension Install
wget, git-lfs net-tools 설치
```
sudo dnf -y install wget git-lfs net-tools
```
<br>

Development Tools 설치 -- 필요시 소스코드등을 컴파일 할때 필요..
```
sudo dnf -y groupinstall 'Development Tools'
```
위 명령어는 "개발 도구" 그룹에 속하는 모든 패키지를 자동으로 설치합니다.
설치 후에는 해당 패키지들을 사용하여 다양한 프로그래밍 작업을 수행할 수 있습니다. 예를 들어, Python, Java, C/C++, Go 등의 언어를 사용하여 프로그램을 개발할 수 있습니다. 또한, 디버깅 도구, 테스트 도구, 라이브러리 등도 함께 설치되므로 개발 작업을 더욱 효율적으로 수행할 수 있습니다. 그룹 패키지를 설치하면 여러 개의 개별 패키지를 일일이 설치하는 것보다 빠르고 간편합니다.

## 3. Environment-modules 설치
```
sudo yum -y install environment-modules
```

## 4. java 설치
```
sudo dnf -y install java-11-openjdk-devel java-17-openjdk-devel
```

## 5. miniconda 설치
```
sudo mkdir -p /opt/miniconda3
```
```
sudo chown -R 1000:1000 /opt/miniconda3
```
```
sudo chown -R rocky:rocky /opt/miniconda3
```
```
sudo wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /opt/miniconda3/miniconda.sh
```
```
sudo bash /opt/miniconda3/miniconda.sh -b -u -p /opt/miniconda3
```
```
sudo rm -rf /opt/miniconda3/miniconda.sh
```
```
/opt/miniconda3/bin/conda init bash
```
쉘을 빠져나왔다가 다시 들어가면 설치된 콘다 (base)환경으로 접속됩니다.


## 6. micromamba 설치
```
"${SHELL}" <(curl -L micro.mamba.pm/install.sh)
```
![image](https://github.com/user-attachments/assets/6d0c1b46-d96f-4ef8-bfb0-102462fe52f9)

base 콘다 환경에 micromamba 환경을 설치 합니다.

## 7. jupyterlab 설치
```
conda install -y jupyterlab
```
설치 명령 이후 아래와 같이 쓰기 권한이 없다는 메시지가 나오면
![image](https://github.com/user-attachments/assets/ceae5328-9c79-47a5-affe-aac14a3a110b)

아래 명령을 다시 한번 수행 후,
```
sudo chown -R rocky:rocky /opt/miniconda3
```
주피터랩 설치 명령을 한번 더 수행
```
conda install -y jupyterlab
```
아래와 같이 모든 과정이 "done"으로 표기 되면 설치 완료!!!
![image](https://github.com/user-attachments/assets/3adb1315-15bc-400e-945f-a2d317755077)

## 8. 데이터시각화 라이브러리 bokeh extension 설치
```
conda install -y jupyter_bokeh
```
아래와 같이 모든 과정이 "done"으로 표기 되면 설치 완료!!!
![image](https://github.com/user-attachments/assets/b19891ef-6e90-4015-a578-a8eb6b796c08)

## 9. 아나콘다와 주피터랩의 가상환경을 연결해 주는 nb_conda_kernel 설치
```
conda install nb_conda_kernels
```
아래처럼 나오면 정상 설치!!!
![image](https://github.com/user-attachments/assets/1d479fad-257b-480e-a039-b09d0ce347bb)

## 10. 주피터랩 실행 확인
```
jupyter lab --ip=0.0.0.0 --port=8888 --allow-root --no-browser
```
- 옵션설명
  1. --ip=0.0.0.0 : 접근하는 모든 IP에 대해서 접속을 허용. 
  2. --port=8888 : 8888번 포트로 들어 오는 서비스만 허용
  3. --allow-root : root 권한을 가지고 실행 (윈도우에 관리자 권한으로 실행과 유사)
  4. --no--browser : 브라우저를 띄우지 마라
     
![image](https://github.com/user-attachments/assets/f4ae0f8b-155a-40b7-bef4-58b9e19a5835)

## 11.포트에 대한 개념과 방화벽에 대하 개념 설명 PPT로 설명

![image](https://github.com/user-attachments/assets/ece4e3f6-e754-4edb-bc19-712c788a883e)

## 12. GATK conda 설치
(base) 환경에서 설치 <br>
![image](https://github.com/user-attachments/assets/9727ac36-30a6-46a9-b0e1-4c101aa28775)
```
conda create -y -n gatk python=2.7
```
![image](https://github.com/user-attachments/assets/aa3d417c-ed92-44cc-b28b-8c22791b7592)

gatk 가상환경으로 진입
```
conda activate gatk
```
![image](https://github.com/user-attachments/assets/9eeb679b-6b13-4de0-8082-d79e838309cb)

gatk 모듈 설치
```
conda install -y bioconda::gatk
```
정상 설치 확인!!!
```
gatk3
```
![image](https://github.com/user-attachments/assets/3668a0d8-1fc8-4049-ba11-3d983aa70121)

주피터랩과 gatk 환경 연동
```
conda install -y ipykernel
```
주피터랩 연동 확인
1. (base) 환경에서 주피터랩 실행   
2. gatk 가상환경 아이콘 확인 <br>
![image](https://github.com/user-attachments/assets/5a6735dc-59d0-479a-85f7-94e3243c7fa3)
3. gatk3 명령어 실행 확인 주피터랩에서 외부명령 실행시 명령어 앞에 "느낌표" + 실행하고자하는 명령어 ! <br>
```
!gatk3
```
![image](https://github.com/user-attachments/assets/bd1e779c-fb6e-4703-81dd-46dcae34711b)

# Galaxy 설치
## 1.SSH 서버 접속 및 위치 확인

![image](https://github.com/user-attachments/assets/18b2480a-b6b6-4818-8716-4ec4260f6cea)

(base) 가상환경 확인

![image](https://github.com/user-attachments/assets/05f59f13-1eff-441a-94d8-b48c9c95b789)

(base) 디렉토리 위치 확인 <br>
```
pwd
```
![image](https://github.com/user-attachments/assets/d9c9a7a9-fcf1-4083-be9c-a52cf463072d)

## 2.소스 다운로드
```
git clone https://github.com/galaxyproject/galaxy.git
```
## 3.다운받은 디렉토리로 이동
```
cd ./galaxy
```

## 4.소스 Update
```
git fetch origin && git checkout release_24.1 && git pull --ff-only origin release_24.1
```

## 5.설치
```
sh run.sh
```

# 외부에서 galaxy 접속을 위한 설정
최초에 galaxy를 설치하면 내부에서만 접속이 가능한 상태로 실행이 됩니다.

![image](https://github.com/user-attachments/assets/1416d4e5-38bd-4872-923e-4d4aff207792)

여기에서 Serving on http://127.0.0.1:8080 이 부분을 외부에서 접속이 가능하도록 0.0.0.0:8080 으로 변경합니다.
## 1.서비스 종료
control + c 를 이용하여 갤럭시 웹서비스를 종료 합니다.

## 2.config 변경을 위해 디렉토리 이동
```
cd /home/rocky/galaxy/config
```

## 3.원본 config 파일 복사
```
cp galaxy.yml.sample galaxy.yml
```

## 4.galaxy.yml 파일 수정
```
vi galaxy.yml
```

![image](https://github.com/user-attachments/assets/33ce4ab8-1997-42c7-88be-15f4481888e6)

## 5.galaxy.yml 파일 저장
gunicorn : 웹 서버로 부터 받은 요청을 웹 어플리케이션에 전달해 주는 역할을 함.

웹서버의 설정을 나자신에서 모든 서버의 요청을 받을 수 있도록 변경하는 작업임.

## 6.실행 디렉토리로 이동
```
cd ..
```

## 7.galaxy 다시 실행
```
sh run.sh
```

## 8. 0.0.0.0:8080 으로 서비스가 실행 되었는지 확인

![image](https://github.com/user-attachments/assets/66ac0e5b-57d9-4c94-a940-fc0a9cd1656e)


## 9.브라우저 접속 URL에 자신의 서버공인 IP를 입력 후 8080포트로 접속 확인
크롬등의 브라우저 창을 열고 주소란에 입력 http://210.109.54.95:8080

![image](https://github.com/user-attachments/assets/0e6c827a-337d-4432-bdc4-b01ea62e8490)

# Triodenovo 설치

## 1. 설치 위치
```
cd
```
```
pwd
```
![image](https://github.com/user-attachments/assets/9a4022d5-5c2e-4867-933b-3f36b221bf05)

## 2.파일 다운로드
```
wget --no-check-certificate https://genome.sph.umich.edu/w/images/f/f4/Triodenovo.0.06.tar.gz
```

## 3.파일 압축해제
```
tar -xzvf Triodenovo.0.06.tar.gz
```

## 4.다운로드 한 압축파일 삭제
```
rm -f Triodenovo.0.06.tar.gz
```

## 5.디렉토리 이동
```
cd ./triodenovo.0.06/base
```

## 6.Argument.h 파일 수정
- 변경 전
![image](https://github.com/user-attachments/assets/a1865a6c-4a33-467a-9195-037278aa351f)

```
sed -i '366 c\                 if (strcmp(argv[i+1], "") == 0) {' Argument.h
```
- 변경 후
![image](https://github.com/user-attachments/assets/9cd0be1d-98a0-4277-a7c7-05173f6fa3d3)

## 7.디렉토리 이동
```
cd ../core
```

## 8.Parameters.cpp 파일 수정
- 변경 전
  
![image](https://github.com/user-attachments/assets/1176a7a9-fb1f-49fd-aab8-f3122c9b344e)

```
sed -i '501s/bool/int/g' Parameters.cpp
```
- 변경 후
  
![image](https://github.com/user-attachments/assets/f9c3c9a3-e832-4831-8bc1-881a3e88e387)

## 9.디렉토리 이동
```
cd ..
```

## 10.make
make에 필요한 툴 설치
```
sudo dnf install bzip2-devel
```
```
make
```

## 11.결과 메시지 확인

![image](https://github.com/user-attachments/assets/34fdb5ef-b330-4d52-88cc-ff91d6ff2f26)

## 12.실행파일 확인

```
cd bin
```
```
./triodenovo
```

![image](https://github.com/user-attachments/assets/9c0b3312-ac2a-4341-8da5-78a0805c2a3c)

## 13.디렉토리 등록
```
echo 'export PATH=$PATH:/home/rocky/triodenovo.0.06/bin' >> ~/.bashrc
```
## 14.쉘 재기동
```
source ~/.bachrc
```



# AdmixTools 설치

## 1.설치 위치
```
cd
```
```
pwd
```

![image](https://github.com/user-attachments/assets/50c776f5-de4c-40f4-9506-0f90ab888c33)


## 2.소스 다운로드
```
wget https://github.com/DReichLab/AdmixTools/archive/refs/tags/v7.0.2.zip
```

## 3.컴파일에 필요한 툴 설치
```
sudo dnf install -y gsl-devel openblas-devel
```

## 4.파일 압축 해제
```
unzip v7.0.2.zip
```

## 5. 디렉토리 이동
```
cd ./AdmixTools-7.0.2/src
```

## 6.make
```
make clobber
```
```
make all
```
```
make install
```

## 7.압축파일 삭제
```
cd
```
```
rm -f v7.0.2.zip
```

## 8.프로그램 확인
```
cd AdmixTools-7.0.2/bin
```
```
ls -lrt
```
![image](https://github.com/user-attachments/assets/240bd318-7e73-410e-be8f-21d3a14cfdaa)

## 9.실행 디렉토리 등록
```
cd
```
```
echo 'export PATH=$PATH:/home/rocky/AdmixTools-7.0.2/bin' >> ~/.bashrc
```

# R 설치

## 1.가상환경 생성
```
conda create -y -n r_env python=3.10
```

## 2.가상환경 진입
```
conda activate r_env
```

## 3. R 설치
```
sudo dnf install -y R
```

## 4. RServer 설치
설치 파일 다운로드
```
wget https://download2.rstudio.org/server/rhel9/x86_64/rstudio-server-rhel-2024.09.0-375-x86_64.rpm
```
```
sudo yum install rstudio-server-rhel-2024.09.0-375-x86_64.rpm
```

## 5. SELinux 설정 및 rocky 비밀번호 생성

디렉토리 이동
```
cd /etc/selinux
```

config 파일 수정
```
sudo sed -i '22s/SELINUX=permissive/SELINUX=disabled/g' config
```

파일 수정 확인
```
cat config
```
![image](https://github.com/user-attachments/assets/673ecf76-eace-4186-9e5d-7d23c68c4c4a)


rocky 계정 비밀 번호 생성
```
sudo passwd rocky
```
원하는 비밀번호 입력 후 비밀번호 확인하여 등록

![image](https://github.com/user-attachments/assets/d133a5a7-8c0c-4107-aedf-fc93a5fc4d4b)


## 6. 서비스 포트 확인
```
sudo netstat -nltp
```

## 7. 서비스 접속

서버공인IP:8787
http://210.109.54.95:8787

![image](https://github.com/user-attachments/assets/d4f3536b-73c5-4163-a540-13678f2f3a97)

ID  : rocky

PWD : 위에서 지정한 비밀번호

![image](https://github.com/user-attachments/assets/99d90262-5b90-4a73-802e-38c3ba35fa93)



































