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
source-git-commit: a3cf926bde4a4b3a0810058e84ac01012a4a3a57
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 3%

---

# 디자이너 설치 및 구성{#installing-and-configuring-designer}

## 전제 조건 {#pre-requisites}

AEM Forms Designer 설치 프로그램에는 32비트 버전의 가 필요합니다 [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-us/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0) 및 [Visual C++ redistributable runtime package 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). 설치를 시작하기 전에 이전에 언급된 재배포 가능 런타임 패키지가 설치되어 있는지 확인하십시오.

디자이너를 설치하거나 제거하려면 관리자 권한이 필요합니다.

## Designer 설치 {#install-designer}

디자이너는 독립 실행형 설치 프로그램으로 사용할 수 있으며 WorkBench와 함께 번들로 제공됩니다. Designer용 독립형 설치 프로그램을 사용하는 경우 다음 단계를 수행하십시오.

1. Adobe에서 디자이너 다운로드 [라이선스 웹 사이트](https://licensing.adobe.com/).

   >[!NOTE]
   >
   >이전 버전의 Designer가 설치되어 있는 경우 계속하기 전에 이전 버전을 제거하십시오.

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


