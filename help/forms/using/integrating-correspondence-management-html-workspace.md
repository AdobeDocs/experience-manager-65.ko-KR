---
title: AEM Forms 작업 영역에서 타사 애플리케이션 통합
seo-title: AEM Forms 작업 영역에서 타사 애플리케이션 통합
description: AEM Forms 작업 영역의 통신 관리와 같은 타사 애플리케이션을 통합할 수 있습니다.
seo-description: AEM Forms 작업 영역의 통신 관리와 같은 타사 앱을 통합하는 방법.
uuid: 7654cf86-b896-4db2-8f5d-6c1b2e6c229f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f70f21e3-3bec-490d-889e-faf496fb738b
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# AEM Forms 작업 영역에서 타사 애플리케이션 통합{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms 작업 공간에서는 양식 및 문서에 대한 작업 지정 및 완료 활동 관리를 지원합니다. 이러한 양식과 문서는 XDP, PDF, HTML 또는 Flex 포맷으로 렌더링된 XDP 양식, Flex® 양식 또는 안내서(더 이상 사용되지 않음)가 될 수 있습니다.

이러한 기능은 더욱 향상되었습니다. 이제 AEM Forms는 AEM Forms 작업 영역과 유사한 기능을 지원하는 타사 애플리케이션과의 공동 작업을 지원합니다. 이 기능의 일반적인 부분은 작업의 할당 및 후속 승인 워크플로우입니다. AEM Forms는 AEM Forms Enterprise 사용자를 위한 단일 통합 환경을 제공하므로 지원되는 애플리케이션에 대한 모든 작업 할당 또는 승인을 AEM Forms 작업 영역을 통해 처리할 수 있습니다.

예를 들어, AEM Forms 작업 영역과의 통합을 위한 샘플 후보로 통신 관리를 고려해 보겠습니다. 통신 관리에는 &#39;편지&#39;라는 개념이 있는데, 이것은 렌더링할 수 있고 행동을 허용하는 것이다.

## 통신 관리 에셋 만들기 {#create-correspondence-management-assets}

먼저 AEM Forms 작업 영역에서 렌더링되는 샘플 통신 관리 템플릿을 만듭니다. 자세한 내용은 문자 [템플릿](../../forms/using/create-letter.md)만들기를 참조하십시오.

통신 관리 템플릿을 성공적으로 렌더링할 수 있는지 확인하려면 URL의 통신 관리 템플릿에 액세스하십시오. URL은 `https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`

여기서 `encodedLetterId` 은 URL 인코딩된 문자 ID입니다. Workbench에서 작업 영역 작업의 렌더링 프로세스를 정의할 때 동일한 문자 ID를 지정합니다.

## AEM 작업 공간에서 편지 렌더링 및 제출 작업 만들기 {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

이러한 단계를 실행하기 전에 다음 그룹의 구성원인지 확인하십시오.

* cm-agent-users
* 작업 영역 사용자

자세한 내용은 사용자 [추가 및 구성을](/help/forms/using/admin-help/adding-configuring-users.md)참조하십시오.

AEM 작업 공간에서 편지를 렌더링하고 제출하는 작업을 만들려면 다음 단계를 따르십시오.

1. Launch Workbench. localhost에 관리자로 로그인합니다.
1. 파일 > 새로 만들기 > 응용 프로그램을 클릭합니다. 응용 프로그램 이름 필드에 입력한 다음 마침을 `CMDemoSample` 클릭합니다.
1. 을 `CMDemoSample/1.0` 선택하고 마우스 오른쪽 버튼을 클릭합니다 `NewProcess`. 이름 필드에 입력한 다음 마침을 `CMRenderer` 클릭합니다.
1. 시작 지점 활동 선택기를 드래그하여 구성합니다.

   1. 프레젠테이션 데이터에서 CRX 자산 사용을 선택합니다.

      ![useacrxasset](assets/useacrxasset.png)

   1. 자산을 찾습니다. 양식 자산 선택 대화 상자에서 문자 탭에 서버의 모든 문자가 나열됩니다.

      ![문자 탭](assets/letter_tab_new.png)

   1. 적절한 문자를 선택하고 확인을 **클릭합니다**.

1. 작업 프로필 관리를 클릭합니다. 작업 프로필 관리 대화 상자가 나타납니다. 렌더링 프로세스 및 제출 프로세스가 적절하게 선택되었는지 확인합니다.
1. 데이터 XML 파일이 있는 문자를 열려면 데이터 준비 프로세스에서 적절한 데이터 파일을 찾아 선택합니다.
1. 확인을 클릭합니다.
1. 시작 지점 출력 및 작업 첨부에 대한 변수를 정의합니다. 정의된 변수에는 시작 지점 출력 및 작업 첨부 데이터가 포함됩니다.
1. (선택 사항) 워크플로우에서 다른 사용자를 추가하려면 활동 선택기를 드래그한 다음 구성하고 사용자에게 할당합니다. 사용자 지정 래퍼(아래에 제공된 샘플)를 작성하거나 DSC(아래 제공)를 다운로드하여 설치하면 문자 템플릿, 시작 지점 출력 및 작업 첨부를 확장할 수 있습니다.

   샘플 사용자 지정 래퍼는 아래와 같습니다.

   ```java
   public LetterInstanceInfo getLetterInstanceInfo(Document dataXML) throws Exception {
   try {
   if(dataXML == null)
   throw new Exception("dataXML is missing");
   
   CoreService coreService = getRemoteCoreService();
   if (coreService == null)
   throw new Exception("Unable to retrive service. Please verify connection details.");
   Map<String, Object> result = coreService.getLetterInstanceInfo(IOUtils.toString(dataXML.getInputStream(), "UTF-8"));
   LetterInstanceInfo letterInstanceInfo = new LetterInstanceInfo();
   
   List<Document> attachmentDocs = new ArrayList<Document>();
   List<byte[]> attachments = (List<byte[]>)result.get(CoreService.ATTACHMENT_KEY);
   if (attachments != null){
   for (byte[] attachment : attachments)
   { attachmentDocs.add(new Document(attachment)); }
   
   }
   letterInstanceInfo.setLetterAttachments(attachmentDocs);
   
   byte[] updateLayout = (byte[])result.get(CoreService.LAYOUT_TEMPLATE_KEY);
   if (updateLayout != null)
   { letterInstanceInfo.setLetterTemplate(new Document(updateLayout)); }
   
   else
   { throw new Exception("template bytes missing while getting Letter instance Info."); }
   
   return letterInstanceInfo;
   } catch (Exception e)
   { throw new Exception(e); }
   
   }
   ```

   [파일 다운로드](assets/dscsample.zip)DSC:샘플 DSC는 위에 첨부된 DSCSample.zip 파일에서 사용할 수 있습니다. DSCSample.zip 파일을 다운로드하고 압축을 해제합니다. DSC 서비스를 사용하기 전에 구성해야 합니다. 자세한 내용은 DSC [서비스 구성을 참조하십시오](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p).

   활동 정의 대화 상자에서 getLetterInstanceInfo와 같은 적절한 활동을 선택하고 확인을 **클릭합니다**.

1. 애플리케이션을 배포합니다. 메시지가 표시되면 자산을 체크 인하고 저장합니다.
1. https://&#39;의 AEM 양식 작업 영역에 로그인합니다[.]:[port]&#39;/lc/content/ws.
1. 추가한 작업을 엽니다, CMRenderer. 통신 관리 편지가 나타납니다.

   ![cminworkspace](assets/cminworkspace.png)

1. 필요한 자료를 작성하고 편지를 제출하시오. 창문이 닫혔다. 이 프로세스에서 작업은 9단계의 워크플로우에 지정된 사용자에게 할당됩니다.

   >[!NOTE]
   >
   >서신의 모든 필수 변수가 채워질 때까지 제출 단추가 활성화되지 않습니다.
