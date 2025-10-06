---
title: ' [!DNL Workfront for Experience Manager enhanced connector] 설치'
description: ' [!DNL Workfront for Experience Manager enhanced connector] 설치'
role: Admin
feature: Workfront Integrations and Apps
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
hide: true
solution: Experience Manager, Workfront
source-git-commit: 633b1378d97ea0544f27822fb5801caa3ed15f8e
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 3%

---

# [!DNL Workfront for Experience Manager enhanced connector] 설치 {#assets-integration-overview}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=ko) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Experience Manager]에서 관리자 액세스 권한이 있는 사용자가 향상된 커넥터를 설치합니다. 설치하기 전에 플랫폼 지원 및 기타 [커넥터에 대한 필수 구성 요소](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience)를 검토하십시오.

>[!IMPORTANT]
>
>* Adobe에서는 인증된 파트너 또는 [!DNL Adobe Workfront for Experience Manager enhanced connector]을(를) 통해서만 [!DNL Adobe Professional Services]을(를) 배포하고 구성해야 합니다. 인증 파트너 또는 [!DNL Adobe Professional Services] 없이 배포 및 구성된 경우 Adobe에서 지원하지 않습니다.
>
>* Adobe은 이 커넥터를 중복 커넥터로 만드는 [!DNL Adobe Workfront] 및 [!DNL Adobe Experience Manager]에 대한 업데이트를 릴리스할 수 있습니다. 이러한 경우 고객은 이 커넥터를 사용하지 않도록 전환해야 할 수 있습니다.
>
>* Adobe은 향상된 커넥터 버전 1.7.4 이상을 지원합니다. 이전 프리릴리스 및 사용자 지정 버전은 지원되지 않습니다. 향상된 커넥터 버전을 확인하려면 `digital.hoodoo`패키지 관리자[의 왼쪽 창에서 사용할 수 있는 &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ko) 그룹으로 이동하십시오.
>
>* [Workfront for Experience Manager Assets 강화 커넥터에 대한 파트너 인증 시험](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)을 참조하세요. 시험에 대한 자세한 내용은 [시험 가이드](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)를 참조하세요.

커넥터를 설치하려면 다음 단계를 수행하십시오.

1. [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)에서 커넥터를 다운로드합니다.
1. [방화벽을 구성합니다](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. Dispatcher에서 이름이 `authorization`, `username` 및 `apikey`인 HTTP 헤더를 허용합니다. `GET`에 `POST`, `PUT` 및 `/bin/workfront-tools` 요청을 허용합니다.
1. [!DNL Experience Manager] 저장소에 다음 경로가 없는지 확인하십시오.

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. [!UICONTROL 패키지 관리자]를 사용하여 패키지를 설치하십시오. 패키지 설치 방법은 [패키지 관리자 설명서](/help/sites-administering/package-manager.md)를 참조하세요.
1. `wf-workfront-users` 사용자 그룹에 [!DNL Experience Manager]을(를) 만들고 `jcr:all`에 `/content/dam` 권한을 할당합니다.
1. **`ntFolderDamLucene(/oak:index/ntFolderDamLucene)`**&#x200B;에 대한 기본 제공 인덱스 정의에 사용자 지정 속성을 추가하십시오. 아래 단계를 실행합니다.
   * **`nt:unstructured`**(이)라는 **`wfReferenceNumber`** 속성을 다음 위치에 추가:
     `/oak:index/ntFolderDamLucene/indexRules/nt:folder/properties/wfReferenceNumber`
   * `index /oak:index/ntFolderDamLucene`(으)로 리인덱싱 플래그를 전환하여 `true`을(를) 리인덱싱합니다.

시스템 사용자 `workfront-tools`이(가) 자동으로 만들어지고 필요한 권한이 자동으로 관리됩니다. 커넥터를 사용하는 [!DNL Workfront]의 모든 사용자는 자동으로 이 그룹의 일부로 추가됩니다.

>[!NOTE]
>
> 회사 프록시 서버를 사용하는 경우 [!DNL workfront]향상된 Workfront 커넥터[!UICONTROL 에 대한 &#x200B;]Apache HTTP 구성 요소 프록시 구성 PID[!UICONTROL 에 &#x200B;]을(를) 포함하여 인식하십시오. 필요한 PID 형식은 `org.apache.http.proxyconfigurator~workfront`입니다.

## [!DNL Experience Manager]과(와) [!DNL Workfront] 간의 연결 구성 {#configure-connection}

Workfront에 대한 연결을 만들려면 다음 단계를 수행하십시오.

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 클라우드 서비스]** > **[!UICONTROL Workfront 도구 구성]**&#x200B;을 선택합니다.

1. 왼쪽 패널에서 `workfront-tools`을(를) 선택하고 페이지의 오른쪽 상단 영역에서 **[!UICONTROL 만들기]** 옵션을 선택합니다.

1. **[!UICONTROL Workfront 연결]** 대화 상자에서 [!DNL Workfront] 배포에 대한 필요한 세부 정보를 입력하고 **[!UICONTROL Workfront에 연결]** 옵션을 선택합니다. 연결되면 [!DNL Workfront] 환경에서 [!DNL Workfront] 문서 사용자 지정 통합이 자동으로 만들어집니다.

   ![[!DNL Experience Manager] 및 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png) 연결

1. 연결을 확인하려면 [!DNL Workfront]에서 API 키에 액세스하고 API 키가 동일하며 연결이 **[!UICONTROL 활성화됨]**&#x200B;인지 확인하십시오. 이렇게 하려면 **[!UICONTROL 에서]**&#x200B;설정&#x200B;**[!UICONTROL >]**&#x200B;문서&#x200B;**[!UICONTROL >]**&#x200B;사용자 지정 통합[!DNL Workfront]을 선택하세요.

## [!DNL Workfront for Experience Manager enhanced connector] 업데이트 {#update-enhanced-connector-for-workfront}

Experience Manager Assets을 사용하면 [!DNL Workfront for Experience Manager enhanced connector]을(를) 이전 버전에서 최신 버전으로 업데이트할 수 있습니다.

[!DNL Workfront for Experience Manager enhanced connector]을(를) 최신 버전으로 업데이트하려면:

1. [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)에서 향상된 커넥터의 최신 버전을 다운로드하십시오.
1. [!UICONTROL 패키지 관리자]를 사용하여 패키지를 설치하십시오. 패키지 설치 방법은 [패키지 관리자 설명서](/help/sites-administering/package-manager.md)를 참조하세요.
