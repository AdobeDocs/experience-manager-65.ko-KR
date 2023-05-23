---
title: Designer 설치 및 구성
seo-title: Installing and configuring Designer
description: 디자이너는 독립 실행형 설치 관리자로 사용할 수 있으며 Workbench와 함께 번들로 제공됩니다. 독립형 Designer를 설치하는 방법에 대해 알아봅니다.
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
source-git-commit: 1b2d743f8f2172c4e4663917d598734cb1ea1ea4
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Designer 설치 및 구성{#installing-and-configuring-designer}

## 전제 조건 {#pre-requisites}

* 32비트 버전 설치  [Visual C++ 2019 재배포 가능 패키지(x86)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). 설치를 시작하기 전에 앞에서 언급한 재배포 가능 런타임 패키지가 설치되어 있는지 확인하십시오.
* AEM Forms Designer를 설치 또는 제거할 수 있는 관리자 권한이 있는 사용자입니다.

## AEM Forms Designer 설치 {#install-designer}

디자이너는 독립 실행형 설치 프로그램으로 사용할 수 있으며 WorkBench와 번들로 제공됩니다. AEM Forms Designer용 독립형 설치 프로그램을 사용하는 경우 다음 단계를 수행하십시오.

1. 이전 버전의 AEM Forms Designer가 이미 설치되어 있는 경우 제거합니다.
1. 에서 Designer 다운로드 [Adobe 라이선스 웹 사이트](https://licensing.adobe.com/).

   >[!NOTE]
   >
   > * Adobe Experience Manager 6.5 Forms 서비스 팩 15(6.5.15.0) 이상 Forms Designer 버전에는 서비스 팩 버전도 포함되어 있습니다. 예를 들어 서비스 팩 15의 경우 버전 번호는 6.5.15.20221112.1.0입니다. 이 예에서 6.5.15는 서비스 팩 버전입니다.


1. setup.exe를 두 번 클릭하여 AEM Forms Designer 설치 관리자를 실행합니다.
1. 계속 진행하여 개인화 화면에 세부 정보와 일련 번호를 입력합니다.
1. 사용권 계약에 동의하면 다음 을 클릭하여 계속 진행하십시오.
1. (선택 사항) 원하는 위치에 Designer를 설치하려면 기본 설치 경로를 변경합니다. 다음을 클릭합니다.
1. 환경 설정을 변경하려면 [뒤로]를 클릭하십시오. Designer를 설치하려면 설치를 클릭합니다.
1. 설치가 완료되면 마침 을 클릭합니다.

또는 수동 또는 자동 모드를 사용하여 명령줄을 통해 AEM Forms Designer를 설치할 수 있습니다.

* 수동 명령줄 설치: 설치가 진행 중임을 나타내는 진행률 표시줄이 표시되지만 프롬프트 또는 오류 메시지는 표시되지 않습니다. 시작한 후에는 설치를 취소할 수 없습니다.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* 자동 명령줄 설치: 설치 프로그램은 사용자 인터페이스를 표시하지 않고 설치를 실행합니다. 프롬프트, 메시지 또는 대화 상자가 표시되지 않습니다. 시작한 후에는 설치를 취소할 수 없습니다.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## AEM Forms Designer 업데이트 {#update-forms-designer}

AEM Forms Designer 6.5.16.0의 최신 버전을 업데이트하는 동안 두 가지 경우가 있습니다.

* **사례 1**: 사용자의 AEM Forms Designer 버전이 6.5.15.0 이전인 경우.
* **사례 2**: 사용자에게 6.5.15.0 AEM Forms Designer 버전이 있는 경우.

+++**사용자의 AEM Forms Designer 버전이 6.5.15.0 이전인 경우.**

AEM Forms Designer용 독립형 설치 프로그램을 사용하는 경우 다음 단계를 수행하십시오.

1. 설치 전 **AEM Forms Designer 6.5.16.0**, 사용자는 이전 버전을 모두 제거해야 합니다.
1. 다운로드 및 설치 [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) AEM 양식 릴리스 페이지에서 참조할 수 있습니다.
1. 의 성공적인 설치 후 **AEM Forms Designer 6.5.15.0**, 다운로드 및 설치 [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 다운로드한 설치 관리자 파일을 두 번 클릭하여

+++

+++**사용자에게 6.5.15.0 AEM Forms Designer 버전이 있는 경우**

AEM Forms Designer용 독립형 설치 프로그램을 사용하는 경우 다음 단계를 수행하십시오.
1. 에서 최신 버전의 AEM Forms Designer 다운로드 [소프트웨어 배포 포털](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. 다운로드한 설치 관리자 파일을 두 번 클릭하여 최신 버전의 AEM Forms Designer를 설치합니다.

+++