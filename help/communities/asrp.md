---
title: ASRP - Adobe 저장소 리소스 공급자
seo-title: ASRP - Adobe 저장소 리소스 공급자
description: 관계형 데이터베이스를 공용 저장소로 사용하도록 AEM Communities 설정
seo-description: 관계형 데이터베이스를 공용 저장소로 사용하도록 AEM Communities 설정
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
role: Administrator
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# ASRP - Adobe 저장소 리소스 공급자 {#asrp-adobe-storage-resource-provider}

## ASRP {#about-asrp} 정보

AEM Communities이 ASRP를 일반 스토어로 사용하도록 구성된 경우 동기화 또는 복제 없이 모든 작성자 및 게시 인스턴스에서 사용자가 생성한 컨텐츠(UGC)에 액세스할 수 있습니다.

[SRP 옵션](/help/communities/working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](/help/communities/topologies.md)도 참조하십시오.

## 요구 사항 {#requirements}

ASRP를 사용하려면 추가 라이센스가 필요합니다.

UGC용 ASRP를 사용하도록 AEM Communities 사이트를 구성하려면 계정 담당자에게 다음 사항을 문의하십시오.

* 데이터 센터 URL(ASRP 끝점의 주소)
* 소비자 키
* 비밀 키
* 보고서 세트 ID

소비자 및 비밀 키는 회사의 모든 보고서 세트에서 공유됩니다. 테넌트당 보고서 세트가 한 개 있습니다.

## 구성 {#configuration}

### ASRP {#select-asrp} 선택

[스토리지 구성 콘솔](/help/communities/srp-config.md)에서는 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

**AEM 작성자 인스턴스에서:**

* 전역 탐색에서 **[!UICONTROL 도구 > 커뮤니티 > 저장소 구성]**&#x200B;으로 이동하고 **[!UICONTROL ASRP(Storage Resource Provider) Adobe]**&#x200B;을 선택합니다.

![asrp 기본값](assets/asrp-default.png)

다음은 프로비전 프로세스에서 가져온 정보입니다.

* **데이터 센터 URL**:계정 담당자에게 식별된 프로덕션 데이터 센터를 선택하려면 풀다운을 사용합니다.
* **기본 보고서 세트**:기본 보고서 세트의 이름을 입력합니다.
* **소비자 키**:소비자 키를 입력합니다.
* **비밀**:암호를 입력합니다.
* **제출**&#x200B;을 선택합니다.

게시 인스턴스 준비:

* [암호화 키 복제](#replicate-the-crypto-key)
* [구성 복제](#publishing-the-configuration)

구성을 제출한 후 연결을 테스트합니다.

* **테스트 구성**&#x200B;을 선택합니다.

   각 작성자 및 게시 인스턴스에 대해 스토리지 구성 콘솔에서 데이터 센터에 대한 연결을 테스트합니다.

* 프로필 데이터의 사이트 URL이 데이터 센터에서 링크](#externalize-links)외부화를 통해 라우트할 수 있는지 확인합니다.[

### 암호화 키 {#replicate-the-crypto-key} 복제

소비자 키와 비밀 키가 암호화되었습니다. 키가 제대로 암호화되거나 해독되려면 기본 Granite Crypto 키가 모든 AEM 인스턴스에서 동일해야 합니다.

[암호화 키 복제](/help/communities/deploy-communities.md#replicate-the-crypto-key)의 지침을 따르십시오.

### 링크 {#externalize-links} 외부화

올바른 프로필 및 프로필 이미지 링크를 보려면 [Link Externalizer](/help/sites-developing/externalizer.md)를 올바르게 구성해야 합니다.

도메인을 ASRP(데이터 센터 URL)에서 라우팅할 수 있는 URL로 설정해야 합니다.

### 시간 동기화 {#time-synchronization}

ASRP 종단점으로 인증하려면 호스팅된 AEM Communities을 실행하는 컴퓨터가 [NTP(네트워크 시간 프로토콜)](https://www.ntp.org/)과 같이 동기화된 시간이어야 합니다.

### 구성 {#publishing-the-configuration} 게시

ASRP는 모든 작성자 및 게시 인스턴스에서 공용 저장소로 식별되어야 합니다.

게시 환경에서 동일한 구성을 사용할 수 있도록 하려면 다음을 수행하십시오.

AEM 작성자 인스턴스에서:

* 기본 메뉴에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 복제]**&#x200B;로 이동합니다.
* **트리 활성화** 선택
* **시작 경로**:찾아보기  `/conf/global/settings/communities/srpc/`
* **Only Modified** 선택 취소
* **활성화** 선택

## AEM 6.0에서 업그레이드 {#upgrading-from-aem}

>[!CAUTION]
>
>게시된 커뮤니티 사이트에서 ASRP를 활성화하면 온-프레미스 스토리지와 클라우드 스토리지 간에 데이터 동기화가 없으므로 [JCR](/help/communities/jsrp.md)에 이미 저장된 UGC가 더 이상 표시되지 않습니다.

**`AEM Communities Extension`** 는 이전에 AEM 6.0 소셜 커뮤니티에서 클라우드 서비스로 도입되었습니다. AEM 6.1 Communities에서는 클라우드 구성이 필요하지 않으며 [스토리지 구성 콘솔](/help/communities/srp-config.md)에서 ASRP를 선택하면 됩니다.

새로운 저장소 구조 때문에 소셜 커뮤니티에서 Communities로 업그레이드할 때 [업그레이드](/help/communities/upgrade.md#adobe-cloud-storage) 지침을 따라야 합니다.

## 사용자 데이터 관리 {#managing-user-data}

게시 환경에 자주 입력되는 *사용자*, *사용자 프로필* 및 *사용자 그룹*&#x200B;에 대한 자세한 내용은 를 참조하십시오.

* [사용자 동기화](/help/communities/sync.md)
* [사용자 및 사용자 그룹 관리](/help/communities/users.md)

## 문제 해결 {#troubleshooting}

### {#ugc-disappears-after-upgrade} 업그레이드 후 UGC가 사라짐

기존 AEM 6.0 소셜 커뮤니티 사이트에서 업그레이드하는 경우 [업그레이드 지침](/help/communities/upgrade.md#adobe-cloud-storage)을 따라야 합니다. 그렇지 않으면 UGC가 유실됩니다.

### 인증 오류 {#authentication-errors}

데이터 센터 URL에 대한 인증 오류를 수신하고 AEM error.log에 오래된 타임스탬프에 대한 메시지가 포함된 경우 시간 동기화가 발생하고 있는지 확인합니다.

모든 AEM 작성자 및 게시 서버를 시간 동기화하려면 [NTP(네트워크 시간 프로토콜)](https://www.ntp.org/) 등의 도구를 사용합니다.

### 새 컨텐츠가 검색 {#new-content-does-not-appear-in-searches}에 나타나지 않습니다.

Adobe 클라우드 스토리지 인프라는 *최종 일관성*&#x200B;을 사용하여 확장 및 성능 목표를 달성합니다. 따라서 새 컨텐츠는 즉시 사용할 수 없으며 검색 결과에 표시되는 데 몇 초가 소요됩니다.

최종 일관성에 영향을 주는 간격을 모니터링하는 동안 새 컨텐츠가 검색에 표시되는 데 몇 초 이상 걸리는 경우 계정 담당자에게 문의하십시오.

### ASRP {#ugc-not-visible-in-asrp}에 UGC가 표시되지 않음

저장소 옵션의 구성을 확인하여 ASRP가 기본 공급자로 구성되었는지 확인하십시오. 기본적으로 저장소 리소스 공급자는 ASRP가 아니라 JSRP입니다.

모든 작성 및 게시 AEM 인스턴스에서 Storage Configuration 콘솔을 다시 방문하거나 AEM 저장소를 확인합니다.

JCR에서 [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)인 경우:

* [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp) 노드를 포함하지 않습니다. 즉, 스토리지 공급자가 JSRP입니다.
* srpc 노드가 있고 [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) 노드를 포함하는 경우 기본 구성의 속성은 ASRP를 기본 공급자로 정의합니다.
