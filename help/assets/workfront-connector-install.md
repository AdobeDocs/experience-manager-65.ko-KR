---
title: 설치  [!DNL Workfront for Experience Manager enhanced connector]
description: 설치  [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 4%

---

#  설치 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en) |
| AEM 6.5 | 이 문서 |
| AEM 6.4 | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-connector-install.html?lang=en) |

에 관리자 액세스 권한이 있는 사용자 [!DNL Adobe Experience Manager] 향상된 커넥터를 설치합니다. 설치하기 전에 플랫폼 지원 및 기타 를 검토하십시오 [커넥터를 위한 사전 요구 사항](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe을 사용하려면 [!DNL Adobe Workfront for Experience Manager enhanced connector] 인증된 파트너를 통해 [!DNL Adobe Professional Services]. 인증된 파트너 또는 [!DNL Adobe Professional Services]Adobe에서 지원하지 않습니다.
>
>* Adobe은 [!DNL Adobe Workfront] 및 [!DNL Adobe Experience Manager] 이렇게 하면 커넥터가 이중화됩니다. 이러한 경우 고객은 이 커넥터를 사용하는 상태에서 전환해야 할 수 있습니다.
>
>* Adobe은 향상된 커넥터 버전 1.7.4 이상을 지원합니다. 이전 사전 릴리스 및 사용자 지정 버전은 지원되지 않습니다. 향상된 커넥터 버전을 확인하려면 `digital.hoodoo` 의 왼쪽 창에서 사용할 수 있는 그룹 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ko-KR).
>
>* 자세한 내용은 [Experience Manager Assets Enhanced Connector용 Workfront의 파트너 인증 시험](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 시험에 대한 자세한 내용은 [시험 안내서](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


커넥터를 설치하려면 다음 단계를 수행하십시오.

1. 커넥터 다운로드 위치 [[!DNL Software Distribution] 링크](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [방화벽 구성](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. 디스패처에서 이름이 인 HTTP 헤더를 허용합니다. `authorization`, `username`, 및 `apikey`. 허용 `GET`, `POST`, 및 `PUT` 요청 `/bin/workfront-tools`.
1. 다음 경로가 [!DNL Experience Manager] 저장소:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 를 사용하여 패키지 설치 [!UICONTROL 패키지 관리자]. 패키지를 설치하는 방법은 다음을 참조하십시오 [패키지 관리자 설명서](/help/sites-administering/package-manager.md).
1. 만들기 `wf-workfront-users` in [!DNL Experience Manager] 사용자 그룹 및 권한 할당 `jcr:all` to `/content/dam`.

시스템 사용자 `workfront-tools` 는 자동으로 만들어지며 필요한 권한은 자동으로 관리됩니다. 의 모든 사용자 [!DNL Workfront] 커넥터를 사용하는 사용자는 자동으로 이 그룹의 일부로 추가됩니다.

## 다음 사이의 연결 구성 [!DNL Experience Manager] 및 [!DNL Workfront] {#configure-connection}

Workfront과의 연결을 만들려면 다음 단계를 수행하십시오.

1. in [!DNL Experience Manager], 선택 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront 도구 구성]**.

1. 선택 `workfront-tools` 왼쪽 패널에서 을(를) 선택하고 을(를) 선택합니다. **[!UICONTROL 만들기]** 옵션 을 클릭합니다.

1. 에서 **[!UICONTROL Workfront 연결]** 대화 상자에서 필요한 세부 정보를 제공합니다 [!DNL Workfront] 배포 후 **[!UICONTROL Workfront에 연결]** 선택 사항입니다. 연결되면 [!DNL Workfront] 문서 사용자 지정 통합은 [!DNL Workfront] 환경.

   ![Connect [!DNL Experience Manager] 및 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 연결을 확인하려면 [!DNL Workfront] 및 API 키가 동일하고 연결이 **[!UICONTROL 활성화됨]**. 이렇게 하려면 을(를) 선택합니다. **[!UICONTROL 설정]** > **[!UICONTROL 문서]** > **[!UICONTROL 사용자 지정 통합]** in [!DNL Workfront].

## 업데이트 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets을 사용하면 [!DNL Workfront for Experience Manager enhanced connector] 이전 버전에서 최신 버전으로 마이그레이션 하는 것이 좋습니다.

를 업데이트하려면 [!DNL Workfront for Experience Manager enhanced connector] 최신 버전으로 마이그레이션:

1. 향상된 커넥터의 최신 버전을 다운로드하십시오. [[!DNL Software Distribution] 링크](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. 를 사용하여 패키지 설치 [!UICONTROL 패키지 관리자]. 패키지를 설치하는 방법은 다음을 참조하십시오 [패키지 관리자 설명서](/help/sites-administering/package-manager.md).
