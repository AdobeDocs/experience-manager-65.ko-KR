---
title: 초안 및 제출 데이터 서비스 사용자 정의
description: AEM Forms은 기본적으로 초안 및 제출된 적응형 양식을 Publish 인스턴스의 기본 노드에 저장합니다. 그러나 AEM Forms의 초안 및 제출 데이터 서비스를 구성하여 초안 및 제출된 적응형 양식의 저장소를 사용자 지정할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: ed10ef8c-7b9c-43cf-bea8-7cf9742a8cac
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 초안 및 제출 데이터 서비스 사용자 정의 {#customizing-draft-and-submission-data-services}

## 개요 {#overview}

AEM Forms을 사용하면 적응형 양식을 초안으로 저장할 수 있습니다. 초안 기능은 사용자에게 진행 중인 작업 양식을 유지 관리할 수 있는 옵션을 제공합니다. 그런 다음 사용자는 모든 장치에서 언제든지 양식을 작성하여 제출할 수 있습니다.

기본적으로 AEM Forms은 Publish 인스턴스의 초안 및 제출과 연관된 사용자 데이터를 `/content/forms/fp` 노드.

그러나 AEM Forms 포털 구성 요소는 초안 및 제출에 대한 사용자 데이터 저장의 구현을 사용자 정의할 수 있는 데이터 서비스를 제공합니다. 예를 들어 조직에 현재 구현된 데이터 저장소에 데이터를 저장할 수 있습니다.

사용자 데이터의 저장소를 사용자 지정하려면 다음을 구현해야 합니다 [초안 데이터](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) 및 [제출 데이터](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p) 서비스.

## 사전 요구 사항 {#prerequisites}

* 사용 [Forms 포털 구성 요소](/help/forms/using/enabling-forms-portal-components.md)
* 만들기 [Forms 포털 페이지](/help/forms/using/creating-form-portal-page.md)
* 사용 [Forms 포털용 적응형 양식](/help/forms/using/draft-submission-component.md)
* 학습 [사용자 정의 스토리지의 구현 세부 정보](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## 초안 데이터 서비스 {#draft-data-service}

사용자 초안 데이터의 저장소를 사용자 지정하려면 의 모든 메서드에 대한 구현을 제공해야 합니다. `DraftAFDataService` 인터페이스.

메서드와 해당 인수에 대한 설명은 인터페이스의 다음 코드 샘플에 제공됩니다.

```java
public interface DraftAFDataService {

 /**
  * Deletes the user data stored against the ID passed as the argument
  *
  * @param draftDataID
  * @return status for the just occurred delete draft UserData operation
  * @throws FormsPortalException
  */
 public Boolean deleteAFDraftUserData (String draftDataID) throws FormsPortalException;

 /**
  * Saves user data provided in the argument map
  *
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") if there is update
  * @return userData ID would be returned which needs to be saved in metadata node
  * @throws FormsPortalException
  */
 public String saveAFUserData (Map<String, Object> draftUserDataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as the argument
  *
  * @param Draft DataID
  * @return guideState (which would then be populated in adaptive form to reload the draft) which is stored against draftDataID
  * @throws FormsPortalException
  */
 public byte[] getAFDraftUserData(String draftDataID) throws FormsPortalException;

 /**
  * Saves the attachments for current adaptive form instance
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String saveAttachments(byte[] attachmentBytes) throws FormsPortalException;
}
```

## 제출 데이터 서비스 {#submission-data-service}

사용자 제출 데이터의 저장소를 사용자 지정하려면 의 모든 메서드에 대한 구현을 제공해야 합니다. `SubmittedAFDataService` 인터페이스.

메서드와 해당 인수에 대한 설명은 인터페이스의 다음 코드 샘플에 제공됩니다.

```java
public interface SubmittedAFDataService {

 /**
  * Submits the user data passed in argument map
  *
  * @param submittedAFUserdataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID")
  * @return userData ID is returned that needs to be saved in the metadata node
  * @throws FormsPortalException
  */
 public String submitAFUserData (Map<String, Object> submittedAFUserdataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as argument
  *
  * @param submitDataID
  * @return guideState which would be used to open DOR
  * @throws FormsPortalException
  */
 public byte[] getSubmittedAFUSerData(String submitDataID) throws FormsPortalException;

 /**
  * Deletes user data stored against the ID passed as argument
  *
  * @param Submit DataID
  * @return status of the delete operation on Submitted User data
  * @throws FormsPortalException
  */

 public Boolean deleteSubmittedAFUserData(String submitDataID) throws FormsPortalException;

 /**
  * Submits the attachment bytes passed as argument
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String submitAttachments(Object attachmentBytes) throws FormsPortalException;

}
```
