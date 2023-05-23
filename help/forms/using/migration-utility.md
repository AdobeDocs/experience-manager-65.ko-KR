---
title: AEM Forms 에셋 및 문서 마이그레이션
seo-title: Migrate AEM Forms assets and documents
description: 마이그레이션 유틸리티를 사용하면 AEM Forms 에셋 및 문서를 AEM 6.3 Forms 또는 이전 버전에서 AEM 6.4 Forms으로 마이그레이션할 수 있습니다.
seo-description: The Migration utility allows you to Migrate AEM Forms assets and documents from AEM 6.3 Forms or prior versions to AEM 6.4 Forms.
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
role: Admin
exl-id: 0f9aab7d-8e41-449a-804b-7e1bfa90befd
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 2%

---

# AEM Forms 에셋 및 문서 마이그레이션{#migrate-aem-forms-assets-and-documents}

마이그레이션 유틸리티는 [적응형 Forms 에셋](../../forms/using/introduction-forms-authoring.md), [클라우드 구성](/help/sites-developing/extending-cloud-config.md), 및 [서신 관리 에셋](/help/forms/using/cm-overview.md) 이전 버전에서 사용된 형식에서 AEM 6.5 Forms에서 사용된 형식으로 변환되었습니다. 마이그레이션 유틸리티를 실행하면 다음이 마이그레이션됩니다.

* 적응형 양식을 위한 사용자 정의 구성 요소
* 적응형 양식 및 서신 관리 템플릿
* 클라우드 구성
* 서신 관리 및 적응형 양식 에셋

>[!NOTE]
>
>위치 외 업그레이드 시 서신 관리 에셋의 경우 에셋을 가져올 때마다 마이그레이션을 실행할 수 있습니다. 서신 관리 마이그레이션의 경우 Forms 호환성 패키지를 설치해야 합니다.

## 마이그레이션 방법 {#approach-to-migration}

다음을 수행할 수 있습니다. [업그레이드](../../forms/using/upgrade.md) AEM Forms 6.4, 6.3 또는 6.2에서 최신 버전의 AEM Forms 6.5로 전환하거나 새로 설치합니다. 이전 설치를 업그레이드했는지 또는 새 설치를 수행했는지 여부에 따라 다음 중 하나를 수행해야 합니다.

**즉각적으로 업그레이드**

원본 위치 업그레이드를 수행한 경우 업그레이드된 인스턴스에 이미 에셋과 문서가 있습니다. 그러나 에셋 및 문서를 사용하려면 먼저 를 설치해야 합니다 [AEMFD 호환성 패키지](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) (서신 관리 호환성 패키지 포함)

그런 다음 다음을 수행하여 에셋 및 문서를 업데이트해야 합니다. [마이그레이션 유틸리티 실행](#runningmigrationutility).

**위치 외에서 설치하는 경우**

잘못된(새로운) 설치인 경우 에셋 및 문서를 사용하려면 먼저 설치해야 합니다 [AEMFD 호환성 패키지](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) (서신 관리 호환성 패키지 포함).

그런 다음 새 설정에서 자산 패키지(zip 또는 cmp)를 가져온 다음, 다음과 같이 자산 및 문서를 업데이트해야 합니다 [마이그레이션 유틸리티 실행](#runningmigrationutility). Adobe은 마이그레이션 유틸리티를 실행한 후에만 새 설정에서 새 자산을 만들 것을 권장합니다.

기한: [이전 버전과의 호환성 관련](/help/sites-deploying/backward-compatibility.md) crx-repository에 있는 몇 개의 폴더의 위치인 변경 사항이 변경되었습니다. 종속성(사용자 정의 라이브러리 및 에셋)을 이전 설정에서 새 환경으로 수동으로 내보내고 가져옵니다.

## 마이그레이션을 진행하기 전에 읽기 {#prerequisites}

서신 관리 자산의 경우:

* 이전 플랫폼에서 가져온 자산의 경우 속성이 추가됩니다. **fd:version=1.0**.
* AEM 6.1 Forms 이후 주석은 즉시 사용할 수 없습니다. 이전에 추가한 주석은 에셋에서 사용할 수 있지만 인터페이스에 자동으로 표시되지 않습니다. 댓글이 표시되도록 하려면 AEM Forms 사용자 인터페이스에서 extendedProperties 속성을 사용자 정의해야 합니다.
* LiveCycle ES4 등 이전 버전 일부에서는 Flex RichTextEditor를 사용하여 텍스트를 편집했지만, AEM 6.1 Forms 이후로는 HTML 편집기가 사용됩니다. 이러한 렌더링 및 글꼴 모양 때문에 글꼴, 글꼴 크기 및 글꼴 여백은 작성자 사용자 인터페이스의 이전 버전과 다를 수 있습니다. 그러나 렌더링할 때는 문자가 동일하게 표시됩니다.
* 텍스트 모듈의 목록이 개선되어 이제 다르게 렌더링됩니다. 시각적인 차이가 있을 수 있습니다. 텍스트 모듈에서 목록을 사용하는 문자를 렌더링하고 확인하는 것이 좋습니다.
* 이미지 콘텐츠 모듈이 DAM 에셋으로 변환되고 마이그레이션 중에 레이아웃 및 조각이 양식에 추가되므로 이러한 모듈에 대한 업데이트한 사람 속성이 관리자로 변경됩니다.
* 에셋의 버전 내역은 마이그레이션되지 않으며 마이그레이션 후에는 사용할 수 없습니다. 마이그레이션 후 후속 버전 내역이 유지됩니다.
* AEM 6.1 Forms 이후 게시 준비 상태가 더 이상 사용되지 않으므로 게시 준비 상태의 모든 자산이 수정됨 상태로 변경됩니다.
* 사용자 인터페이스가 AEM Forms 6.3에서 업데이트되므로 맞춤화를 수행하는 단계도 다릅니다. 6.3 이전 버전에서 마이그레이션하는 경우 사용자 지정을 다시 실행해야 합니다.
* 레이아웃 조각이 /content/apps/cm/layouts/fragmentlayouts/1001에서 /content/apps/cm/modules/fragmentlayouts로 이동합니다. 에셋의 데이터 사전 참조는 이름 대신 데이터 사전의 경로를 표시합니다.
* 텍스트 모듈에서 정렬에 사용되는 모든 탭 공간을 재조정해야 합니다. 자세한 내용은 [서신 관리 - 탭 간격을 사용하여 텍스트 정렬](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* Asset Composer 구성이 서신 관리 구성으로 변경되었습니다.
* 에셋은 기존 텍스트 및 기존 목록과 같은 이름의 폴더로 이동됩니다.

## 마이그레이션 유틸리티 사용 {#using-the-migration-utility}

### 마이그레이션 유틸리티 실행 {#runningmigrationutility}

자산을 변경하거나 자산을 만들기 전에 마이그레이션 유틸리티를 실행하십시오. 변경하거나 자산을 만든 후에는 유틸리티를 실행하지 않는 것이 좋습니다. 마이그레이션 프로세스가 실행되는 동안 서신 관리 또는 적응형 Forms Assets 사용자 인터페이스가 열리지 않도록 하십시오.

마이그레이션 유틸리티를 처음 실행하면 다음과 같은 경로와 이름으로 로그가 만들어집니다. `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. 이 로그는 서신 관리 및 적응형 Forms 마이그레이션 정보(예: 에셋 이동)로 계속 업데이트됩니다.

>[!NOTE]
>
>마이그레이션 유틸리티를 실행하기 전에 crx 저장소를 백업했는지 확인하십시오.

1. 브라우저 세션에서 AEM 작성자 인스턴스에 관리자로 로그인합니다.

1. 브라우저에서 다음 URL을 엽니다.

   https://[*호스트 이름*]:[*포트*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   브라우저에는 네 가지 옵션이 표시됩니다.

   * AEM Forms 에셋 마이그레이션
   * 적응형 Forms 맞춤형 구성 요소 마이그레이션
   * 적응형 Forms 템플릿 마이그레이션
   * AEM Forms 클라우드 구성 마이그레이션

1. 마이그레이션을 수행하려면 다음을 수행하십시오.

   * 마이그레이션하려면 **assets**, AEM Forms Assets 마이그레이션 을 탭하고 다음 화면에서 을 탭합니다. **마이그레이션 시작**. 다음 항목이 마이그레이션됩니다.

      * 적응형 양식
      * 문서 단편
      * 테마
      * 편지
      * 데이터 사전

   >[!NOTE]
   >
   >에셋을 마이그레이션하는 동안 &quot;다음에 대한 충돌 발견...&quot;과 같은 경고 메시지가 표시될 수 있습니다. 이러한 메시지는 적응형 양식의 일부 구성 요소에 대한 규칙을 마이그레이션할 수 없음을 나타냅니다. 예를 들어, 구성 요소에 규칙과 스크립트가 모두 있는 이벤트가 있는 경우, 스크립트 후에 규칙이 발생하면 구성 요소에 대한 규칙 중 어느 것도 마이그레이션되지 않습니다. 다음을 수행할 수 있습니다. [규칙 편집기를 열어 이러한 규칙 마이그레이션](#migrate-rules) 를 참조하십시오.

   * 적응형 양식 사용자 지정 구성 요소를 마이그레이션하려면 다음을 누릅니다. **적응형 Forms 맞춤형 구성 요소 마이그레이션** 그리고 사용자 지정 구성 요소 마이그레이션 페이지에서 을 누릅니다. **마이그레이션 시작**. 다음 항목이 마이그레이션됩니다.

      * 적응형 Forms을 위해 작성된 사용자 지정 구성 요소
      * 구성 요소 오버레이(있는 경우)
   * 적응형 양식 템플릿을 마이그레이션하려면 다음을 누르십시오. **적응형 Forms 템플릿 마이그레이션** 그리고 사용자 지정 구성 요소 마이그레이션 페이지에서 을 누릅니다. **마이그레이션 시작**. 다음 항목이 마이그레이션됩니다.

      * 적응형 양식 템플릿 `/apps` 또는 `/conf` AEM 템플릿 편집기 사용.
   * AEM Forms 클라우드 구성 서비스를 마이그레이션하여 터치 지원 UI(아래)가 포함된 새로운 컨텍스트 인식 클라우드 서비스 패러다임을 활용합니다 `/conf`). AEM Forms 클라우드 구성 서비스를 마이그레이션할 때에서 클라우드 서비스 `/etc` 이동 위치: `/conf`. 기존 경로를 사용하는 클라우드 서비스 사용자 지정이 없는 경우(`/etc`) 6.5로 업그레이드한 후 바로 마이그레이션 유틸리티를 실행하고 클라우드 구성 Touch UI를 사용하여 추가 작업을 하는 것이 좋습니다. 기존 클라우드 서비스 사용자 정의가 있는 경우 마이그레이션된 경로에 맞게 사용자 정의가 업데이트될 때까지 업그레이드된 설정에서 클래식 UI를 계속 사용합니다(`/conf`) 그런 다음 마이그레이션 유틸리티를 실행합니다.

   마이그레이션하려면 **AEM Forms 클라우드 서비스**, 다음을 포함하는 AEM Forms 클라우드 구성 마이그레이션(클라우드 구성 마이그레이션은 AEMFD 호환성 패키지와 독립적)을 탭하고 AEM Forms 클라우드 구성 마이그레이션 을 탭한 다음 구성 마이그레이션 페이지에서 을 탭합니다 **마이그레이션 시작**:

   * 양식 데이터 모델 클라우드 서비스

      * 소스 경로: `/etc/cloudservices/fdm`
      * Target 경로: `/conf/global/settings/cloudconfigs/fdm`
   * Recaptcha

      * 소스 경로: `/etc/cloudservices/recaptcha`
      * Target 경로: `/conf/global/settings/cloudconfigs/recaptcha`
   * Adobe Sign

      * 소스 경로: `/etc/cloudservices/echosign`
      * Target 경로: `/conf/global/settings/cloudconfigs/echosign`
   * Typekit 클라우드 서비스

      * 소스 경로: `/etc/cloudservices/typekit`
      * Target 경로: `/conf/global/settings/cloudconfigs/typekit`

   마이그레이션 프로세스가 진행될 때 브라우저 창에 다음 항목이 표시됩니다.

   * 에셋이 업데이트될 때: 에셋이 정상적으로 업데이트되었습니다.
   * 마이그레이션이 완료되면: 에셋에 대한 마이그레이션을 완료했습니다.

   실행 시 마이그레이션 유틸리티는 다음을 수행합니다.

   * **에셋에 태그를 추가합니다.**: &quot;서신 관리 : 마이그레이션된 에셋&quot; / &quot;적응형 Forms : 마이그레이션된 에셋&quot; 태그를 추가합니다. 로 이동하여 사용자가 마이그레이션된 에셋을 식별할 수 있도록 합니다. 마이그레이션 유틸리티를 실행하면 시스템의 모든 기존 자산이 마이그레이션됨으로 표시됩니다.
   * **태그 생성**: 이전 시스템에 있는 카테고리 및 하위 카테고리가 태그로 만들어진 다음, 이러한 태그가 AEM의 관련 서신 관리 에셋과 연결됩니다. 예를 들어 편지 템플릿의 범주(클레임)와 하위 범주(클레임)가 태그로 생성됩니다.










1. 마이그레이션 유틸리티 실행이 완료되면 [하우스키핑 작업](#housekeepingtasks).

#### 규칙 편집기를 사용하여 규칙 마이그레이션 {#migrate-rules}

이러한 구성 요소는 적응형 Forms 편집기의 규칙 편집기에서 열어 마이그레이션할 수 있습니다.

* 사용자 지정 구성 요소에서 규칙 및 스크립트(6.3에서 업그레이드하는 경우 필요하지 않음)를 마이그레이션하려면 적응형 Forms 사용자 지정 구성 요소 마이그레이션 을 탭하고 다음 화면에서 마이그레이션 시작 을 탭합니다. 다음 항목이 마이그레이션됩니다.

   * 규칙 편집기(6.1 FP1 이상)를 사용하여 생성된 규칙 및 스크립트

   * 6.1 및 이전 버전의 UI에서 스크립트 탭을 사용하여 작성된 스크립트

* 템플릿을 마이그레이션하려면(6.3 및 6.4에서 업그레이드하는 경우 필요하지 않음) 적응형 Forms 템플릿 마이그레이션 을 탭하고 다음 화면에서 마이그레이션 시작 을 탭합니다. 다음 항목이 마이그레이션됩니다.

   * 이전 템플릿 - AEM 6.1 Forms 또는 이전 버전을 사용하여 /apps에 생성된 적응형 양식 템플릿. 여기에는 템플릿 구성 요소에서 정의된 스크립트가 포함됩니다.

   * 새 템플릿 - /conf 아래에 템플릿 편집기를 사용하여 작성된 적응형 양식 템플릿. 여기에는 규칙 편집기를 사용하여 만든 규칙과 스크립트의 마이그레이션이 포함됩니다.

### 마이그레이션 유틸리티 실행 후 하우스키핑 작업 {#housekeepingtasks}

마이그레이션 유틸리티를 실행한 후 다음 하우스키핑 작업을 수행하십시오.

1. 레이아웃 및 단편 레이아웃의 XFA 버전이 3.3 이상인지 확인합니다. 이전 버전의 레이아웃 및 단편 레이아웃을 사용하는 경우 편지 렌더링에 문제가 있을 수 있습니다. 이전 XFA의 버전을 최신 버전으로 업데이트하려면 다음 단계를 완료하십시오.

   1. [XFA를 zip 파일로 다운로드](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) Forms 사용자 인터페이스에서 다음을 수행합니다.
   1. 파일을 추출합니다.
   1. 최신 Designer에서 XFA 파일을 열고 저장합니다. XFA 버전이 최신 버전으로 업데이트됩니다.
   1. Forms 사용자 인터페이스에서 XFA를 업로드합니다.

1. 마이그레이션 전에 이전 시스템에 게시된 모든 자산을 게시합니다. 마이그레이션 유틸리티는 작성자 인스턴스의 자산만 업데이트하며, 게시 인스턴스의 자산을 업데이트하려면 자산을 게시해야 합니다.

1. AEM Forms 6.4 및 6.5에서 양식 사용자 그룹의 일부 권한이 변경되었습니다. 모든 사용자가 스크립트가 포함된 XDP 및 적응형 Forms을 업로드하거나 코드 편집기를 사용할 수 있도록 하려면 해당 사용자를 forms-power-users 그룹에 추가해야 합니다. 마찬가지로 템플릿 작성자는 더 이상 규칙 편집기에서 코드 편집기를 사용할 수 없습니다. 사용자가 코드 편집기를 사용할 수 있도록 af-template-script-writers 그룹에 추가합니다. 그룹에 사용자를 추가하는 방법에 대한 지침은 [사용자 및 사용자 그룹 관리](/help/communities/users.md).
