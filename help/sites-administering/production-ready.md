---
title: 프로덕션 준비 모드에서 AEM 실행
seo-title: 프로덕션 준비 모드에서 AEM 실행
description: 프로덕션 준비 모드에서 AEM을 실행하는 방법을 알아봅니다.
seo-description: 프로덕션 준비 모드에서 AEM을 실행하는 방법을 알아봅니다.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# 프로덕션 준비 모드에서 AEM 실행{#running-aem-in-production-ready-mode}

AEM 6.1을 통해 Adobe는 프로덕션 환경에서 배포할 AEM 인스턴스를 준비하는 데 필요한 단계를 자동화하기 위한 새로운 `"nosamplecontent"` 실행 모드를 제공합니다.

새 실행 모드는 보안 체크리스트에 설명된 보안 모범 사례를 따르도록 인스턴스를 자동으로 구성할 뿐만 아니라 프로세스의 모든 샘플 geometrixx 응용 프로그램 및 구성을 제거합니다.

>[!NOTE]
>
>실용적인 이유로 인해 AEM Production 준비 모드는 인스턴스 보안에 필요한 대부분의 작업만 다루므로 프로덕션 환경에서 작업하기 전에 보안 [체크리스트를](/help/sites-administering/security-checklist.md) 참조하십시오.
>
>또한 프로덕션 준비 모드에서 AEM을 실행하면 CRXDE Lite에 대한 액세스가 효과적으로 비활성화됩니다. 디버깅을 위해 필요한 경우 AEM에서 [CRXDE Lite 활성화를 참조하십시오](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

프로덕션 준비 모드에서 AEM을 실행하려면 실행 모드 스위치를 `nosamplecontent` `-r` 통해 기존 시작 인수에 AEM을 추가하면 됩니다.

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

예를 들어 프로덕션 준비 기능을 사용하여 다음과 같이 MongoDB 지속성이 있는 작성자 인스턴스를 시작할 수 있습니다.

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 프로덕션 준비 모드에서 일부 변경 {#changes-part-of-the-production-ready-mode}

특히 AEM이 프로덕션 준비 모드에서 실행될 때 다음 구성 변경이 수행됩니다.

1. CRXDE **지원 번들** ( `com.adobe.granite.crxde-support`)은 프로덕션 준비 모드에서 기본적으로 비활성화됩니다. Adobe Public Maven 저장소에서 언제든지 설치할 수 있습니다. AEM 6.1의 경우 버전 3.0.0이 필요합니다.

1. 저장소 **() 번들에** 대한 Apache Sling Simple WebDAV Access는 `org.apache.sling.jcr.webdav`작성자 **** 인스턴스에서만 사용할 수 있습니다.

1. 새로 만든 사용자는 첫 번째 로그인 시 암호를 변경해야 합니다. 관리 사용자에게는 적용되지 않습니다.
1. **Apache Java 스크립트 처리기에 대한 디버그 정보** 생성이 **비활성화됩니다**.

1. **매핑된 컨텐츠** 및 **디버그 정보** 생성이 Apache Sling JSP 스크립트 핸들러에 대해 **비활성화됩니다**.

1. 요일 **CQ WCM** 필터가 `edit` 작성자와 **게시 인스턴스** 게시 시 `disabled` 게시되도록 설정되어 **** 있습니다.

1. **Adobe Granite HTML 라이브러리 관리자는** 다음 설정으로 구성됩니다.

   1. **** 축소: `enabled`
   1. **** 디버그: `disabled`
   1. **** Gzip: `enabled`
   1. **** 타이밍: `disabled`

1. Apache **Sling GET** Servlet은 다음과 같이 기본적으로 보안 구성을 지원하도록 설정됩니다.

| **구성** | **작성** | **게시** |
|---|---|---|
| TXT 변환 | 비활성화됨 | 비활성화됨 |
| HTML 변환 | 비활성화됨 | 비활성화됨 |
| JSON 변환 | 활성화됨 | 활성화됨 |
| XML 변환 | 비활성화됨 | 비활성화됨 |
| json.maximumresults | 1000 | 100 |
| 자동 색인 | 비활성화됨 | 비활성화됨 |

