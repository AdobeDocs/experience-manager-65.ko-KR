---
title: 정책으로 보호된 문서에 대한 액세스 제어
seo-title: 정책으로 보호된 문서에 대한 액세스 제어
description: 정책으로 보호된 문서에 대한 액세스를 보고, 관리하고 제어하는 방법을 살펴봅니다.
seo-description: 정책으로 보호된 문서에 대한 액세스를 보고, 관리하고 제어하는 방법을 살펴봅니다.
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
feature: 문서 보안
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2190'
ht-degree: 0%

---


# 정책으로 보호된 문서 {#controlling-access-to-policy-protected-documents} 액세스 제어

배포 범위에 관계없이 받는 사람이 정책으로 보호된 문서를 사용하는 방법을 제어할 수 있습니다.

문서 페이지에서는 다음 작업을 수행할 수 있습니다.

* 정책으로 보호된 문서의 세부 정보를 검색하고 볼 수 있습니다. 문서 이름, 게시자 이름, 정책 이름 및 정책이 적용된 날짜에 대한 정보를 볼 수 있습니다. 문서를 보호하는 정책이 삭제되면 정책 이름 아래에 삭제된 정책 ID도 볼 수 있습니다. 사용자는 정책으로 보호된 문서를 보고 관리할 수 있습니다. 관리자는 정책으로 보호된 모든 문서를 보고 관리할 수 있습니다.
* 문서에 적용되는 정책의 세부 사항을 변경합니다. 사용자는 자신의 정책을 편집하고, 관리자는 공유 및 개인 정책을 편집할 수 있으며, 정책 집합 코디네이터는 권한이 있는 정책 집합에서 공유 정책을 편집할 수 있습니다. 문서 세부 정보 페이지에서 문서와 연결된 정책에 직접 액세스할 수 있습니다.
* 정책으로 보호된 문서에 대한 액세스 권한을 취소하거나 복원합니다. 관리자는 모든 문서에 대한 액세스 권한을 취소하거나 회복할 수 있습니다. 정책 집합 코디네이터(문서 관리 권한이 있는 사람)는 정책 집합에서 공유 정책을 사용하는 정책으로 보호된 문서에 대한 액세스를 취소하거나 회복할 수 있습니다. 사용자가 문서를 보호하는 정책을 만들었거나 정책이 이 기능을 허용하는 공유 문서인 경우 정책으로 보호된 문서에 대한 액세스를 취소할 수 있습니다.
* 문서에 적용되는 정책을 전환합니다. 문서에 정책을 적용하는 사용자는 정책을 만든 경우 또는 이 기능을 활성화하는 공유 정책인 경우 정책을 전환할 수 있습니다. 정책 집합 코디네이터는 정책 집합에서 정책을 전환할 수 있습니다. 관리자는 문서에 적용되는 정책을 전환할 수 있습니다.

문서가 정책으로 보호되고 액세스 권한을 취소하거나 적용된 정책을 전환하면 변경 내용이 다음과 같이 적용됩니다.

* 문서가 온라인 상태인 경우 사용자가 문서를 열지 않은 즉시 변경 내용이 적용됩니다. 이 경우 변경 사항을 적용하려면 문서를 닫아야 합니다.
* 받는 사람이 오프라인으로 문서를 사용하는 경우(예: 랩탑에서), 이 변경 사항은 받는 사람이 정책으로 보호된 문서를 열어 문서 보안과 동기화하면 이후에 적용됩니다.

## 문서 {#view-information-about-a-document} 정보 보기

문서 페이지에 나열되는 각 문서에 대해 문서 이름, 발행자 이름, 정책 이름 및 문서가 보호된 날짜를 볼 수 있습니다. 문서를 보호하는 정책이 삭제되면 정책 이름 아래에 정책 ID가 나열됩니다.

문서 세부 정보 페이지에서 아래에 설명된 특정 문서에 대한 자세한 내용을 볼 수도 있습니다.

>[!NOTE]
>
>전자 메일 메시지에 첨부된 문서의 수신자를 위해 Microsoft Outlook에서 자동으로 생성된 정책에 액세스하려면 [문서 세부 사항] 페이지의 [정책 이름] 링크를 사용해야 합니다. 이러한 정책은 정책 페이지에 나타나지 않습니다.

**문서 이름:** 선택한 문서의 이름입니다.

**문서 ID:** 정책이 문서에 적용될 때 문서 보안이 지정하는 고유 식별자입니다. document security에서는 이 숫자를 사용하여 문서를 추적합니다.

**문서 상태:** 문서의 상태(예: 활성 또는 해지됨).

**게시자:** 문서에 정책을 첨부한 사용자의 이름입니다.

**정책 이름:** 문서를 보호하는 데 사용되는 정책의 이름입니다. 이름을 클릭하여 정책을 열 수 있습니다. Outlook의 전자 메일 메시지에 첨부된 문서의 수신자를 위해 Acrobat에서 생성하는 정책에 액세스하려면 이 링크를 사용해야 합니다. 이러한 정책은 정책 페이지에 나타나지 않습니다.

**정책 유형:** 문서에 적용된 정책 유형입니다.

**게시된 날짜:** 정책이 문서에 적용된 날짜입니다.

**관련 반복: 문서에 관련 반복이** 있는 경우 이 항목도 목록에 표시됩니다. 문서에 대한 관련 반복 목록을 보려면 링크를 클릭합니다.

사용자는 보호된 문서에 대한 정보를 볼 수 있습니다. 관리자는 정책으로 보호된 모든 사용자가 문서에 대한 정보를 볼 수 있습니다. 정책 집합 코디네이터는 정책 집합에서 정책으로 보호된 문서에 대한 정보를 볼 수 있습니다.

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 문서 목록에서 해당 문서를 클릭합니다. 문서에 대한 세부 정보를 표시하는 [문서 세부 사항] 페이지가 열립니다. 또한 이 페이지에서는 문서 액세스를 취소하고, 정책을 전환하고, 이 문서와 관련된 이벤트를 볼 수 있는 옵션도 제공합니다.

## 문서 {#view-related-iterations-for-a-document} 관련 반복 보기

관련 반복 추적이 활성화되면 다양한 사용자가 저장한 문서의 버전을 추적할 수 있습니다. 이 기능은 PTC Pro/ENGINEER Wildfire와 같은 특정 응용 프로그램에서만 지원됩니다.

이 기능은 여러 사용자가 공동 작업하고 동일한 문서의 다른 버전을 저장하는 경우에 유용합니다. 문서 보안은 다양한 반복을 추적할 수 있습니다.따라서 다른 버전에 대한 문서 정보를 쉽게 볼 수 있습니다.

이 기능이 활성화되어 있으면 문서 페이지에서 관련 반복을 볼 수 있습니다.

1. 문서의 문서 세부 정보 페이지를 봅니다. 자세한 내용은 [문서](controlling-access-policy-protected-documents.md#view-information-about-a-document)에 대한 정보 보기를 참조하십시오.
1. 관련 반복 보기를 클릭합니다. 이 옵션은 해당 기능이 활성화된 경우에만 사용할 수 있습니다. 관련 반복 목록이 나타납니다. 각 반복에 대해 다음 정보를 볼 수 있습니다.

   * **반복:** 파일 이름입니다. 원래 파일 이름과 다를 수 있으며 끝에 버전 번호가 추가됩니다.
   * **게시자:** 원본 문서의 게시자입니다.
   * **작성자:** 반복을 저장한 사용자입니다.
   * **작성일:** 반복이 저장된 날짜 및 시간입니다.
   * **정책:** 반복을 보호하는 정책입니다. 서로 다른 반복은 다른 정책에 의해 보호될 수 있습니다.

1. 해당 이터레이션에 대한 문서 세부 정보 페이지를 표시하려면 이터레이션의 파일 이름을 클릭합니다.

## 문서 {#revoking-and-reinstating-access-to-documents} 액세스 취소 및 재개

정책으로 보호된 문서에 대한 액세스 권한을 취소하거나 회복할 수 있습니다.

**사용자: 정책을 적용하는 사용자에 대해 취소 기능이 활성화된 공유 정책 또는 개인 정책으로 보호된 문서에 대한 액세스를 취소하거나 회복할** 수 있습니다. 문서에 대한 액세스 권한을 취소하거나 정책을 전환할 수 없는 사용자는 관리자에게 문의해야 합니다.

**관리자:개인 또는 공유 정책으로 보호된 문서를 비롯하여 정책으로 보호된 문서에 대한 액세스 권한을 취소하거나 회복할** 수 있습니다. 관리자가 공유 정책으로 보호된 문서에 대한 액세스를 폐지하면 관리자만 해당 문서에 대한 액세스 권한을 복원할 수 있습니다.

**정책 집합 코디네이터: 정책 집합에서 보호하는 문서에 대한 액세스 권한을 취소하거나 회복할** 수 있습니다.

문서 액세스 권한을 취소하거나 복귀하면 다음과 같은 시간에 변경 사항이 적용됩니다.

* 문서가 온라인 상태이고 닫혀 있으면 받는 사람이 정책으로 보호된 문서를 열어 문서 보안과 동기화하면 변경 내용이 적용됩니다.
* 문서가 온라인 상태이고 열려 있으면 받는 사람이 문서를 닫을 때 변경 사항이 적용됩니다.
* 문서가 오프라인 상태인 경우(랩탑과 같이 인터넷에 연결되지 않은 상태로 사용) 수신자가 다음에 문서 보안과 동기화될 때 변경 내용이 적용됩니다.

**정책으로 보호된 문서에 대한 액세스 취소**

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 해당 문서 옆의 확인란을 선택하고 취소를 클릭합니다. 한 번에 여러 문서에 대한 액세스를 취소할 수 있습니다.
1. 해지된 후 문서를 열려고 하는 사용자에게 표시할 메시지를 선택합니다.

   * **일반 메시지:** 작성자가 문서를 해지했음을 나타냅니다.
   * **문서 종료됨:** 작성자가 문서를 종료했음을 나타냅니다.
   * **수정된 문서**:작성자가 문서를 수정했음을 나타냅니다.

1. (선택 사항) 새 버전의 문서를 사용할 수 있는 경우 URL을 입력하고 [테스트]를 클릭하여 URL을 확인합니다.
1. 확인을 클릭한 다음 확인을 다시 클릭하여 문서 페이지로 돌아갑니다.

**문서 액세스 권한 복원**

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 문서 목록에서 해당 문서를 클릭합니다.
1. 취소 해제를 클릭한 다음 확인을 클릭합니다.

## 문서 {#switch-a-policy-that-is-applied-to-a-document}에 적용되는 정책 전환

사용자, 정책 집합 코디네이터 및 관리자는 정책으로 보호된 문서에 적용되는 정책을 전환할 수 있습니다. 한 번에 하나의 정책만 문서에 적용할 수 있습니다. 사용자가 정책을 만들었거나 정책이 이 기능이 활성화된 공유 문서인 경우 정책으로 보호된 문서에 적용되는 정책을 전환할 수 있습니다. 그렇지 않으면 관리자 또는 정책 집합 코디네이터가 정책을 전환해야 합니다. 관리자는 사용자의 정책으로 보호된 문서에 대한 정책을 전환할 수 있습니다. 정책 집합 코디네이터는 정책 집합에서 정책을 전환할 수 있습니다.

정책을 전환하면 다음과 같이 새 정책이 적용됩니다.

* 문서가 온라인 상태이고 닫힌 경우, 받는 사람이 정책으로 보호된 문서를 온라인으로 열어 문서 보안과 동기화하면 변경 내용이 적용됩니다.
* 문서가 온라인 상태이고 열려 있으면 사용자가 문서를 닫으면 변경 사항이 적용됩니다.
* 문서가 오프라인 상태인 경우(랩탑과 같이 인터넷에 활성 연결이나 네트워크 연결 없이 사용), 사용자가 정책으로 보호된 문서를 온라인으로 열어 다음에 문서 보안과 동기화하면 변경 내용이 적용됩니다.

>[!NOTE]
>
>현재 이 액세스 권한이 없는 정책으로 보호된 문서에 대한 익명 액세스를 허용하려면 클라이언트 응용 프로그램에서 기존 정책을 제거한 다음 익명 액세스를 허용하는 정책을 적용합니다. 정책을 전환하더라도 사용자가 문서에 액세스하려면 여전히 로그인해야 합니다.

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 문서 목록에서 해당 문서를 클릭합니다.
1. 정책 전환을 클릭합니다. 최대 100개의 정책 목록이 표시됩니다.
1. 원하는 정책이 표시되지 않으면 찾기 목록에서 정책 이름 또는 정책 ID를 선택하고 이름 또는 ID를 입력한 다음 찾기를 클릭합니다.
1. 목록에서 새 정책을 클릭합니다.
1. 정책 전환을 클릭한 다음 확인을 클릭하여 문서 페이지로 돌아갑니다.

## 문서 {#search-for-a-document} 검색

목록에서 사용할 수 있는 날짜 범위 기준 및 검색 기준의 조합을 사용하여 문서 페이지에서 문서를 검색할 수 있습니다. 이러한 기준에는 문서 이름, 정책 이름 또는 모든 문서가 포함됩니다.

일부 추가 검색 옵션은 관리자만 사용할 수 있습니다.

**문서 ID:** 정책이 적용될 때 문서 보안이 문서에 할당하는 고유 ID 번호입니다.

**문서 이름:** 문서의 이름입니다.

**게시자 이름:** 문서에 정책을 첨부한 사용자의 이름입니다. 모든 도메인 또는 지정된 도메인에서 사용자를 선택할 수 있습니다.

**정책 ID:** 문서에 첨부된 정책의 ID 번호입니다.

**정책 이름:** 문서에 첨부된 정책의 이름입니다.

**모든 문서:** 관리자 및 사용자가 보호하는 모든 문서. 모든 문서 옵션을 사용하여 검색하면 긴 문서 목록이 반환됩니다.

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 찾기 목록에서 필요한 검색 기준을 선택합니다.

   문서 ID, 문서 이름, 게시자 이름, 정책 ID, 정책 이름 또는 모든 문서와 같은 기준을 지정할 수 있습니다.

   게시자 이름을 지정하는 경우 주소록 아이콘을 클릭하고 사용자를 검색할 도메인을 지정하고 확인을 클릭하여 문서 검색 페이지로 돌아갑니다.

1. (선택 사항) 날짜 목록에서 날짜 범위 옵션을 선택합니다. 사용자 지정 날짜를 선택하는 경우 나타나는 상자에 yyy/mm/dd 형식으로 날짜를 입력하거나 날짜 선택기를 사용하여 날짜 범위를 지정합니다.

   * 달력을 클릭하여 날짜 선택기를 엽니다.
   * 연도 및 월을 찾으려면 화살표를 사용합니다.
   * 달력에서 날짜를 클릭합니다.
   * 확인을 클릭하여 날짜 선택기를 닫습니다.

1. 찾기를 클릭합니다.

## 문서 목록 정렬 {#sort-the-document-list}

열 제목별로 문서 목록을 정렬할 수 있습니다. 열 머리글 옆에 있는 삼각형 아이콘은 현재 정렬에 사용되는 열을 나타냅니다. 위쪽 포인팅 삼각형은 오름차순으로, 아래쪽 삼각형은 내림차순으로 나타냅니다.

1. 문서 보안 페이지에서 문서를 클릭합니다.
1. 적절한 열 머리글을 클릭합니다.
1. 정렬 순서를 변경하려면 열을 다시 클릭합니다.

## 보호된 문서 {#add-cover-page-to-policy-protected-documents}에 표지 페이지 추가

Adobe PDF 뷰어가 아닌 대부분의 경우 문서 보안 문서를 열면 첫 번째 페이지가 빈 페이지로 표시되거나 문서를 열지 않고 응용 프로그램이 중단됩니다.

0페이지(래퍼 문서) 지원을 사용하여 Adobe PDF이 아닌 뷰어가 보호된 문서를 열고 문서의 표지 페이지를 표시할 수 있습니다.

>[!NOTE]
>
>Adobe Reader/Acrobat 또는 모바일 Reader에서 이러한 문서(페이지 0 포함)를 볼 때 보호된 문서는 기본적으로 열립니다.

**정책으로 보호된 문서에 표지 페이지를 추가하려면**

워크벤치에서 다음 프로세스를 사용하십시오.

**표지 페이지가 있는 Protect 문서:** 지정된 정책으로 PDF 문서를 보호하고 문서에 표지 페이지를 추가합니다.

**보호된 문서 추출:** 표지 페이지를 사용하여 PDF 문서에서 정책으로 보호된 PDF 문서를 추출합니다.

다음 문서 보안 API를 사용하십시오.

**protectDocumentWithCoverPage: 지정된 정책으로 지정된 PDF를** 보호하고, 표지 페이지와 보호된 문서를 첨부 파일 
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument:표지 페이지가 있는 문서의 첨부 문서인 보호된 문서를** 추출합니다. 표지 페이지가 있는 문서는 protectDocumentWithCoverPage 메서드를 사용하여 만들 수 있습니다
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`