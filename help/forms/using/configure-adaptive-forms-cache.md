---
title: 적응형 양식 캐시 구성
seo-title: 적응형 양식 캐시 구성
description: '적응형 양식 캐시는 적응형 양식 및 문서를 위해 특별히 고안되었습니다. 적응형 양식 또는 문서를 클라이언트에서 렌더링하는 데 필요한 시간을 단축하기 위한 목적으로 적응형 양식과 적응형 문서를 캐시합니다. '
seo-description: '적응형 양식 캐시는 적응형 양식 및 문서를 위해 특별히 고안되었습니다. 적응형 양식 또는 문서를 클라이언트에서 렌더링하는 데 필요한 시간을 단축하기 위한 목적으로 적응형 양식과 적응형 문서를 캐시합니다. '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 적응형 양식 캐시 구성{#configure-adaptive-forms-cache}

캐시는 데이터 액세스 시간을 단축하고, 지연을 줄이고, 입출력(I/O) 속도를 향상시키는 메커니즘입니다. 적응형 양식 캐시는 사전 채워진 데이터를 저장하지 않고 적응형 양식의 HTML 컨텐츠 및 JSON 구조만 저장합니다. 클라이언트에서 응용 양식이나 문서를 렌더링하는 데 필요한 시간을 줄이는 데 도움이 됩니다. 적응형 양식을 위해 특별히 설계되었으며 적응형 문서를 지원합니다.

>[!NOTE]
>
>적응형 양식 캐시를 사용하는 경우 AEM Dispatcher를 사용하여 적응형 양식 또는 문서의 클라이언트 라이브러리(CSS 및 JavaScript)를 캐시합니다.

>[!NOTE]
>
>사용자 지정 구성 요소를 개발하는 동안, 개발에 사용되는 서버에서 응용 양식 캐시를 사용하지 않도록 설정하십시오.

## 캐시 구성 {#configure-the-cache}

적응형 양식 캐시를 구성하려면 다음 단계를 수행하십시오.

1. https://&#39;의 AEM 웹 콘솔 구성[관리자로]이동합니다.[server]:port&#39;/system/console/configMgr.
1. 적응형 **양식 및 대화형 통신 웹 채널 구성을** 클릭하여 구성 값을 편집합니다.
1. 구성 값 편집 대화 상자에서 적응형 양식 수 필드에 AEM Forms 서버의 인스턴스가 캐싱할 수 있는 최대 양식 또는 문서 **수를 지정합니다** . 기본값은 100입니다.

   >[!NOTE]
   >
   >캐시를 비활성화하려면 [적응형 양식 수] 필드의 값을 **0으로 설정합니다**. 캐시는 재설정되며 캐시 구성을 비활성화하거나 변경하면 모든 양식과 문서가 캐시에서 제거됩니다.

   ![적응형 양식 HTML 캐시를 위한 구성 대화 상자](assets/cache-configuration-edit.png)

1. Click **Save** to save the configuration.

