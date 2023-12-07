---
title: Geometrixx 사이트 제거
description: 샘플 Geometrixx 콘텐츠를 제거하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Geometrixx 사이트 제거{#removing-the-geometrixx-sites}

AEM에는 샘플 Geometrixx 웹 사이트 세트가 포함되어 있습니다. 다음을 통해 이 샘플 콘텐츠를 제거할 수 있습니다. **패키지 관리자**.

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

개별 패키지를 제거하려면 **제거** 그 소포에.

다음과 같은 슈퍼 패키지도 있습니다.

* `cq-geometrixx-all-pkg-5.6.12.zip`

이 패키지에는 위의 모든 개별 패키지가 포함됩니다. 모든 geometrixx 관련 콘텐츠를 한 번에 제거하려면 **제거** 이 패키지에. 슈퍼 패키지가 설치되지 않은 상태로 전환되고 모든 개별 패키지가 패키지 관리자 보기에서 사라집니다.

이제 데모 사이트가 없는 &quot;빈&quot; AEM 인스턴스가 있습니다.

>[!NOTE]
>
>업그레이드 시 Geometrixx 사이트가 자동으로 다시 설치됩니다. 이러한 샘플을 원하지 않는 경우 업그레이드 후 Geometrixx 웹 사이트를 제거하십시오.

