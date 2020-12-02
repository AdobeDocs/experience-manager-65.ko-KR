---
title: AEM Forms 작업 공간에서 타사 애플리케이션 통합
seo-title: AEM Forms 작업 공간에서 타사 애플리케이션 통합
description: AEM Forms 작업 공간에서 통신 관리와 같은 타사 애플리케이션을 통합할 수 있습니다.
seo-description: AEM Forms 작업 공간에서 통신 관리와 같은 서드파티 앱을 통합하는 방법
uuid: 7654cf86-b896-4db2-8f5d-6c1b2e6c229f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f70f21e3-3bec-490d-889e-faf496fb738b
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# AEM Forms 작업 공간에서 타사 애플리케이션 통합{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms 작업 공간에서는 양식 및 문서에 대한 작업 지정 및 완료 활동을 관리할 수 있습니다. 이러한 양식과 문서는 XDP, PDF, HTML 또는 Flex 형식으로 렌더링된 XDP Forms, Flex ® 양식 또는 안내선(더 이상 사용되지 않음)이 될 수 있습니다.

이러한 기능이 더욱 향상되었습니다. AEM Forms은 이제 AEM Forms 작업 공간과 유사한 기능을 지원하는 타사 애플리케이션과의 공동 작업을 지원합니다. 이 기능의 일반적인 부분은 작업의 할당 및 후속 승인 워크플로입니다. AEM Forms은 AEM Forms 엔터프라이즈 사용자를 위한 단일 통합 경험을 제공하므로 지원되는 애플리케이션에 대한 모든 작업 할당 또는 승인을 AEM Forms 작업 영역을 통해 처리할 수 있습니다.

예를 들어 통신 관리를 AEM Forms 작업 공간과의 통합 샘플 후보로 간주합니다. 통신관리사는 &#39;편지&#39;라는 개념을 가지고 있는데, 이것은 렌더링할 수 있고 행동을 허락한다.

## 통신 관리 자산 만들기 {#create-correspondence-management-assets}

먼저 AEM Forms 작업 공간에서 렌더링되는 샘플 통신 관리 템플릿을 만듭니다. 자세한 내용은 [문자 템플릿 만들기](../../forms/using/create-letter.md)를 참조하십시오.

통신 관리 템플릿을 성공적으로 렌더링할 수 있는지 확인하려면 URL의 통신 관리 템플릿에 액세스하십시오. URL에 `https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`과 유사한 패턴이 있습니다.

여기서 `encodedLetterId`은 URL 인코딩 문자 ID입니다. Workbench에서 작업 공간 작업의 렌더링 프로세스를 정의할 때 동일한 문자 ID를 지정합니다.

## AEM 작업 공간 {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}에서 편지를 렌더링하고 제출하는 작업 만들기

이러한 단계를 실행하기 전에 다음 그룹의 구성원인지 확인하십시오.

* cm-agent-users
* 작업 공간 사용자

자세한 내용은 [사용자 추가 및 구성](/help/forms/using/admin-help/adding-configuring-users.md)을 참조하십시오.

AEM 작업 공간에서 편지를 렌더링하고 제출하는 작업을 만들려면 다음 단계를 수행하십시오.

1. Launch Workbench. localhost에 관리자로 로그인합니다.
1. 파일 > 새로 만들기 > 응용 프로그램을 클릭합니다. 응용 프로그램 이름 필드에 `CMDemoSample`을 입력한 다음 마침을 클릭합니다.
1. `CMDemoSample/1.0`을 선택하고 `NewProcess`을 마우스 오른쪽 단추로 클릭합니다. 이름 필드에 `CMRenderer`을 입력한 다음 마침을 클릭합니다.
1. 시작 지점 활동 선택기를 드래그하여 구성합니다.

   1. 프레젠테이션 데이터에서 CRX 자산 사용을 선택합니다.

      ![usacrxasset](assets/useacrxasset.png)

   1. 자산을 찾습니다. 양식 자산 선택 대화 상자에서 문자 탭에 서버의 모든 문자가 나열됩니다.

      ![문자 탭](assets/letter_tab_new.png)

   1. 적절한 문자를 선택하고 **확인**&#x200B;을 클릭합니다.

1. 작업 프로필 관리를 클릭합니다. 작업 프로필 관리 대화 상자가 나타납니다. 렌더링 프로세스 및 제출 프로세스가 적절하게 선택되었는지 확인합니다.
1. 데이터 XML 파일이 있는 문자를 열려면 데이터 준비 프로세스에서 적절한 데이터 파일을 찾아 선택합니다.
1. 확인을 클릭합니다.
1. 시작점 출력 및 작업 첨부 파일의 변수를 정의합니다. 정의된 변수에는 시작점 출력 및 작업 첨부 데이터가 포함됩니다.
1. (선택 사항) 워크플로우에서 다른 사용자를 추가하려면 활동 선택기를 드래그하고 구성한 다음 사용자에게 지정합니다. 사용자 지정 래퍼(아래 샘플)를 작성하거나 DSC(아래 제공)를 다운로드하여 설치하면 문자 템플릿, 시작점 출력 및 작업 첨부를 확장할 수 있습니다.

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

   [파일 ](assets/dscsample.zip)
다운로드DSC 다운로드:위에 첨부된 DSCSample.zip 파일에서 샘플 DSC를 사용할 수 있습니다. DSCSample.zip 파일을 다운로드하고 압축을 해제합니다. DSC 서비스를 사용하기 전에 구성해야 합니다. 자세한 내용은 [DSC 서비스 구성](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p)을 참조하십시오.

   활동 정의 대화 상자에서 getLetterInstanceInfo와 같은 적절한 활동을 선택하고 **OK**&#x200B;을 클릭합니다.

1. 응용 프로그램을 배포합니다. 메시지가 표시되면 자산을 저장합니다.
1. https://&#39;[server]:[port]&#39;/lc/content/ws에서 AEM 양식 작업 영역에 로그인합니다.
1. 추가한 작업을 엽니다, CMRenderer. 통신 관리 편지가 나타납니다.

   ![cminworkspace](assets/cminworkspace.png)

1. 필요한 자료를 작성하고 편지를 제출하세요. 창문이 닫혀요 이 프로세스에서는 9단계의 워크플로우에 지정된 사용자에게 작업이 할당됩니다.

   >[!NOTE]
   >
   >서신의 모든 필수 변수가 채워질 때까지 제출 단추가 활성화되지 않습니다.
