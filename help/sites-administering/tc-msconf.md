---
title: Microsoft Translator에 연결
seo-title: Connecting to Microsoft Translator
description: AEM을 Microsoft Translator에 연결하는 방법을 알아봅니다.
seo-description: Learn how to connect AEM to Microsoft Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 35%

---

# Microsoft Translator에 연결{#connecting-to-microsoft-translator}

AEM 페이지 컨텐츠, 커뮤니티 컨텐츠 또는 자산을 번역할 때 Microsoft 번역 계정을 사용할 Microsoft Translator 클라우드 서비스에 대한 구성을 만듭니다.

| 속성 | 설명 |
|---|---|
| 번역 레이블 | 번역 서비스의 표시 이름. |
| 번역 속성 | (선택 사항) 사용자 생성 콘텐츠의 경우, 번역된 텍스트 옆에 표시되는 속성 (예: `Translations by Microsoft`). |
| 작업 영역 ID | (선택 사항) 사용할 맞춤화된 Microsoft Translator 엔진의 ID. |
| 구독 키 | Microsoft Translator에 대한 Microsoft 구독 키. |

구성을 만든 다음에는 [생성된 구성을 활성화](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations)해야 합니다.

다음 절차에서는 터치에 적합한 UI를 사용하여 Microsoft 번역기 구성을 만듭니다.

1. 레일에서 도구 > Cloud Services 를 클릭하거나 탭합니다.
1. Microsoft Translator 영역에서 구성 표시 를 클릭하거나 탭합니다.
1. 사용 가능한 구성 옆에 있는 + 링크를 클릭합니다.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 구성의 제목을 입력합니다. 제목을 통해 클라우드 서비스 콘솔과 페이지 속성 드롭다운 목록에서 구성을 식별합니다. 기본 이름은 제목을 기반으로 합니다. 필요한 경우 구성을 저장하는 저장소 노드에 사용할 이름을 입력합니다. 저장소 노드의 경로인 상위 구성 속성에 기본값을 사용해야 합니다.
1. 만들기를 클릭합니다.
1. 대화 상자가 나타나면 속성에 대한 값을 입력한 다음 확인을 클릭합니다.

## 샘플 Microsoft Translator Cloud Service 구성 {#sample-microsoft-translator-cloud-service-configurations}

다음 Microsoft Translator 클라우드 서비스 구성이 Geometrixx 샘플과 함께 설치됩니다. 일부 샘플 구성에서는 월별 최대 20,000개의 무료 번역 문자를 허용하는 평가판 Microsoft 번역 계정을 사용합니다.

### Microsoft Translator 평가판 라이센스 {#microsoft-translator-trial-license}

Microsoft Translator 평가판 라이선스 구성은 Geometrixx Outdoors 샘플 패키지와 함께 설치되는 샘플 구성입니다. 이 구성에서는 매월 20,000개의 번역된 문자를 허용하는 무료 구독이 있는 Microsoft Translator 계정을 사용합니다.

### Microsoft Translator 평가판 라이센스 - Geometrixx-outdoors {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft Translator 평가판 라이센스 - Geometrixx-outdoors 구성은 Geometrixx Outdoors과 함께 설치되는 샘플 구성입니다. 이 구성에서는 Microsoft Translator 평가판 라이센스 구성과 동일한 무료 Microsoft Translator 계정을 사용합니다. 이 계정에는 매월 200,000개의 번역된 문자를 허용하는 무료 구독이 있습니다.

이 Microsoft Translator 구성은 Geometrixx Outdoors 샘플 사이트의 컨텐츠 유형에 사용하도록 최적화되었습니다.

### Microsoft Translator 체험판 라이선스 구성 업그레이드 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft Translation 구성 페이지는 프로덕션 시스템에 적합한 계정 구독을 얻기 위한 Microsoft 웹 사이트로 간편하게 이동할 수 있는 링크를 제공합니다.

1. 레일에서 도구 > 작업 > 클라우드 > Cloud Services 를 클릭하거나 탭합니다.
1. Microsoft Translator 영역에서 구성 표시 를 클릭하거나 탭한 다음, Microsoft Translator Trial License(Microsoft 번역 구성)를 클릭하거나 탭합니다.

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 구성 페이지에서 Upgrade Subscription 을 클릭합니다. 열려 있는 Microsoft 웹 페이지를 사용하여 계정을 구성합니다.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Microsoft Translator 엔진 맞춤화 {#customizing-your-microsoft-translator-engine}

Microsoft Translation 구성 페이지는 Microsoft Translator 엔진을 맞춤화하기 위한 Microsoft 웹 사이트로 간편하게 이동할 수 있는 링크를 제공합니다. ([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. 레일에서 도구 > 작업 > 클라우드 > Cloud Services 를 클릭하거나 탭합니다.
1. Microsoft Translator 영역에서 구성 표시 를 클릭하거나 탭한 다음, 사용자 지정할 구성을 클릭하거나 탭합니다.
1. 구성 페이지에서 번역기 사용자 지정을 클릭합니다. 화면에 표시되는 Microsoft 웹 페이지를 사용하여 서비스를 맞춤화합니다.

## Translator 서비스 구성 활성화 {#activating-the-translator-service-configurations}

게시 인스턴스에 복제되는 번역된 콘텐츠를 지원하려면 클라우드 서비스 구성을 활성화해야 합니다. 다음 방법 사용 [전체 섹션(트리) 활성화](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) Microsoft Translator 또는 타사 클라우드 서비스 구성을 저장하는 저장소 노드를 활성화하려면 해당 노드는 다음과 같은 상위 노드 아래에 위치합니다.

* Microsoft 번역 서비스: /libs/settings/cloudconfigs/translation/msft-translation
* 타사 번역: /etc/cloudservices/machine-translation
