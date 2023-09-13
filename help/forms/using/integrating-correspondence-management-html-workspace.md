---
title: AEM Forms 작업 영역에서 타사 애플리케이션 통합
description: AEM Forms 작업 영역에서 서신 관리와 같은 서드파티 애플리케이션을 통합합니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 39a3f7db-549f-47f3-8d4f-42d583a4532d
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# AEM Forms 작업 영역에서 서드파티 애플리케이션 통합{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms 작업 영역은 양식 및 문서에 대한 작업 할당 및 완료 활동 관리를 지원합니다. 이러한 양식 및 문서는 XDP, PDF, HTML 또는 Flex 형식으로 렌더링된 XDP Forms, Flex® 양식 또는 안내서(더 이상 사용되지 않음)일 수 있습니다.

이러한 기능은 더욱 향상되었습니다. 이제 AEM Forms은 AEM Forms 작업 영역과 유사한 기능을 지원하는 타사 애플리케이션과의 공동 작업을 지원합니다. 이 기능의 일반적인 부분은 할당 및 후속 작업 승인 워크플로입니다. AEM Forms은 지원되는 애플리케이션에 대한 모든 작업 할당 또는 승인을 AEM Forms 작업 영역을 통해 처리할 수 있도록 AEM Forms enterprise 사용자를 위한 단일 통합 환경을 제공합니다.

예를 들어 서신 관리를 AEM Forms 작업 영역과의 통합을 위한 샘플 후보로 간주하겠습니다. 서신 관리에는 렌더링할 수 있고 작업을 허용하는 &#39;편지&#39; 개념이 있습니다.

## 서신 관리 에셋 만들기 {#create-correspondence-management-assets}

먼저 AEM Forms 작업 영역에서 렌더링되는 샘플 서신 관리 템플릿을 만듭니다. 자세한 내용은 [편지 템플릿 만들기](../../forms/using/create-letter.md).

해당 URL에서 서신 관리 템플릿에 액세스하여 서신 관리 템플릿이 성공적으로 렌더링될 수 있는지 확인합니다. URL의 패턴은 다음과 유사합니다. `https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`

위치 `encodedLetterId` 는 URL로 인코딩된 문자 ID입니다. Workbench에서 작업 영역 작업에 대한 렌더링 프로세스를 정의할 때 동일한 문자 ID를 지정합니다.

## AEM Workspace에서 편지를 렌더링하고 제출할 작업 만들기 {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

이러한 단계를 실행하기 전에 다음 그룹의 구성원인지 확인하십시오.

* cm-agent-user
* 작업 공간 사용자

자세한 내용은 [사용자 추가 및 구성](/help/forms/using/admin-help/adding-configuring-users.md).

다음 단계를 사용하여 AEM Workspace에서 편지를 렌더링하고 제출할 작업을 생성합니다.

1. Workbench를 시작합니다. Localhost에 관리자로 로그인합니다.
1. 파일 > 새로 만들기 > 응용 프로그램을 클릭합니다. 응용 프로그램 이름 필드에 다음을 입력합니다. `CMDemoSample` 마침을 클릭합니다.
1. 선택 `CMDemoSample/1.0` 마우스 오른쪽 버튼 클릭 `NewProcess`. 이름 필드에 을 입력합니다. `CMRenderer` 마침을 클릭합니다.
1. 시작점 활동 선택기를 드래그하여 구성합니다.

   1. 프레젠테이션 데이터에서 CRX 자산 사용을 선택합니다.

      ![useacrxasset](assets/useacrxasset.png)

   1. 에셋을 찾습니다. 양식 에셋 선택 대화 상자에서 편지 탭에 서버의 모든 문자가 나열됩니다.

      ![Letter 탭](assets/letter_tab_new.png)

   1. 적절한 문자를 선택하고 **확인**.

1. 작업 프로필 관리를 클릭합니다. 작업 프로필 관리 대화 상자가 나타납니다. [렌더링 프로세스] 및 [제출 프로세스]가 적절히 선택되어 있는지 확인합니다.
1. 데이터 XML 파일이 있는 편지를 열려면 데이터 준비 프로세스에서 해당 데이터 파일을 찾아 선택합니다.
1. 확인을 클릭합니다.
1. 시작점 출력 및 작업 첨부에 대한 변수를 정의합니다. 정의된 변수에는 시작점 출력 및 작업 첨부 데이터가 포함됩니다.
1. (선택 사항) 워크플로우에서 다른 사용자를 추가하려면 활동 선택기를 드래그하여 구성한 다음 사용자에게 할당합니다. 사용자 지정 래퍼(아래 샘플)를 작성하거나 DSC(아래 샘플)를 다운로드하여 설치하여 편지 템플릿, 시작점 출력 및 작업 첨부 파일을 추출합니다.

   샘플 사용자 지정 래퍼는 아래와 같습니다.

   ```javascript
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

   [파일 가져오기](assets/dscsample.zip)
DSC 다운로드: 샘플 DSC는 위에 첨부된 DSCSample.zip 파일에서 사용할 수 있습니다. DSCSample.zip 파일을 다운로드하고 압축 해제합니다. DSC 서비스를 사용하기 전에 먼저 구성해야 합니다. 다음을 참조하십시오 [DSC 서비스 구성](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p).

   활동 정의 대화 상자에서 getLetterInstanceInfo 와 같은 적절한 활동을 선택하고 을 클릭합니다 **확인**.

1. 응용 프로그램을 배포합니다. 메시지가 표시되면 자산을 체크인하고 저장합니다.
1. https://&#39;에서 AEM forms 작업 영역에 로그인합니다.[server]:[포트]&#39;/lc/content/ws.
1. 추가한 작업, CMRenderer를 엽니다. 서신 관리 편지가 나타납니다.

   ![cminworkspace](assets/cminworkspace.png)

1. 필요한 자료를 입력하고 편지를 제출하세요. 창이 닫힙니다. 이 프로세스에서는 9단계의 워크플로우에 지정된 사용자에게 작업이 할당됩니다.

   >[!NOTE]
   >
   >편지의 필수 변수를 모두 채울 때까지 제출 단추를 사용할 수 없습니다.
