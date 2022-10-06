---
title: 프로덕션 준비 모드에서 AEM 실행
seo-title: Running AEM in Production Ready Mode
description: 프로덕션 준비 모드에서 AEM을 실행하는 방법을 알아봅니다.
seo-description: Learn how to run AEM in Production Ready Mode.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 4%

---

# 프로덕션 준비 모드에서 AEM 실행{#running-aem-in-production-ready-mode}

AEM 6.1에서 Adobe은 새로운 기능을 도입했습니다 `"nosamplecontent"` 프로덕션 환경에서 배포할 AEM 인스턴스를 준비하는 데 필요한 단계를 자동화하는 실행 모드.

새 실행 모드에서는 보안 체크리스트에 설명된 보안 모범 사례를 준수하도록 인스턴스를 자동으로 구성할 수 있을 뿐만 아니라 프로세스에서 모든 샘플 geometrixx 애플리케이션 및 구성을 제거합니다.

>[!NOTE]
>
>실용적인 이유로 인해 AEM Production Ready Mode는 인스턴스 보안에 필요한 대부분의 작업만 포함하므로 [Security 검사 목록](/help/sites-administering/security-checklist.md) 프로덕션 환경에서 사용하기 전에
>
>또한 프로덕션 준비 모드에서 AEM을 실행하면 CRXDE Lite에 대한 액세스가 효과적으로 비활성화될 수 있습니다. 디버깅을 위해 필요한 경우 [AEM에서 CRXDE Lite 활성화](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

프로덕션 준비 모드에서 AEM을 실행하려면 를 추가하면 됩니다. `nosamplecontent` 사용 `-r` 실행 모드에서 기존 시작 인수로 전환합니다.

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

예를 들어 다음과 같이 MongoDB 지속성이 있는 작성자 인스턴스를 시작할 때 프로덕션 준비 를 사용할 수 있습니다.

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 프로덕션 준비 모드의 일부 변경 {#changes-part-of-the-production-ready-mode}

보다 구체적으로, AEM이 프로덕션 준비 모드에서 실행될 때 다음 구성 변경이 수행됩니다.

1. 다음 **CRXDE 지원 번들** ( `com.adobe.granite.crxde-support`)은 프로덕션 준비 모드에서 기본적으로 비활성화됩니다. Adobe 공용 Maven 저장소에서 언제든지 설치할 수 있습니다. AEM 6.1에는 버전 3.0.0이 필요합니다.

1. 다음 **저장소에 대한 Apache Sling Simple WebDAV 액세스** ( `org.apache.sling.jcr.webdav`) 번들은에서 사용할 수 있습니다. **작성자** 인스턴스.

1. 새로 만든 사용자는 첫 번째 로그인 시 암호를 변경해야 합니다. 관리자 사용자에게는 적용되지 않습니다.
1. **디버그 정보 생성** 이 비활성화되어 있습니다. **Apache Sling Java Script 핸들러**.

1. **매핑된 콘텐츠** 및 **디버그 정보 생성** 에 대해 비활성화되어 있습니다. **Apache Sling JSP 스크립트 핸들러**.

1. 다음 **일 CQ WCM 필터** 가 로 설정되어 있습니다. `edit` on **작성자** 및 `disabled` on **게시** 인스턴스.

1. 다음 **Adobe Granite HTML 라이브러리 관리자** 는 다음 설정으로 구성됩니다.

   1. **축소:** `enabled`
   1. **디버그:** `disabled`
   1. **Gzip:** `enabled`
   1. **시간:** `disabled`

1. 다음 **Apache Sling GET 서블릿** 은 기본적으로 다음과 같이 보안 구성을 지원하도록 설정되어 있습니다.

| **구성** | **작성자** | **게시** |
|---|---|---|
| TXT 표현물 | 비활성화됨 | 비활성화됨 |
| HTML 표현물 | 비활성화됨 | 비활성화됨 |
| JSON 표현물 | 활성화됨 | 활성화됨 |
| XML 변환 | 비활성화됨 | 비활성화됨 |
| json.maximumresults | 1000 | 100 |
| 자동 인덱스 | 비활성화됨 | 비활성화됨 |
