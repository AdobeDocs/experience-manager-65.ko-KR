---
title: AEM Forms을 Adobe Analytics과 통합하는 방법
description: AEM Forms은 Adobe Analytics과 통합되어 게시된 양식에 대한 성능 지표를 캡처하고 추적합니다.
docset: aem65
exl-id: 030fe9f2-cd41-4290-b8a6-2f9ade6b5789
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---

# [!DNL Adobe Launch]을(를) 사용하는 분석 {#analyticsusingadobelaunch}

AEM Forms은 [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en)과(와) 통합되어 게시된 양식의 성능 지표를 캡처하고 추적할 수 있습니다. 이러한 지표를 분석하는 목표는 비즈니스 사용자가 최종 사용자 동작에 대한 통찰력을 얻고 데이터 캡처 경험을 최적화할 수 있도록 하는 것입니다. 적응형 Forms용 Adobe Analytics을 통해 로그인한 사용자와 로그인하지 않은(익명의) 사용자의 행동을 포착하고 추적할 수 있습니다.

Cloud Service 프레임워크를 사용하여 분석을 수행할 수도 있습니다. AEM Forms을 Cloud Service 프레임워크와 통합하는 방법에 대한 자세한 내용은 [Cloud Service 프레임워크를 사용하여 분석](/help/forms/using/configure-analytics-forms-documents.md)을 참조하십시오. Cloud Service 프레임워크를 사용하여 Analytics보다 Adobe Launch를 사용할 때의 주요 장점은 기본 이벤트 외에 사용자 지정 이벤트를 정의할 수도 있다는 것입니다. 사용자 지정된 이벤트는 규칙 편집기 또는 고객 clientlibs를 사용하여 정의되며 [!DNL Adobe Analytics]의 이벤트에 매핑됩니다.

이 문서에 언급된 작업을 수행한 후 다음 비디오에 나와 있는 대로 [!DNL Adobe Analytics]에서 보고서를 구성하고 볼 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/337262)

[!DNL Adobe Analytics]을(를) 사용하여 적응형 양식을 사용하는 동안 사용자가 직면한 상호 작용 패턴 및 문제를 발견할 수 있습니다. 기본적으로 [!DNL Adobe Analytics]은(는) 다음 이벤트에 대한 정보를 추적하고 저장합니다.

* **Render**: 양식을 연 횟수입니다.

* **제출**: 양식을 제출한 횟수입니다.

* **중단**: 양식을 완료하지 않고 사용자가 나가는 횟수입니다.

* **오류**: 패널 및 패널의 필드에서 발생한 오류 수입니다.

* **도움말**: 사용자가 패널 및 패널의 필드를 여는 횟수입니다.

* **필드 방문**: 사용자가 양식의 필드를 방문한 횟수입니다.

* **저장**: 사용자가 Forms 포털에 양식을 저장한 횟수입니다.

기본 이벤트 외에도 사용자 지정 이벤트를 정의할 수도 있습니다.

다음 그림은 [!DNL Adobe Analytics]에서 보고서를 보기 전에 수행해야 하는 작업을 보여 줍니다.

![Analytics 개요](/help/forms/using/assets/analyticsworkflow.png)

## 1. [!DNL Adobe Analytics] 구성 {#Configure-adobe-analytics}

[!DNL Adobe Analytics]을(를) 구성하기 전에 다음을 만드십시오.

* [Adobe Experience Cloud](https://experience.adobe.com/#/home)에 로그온할 Adobe ID.
* [보고서 세트](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### AEM Forms 및 [!DNL Adobe Analytics] 확장 설치 {#install-extensions}

AEM Forms 및 [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) 확장을 구성하려면 다음 단계를 수행하십시오.

1. Adobe Experience Cloud에 로그온하고 회사에 적합한 이름을 선택합니다.

1. **[!UICONTROL 실행/데이터 수집]**&#x200B;을 선택하고 **[!UICONTROL 실행/데이터 수집으로 이동]**&#x200B;을 선택합니다.

1. **[!UICONTROL 새 속성]**&#x200B;을 선택하고 구성 이름을 지정하십시오.

1. 도메인 이름을 지정하고 **[!UICONTROL 저장]**&#x200B;을 선택하여 속성을 저장합니다.

1. 태그 속성 목록에서 사용할 수 있는 구성 이름을 선택합니다.

1. **[!UICONTROL 작성]** 섹션에서 **[!UICONTROL 확장]**&#x200B;을 선택합니다.

1. **[!UICONTROL 카탈로그]**&#x200B;를 선택하고 **[!UICONTROL Adobe Experience Manager Forms]** 확장에 대해 **[!UICONTROL 설치]**&#x200B;를 선택합니다. **[!UICONTROL Adobe Experience Manager Forms]**&#x200B;이(가) **설치됨** 탭에서 사용할 수 있는 설치된 확장 목록에 표시됩니다.

1. **[!UICONTROL Adobe Analytics]** 확장에 대해 **[!UICONTROL 설치]**&#x200B;를 선택합니다.
1. **[!UICONTROL 개발 보고서 세트]**, **[!UICONTROL 스테이징 보고서 세트]** 및 **[!UICONTROL 제품 보고서 세트]** 드롭다운 목록에서 보고서 세트 이름을 선택하고 **[!UICONTROL 저장]**&#x200B;을 선택하여 확장을 저장합니다.

### 데이터 요소 구성 {#configure-data-elements}

이벤트에 대해 만들어진 규칙에서 구성된 데이터 요소를 선택할 수 있습니다. 적응형 양식에서 이벤트가 발생하면 AEM Forms에서 이러한 데이터 요소를 [!DNL Adobe Analytics](으)로 보냅니다.

**[!UICONTROL Adobe Experience Manager Forms]** 확장을 설치한 후 다음 데이터 요소를 만들 수 있습니다.

<table>
 <tbody>
  <tr>
   <td>필드 이름</th>
   <td>필드 제목</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>FormTitle<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>패널 제목<br /> </td>
   <td>체류 시간</td>
  </tr>
 </tbody>
</table>

데이터 요소를 구성하려면 다음 단계를 수행하십시오.

1. **[!UICONTROL 작성]** 섹션에서 **[!UICONTROL 데이터 요소]**&#x200B;를 선택합니다.

1. **[!UICONTROL 새 데이터 요소 만들기]**&#x200B;를 선택합니다.

1. 데이터 요소의 이름을 지정합니다. 예: FormTitle 데이터 요소 유형에 대한 Form Title.

1. **[!UICONTROL Adobe Experience Manager Forms]**&#x200B;을(를) 확장 이름으로 지정하십시오.

1. **[!UICONTROL 데이터 요소 형식]**&#x200B;을(를) 선택하십시오.

1. 데이터 요소를 저장하려면 **[!UICONTROL 저장]**&#x200B;을(를) 선택하십시오.

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### 규칙 구성 {#configure-rules}

**[!UICONTROL Adobe Experience Manager Forms]** 확장을 기반으로 규칙을 만들려면 다음 단계를 수행하십시오.

1. **[!UICONTROL 작성]** 섹션에서 **[!UICONTROL 규칙]**&#x200B;을(를) 선택합니다.

1. **[!UICONTROL 새 규칙 만들기]**&#x200B;를 선택합니다.

1. 규칙 이름을 지정합니다. 예를 들어 양식 제출을 사용하여 양식 제출을 기록할 수 있습니다.

1. **[!UICONTROL 이벤트]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 선택합니다.

1. **[!UICONTROL Adobe Experience Manager Forms]**&#x200B;을(를) 확장 이름으로 지정하십시오.

1. 이벤트 유형을 선택합니다. **[!UICONTROL 이름]** 필드에 대한 입력은 선택한 이벤트 유형에 따라 자동으로 채워집니다.

1. 이벤트를 저장하려면 **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택하십시오.

1. **[!UICONTROL 작업]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 선택합니다.

1. **[!UICONTROL Adobe Analytics]**&#x200B;을(를) 확장 이름으로 지정하십시오.

1. **[!UICONTROL 변수 설정]**&#x200B;을(를) 작업 유형으로 선택합니다. 드롭다운 목록에서 사용할 수 있는 옵션은 다음과 같습니다.

   * **[!UICONTROL 변수 설정]**: 이 작업 형식을 사용하여 선택한 데이터 요소를 AEM Forms에서 [!DNL Adobe Analytics](으)로 보내는 이벤트 형식을 정의합니다.

   * **[!UICONTROL 비콘 보내기]**: 이 작업 형식을 사용하여 AEM Forms에서 [!DNL Adobe Analytics](으)로 데이터를 보냅니다.

   * **[!UICONTROL 변수 지우기]**: 이벤트가 [!DNL Adobe Analytics]에 한 번만 등록되도록 데이터 추적을 지우려면 이 작업 유형을 사용하십시오.

     권장 접근 방법은 **[!UICONTROL 변수 설정]** 작업 유형을 사용하여 이벤트 및 데이터 요소를 구성한 다음, **[!UICONTROL 비콘 보내기]**&#x200B;를 사용하여 데이터를 보낸 다음, **[!UICONTROL 변수 지우기]**&#x200B;를 사용하여 데이터 추적을 지우는 것입니다.

1. **[!UICONTROL Props]** 섹션에서 드롭다운 목록에서 사용할 수 있는 보고서 세트 옵션을 [데이터 요소 구성](#configure-data-elements)을 사용하여 정의된 데이터 요소와 매핑합니다.

   예를 들어 양식을 제출할 때 **양식 제목** 데이터 요소를 AEM Forms에서 [!DNL Adobe Analytics](으)로 보내려면 다음을 수행하십시오.
   1. **[!UICONTROL Prop]** 섹션에서 보고서 세트에서 사용할 수 있는 양식 제목에 대한 prop을 선택한 다음 ![데이터베이스 아이콘](/help/forms/using/assets/database-icon.svg)을 선택하여 [데이터 요소 구성](#configure-data-elements)에서 만든 양식 제목에 매핑합니다.

      ![define-props](/help/forms/using/assets/define-props.png)

   1. 목록에 더 많은 데이터 요소를 추가하려면 **[!UICONTROL 다른 항목 추가]**&#x200B;를 선택하십시오.

1. **[!UICONTROL 이벤트]** 섹션에서 보고서 세트에 있는 옵션에서 이벤트를 선택하고 **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택합니다.

1. **[!UICONTROL 작업]** 섹션에서 +를 선택하고 **[!UICONTROL Adobe Analytics]**&#x200B;을(를) 확장 이름으로 지정합니다.

1. 작업 유형으로 **[!UICONTROL 비콘 보내기]**&#x200B;를 선택합니다. 오른쪽 창에서 **[!UICONTROL s.t()]**&#x200B;을(를) 선택하여 [!DNL Adobe Analytics]에 데이터를 보내고 페이지 보기로 처리하거나 **[!UICONTROL s.tl()]**&#x200B;을(를) 선택하여 [!DNL Adobe Analytics]에 데이터를 보내고 페이지 보기로 처리하지 않습니다. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택합니다.

1. **[!UICONTROL 작업]** 섹션에서 +를 선택하고 **[!UICONTROL Adobe Analytics]**&#x200B;을(를) 확장 이름으로 지정합니다.

1. **[!UICONTROL 변수 지우기]**&#x200B;를 작업 유형으로 선택합니다. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택합니다. 이 단계를 수행하면 **[!UICONTROL 작업]** 섹션이 다음과 같이 표시됩니다.
   ![작업 구성](/help/forms/using/assets/actions-config.png)

   요구 사항에 따라 **[!UICONTROL 작업]** 섹션을 사용자 지정합니다. 예를 들어, 작업 흐름에서 두 개의 **비콘 보내기** 단계를 정의하여 [!DNL Adobe Analytics]에 데이터를 보내고 한 단계에서 페이지 보기로 처리하며 [!DNL Adobe Analytics]에 데이터를 보내고 두 번째 단계에서는 페이지 보기로 처리하지 않을 수 있습니다.

   ![작업 구성](/help/forms/using/assets/actions-config-2.png)

1. 규칙을 저장하려면 **[!UICONTROL 저장]**&#x200B;을(를) 선택하십시오.

   중단, 오류, 필드 방문, 도움말, 렌더링, 저장 및 제출과 같은 모든 이벤트 유형에 대한 규칙을 만들 수 있습니다.

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Publish 흐름 {#publish-flow}

데이터 요소를 만들어 규칙에 사용한 후 구성을 게시하여 [!DNL Adobe Analytics]에서 양식 데이터를 수집합니다.

구성을 게시하려면 다음 단계를 수행하십시오.

1. **[!UICONTROL 게시]** 섹션에서 **[!UICONTROL 게시 흐름]**&#x200B;을 선택합니다.

1. **[!UICONTROL 라이브러리 추가]**&#x200B;를 선택하고 이름을 지정한 다음 라이브러리의 환경을 선택하십시오.

1. **[!UICONTROL 변경된 모든 리소스 추가]**&#x200B;를 선택한 다음 **[!UICONTROL 개발에 저장 및 빌드]**&#x200B;를 선택합니다.

1. **[!UICONTROL 개발]** 섹션에서 ![추가 옵션](/help/forms/using/assets/more-options-icon.svg)을 선택한 다음 **[!UICONTROL 프로덕션에 대한 승인 및 Publish]**&#x200B;을 선택합니다.

1. 변경 내용을 확인하고 게시 흐름이 곧 **[!UICONTROL 게시됨]** 섹션에 표시됩니다.

![Publish 흐름](/help/forms/using/assets/publish-flow.png)

## 2. AEM Forms 구성 {#configure-aem-forms}

Adobe 실행 구성을 만들기 전에 Adobe 실행을 클라우드 솔루션으로 사용하여 [Adobe IMS 구성을 만드십시오](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### Adobe Launch 구성 만들기 {#create-adobe-launch-configuration}

Adobe Launch 구성을 만들려면 다음 단계를 수행하십시오.

1. AEM Forms 작성자 인스턴스에서 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 실행 구성 Adobe]**&#x200B;로 이동합니다.

1. 구성을 만들 폴더를 선택하고 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

1. **[!UICONTROL 제목]** 필드에 구성의 제목을 지정합니다.

1. [연결된 Adobe IMS 구성](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html)을(를) 선택하십시오.

1. [Adobe Analytics을 구성하는 동안](#Configure-adobe-analytics)에 사용된 회사 이름을 선택하십시오.

1. [Adobe Analytics을 구성하는 동안](#install-extensions)만든 속성의 이름을 선택하십시오.

1. **[!UICONTROL 저장 후 닫기]**&#x200B;를 선택합니다.

1. 구성을 Publish에 추가합니다.

### 적응형 양식에 [!DNL Adobe Analytics] 사용 {#enable-analytics-adaptive-form}

기존 적응형 양식에서 [!DNL Adobe Launch] 구성을 사용하려면:

1. AEM Forms 작성자 인스턴스에서 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;로 이동합니다.
1. 적응형 양식을 선택하고 **[!UICONTROL 속성]**&#x200B;을 선택합니다.
1. **[!UICONTROL 기본]** 탭에서 Adobe 실행 구성을 만드는 동안 사용되는 [구성 컨테이너](#create-adobe-launch-configuration)를 선택합니다.
1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 선택합니다. [!DNL Adobe Analytics]에 대해 적응형 양식을 사용할 수 있습니다.
1. 양식 Publish.

적응형 양식에 대해 [!DNL Adobe Analytics]을(를) 사용하도록 설정한 후 AEM Forms과 [!DNL Adobe Analytics] 사이에 적절한 데이터 이벤트 흐름이 있으면 [유효성 검사](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon)할 수 있습니다. AEM Forms과 Adobe Analytics 통합이 완료되었습니다. 이제 [Adobe Analytics에서 보고서를 구성하고 볼 수 있습니다](#view-reports-adobe-analytics).

>[!NOTE]
>[Cloud Service 프레임워크를 사용하는 Analytics](/help/forms/using/configure-analytics-forms-documents.md)와 **Adobe 실행을 사용하는 Analytics** 기능을 동시에 사용할 수 있는 경우 **Adobe 실행을 사용하는 Analytics**&#x200B;가 우선합니다.
> 

### 사용자 지정 이벤트 캡처를 위한 규칙 만들기(선택 사항) {#capture-custom-events}

규칙 편집기를 사용하여 적응형 양식의 특정 필드에 대한 규칙을 만들어 적응형 양식에서 [!DNL Adobe Analytics](으)로 Analytics 데이터를 보냅니다.

2단계 프로세스에서는 적응형 양식의 필드에 규칙을 정의합니다. 규칙이 이벤트를 전달합니다. 이벤트 이름은 Adobe Launch의 사용자 지정 캡처 이벤트에 매핑됩니다.

적응형 양식에서 규칙 편집기를 사용하여 규칙을 만들려면 다음 작업을 수행하십시오.

1. 필드를 선택하고 ![규칙 편집기](/help/forms/using/assets/rule-editor-icon.svg)를 선택하여 규칙 편집기 페이지를 엽니다.
1. 규칙의 [!UICONTROL When] 섹션에서 조건을 정의합니다.
1. 규칙의 [!UICONTROL Then] 섹션에서 **[!UICONTROL 작업 선택]** 드롭다운 목록에서 **[!UICONTROL 이벤트 발송]**&#x200B;을 선택합니다.
1. **[!UICONTROL 이벤트 이름 입력]** 필드에 이벤트 이름을 지정하십시오.

예를 들어 생년월일이 특정 날짜 이전인 경우 AEM Forms은 **보안** 이벤트를 발송합니다.

![이벤트 발송](/help/forms/using/assets/security-event.png)

이벤트를 [!DNL Adobe Analytics]의 사용자 지정 캡처 이벤트에 매핑하려면 다음을 수행하십시오.

1. [규칙을 만듭니다](#configure-rules).

1. **[!UICONTROL 이벤트]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 선택합니다.

1. **[!UICONTROL Adobe Experience Manager Forms]**&#x200B;을(를) 확장 이름으로 지정하십시오.

1. **[!UICONTROL 이벤트 유형]** 드롭다운 목록에서 **[!UICONTROL 사용자 지정 이벤트 캡처]**&#x200B;를 선택합니다.

1. 규칙 편집기를 사용하여 규칙을 만드는 동안 4단계에서 지정한 이벤트의 이름을 지정합니다.

1. **변경 내용 유지**&#x200B;를 선택하고 [규칙 구성](#configure-rules)에 지정된 나머지 작업을 수행합니다.

## 3. [!DNL Adobe Analytics]에서 보고서 구성 및 보기 {#view-reports-adobe-analytics}

이벤트 데이터를 [!DNL Adobe Analytics]에 보내도록 적응형 양식을 구성한 후 [!DNL Adobe Analytics]에서 보고서를 볼 수 있습니다.

1. ![제품 선택](/help/forms/using/assets/select-analytics.png)을 선택하고 **[!UICONTROL 분석]**&#x200B;을 선택합니다.

1. **[!UICONTROL 프로젝트 만들기]**&#x200B;를 선택하고 **[!UICONTROL 빈 프로젝트]**&#x200B;를 선택합니다.

1. 자유 형식의 오른쪽 상단에 있는 드롭다운 목록에서 보고서 세트 이름을 선택합니다.

1. 모든 양식 제목을 보려면 **[!UICONTROL 차원 항목 검색]** 텍스트에서 **양식 제목**&#x200B;을 지정하십시오.

1. 적응형 양식 제목을 **[!UICONTROL 여기에 세그먼트(또는 다른 구성 요소) 놓기]** 텍스트 상자에 놓습니다.

1. **[!UICONTROL 지표]** 섹션에서 추적할 이벤트를 **[!UICONTROL 여기에 지표(또는 다른 구성 요소) 놓기]** 텍스트 상자에 놓습니다.

1. ![시각화](/help/forms/using/assets/visualization-icon.svg)를 선택하고 차트 유형을 자유 형식 섹션에 놓습니다. 마찬가지로 여러 차트 유형을 자유 형식 섹션에 추가할 수 있습니다.

1. Ctrl + S 키를 선택하고 프로젝트를 저장할 이름을 지정합니다.

양식 분석 보고서 보기에 대한 자세한 내용은 [AEM Forms 분석 보고서 보기 및 이해](../../forms/using/view-understand-aem-forms-analytics-reports.md)를 참조하십시오.
