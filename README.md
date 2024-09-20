# 카카오클라우드 VM 생성
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


# GATK 연구환경 설정

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

#### dnf config-manager 명령어는 CentOS Linux 8 이상 버전에서 제공되는 DNF(Dandified Yum) 패키지 매니저에서 사용되는 명령어이며 crb 패키지가 활성화되고, 이후 dnf update 또는 dnf upgrade 명령을 실행하면 crb 패키지가 설치됩니다
```
sudo dnf config-manager --set-enabled crb
```
추가된 crb 레파지토리 확인
```
sudo dnf repolist
```
![image](https://github.com/user-attachments/assets/8cf154ba-3f50-4633-97ab-fdf4ef768bed)

#### RPM 추가 epel-next-release, epel-release
RPM(Red Hat Package Manager)은 레드햇 리눅스 계열 운영체제에서 사용되는 패키지 관리 도구입니다. RPM은 소프트웨어 패키지를 설치, 삭제, 업그레이드 및 유지보수하는데 사용됩니다.
```
sudo dnf -y install \
    https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm \
    https://dl.fedoraproject.org/pub/epel/epel-next-release-latest-9.noarch.rpm
```
추가된 레파지토리 확인
```
sudo dnf repolist
```
![image](https://github.com/user-attachments/assets/ced4eebf-2c39-4b83-8da7-7afe94ef4d96)

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
패키지 업그레이드를 강제로 실행하면서 기존 의존성 문제를 무시하고 최신 버전으로 업데이트하는 옵션입니다.


## Documentation for individual modules

Services | Documentation | Install Command
------------ | ------------- | -------------
*Server* | [**Server**](https://github.com/NaverCloudPlatform/ncloud-sdk-python/blob/master/lib/services/server/README.md) | pip install ncloud-server
*Loadbalancer* | [**Loadbalancer**](https://github.com/NaverCloudPlatform/ncloud-sdk-python/blob/master/lib/services/loadbalancer/README.md) | pip install ncloud-loadbalancer
*Autoscaling* | [**Autoscaling**](https://github.com/NaverCloudPlatform/ncloud-sdk-python/blob/master/lib/services/autoscaling/README.md) | pip install ncloud-autoscaling
*CDN* | [**CDN**](https://github.com/NaverCloudPlatform/ncloud-sdk-python/blob/master/lib/services/cdn/README.md) | pip install ncloud-cdn
*CloudDB* | [**CloudDB**](https://github.com/NaverCloudPlatform/ncloud-sdk-python/blob/master/lib/services/clouddb/README.md) | pip install ncloud-clouddb
*Server(VPC)* | [**Server(VPC)**](https://github.com/NaverCloudPlatform/ncloud-sdk-python/blob/master/lib/services/vserver/README.md) | pip install ncloud-vserver
*VPC* | [**VPC**](https://github.com/NaverCloudPlatform/ncloud-sdk-python/blob/master/lib/services/vpc/README.md) | pip install ncloud-vpc
*Nas(VPC)* | [**Nas(VPC)**](https://github.com/NaverCloudPlatform/ncloud-sdk-python/blob/master/lib/services/vnas/README.md) | pip install ncloud-vnas
*Autoscaling(VPC)* | [**Autoscaling(VPC)**](https://github.com/NaverCloudPlatform/ncloud-sdk-python/blob/master/lib/services/vautoscaling/README.md) | pip install ncloud-vautoscaling
*Loadbalancer(VPC)* | [**Loadbalancer(VPC)**](https://github.com/NaverCloudPlatform/ncloud-sdk-python/blob/master/lib/services/vloadbalancer/README.md) | pip install ncloud-vloadbalancer


### License

```
Copyright (c) 2021 NAVER Cloud Corp.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```
