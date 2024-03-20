---
title: 초안 및 제출 구성 요소에 대한 사용자 지정 저장소
description: 초안 및 제출용 사용자 데이터 저장소를 사용자 지정하는 방법을 참조하십시오.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
feature: Forms Portal
exl-id: b1300eeb-2653-4bb5-b2fd-88048c9c43b9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# 초안 및 제출 구성 요소에 대한 사용자 지정 저장소 {#custom-storage-for-drafts-and-submissions-component}

## 개요 {#overview}

AEM Forms을 사용하면 양식을 초안으로 저장할 수 있습니다. 초안 기능을 사용하면 모든 장치에서 나중에 작성 및 제출할 수 있는 진행 중인 양식 을 유지 관리할 수 있습니다.

기본적으로 AEM Forms은 양식 초안 및 제출과 관련된 사용자 데이터를 `/content/forms/fp` 게시 인스턴스의 노드 또한 AEM Forms 포털 구성 요소는 데이터 서비스를 제공합니다. 이 데이터 서비스를 사용하여 초안 및 제출에 대한 사용자 데이터 저장 구현을 사용자 지정할 수 있습니다. 예를 들어 데이터 저장소에 사용자 데이터를 저장할 수 있습니다.

## 사전 요구 사항  {#prerequisites}

* 사용 [Forms 포털 구성 요소](/help/forms/using/enabling-forms-portal-components.md)
* 만들기 [Forms 포털 페이지](/help/forms/using/creating-form-portal-page.md)
* 사용 [Forms 포털용 적응형 양식](/help/forms/using/draft-submission-component.md)
* 학습 [사용자 정의 스토리지의 구현 세부 정보](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## 초안 데이터 서비스 {#draft-data-service}

초안에 대한 사용자 데이터 저장소를 사용자 지정하려면 의 모든 메서드를 구현해야 합니다 `DraftDataService` 인터페이스. 다음 샘플 코드에서는 메서드와 인수에 대해 설명합니다.

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null if there is creation
     * @param draftDataID: unique identifier associated with the form data
     * @param formName: name of the form whose draft is being saved
     * @param formData: user data associated with this draft
     * @return userdataID corresponding to which user data has been stored and which can be used later to retrieve this user data
     * @throws FormsPortalException
     */
    public String saveData (String draftDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Returns the user data stored against the ID passed as the argument
     * @param userDataID: unique data id for user data associated with a draft
     * @return user data associated with this data ID
     * @throws FormsPortalException
     */

    public byte[] getData (String userDataID) throws FormsPortalException;

    /**
     * To delete data associated with this draft
     * @param userDataID: unique data id for data associated with a draft
     * @return status of delete operation on data associated with this draft
     * @throws FormsPortalException
     */

    public boolean deleteData (String userDataID) throws FormsPortalException;

    /**
     * Saves the attachment for current form instance
     * @param attachmentsBytes: byte array of the attachment to be saved
     * @return unique id (attachmentID) for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment (byte[] attachmentBytes) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

>[!NOTE]
>
>초안 ID 필드의 최소 값은 26자입니다. Adobe은 초안 ID 길이를 26자 이상으로 설정할 것을 권장합니다.

## 제출 데이터 서비스 {#submission-data-service}

제출을 위해 사용자 데이터의 저장소를 사용자 정의하려면 `SubmitDataService` 인터페이스. 다음 샘플 코드에서는 메서드와 인수에 대해 설명합니다.

```java
/**
 * SubmitDataService service will get/delete/submit user data (attachments and form data) filled with a submission of Form
 */
public interface SubmitDataService {

    /**
     * Submits the user data passed in argument map
     * @param userDataID, unique identifier associated with this user data
     * @param formName, name of the form whose draft is being submitted
     * @param formData, user data associated with this submission
     * @return userdataID, corresponding to which the user data has been stored and which can be used later to retrieve this data
     * @throws FormsPortalException
     */
    public String saveData (String userDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Submits the user data provided as byte array
     * @param id
     * @param data
     * @return id corresponding to saved data
     * @throws FormsPortalException
     */
    public String saveData (String id, byte[] data) throws FormsPortalException;

    /** Submits the user data provided as byte array asynchronously for the user name provided in the options map
     * @param data data to be saved in bytes
     * @param options map containing options that affect this save
     * @return id of the saved data instance
     */
    public String saveDataAsynchronusly(byte[] data, Map<String, Object> options) throws FormsPortalException;

    /**
     * Gets the user data stored against the ID passed as argument
     * @param userDataID: unique id associated with this user data for this submission
     * @return user data associated with this submission
     * @throws FormsPortalException
     */
    public byte[] getData(String userDataID) throws FormsPortalException;

    /**
     * Deletes user data stored against the userDataID
     * @param userDataID: unique id associated with this user data for this submission
     * @return status of the delete operation on this submission
     * @throws FormsPortalException
     */

    public boolean deleteData(String userDataID) throws FormsPortalException;

    /**
     * Submits the attachment bytes passed as argument
     * @param attachmentsBytes: would expect byte array of the attachment for this submission
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment(byte[] attachmentBytes) throws FormsPortalException;

    /** Submits the attachment bytes passed as argument asynchronously for the user id provided in options map.
     * @param attachmentBytes would expect byte array of the attachment for this submission
     * @param options map containing options that affect this save
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachmentAsynchronously(byte[] attachmentBytes, Map<String, Object> options) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: Unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

Forms 포털은 UUID(Universally Unique Identifier) 개념을 사용하여 초안 및 제출된 모든 양식에 대한 고유 ID를 생성합니다. 고유한 고유 ID를 생성할 수도 있습니다. FPKeyGeneratorService 인터페이스를 구현하고, 해당 메서드를 재정의하고, 사용자 지정 로직을 개발하여 모든 초안 및 제출된 양식에 대해 사용자 지정 고유 ID를 생성할 수 있습니다. 또한 사용자 지정 ID 생성 구현의 서비스 등급을 0보다 높게 설정합니다. 기본 구현 대신 사용자 지정 구현이 사용되도록 합니다.

```java
public interface FPKeyGeneratorService {
    /**
     * returns a unique id for draft and submission
     *
     * @param none
     * @return unique id in string format as per the implementation
     * @throws FormsPortalException
     */
    public String getUniqueId() throws FormsPortalException;
}
```

아래 주석을 사용하여 위 코드로 생성된 사용자 지정 ID에 대한 서비스 등급을 높일 수 있습니다.

`@Properties(value = { @Property(name = "service.ranking", intValue = 15) } )`

위의 주석을 사용하려면 다음 내용을 프로젝트로 가져옵니다.

```java
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
```
