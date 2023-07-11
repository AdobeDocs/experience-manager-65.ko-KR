---
title: 프로덕션 준비 모드에서 AEM 실행
description: 프로덕션 준비 모드에서 AEM을 실행하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 4%

---

# 프로덕션 준비 모드에서 AEM 실행{#running-aem-in-production-ready-mode}

AEM 6.1에서 Adobe은 새로운 `"nosamplecontent"` 실행 모드는 프로덕션 환경에서 배포할 AEM 인스턴스를 준비하는 데 필요한 단계를 자동화하는 데 목적이 있습니다.

새 실행 모드는 보안 확인 목록에 설명된 보안 모범 사례를 준수하도록 인스턴스를 자동으로 구성할 뿐만 아니라 프로세스에서 모든 샘플 Geometrixx 애플리케이션 및 구성을 제거합니다.

>[!NOTE]
>
>현실적인 이유로 AEM 프로덕션 준비 모드는 인스턴스 확보에 필요한 대부분의 작업만 담당하므로 다음을 참조하는 것이 좋습니다. [보안 검사 목록](/help/sites-administering/security-checklist.md) 프로덕션 환경으로 시작하기 전에
>
>또한 프로덕션 준비 모드에서 AEM을 실행하면 CRXDE Lite에 대한 액세스가 효과적으로 비활성화됩니다. 디버깅을 위해 필요한 경우 다음을 참조하십시오 [AEM에서 CRXDE Lite 활성화](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

프로덕션 준비 모드에서 AEM을 실행하려면 를 추가해야 합니다. `nosamplecontent` 를 통해 `-r` 기존 시작 인수로 실행 모드 전환:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

예를 들어 다음과 같이 MongoDB 지속성이 있는 작성자 인스턴스를 시작할 준비가 된 프로덕션을 사용할 수 있습니다.

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 프로덕션 준비 모드의 일부 변경 {#changes-part-of-the-production-ready-mode}

특히 AEM이 프로덕션 준비 모드에서 실행될 때 다음 구성 변경이 수행됩니다.

1. 다음 **CRXDE 지원 번들** ( `com.adobe.granite.crxde-support`)는 프로덕션 준비 모드에서 기본적으로 비활성화됩니다. Adobe 공개 Maven 저장소에서 언제든지 설치할 수 있습니다. AEM 6.1에는 버전 3.0.0이 필요합니다.

1. 다음 **저장소에 대한 Apache Sling 간단한 WebDAV 액세스** ( `org.apache.sling.jcr.webdav`) 번들은 다음에만 사용할 수 있습니다. **작성자** 인스턴스.

1. 새로 생성된 사용자는 처음 로그인할 때 암호를 변경해야 합니다. 관리자 사용자에게는 적용되지 않습니다.
1. **디버그 정보 생성** 이(가) 다음에 대해 비활성화되어 있습니다. **Apache Sling JavaScript 핸들러**.

1. **매핑된 컨텐츠** 및 **디버그 정보 생성** 다음에 대해 비활성화됨 **Apache Sling JSP Script Handler**.

1. 다음 **일별 CQ WCM 필터** 이(가) (으)로 설정됨 `edit` 날짜 **작성자** 및 `disabled` 날짜 **게시** 인스턴스.

1. 다음 **Adobe Granite HTML 라이브러리 관리자** 는 다음 설정으로 구성됩니다.

   1. **축소:** `enabled`
   1. **디버그:** `disabled`
   1. **Gzip:** `enabled`
   1. **시간:** `disabled`

1. 다음 **Apache Sling GET 서블릿** 는 기본적으로 다음과 같이 보안 구성을 지원하도록 설정됩니다.

| **구성** | **작성자** | **게시** |
|---|---|---|
| TXT 렌디션 | 비활성화됨 | 비활성화됨 |
| HTML 렌디션 | 비활성화됨 | 비활성화됨 |
| JSON 렌디션 | 활성화됨 | 활성화됨 |
| XML 렌디션 | 비활성화됨 | 비활성화됨 |
| json.maximumresults | 1000 | 100 |
| 자동 색인 | 비활성화됨 | 비활성화됨 |
