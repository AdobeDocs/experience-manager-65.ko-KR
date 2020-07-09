---
title: 알려진 문제
description: Adobe Experience Manager 6.5의 알려진 문제에 관한 릴리스 노트입니다
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 0a55ed44cb7fe3320b2196df38fe8492ee03912d
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 57%

---


# 알려진 문제 {#known-issues}

이 페이지는 4월 4일에 출시된 Adobe Experience Manager 6.5의 알려진 문제 목록을 보관합니다.

알려진 문제에 대한 추가 정보가 필요한 경우 [지원 팀에 문의](https://helpx.adobe.com/kr/support/experience-manager.html)하십시오.

## 플랫폼 {#platform}

* CRX-Quickstart 및 해당 컨텐츠가 삭제되는 문제가 보고됩니다.

   이러한 작업 각각에 대해 &quot;htmllibmanager.fileSystemOutputCacheLocation **&quot; 속성이 빈 문자열이 아닌지 확인하십시오.

   1. &quot;*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true&quot;를*&#x200B;호출합니다.
   2. AEM 6.5로 업그레이드
   3. AEM 6.5에서 &quot;lazy content migration&quot;을 실행합니다.

   이 [문제에 대한 자세한 내용 및 해결 방법과 함께 기술 자료](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) 문서를 사용할 수 있습니다.

* AEM 6.5 인스턴스에서 JDK 11을 사용하는 경우 일부 패키지를 배포한 후 일부 페이지가 공백으로 표시될 수 있습니다. 로그 파일에 다음 오류 메시지가 표시됩니다.

   ```
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

이 오류를 해결하려면 다음을 수행하십시오.

1. AEM 인스턴스를 중지합니다. 이동 `<aem_server_path_on_server>crx-quickstart\conf` 후 `sling.properties` 파일을 엽니다. 이 파일의 백업을 수행하는 것이 좋습니다.

2. Search for `org.osgi.framework.bootdelegation=`. 결과를 표시할 `jdk.internal.reflect,jdk.internal.reflect.*` 속성을 추가합니다.

   ```
   org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
   ```

3. 파일을 저장하고 AEM 인스턴스를 다시 시작합니다.

## 자산 {#assets}

* **검색:** 검색 문자열에 선행 공백이 포함된 경우([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786)) 검색이 반환되지 않습니다.
* **폴더 메타데이터 스키마**: 선택 버튼을 추가한 후에 ID 및 값 필드가 예상대로 렌더링되지 않고 삭제 기능이 작동하지 않습니다. (CQ-4261144)
* 자산의 이름을 변경할 때 자산 이름에서 공백을 사용할 수 없습니다. (CQ-4266403)

## 양식 {#forms}

* Linux 운영 시스템에 AEM Forms가 설치된 경우 하드웨어 보안 모듈에 있는 디지털 서명이 작동하지 않습니다. (CQ-4266721)
* (WebSphere의 AEM Forms만 해당) **Forms Workflow** > **태스크 검색** 옵션이 검색 기준으로 **사용자 이름**&#x200B;을 **관리자**&#x200B;로 검색할 경우 결과를 반환하지 않습니다. (CQ-4266457)

* AEM Forms가 JPEG 압축으로 .tif 및 .tiff 파일을 PDF 문서로 변환하지 못합니다. (CQ-4265972)
* **AEM Forms 자산 스캐너** 및 **인터랙티브 커뮤니케이션 마이그레이션 서신** 옵션이 **AEM Forms Migration** 페이지에서 작동하지 않습니다. (CQ-4266572)

* (JBoss 7에만 해당) 이전 버전에서 AEM 6.5 Forms로 업그레이드하면 기본 제출 또는 기본 렌더링 프로세스의 사본을 만들어 사용한 프로세스(.lca)가 이전 버전에서 필요한 작업을 수행하지 못합니다. (CQ-4243928)
* 적응형 양식에서 양식 데이터 모델 서비스가 규칙 편집기에서 호출되어 이미지 선택 구성 요소 값을 동적으로 업데이트하는 경우 이미지 선택 구성 요소 값이 업데이트되지 않습니다. (CQ-4254754)
* AEM Forms Designer installer requires the 32-bit version of [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) and [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). 설치를 시작하기 전에 위에서 설명한 재배포 가능 런타임 패키지가 설치되어 있는지 확인하십시오. (CQ-4265668)

* PDF Generator는 스마트 카드 기반 인증을 지원하지 않습니다.  관리자가 Windows 서버에서 그룹 정책 `Interactive Logon: Require Smart card` 을 활성화하면 기존 PDF Generator 사용자가 모두 무효화됩니다.

* 적응형 양식이 구성 요소의 값을 동적으로 업데이트하도록 구성되고 양식을 호스팅하는 게시 인스턴스에 디스패처를 통해 액세스할 때 필드의 값을 동적으로 업데이트하는 기능의 작동이 중단됩니다. 이 문제를 해결하려면 게시 인스턴스에서 CRXDE를 열고 /libs/fd/af/runtime/clientlibs/guideChartReducer로 이동한 다음 아래에 나열된 속성을 생성합니다.

   * Name: allowProxy
   * Type: Boolean
   * Value: true
   * Protected: False
   * Mandatory: False
   * Multiple: False
   * Auto Created: Flase

   이 속성으로 런타임 폴더 아래의 클라이언트 라이브러리가 프록시에 액세스할 수 있습니다. (CQ-4268679)

* 
   * AEM Forms이 시작되면 경고가 `SAX Security Manager could not be setup` 나타납니다.