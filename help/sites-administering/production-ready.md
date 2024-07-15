---
title: 프로덕션 준비 모드에서 AEM 실행
description: 프로덕션 준비 모드에서 AEM을 실행하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 3%

---

# 프로덕션 준비 모드에서 AEM 실행{#running-aem-in-production-ready-mode}

AEM 6.1에서 Adobe은 프로덕션 환경에서 배포할 AEM 인스턴스를 준비하는 데 필요한 단계를 자동화하는 새로운 `"nosamplecontent"` 실행 모드를 도입했습니다.

새 실행 모드는 보안 확인 목록에 설명된 보안 모범 사례를 준수하도록 인스턴스를 자동으로 구성할 뿐만 아니라 프로세스에서 모든 샘플 Geometrixx 애플리케이션 및 구성을 제거합니다.

>[!NOTE]
>
>현실적인 이유로 AEM 프로덕션 준비 모드는 인스턴스 보안에 필요한 대부분의 작업만 다루게 되므로 프로덕션 환경을 시작하기 전에 [보안 확인 목록](/help/sites-administering/security-checklist.md)을 참조하는 것이 좋습니다.
>
>또한 프로덕션 준비 모드에서 AEM을 실행하면 CRXDE Lite에 대한 액세스가 효과적으로 비활성화됩니다. 디버깅을 위해 필요한 경우 [AEM에서 CRXDE Lite 사용](/help/sites-administering/enabling-crxde-lite.md)을 참조하십시오.

![chlimage_1-83](assets/chlimage_1-83a.png)

프로덕션 준비 모드에서 AEM을 실행하려면 `-r` 실행 모드 스위치를 통해 기존 시작 인수에 `nosamplecontent`을(를) 추가해야 합니다.

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

예를 들어 다음과 같이 MongoDB 지속성이 있는 작성자 인스턴스를 시작할 준비가 된 프로덕션을 사용할 수 있습니다.

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 프로덕션 준비 모드의 일부 변경 {#changes-part-of-the-production-ready-mode}

특히 AEM이 프로덕션 준비 모드에서 실행될 때 다음 구성 변경이 수행됩니다.

1. **CRXDE 지원 번들**(`com.adobe.granite.crxde-support`)은(는) 프로덕션 준비 모드에서 기본적으로 비활성화됩니다. Adobe 공개 Maven 저장소에서 언제든지 설치할 수 있습니다. AEM 6.1에는 버전 3.0.0이 필요합니다.

1. 저장소에 대한 **Apache Sling Simple WebDAV 액세스**( `org.apache.sling.jcr.webdav`) 번들은 **작성자** 인스턴스에서만 사용할 수 있습니다.

1. 새로 생성된 사용자는 처음 로그인할 때 암호를 변경해야 합니다. 관리자 사용자에게는 적용되지 않습니다.
1. **Apache Sling JavaScript 처리기**&#x200B;에 대해 **디버그 정보 생성**&#x200B;을 사용할 수 없습니다.

1. **Apache Sling JSP Script Handler**&#x200B;에 대해 **매핑된 콘텐츠** 및 **디버그 정보 생성**&#x200B;이 비활성화되었습니다.

1. **일 CQ WCM 필터**&#x200B;이(가) **작성자**&#x200B;의 `edit`, **게시** 인스턴스의 `disabled`(으)로 설정되어 있습니다.

1. **Adobe Granite HTML 라이브러리 관리자**&#x200B;가 다음 설정으로 구성되었습니다.

   1. **축소:** `enabled`
   1. **디버그:** `disabled`
   1. **Gzip:** `enabled`
   1. **시간:** `disabled`

1. **Apache Sling GET 서블릿**&#x200B;은(는) 기본적으로 다음과 같이 보안 구성을 지원하도록 설정됩니다.

| **구성** | **작성자** | **Publish** |
|---|---|---|
| TXT 렌디션 | 비활성화됨 | 비활성화됨 |
| HTML 렌디션 | 비활성화됨 | 비활성화됨 |
| JSON 렌디션 | 활성화됨 | 활성화됨 |
| XML 렌디션 | 비활성화됨 | 비활성화됨 |
| json.maximumresults | 1000년 | 100 |
| 자동 색인 | 비활성화됨 | 비활성화됨 |
