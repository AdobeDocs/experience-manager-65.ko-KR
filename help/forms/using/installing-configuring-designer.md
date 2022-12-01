---
title: 디자이너 설치 및 구성
seo-title: Installing and configuring Designer
description: 디자이너는 독립형 설치 프로그램으로 사용할 수 있으며 Workbench와 함께 번들로 제공됩니다. 독립형 Designer 설치 방법을 알아봅니다.
seo-description: Designer is available as a stand-alone installer and is also bundled with Workbench. Learn how to install stand-alone Designer.
uuid: c5b779d1-cb6a-48f4-87d6-48464753e516
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f3a5b5ce-2262-4d5d-a8ae-d59a3a4229e7
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: 85189a4c35d1409690cbb93946369244e8848340
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# 디자이너 설치 및 구성{#installing-and-configuring-designer}

## 전제 조건 {#pre-requisites}

* 32비트 버전 설치  [Visual C++ 2019 재배포 가능(x86)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). 설치를 시작하기 전에 이전에 언급된 재배포 가능 런타임 패키지가 설치되어 있는지 확인하십시오.
* 디자이너를 설치 또는 제거할 관리자 권한이 있는 사용자입니다.

## Designer 설치 {#install-designer}

디자이너는 독립 실행형 설치 프로그램으로 사용할 수 있으며 WorkBench와 함께 번들로 제공됩니다. Designer용 독립형 설치 프로그램을 사용하는 경우 다음 단계를 수행하십시오.

1. 이전 버전의 AEM Forms Designer가 이미 설치되어 있으면 제거합니다.
1. 디자이너 다운로드 위치 [Adobe 라이선스 웹 사이트](https://licensing.adobe.com/).

   >[!NOTE]
   >
   > * Adobe Experience Manager 6.5 Forms 서비스 팩 15(6.5.15.0) 버전의 Forms Designer에도 서비스 팩 버전이 포함되어 있습니다. 예를 들어 서비스 팩 15의 경우 버전 번호는 6.5.15.20221112.1.0입니다. 이 예에서 6.5.15는 서비스 팩 버전입니다.


1. setup.exe를 두 번 클릭하여 Designer 설치 프로그램을 시작합니다.
1. 계속 진행하여 개인화 화면에서 세부 사항 및 일련 번호를 제공합니다.
1. 사용권 계약에 동의하면 다음 을 클릭하여 진행합니다.
1. (선택 사항) 원하는 위치에 디자이너를 설치하려면 기본 설치 경로를 변경합니다. 다음을 클릭합니다.
1. 환경 설정을 변경하려면 뒤로 를 클릭합니다. 디자이너를 설치하려면 [설치]를 클릭합니다.
1. 설치가 완료되면 마침 을 클릭합니다.

또는 수동 또는 자동 모드를 사용하여 명령줄을 통해 디자이너를 설치할 수 있습니다.

* 수동 명령줄 설치: 설치 관리자에 설치 진행 중이지만 프롬프트 또는 오류 메시지가 표시되지 않는 진행률 표시줄이 표시됩니다. 시작되면 설치를 취소할 수 없습니다.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* 자동 명령줄 설치: 설치 프로그램은 사용자 인터페이스를 표시하지 않고 설치를 실행합니다. 프롬프트, 메시지 또는 대화 상자가 표시되지 않습니다. 시작되면 설치를 취소할 수 없습니다.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```
