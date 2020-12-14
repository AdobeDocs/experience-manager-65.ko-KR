---
title: Geometrixx 사이트 제거
seo-title: Geometrixx 사이트 제거
description: 샘플 Geometrixx 컨텐츠를 제거하는 방법을 알아봅니다.
seo-description: 샘플 Geometrixx 컨텐츠를 제거하는 방법을 알아봅니다.
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Geometrixx 사이트 제거 중{#removing-the-geometrixx-sites}

AEM에는 샘플 Geometrixx 웹 사이트 세트가 포함되어 있습니다. **패키지 관리자**&#x200B;를 통해 이 샘플 컨텐츠를 제거할 수 있습니다.

개별 geometrixx 관련 패키지는 다음과 같습니다.

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

개별 패키지를 제거하려면 해당 패키지에서 **제거**&#x200B;를 클릭합니다.

수퍼 패키지도 있다.

* `cq-geometrixx-all-pkg-5.6.12.zip`

이 패키지에는 위의 개별 패키지가 모두 포함됩니다. 모든 geometrixx 관련 컨텐츠를 한 번에 제거하려면 이 패키지에서 **제거**&#x200B;를 클릭합니다. super-package는 제거된 상태로 이동하며 모든 개별 패키지는 패키지 관리자 보기에서 사라집니다.

이제 데모 사이트 없이 &quot;빈&quot; AEM 인스턴스가 있습니다.

>[!NOTE]
>
>업그레이드하면 geometrixx 사이트가 자동으로 다시 설치됩니다. 이러한 샘플이 필요하지 않은 경우 업그레이드 후 geometrixx 웹 사이트를 제거해야 할 수 있습니다.

