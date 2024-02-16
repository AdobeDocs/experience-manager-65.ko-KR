---
title: 편지 및 대화형 커뮤니케이션의 사후 처리
description: 서신 관리에서 편지 후처리를 사용하면 인쇄 및 이메일과 같은 AEM 및 Forms 후처리를 만들고 이를 편지와 통합할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 91ee4422-99c1-4907-a507-5968c6984f28
source-git-commit: 6dbec0f41396c2b41d5324c4ecf6f1f33b1d0780
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# 편지 및 대화형 커뮤니케이션의 사후 처리{#post-processing-of-letters-and-interactive-communications}

## 사후 처리 {#post-processing}

상담원은 편지 및 대화형 커뮤니케이션에 사후 처리 워크플로를 연결하고 실행할 수 있습니다. 실행할 사후 프로세스는 Letter 템플릿의 속성 보기에서 선택할 수 있습니다. 전자 메일, 인쇄, 팩스 또는 최종 편지 보관을 위한 사후 프로세스를 설정할 수 있습니다.

![사후 처리](assets/ppoverview.png)

사후 프로세스를 편지 또는 대화형 통신과 연결하려면 먼저 사후 프로세스를 설정해야 합니다. 제출된 편지에 대해 두 가지 유형의 워크플로우를 실행할 수 있습니다.

1. **Forms Workflow:** AEM Forms on JEE 프로세스 관리 워크플로우입니다. 설정 지침 [Forms Workflow](#formsworkflow).

1. **AEM 워크플로:** AEM 워크플로우는 제출된 편지에 대한 사후 프로세스로도 사용할 수 있습니다. 설정 지침 [AEM 워크플로](../../forms/using/aem-forms-workflow.md).

## 양식 워크플로우 {#formsworkflow}

1. AEM에서 다음 URL을 사용하여 서버에 대한 Adobe Experience Manager 웹 콘솔 구성을 엽니다. `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![구성 관리자](assets/2configmanager-1.png)

1. 이 페이지에서 AEM Forms 클라이언트 SDK 구성을 찾아 클릭하여 확장합니다.
1. 서버 URL에서 JEE 서버의 AEM Forms 이름과 로그인 세부 사항을 입력한 다음 을 클릭합니다. **저장**.

   ![LiveCycle 서버 이름 입력](assets/1cofigmanager.png)

1. 사용자 이름과 암호를 지정합니다.
1. sun.util.calendar가 Deserialization Firewall Configuration에 추가되어 있는지 확인합니다.

   Deserialization Firewall Configuration으로 이동하고 패키지 접두사의 허용 목록에추가된 클래스에서 sun.util.calendar를 추가합니다.

1. 이제 서버가 매핑되고 JEE의 AEM Forms에 있는 사후 프로세스가 문자를 만드는 동안 AEM 사용자 인터페이스에서 사용할 수 있습니다.

   ![나열된 사후 프로세스를 사용하여 편지 화면 만들기](assets/0configmanager.png)

1. 프로세스/서비스를 인증하려면 프로세스 이름을 복사하고 Adobe Experience Manager 웹 콘솔 구성 페이지 > AEM Forms 클라이언트 SDK 구성으로 돌아가 프로세스를 새 서비스로 추가합니다.

   예를 들어, 문자의 속성 페이지에 있는 드롭다운에 프로세스 이름이 Forms Workflow -> ValidCCPostProcess/SaveXML로 표시되면 서비스 이름을 로 추가합니다. `ValidCCPostProcess/SaveXML`.

1. 사후 처리에 JEE의 AEM Forms 워크플로우를 사용하려면 필요한 매개 변수와 출력을 설정하십시오. 매개 변수의 기본값은 아래에 표시되어 있습니다.

   Adobe Experience Manager 웹 콘솔 구성 페이지로 이동합니다. > **[!UICONTROL 서신 관리 구성]** 을 설정하고 다음 매개 변수를 설정합니다.

   1. **inPDFDoc(PDF 문서 매개변수):** PDF 문서를 입력으로 사용합니다. 이 입력에는 렌더링된 문자가 입력으로서 포함됩니다. 표시된 매개변수 이름은 구성할 수 있습니다. 구성의 서신 관리 구성에서 구성할 수 있습니다.
   1. **inXMLDoc(XML 데이터 매개변수):** XML 문서가 입력입니다. 이 입력에는 사용자가 XML 형식으로 입력한 데이터가 포함됩니다.
   1. **inXDPDoc(XDP 문서 매개변수):** XML 문서가 입력입니다. 이 입력에 기본 레이아웃(XDP)이 포함되어 있습니다.
   1. **inAttachmentDocs(첨부 문서 매개 변수):** 목록 입력 매개 변수. 이 입력에는 모든 첨부 파일이 입력으로서 포함됩니다.
   1. **redirectURL(리디렉션 URL 출력):** 리디렉션할 URL을 나타내는 출력 유형입니다.

   양식 워크플로우에는에 지정된 것과 동일한 이름의 입력으로 PDF 문서 매개 변수 또는 XML 데이터 매개 변수가 있어야 합니다 **[!UICONTROL 서신 관리 구성]**. 사후 프로세스 드롭다운에 프로세스를 나열하려면 이 과정이 필요합니다.

## 게시 인스턴스의 설정 {#settings-on-the-publish-instance}

1. 에 로그인 `https://localhost:publishport/aem/forms`.
1. 다음으로 이동 **[!UICONTROL 편지]** 게시 인스턴스에서 사용할 수 있는 게시된 편지를 봅니다.
1. AEM DS 설정을 구성합니다. 다음을 참조하십시오 [AEM DS 설정 구성](../../forms/using/configuring-the-processing-server-url.md).

>[!NOTE]
>
>Forms 또는 AEM 워크플로우를 사용하는 동안 게시 서버에서 제출하기 전에 DS 설정 서비스를 구성해야 합니다. 그렇지 않으면 양식 제출이 실패합니다.

## 편지 인스턴스 검색 {#letter-instances-retrieval}

저장된 편지 인스턴스는 LetterInstanceService에 정의된 다음 API를 사용하여 편지 인스턴스 검색 및 편지 인스턴스 삭제와 같이 추가로 조작할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>서버측 API</strong></td>
   <td><strong>작업 이름</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><p>공개 편지 인스턴스</p> <p>getLetterInstance(문자열 letterInstanceId)</p> <p>ICCException을 throw합니다. </p> </td>
   <td>getLetterInstance</td>
   <td>지정된 문자 인스턴스 가져오기 </td>
  </tr>
  <tr>
   <td>공용 void deleteLetterInstance(String letterInstanceId)에서 ICCException이 발생합니다. </td>
   <td>deleteLetterInstance </td>
   <td>지정한 편지 인스턴스를 삭제했습니다. </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query)에서 ICCException 발생; </td>
   <td>getAllLetterInstances </td>
   <td>이 API는 입력 쿼리 매개 변수를 기반으로 문자 인스턴스를 가져옵니다. 모든 문자 인스턴스를 가져오려면 쿼리 매개 변수를 null로 전달할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>공개 부울 letterInstanceExists(String letterInstanceName)에서 ICCException을 발생시킵니다. </td>
   <td>letter인스턴스 있음 </td>
   <td>지정된 이름으로 LetterInstance가 있는지 확인 </td>
  </tr>
 </tbody>
</table>

## 게시물 프로세스를 편지와 연결 {#associating-a-post-process-with-a-letter}

CCR 사용자 인터페이스에서 다음 단계를 완료하여 POST 프로세스를 문자와 연결합니다.

1. 편지 위에 커서를 놓고 **속성 보기**.
1. **편집**&#x200B;을 선택합니다.
1. 기본 등록 정보에서 사후 프로세스 드롭다운을 사용하여 편지와 연결할 사후 프로세스를 선택합니다. AEM 및 Forms 관련 사후 프로세스가 모두 드롭다운에 나열됩니다.
1. **저장**&#x200B;을 선택합니다.
1. 게시 프로세스를 사용하여 편지를 구성한 후 편지를 게시하고 선택적으로 게시 인스턴스에 AEM DS 설정 서비스에서 처리 URL을 지정합니다. 이렇게 하면 처리 인스턴스에서 사후 프로세스가 실행됩니다.

## 초안 편지 인스턴스 다시 로드  {#reloaddraft}

초안 편지 인스턴스는 다음 URL을 사용하여 사용자 인터페이스에 다시 로드할 수 있습니다.

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstanceID: 제출된 편지 인스턴스의 고유 ID입니다.

초안 편지 저장에 대한 자세한 내용은 [초안 저장 및 편지 인스턴스 제출](../../forms/using/create-correspondence.md#savingdrafts).
