---
title: 서신 및 인터랙티브한 커뮤니케이션의 게시 처리
seo-title: 편지 게시
description: 통신 관리에서 편지 게시 처리를 사용하면 인쇄 및 이메일과 같은 AEM 및 양식 게시물 프로세스를 만들고 이를 문자와 통합할 수 있습니다.
seo-description: 통신 관리에서 편지 게시 처리를 사용하면 인쇄 및 이메일과 같은 AEM 및 양식 게시물 프로세스를 만들고 이를 문자와 통합할 수 있습니다.
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 서신 및 인터랙티브한 커뮤니케이션의 게시 처리{#post-processing-of-letters-and-interactive-communications}

## 사후 처리 {#post-processing}

에이전트는 문자 및 인터랙티브한 커뮤니케이션에 포스트 처리 워크플로우를 연결하고 실행할 수 있습니다. 실행할 게시 프로세스는 편지 템플릿의 속성 보기에서 선택할 수 있습니다. 최종 편지를 이메일, 인쇄, 팩스 또는 보관하도록 게시 프로세스를 설정할 수 있습니다.

![사후 처리](assets/ppoverview.png)

게시물 프로세스를 편지 또는 대화형 통신과 연결하려면 먼저 게시물 프로세스를 설정해야 합니다. 제출된 편지에서는 두 가지 유형의 워크플로우를 실행할 수 있습니다.

1. **** 양식 워크플로우:다음은 JEE 프로세스 관리 워크플로우의 AEM 양식입니다. 양식 워크플로우 설정 [지침](../../forms/using/submit-letter-topostprocess.md#main-pars-header-3).

1. **** AEM 워크플로우:AEM 워크플로우는 제출된 서신의 게시 프로세스로 사용할 수도 있습니다. AEM Workflow 설정 [지침](../../forms/using/aem-forms-workflow.md).

## 양식 워크플로우 {#formsworkflow}

1. AEM에서 다음 URL을 사용하여 서버에 대한 Adobe Experience Manager 웹 콘솔 구성을 엽니다. `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![구성 관리자](assets/2configmanager-1.png)

1. 이 페이지에서 AEM Forms 클라이언트 SDK 구성을 찾아 클릭하여 확장합니다.
1. 서버 URL에서 JEE 서버에 있는 AEM Forms 이름과 로그인 세부 정보를 입력한 다음 저장을 **클릭합니다**.

   ![LiveCycle 서버 이름 입력](assets/1cofigmanager.png)

1. 사용자 이름과 암호를 지정합니다.
1. sun.util.calendar가 Deserialization Firewall Configuration에 추가되었는지 확인합니다.

   Deserialization Firewall Configuration으로 이동하여 패키지 접두사의 Whitellited 클래스에서 sun.util.calendar를 추가합니다.

1. 이제 서버가 매핑되고 JEE의 AEM Forms에서 게시물 프로세스를 AEM 사용자 인터페이스에서 문자를 만들 수 있습니다.

   ![게시물 프로세스가 나열된 편지 화면 만들기](assets/0configmanager.png)

1. 프로세스/서비스를 인증하려면 프로세스 이름을 복사하고 Adobe Experience Manager 웹 콘솔 구성 페이지 > AEM Forms 클라이언트 SDK 구성으로 돌아가서 프로세스를 새 서비스로 추가합니다.

   예를 들어, 문자의 속성 페이지의 드롭다운에 프로세스 이름이 양식 워크플로우 -> ValidCCPostProcess/SaveXML로 표시되면 서비스 이름을 다른 이름으로 추가합니다 `ValidCCPostProcess/SaveXML`.

1. 사후 처리를 위해 JEE 워크플로우에서 AEM Forms를 사용하려면 필요한 매개 변수 및 출력을 설정하십시오. 매개 변수의 기본값은 아래에 표시됩니다.

   Adobe Experience Manager 웹 콘솔 구성 페이지 > 통신 **[!UICONTROL 관리 구성으로]** 이동하여 다음 매개 변수를 설정합니다.

   1. **** inPDFoc(PDF 문서 매개 변수):입력으로 PDF 문서 이 입력에는 렌더링된 문자가 입력으로 포함됩니다. 표시된 매개 변수 이름은 구성할 수 있습니다. 통신 관리 구성을 구성에서 구성할 수 있습니다.
   1. **** inXMLDoc(XML 데이터 매개 변수):입력으로 XML 문서 이 입력에는 사용자가 XML 형식으로 입력한 데이터가 포함됩니다.
   1. **** inXDPDoc(XDP 문서 매개 변수):입력으로 XML 문서 이 입력에는 기본 레이아웃(XDP)이 포함되어 있습니다.
   1. **** inAttachmentDocs(첨부 문서 매개 변수):목록 입력 매개 변수입니다. 이 입력에는 모든 첨부 파일이 입력으로 포함됩니다.
   1. **** redirectURL(리디렉션 URL 출력):리디렉션할 URL을 나타내는 출력 유형입니다.
   양식 워크플로우에는 PDF 문서 매개 변수 또는 XML 데이터 매개 변수가 입력 관리 구성에 지정된 것과 동일한 이름의 **[!UICONTROL 입력이어야 합니다]**. 게시 프로세스 드롭다운에 나열되는 프로세스에 필요합니다.

## 게시 인스턴스의 설정 {#settings-on-the-publish-instance}

1. 에 `https://localhost:publishport/aem/forms`로그인합니다.
1. Letters **[!UICONTROL 로]** 이동하여 게시 인스턴스에서 사용할 수 있는 게시된 문자를 봅니다.
1. AEM DS 설정을 구성합니다. AEM [DS 설정](../../forms/using/configuring-the-processing-server-url-.md)구성을 참조하십시오.

>[!NOTE]
>
>양식 또는 AEM 작업 과정을 사용하는 동안 게시 서버에서 제출하기 전에 DS 설정 서비스를 구성해야 합니다. 그렇지 않으면 양식 제출이 실패합니다.

## 편지 인스턴스 검색 {#letter-instances-retrieval}

LetterInstanceService에 정의된 다음 API를 사용하여 편지 인스턴스 검색 및 문자 인스턴스 삭제와 같은 저장된 문자 인스턴스를 추가로 조작할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>서버측 API</strong></td>
   <td><strong>작업 이름</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><p>Public LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>ICCE 파섹 </p> </td>
   <td>getLetterInstance</td>
   <td>지정된 문자 인스턴스 가져오기 </td>
  </tr>
  <tr>
   <td>public void deleteLetterInstance(String letterInstanceId)는 ICCException을 던집니다. </td>
   <td>deleteLetterInstance </td>
   <td>지정된 문자 인스턴스를 삭제했습니다. </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query)는 ICCException을 발생시킵니다. </td>
   <td>getAllLetterInstances </td>
   <td>이 API는 입력 쿼리 매개 변수를 기반으로 문자 인스턴스를 가져옵니다. 모든 문자 인스턴스를 가져오려면 쿼리 매개 변수를 null로 전달할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>공용 부울 문자 InstanceExists(String letterInstanceName)는 ICCException;을 throw합니다. </td>
   <td>letterInstanceExists </td>
   <td>LetterInstance가 지정된 이름으로 존재하는지 확인 </td>
  </tr>
 </tbody>
</table>

## 게시물 프로세스와 편지 연결 {#associating-a-post-process-with-a-letter}

CCR 사용자 인터페이스에서 다음 단계를 완료하여 게시물 프로세스를 서신과 연결합니다.

1. 편지 위로 마우스를 가져간 다음 속성 보기를 **누릅니다**.
1. **편집**&#x200B;을 선택하십시오.
1. 기본 속성에서 게시물 프로세스 드롭다운을 사용하여 글자와 연결할 게시물 프로세스를 선택합니다. AEM 및 양식 관련 게시 프로세스가 모두 드롭다운에 나열됩니다.
1. 저장을 **누릅니다**.
1. 게시물 프로세스로 문자를 구성한 후, 편지를 게시하고 선택적으로 게시 인스턴스에서 AEM DS 설정 서비스에서 처리 URL을 지정합니다. 이렇게 하면 게시 프로세스가 처리 인스턴스에서 실행됩니다.

## 초안 편지 인스턴스 다시 로드 {#reloaddraft}

다음 URL을 사용하여 사용자 인터페이스에서 초안 문자 인스턴스를 다시 로드할 수 있습니다.

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstaceID:제출된 편지 인스턴스의 고유 ID입니다.

초안 편지 저장에 대한 자세한 내용은 초안 저장 및 [편지 인스턴스](../../forms/using/create-correspondence.md#savingdrafts)제출을 참조하십시오.
