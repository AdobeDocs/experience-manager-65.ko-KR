---
title: 정책으로 보호된 문서에 대한 액세스 권한 제어
description: 정책으로 보호된 문서에 대한 액세스 권한을 보고, 관리하고, 제어하는 방법을 살펴봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 0eb6e769-97c1-41ee-8d12-91bece984947
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '2167'
ht-degree: 100%

---

# 정책으로 보호된 문서에 대한 액세스 권한 제어 {#controlling-access-to-policy-protected-documents}

정책으로 보호된 문서를 아무리 널리 배포하더라도 수신자가 해당 문서를 사용하는 방법을 제어할 수 있습니다.

문서 페이지에서 다음 작업을 수행할 수 있습니다.

* 정책으로 보호된 문서의 세부 정보를 검색하고 확인합니다. 문서 이름, 게시자 이름, 정책 이름, 정책 적용 일자에 대한 정보를 볼 수 있습니다. 문서를 보호하는 정책이 삭제된 경우 정책 이름 아래에서 삭제된 정책 ID를 확인할 수도 있습니다. 사용자는 자체 정책으로 보호된 문서를 보고 관리할 수 있습니다. 관리자는 정책으로 보호된 모든 문서를 보고 관리할 수 있습니다.
* 문서에 적용되는 정책의 세부 정보를 변경합니다. 사용자는 자체 정책을 편집할 수 있고 관리자는 공유 정책과 개인 정책을 편집할 수 있으며 정책 세트 코디네이터는 권한이 있는 정책 세트의 공유 정책을 편집할 수 있습니다. 문서 세부 정보 페이지에서 문서와 연결된 정책에 직접 액세스할 수 있습니다.
* 정책으로 보호된 문서에 대한 액세스 권한을 취소하고 복구합니다. 관리자는 모든 문서에 대한 액세스 권한을 취소하고 복구할 수 있습니다. 문서 관리 권한이 있는 정책 세트 코디네이터는 정책 세트의 공유 정책을 사용하는 정책으로 보호된 문서에 대한 액세스 권한을 취소하고 복구할 수 있습니다. 사용자는 문서를 보호하는 정책을 직접 만들었거나 정책이 해당 기능을 허용하는 공유 정책인 경우 정책으로 보호된 문서에 대한 액세스 권한을 취소할 수 있습니다.
* 문서에 적용되는 정책을 전환합니다. 문서에 정책을 적용하는 사용자는 정책을 직접 만들었거나 정책이 해당 기능을 활성화하는 공유 정책인 경우 정책을 전환할 수 있습니다. 정책 세트 코디네이터는 정책 세트에서 정책을 전환할 수 있습니다. 관리자는 모든 문서에 적용되는 정책을 전환할 수 있습니다.

문서가 정책으로 보호되는 상태에서 액세스 권한을 취소하거나 적용된 정책을 전환하면 변경 사항이 다음과 같이 적용됩니다.

* 문서가 온라인 상태인 경우 사용자가 문서를 열어 두지 않는 한 변경 사항이 즉시 적용됩니다. 이 경우 변경 사항을 적용하려면 사용자가 문서를 닫아야 합니다.
* 수신자가 오프라인(예: 노트북)으로 문서를 사용하는 경우 수신자가 다음에 정책으로 보호된 문서를 열어 문서 보안과 동기화할 때 변경 사항이 적용됩니다.

## 문서 정보 보기 {#view-information-about-a-document}

문서 페이지에 나열된 각 문서에 대해 문서 이름, 게시자 이름, 정책 이름, 문서가 보호된 일자를 확인할 수 있습니다. 문서를 보호하는 정책이 삭제된 경우 정책 ID는 정책 이름 아래에 나열됩니다.

또한 아래에 설명된 대로 특정 문서에 대한 자세한 내용은 문서 세부 정보 페이지에서 볼 수 있습니다.

>[!NOTE]
>
>문서 세부 정보 페이지의 정책 이름 링크를 사용하면 이메일 메시지에 첨부된 문서의 수신자를 위해 Microsoft Outlook에서 자동 생성된 정책에 액세스할 수 있습니다. 해당 정책은 정책 페이지에 나타나지 않습니다.

**문서 이름:** 선택한 문서의 이름입니다.

**문서 ID:** 정책이 문서에 적용될 때 문서 보안에서 할당하는 고유 식별자입니다. 문서 보안은 이 번호를 사용하여 문서를 추적합니다.

**문서 상태:** 문서 상태(예: 활성 또는 취소됨)입니다.

**게시자:** 문서에 정책을 첨부한 사용자 이름입니다.

**정책 이름:** 문서를 보호하는 데 사용되는 정책 이름입니다. 이름을 클릭하면 정책을 열 수 있습니다. 이 링크를 사용하면 Outlook의 이메일 메시지에 첨부된 문서 수신자를 위해 Acrobat에서 생성하는 정책에 액세스할 수 있습니다. 해당 정책은 정책 페이지에 나타나지 않습니다.

**정책 유형:** 문서에 적용된 정책 유형입니다.

**게시 일자:** 정책이 문서에 적용된 일자입니다.

**관련 반복:** 문서에 관련 반복이 있는 경우 이 항목도 목록에 나타납니다. 이 링크를 클릭하면 해당 문서의 관련 반복 목록을 볼 수 있습니다.

사용자는 보호된 문서에 대한 정보를 볼 수 있습니다. 관리자는 사용자가 정책으로 보호한 문서에 대한 정보를 볼 수 있습니다. 정책 세트 코디네이터는 자체 정책 세트에서 정책으로 보호되는 문서에 대한 정보를 볼 수 있습니다.

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 문서 목록에서 해당 문서를 클릭합니다. 문서 세부 정보 페이지가 열리고 문서에 대한 자세한 정보가 표시됩니다. 이 페이지에서는 문서 액세스 권한 취소, 정책 전환, 해당 문서와 관련된 이벤트 보기에 대한 옵션도 제공합니다.

## 문서에 대한 관련 반복 보기 {#view-related-iterations-for-a-document}

관련 반복 추적이 활성화된 경우 다양한 사용자가 저장한 문서 버전을 추적할 수 있습니다. 이 기능은 PTC Pro/ENGINEER Wildfire와 같은 특정 애플리케이션에서만 지원됩니다.

이 기능은 여러 사용자가 공동 작업하여 동일한 문서의 여러 버전을 저장할 때 유용합니다. 문서 보안을 통해 다양한 반복을 추적할 수 있으므로 다양한 버전에 대한 문서 정보를 쉽게 볼 수 있습니다.

이 기능을 활성화하면 문서 페이지에서 문서의 관련 반복을 볼 수 있습니다.

1. 문서의 문서 세부 정보 페이지를 봅니다. ([문서 정보 보기](controlling-access-policy-protected-documents.md#view-information-about-a-document)를 참조하십시오.)
1. 관련 반복 보기를 클릭합니다. 이 옵션은 해당 기능이 활성화되어 있는 경우에만 사용할 수 있습니다. 관련 반복 목록이 나타납니다. 각 반복에 대해 다음 정보를 볼 수 있습니다.

   * **반복:** 파일 이름입니다. 원래 파일 이름과 다를 수 있으며 파일 이름 끝에 버전 번호가 추가됩니다.
   * **게시자:** 원본 문서의 게시자입니다.
   * **만든 사람:** 반복을 저장한 사용자입니다.
   * **만든 일자:** 반복이 저장된 일자 및 시간입니다.
   * **정책:** 반복을 보호하는 정책입니다. 각 반복은 각기 다른 정책으로 보호될 수 있습니다.

1. 해당 반복의 문서 세부 정보 페이지를 표시하려면 반복의 파일 이름을 클릭합니다.

## 문서에 대한 액세스 권한 취소 및 복구 {#revoking-and-reinstating-access-to-documents}

정책으로 보호된 문서에 대한 액세스 권한을 취소하고 복구할 수 있습니다.

**사용자:** 자체 개인 정책이나 정책을 적용하는 사용자에 대해 취소 기능이 활성화된 공유 정책으로 보호하는 문서에 대한 액세스 권한을 취소하거나 복구할 수 있습니다. 문서에 대한 액세스 권한을 취소하거나 정책을 전환할 수 없는 사용자는 관리자에게 문의해야 합니다.

**관리자:** 개인 정책 또는 공유 정책으로 보호되는 문서를 포함하여 정책으로 보호된 모든 문서에 대한 액세스 권한을 취소하거나 복구할 수 있습니다. 관리자가 공유 정책으로 보호되는 문서에 대한 액세스 권한을 취소하는 경우 관리자만이 해당 문서에 대한 액세스 권한을 복구할 수 있습니다.

**정책 세트 코디네이터:** 정책 세트의 정책으로 보호하는 문서에 대한 액세스 권한을 취소하거나 복구할 수 있습니다.

문서 액세스 권한을 취소하거나 복구하면 변경 사항은 다음 시점에 적용됩니다.

* 문서가 온라인 상태이고 닫혀 있는 경우 수신자가 다음에 정책으로 보호된 문서를 열어 문서 보안과 동기화할 때 변경 사항이 적용됩니다.
* 문서가 온라인 상태이고 열려 있는 경우 수신자가 문서를 닫으면 변경 사항이 적용됩니다.
* 인터넷에 연결되지 않은 상태(예: 노트북)에서 사용하는 것과 같이 문서가 오프라인 상태인 경우 수신자가 다음에 문서 보안과 동기화할 때 변경 사항이 적용됩니다.

**정책으로 보호된 문서에 대한 액세스 권한 취소**

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 해당 문서 옆에 있는 확인란을 선택하고 취소를 클릭합니다. 한 번에 여러 문서에 대한 액세스 권한을 취소할 수 있습니다.
1. 문서가 취소된 후 해당 문서를 열려고 시도하는 사용자에게 표시할 메시지를 선택합니다.

   * **일반 메시지:** 작성자가 문서를 취소했음을 나타냅니다.
   * **문서가 종료됨:** 작성자가 문서를 종료했음을 나타냅니다.
   * **문서가 수정됨**: 작성자가 문서를 수정했음을 나타냅니다.

1. (선택 사항) 문서의 최신 버전이 있는 경우 URL을 입력하고 테스트를 클릭하여 URL을 확인합니다.
1. 확인을 클릭한 후 다시 확인을 클릭하여 문서 페이지로 돌아갑니다.

**문서 액세스 권한 복구**

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 문서 목록에서 해당 문서를 클릭합니다.
1. 취소 해제를 클릭한 후 확인을 클릭합니다.

## 문서에 적용되는 정책 전환 {#switch-a-policy-that-is-applied-to-a-document}

사용자, 정책 세트 코디네이터 및 관리자는 정책으로 보호된 문서에 적용되는 정책을 전환할 수 있습니다(한 번에 하나의 정책만 문서에 적용할 수 있습니다). 사용자는 정책을 직접 만들었거나 정책이 해당 기능이 활성화된 공유 정책인 경우 자체 정책으로 보호된 문서에 적용되는 정책을 전환할 수 있습니다. 그렇지 않으면 관리자 또는 정책 세트 코디네이터가 정책을 전환해야 합니다. 관리자는 모든 사용자의 정책으로 보호된 문서에 대한 정책을 전환할 수 있습니다. 정책 세트 코디네이터는 정책 세트에서 정책을 전환할 수 있습니다.

정책을 전환하면 새 정책이 다음과 같이 적용됩니다.

* 문서가 온라인 상태이고 닫혀 있는 경우 수신자가 다음에 정책으로 보호된 문서를 온라인에서 열어 문서 보안과 동기화할 때 변경 사항이 적용됩니다.
* 문서가 온라인 상태이고 열려 있는 경우 사용자가 문서를 닫으면 변경 사항이 적용됩니다.
* 활성 인터넷이나 네트워크에 연결되지 않은 상태(예: 노트북)에서 사용하는 것과 같이 문서가 오프라인 상태 경우 사용자가 다음에 정책으로 보호된 문서를 온라인에서 열어 문서 보안과 동기화할 때 변경 사항이 적용됩니다.

>[!NOTE]
>
>현재 익명 액세스 권한이 없는 정책으로 보호된 문서에 익명으로 액세스할 수 있도록 허용하려면 클라이언트 애플리케이션에서 기존 정책을 제거한 후 익명 액세스를 허용하는 정책을 적용하십시오. 정책을 전환하는 경우에도 사용자가 여전히 문서에 액세스하려면 로그인해야 합니다.

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 문서 목록에서 해당 문서를 클릭합니다.
1. 정책 전환을 클릭합니다. 최대 100개의 정책 목록이 나타납니다.
1. 원하는 정책이 표시되지 않으면 찾기 목록에서 정책 이름이나 정책 ID를 선택하고 이름이나 ID를 입력한 후 찾기를 클릭합니다.
1. 목록에서 새 정책을 클릭합니다.
1. 정책 전환을 클릭한 후 확인을 클릭하여 문서 페이지로 돌아갑니다.

## 문서 검색 {#search-for-a-document}

목록에서 제공되는 일자 범위 기준과 검색 기준을 조합하여 문서 페이지에서 문서를 검색할 수 있습니다. 이러한 기준에는 문서 이름, 정책 이름 또는 모든 문서가 포함됩니다.

일부 추가 검색 옵션은 관리자에게만 제공됩니다.

**문서 ID:** 정책이 적용될 때 문서 보안에서 문서에 할당하는 고유 ID 번호입니다.

**문서 이름:** 문서 이름입니다.

**게시자 이름:** 문서에 정책을 첨부한 사용자 이름입니다. 모든 도메인 또는 지정된 도메인에서 사용자를 선택할 수 있습니다.

**정책 ID:** 문서에 첨부된 정책의 ID 번호입니다.

**정책 이름:** 문서에 첨부된 정책 이름입니다.

**모든 문서:** 모든 문서는 관리자와 사용자가 보호합니다. 모든 문서 옵션을 사용하여 검색하면 긴 문서 목록이 반환될 수도 있습니다.

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 찾기 목록에서 필요한 검색 기준을 선택합니다.

   검색 기준을 문서 ID, 문서 이름, 게시자 이름, 정책 ID, 정책 이름 또는 모든 문서로 지정할 수 있습니다.

   게시자 이름을 지정하는 경우 주소록 아이콘을 클릭하고 사용자를 검색할 도메인을 지정한 후 확인을 클릭하여 문서 검색 페이지로 돌아갑니다.

1. (선택 사항) 일자 목록에서 일자 범위 옵션을 선택합니다. 사용자 정의 일자를 선택하는 경우 표시되는 상자에 yyyy/mm/dd 형식으로 일자를 입력하거나 날짜 선택기를 사용하여 일자 범위를 지정합니다.

   * 캘린더를 클릭하여 날짜 선택기를 엽니다.
   * 화살표를 사용하여 연도와 월을 찾습니다.
   * 캘린더에서 해당 월의 날짜를 클릭합니다.
   * 확인을 클릭하여 날짜 선택기를 닫습니다.

1. 찾기를 클릭합니다.

## 문서 목록 정렬 {#sort-the-document-list}

문서 목록을 열 제목별로 정렬할 수 있습니다. 열 제목 옆에 있는 삼각형 아이콘은 현재 정렬에 사용된 열을 나타냅니다. 위를 가리키는 삼각형은 오름차순을 나타내고 아래를 가리키는 삼각형은 내림차순을 나타냅니다.

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 해당 열 제목을 클릭합니다.
1. 정렬 순서를 변경하려면 열을 다시 클릭합니다.

## 정책으로 보호된 문서에 표지 추가 {#add-cover-page-to-policy-protected-documents}

Adobe가 아닌 PDF 뷰어를 사용하는 경우 문서 보안으로 보호된 문서를 열면 첫 페이지가 빈 페이지로 표시되거나 애플리케이션이 문서를 열지 않고 중단됩니다.

0페이지(래퍼 문서) 지원을 사용하면 Adobe가 아닌 PDF 뷰어에서 보호된 문서를 열고 문서에 표지를 표시할 수 있습니다.

>[!NOTE]
>
>Adobe Reader/Acrobat 또는 Mobile Reader에서 해당 문서(0페이지 포함)를 볼 때 기본적으로 보호된 문서가 열립니다.

**정책으로 보호된 문서에 표지를 추가하는 방법**

워크벤치에서 다음 프로세스를 사용합니다.

**표지가
포함된 문서 보호:** 지정된 정책으로 PDF 문서를 보호하고 문서에 표지를 추가합니다.

**보호된 문서 추출:** 표지가 포함된 PDF 문서에서 정책으로 보호된 PDF 문서를 추출합니다.

다음과 같은 문서 보안 API를 사용합니다.

**protectDocumentWithCoverPage:** 지정된 정책으로 특정 PDF를 보호하고 표지와 보호된 문서가 첨부 파일로 포함된 문서를 반환합니다. 
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument:** 표지가 포함된 문서의 첨부 파일인 보호된 문서를 추출합니다. 표지가 포함된 문서는 protectDocumentWithCoverPage 메서드를 사용하여 만들 수 있습니다.
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`
