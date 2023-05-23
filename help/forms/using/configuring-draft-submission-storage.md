---
title: 초안 및 제출을 위한 스토리지 서비스 구성
seo-title: Configuring storage services for drafts and submissions
description: 초안 및 제출용 저장소를 구성하는 방법 알아보기
seo-description: Learn how to configure storage for drafts and submissions
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 초안 및 제출을 위한 스토리지 서비스 구성 {#configuring-storage-services-for-drafts-and-submissions}

## 개요 {#overview}

AEM Forms을 사용하여 다음을 저장할 수 있습니다.

* **초안**: 최종 사용자가 작성하여 나중에 제출할 수 있도록 저장한 후 나중에 제출하는 진행 중인 양식.

* **제출**: 사용자 제공 데이터를 포함하는 제출된 양식입니다.

AEM Forms 포털 데이터 및 메타데이터 서비스는 초안 및 제출을 지원합니다. 기본적으로 데이터는 게시 인스턴스에 저장되며, 그런 다음 구성된 작성자 인스턴스에 역복제되어 다른 게시 인스턴스에 복제할 수 있습니다.

기존 기본 제공 접근 방식의 문제점은 PII(개인 식별 정보)일 수 있는 데이터를 포함하여 게시 인스턴스에 모든 데이터를 저장한다는 것입니다.

위에서 언급한 기본 접근 방식 외에도 양식 데이터를 로컬에 저장하는 대신 처리에 직접 푸시하는 대체 구현도 사용할 수 있습니다. 게시 인스턴스에 잠재적으로 중요한 데이터를 저장할 우려가 있는 고객은 데이터가 처리 서버로 전송되는 대체 구현을 선택할 수 있습니다. 작성자 인스턴스에서 처리되므로 일반적으로 보안 영역에 유지됩니다.

>[!NOTE]
>
>Forms 포털 제출 액션을 사용하거나 적응형 양식에서 Forms 포털에 데이터 저장 옵션을 활성화하면 양식 데이터가 AEM 저장소에 저장됩니다. 프로덕션 환경에서는 초안 또는 제출된 양식 데이터를 AEM 저장소에 저장하지 않는 것이 좋습니다. 대신 초안 및 제출 구성 요소를 엔터프라이즈 데이터베이스와 같은 보안 저장소와 통합하여 초안 및 제출된 양식 데이터를 저장해야 합니다.
>
>자세한 내용은 [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](/help/forms/using/integrate-draft-submission-database.md).

## Forms 포털 초안 및 제출 서비스 구성 {#configuring-forms-portal-drafts-and-submissions-services}

AEM 웹 콘솔 구성에서( `https://[host]:'port'/system/console/configMgr`), 클릭하여 열기 **Forms 포털 초안 및 제출 구성** 편집 모드로 전환됩니다.

아래 설명된 대로 요구 사항에 따라 속성 값을 지정합니다.

### 게시 인스턴스에 데이터를 저장하는 기본 서비스 {#out-of-the-box-services-to-store-data-on-publish-instance}

데이터는 구성된 작성자 인스턴스에 역복제됩니다.

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>값</th>
  </tr>
  <tr>
   <td>Forms 포털 초안 데이터 서비스(초안 데이터 서비스용 식별자 (<strong>draft.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms 포털 초안 메타데이터 서비스(초안 메타데이터 서비스용 식별자 (<strong>draft.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms 포털 데이터 서비스 제출(데이터 서비스 제출용 식별자(<strong>submit.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms 포털 제출 메타데이터 서비스(제출 메타데이터 서비스용 식별자 (<strong>submit.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### 원격 처리 인스턴스에 데이터를 저장할 수 있는 기본 서비스 {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

데이터는 구성된 원격 인스턴스에 직접 푸시됨

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>값</th>
  </tr>
  <tr>
   <td>Forms 포털 초안 데이터 서비스(초안 데이터 서비스용 식별자 (<strong>draft.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms 포털 초안 메타데이터 서비스(초안 메타데이터 서비스용 식별자 (<strong>draft.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms 포털 데이터 서비스 제출(데이터 서비스 제출용 식별자(<strong>submit.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms 포털 제출 메타데이터 서비스(제출 메타데이터 서비스용 식별자 (<strong>submit.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

위에 지정된 구성 외에도 구성된 원격 처리 인스턴스에 대한 정보를 제공합니다.

AEM 웹 콘솔 구성에서( `https://[host]:'port'/system/console/configMgr`), 클릭하여 열기 **AEM DS 설정 서비스** 편집 모드로 전환됩니다. AEM DS 설정 서비스 대화 상자에서 처리 서버 URL, 처리 서버 사용자 이름 및 암호에 대한 정보를 제공합니다.

>[!NOTE]
>
>데이터베이스에 사용자 데이터를 저장하기 위한 샘플 구현도 제공된다. 외부 데이터베이스에 사용자 데이터를 저장하도록 데이터 및 메타데이터 서비스를 구성하는 방법을 이해하려면 다음을 참조하십시오. [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](/help/forms/using/integrate-draft-submission-database.md).
