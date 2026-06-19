---
title: 문서 보안을 위해 외부 브라우저에서 확장 인증 구성
description: 사용자가 시스템 기본 웹 브라우저를 사용하여 Acrobat 또는 Reader에서 정책으로 보호된 PDF 문서에 대해 인증할 수 있도록 외부 브라우저 인증을 구성하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: a452674c-aea0-45d6-88cd-438af539d355
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 89a07256cd5bb850aac19565ad86273322fa1f31
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 1%

---

# 문서 보안을 위해 외부 브라우저에서 확장 인증 구성 {#configure-external-browser-authentication-document-security}

>[!NOTE]
>
> AEM Forms 관리 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

외부 브라우저에서 확장 인증을 사용하면 Acrobat 또는 Reader 내에 임베드된 브라우저 컨트롤 대신 시스템의 기본 웹 브라우저(예: Microsoft Edge 또는 Google Chrome)를 사용하여 정책으로 보호된 PDF 문서에 대해 인증할 수 있습니다. 이를 통해 PassKey, 생체 인식 인증 및 최신 브라우저가 필요한 기타 IDP(Identity Provider) 기능과 같은 최신 인증 방법을 사용할 수 있습니다.

활성화되면 Acrobat 또는 Reader에서 정책으로 보호된 문서를 열면 사용자의 기본 브라우저에서 IDP 로그인 페이지가 실행됩니다. 인증 후 사용자는 자동으로 Acrobat 또는 Reader으로 다시 리디렉션되고 문서의 잠금이 해제됩니다.

## 사전 요구 사항 {#prerequisites}

외부 브라우저 인증을 구성하기 전에 다음 요구 사항이 충족되는지 확인하십시오.

* 서비스 팩 6.5.25.0이(가) 배포된 JEE의 AEM Forms 6.5 또는 지원되는 애플리케이션 서버(JBoss, WebLogic 또는 WebSphere)에 해당 JEE 핫픽스 패치가 설치된 서비스 팩 6.5.24.0. AEM Forms JEE 핫픽스2 6.5.24.0](#software-distribution-links)에 대한 [소프트웨어 배포 링크를 참조하십시오.
* 확장 인증(타사 인증)이 이미 활성화되었으며 IDP에서 작동합니다. [서버 구성 설정](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings) 및 [확장 인증 공급자 추가](/help/forms/using/admin-help/configuring-client-server-options.md#add-the-extended-authentication-provider)를 참조하십시오.
* 최신 업데이트를 사용하여 클라이언트 Windows PC에 설치된 Adobe Acrobat Pro 또는 Adobe Acrobat Reader(64비트)

>[!NOTE]
>
> 외부 브라우저 인증에는 클라이언트에서 지원되는 버전의 Adobe Acrobat 또는 Adobe Acrobat Reader이 필요합니다. 버전 세부 사항 및 업데이트는 [Acrobat 릴리스 노트(2026년 3월 연속 추적)](https://www.adobe.com/devnet-docs/acrobatetk/tools/ReleaseNotesDC/continuous/dccontinuousmarch2026.html#dccontinuousmarchtwentytwentysix)를 참조하십시오.

### AEM Forms JEE 핫픽스2 6.5.24.0에 대한 소프트웨어 배포 링크 {#software-distribution-links}

외부 브라우저 인증은 JEE 서비스 팩 6.5.25.0 이상의 AEM Forms에서 사용할 수 있습니다.

JEE 서비스 팩 6.5.24.0 또는 이전 버전의 AEM Forms을 사용하는 경우 다음 중 하나를 수행하십시오.

* JEE 서비스 팩 6.5.25.0의 [AEM Forms](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)&#x200B;(으)로 업그레이드하십시오.
* 아래 링크를 사용하여 응용 프로그램 서버 및 플랫폼용 AEM Forms JEE 핫픽스 6.5.24.0 패치를 설치하십시오.

[AEM Forms Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 플랫폼에 대한 Adobe JEE 핫픽스 6.5.24.0 패치를 다운로드하여 설치하십시오.

**JBos**

* Windows: [JBoss JEE 서버용 Windows에서 AEM 서비스 팩 6.5.24.0용 핫픽스](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-jboss.zip)
* Linux: [JBoss JEE 서버용 Linux의 AEM 서비스 팩 6.5.24.0용 핫픽스](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-jboss.tar.gz)

**WebSphere**

* Windows: [WebSphere JEE 서버용 Windows에서 AEM 서비스 팩 6.5.24.0용 핫픽스](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-websphere.zip)
* Linux: [WebSphere JEE 서버용 Linux의 AEM 서비스 팩 6.5.24.0용 핫픽스](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-websphere.tar.gz)

**WebLogic**

* Windows: [WebLogic JEE 서버용 Windows에서 AEM 서비스 팩 6.5.24.0용 핫픽스](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-weblogic.zip)
* Linux: [WebLogic JEE 서버용 Linux의 AEM 서비스 팩 6.5.24.0용 핫픽스](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-weblogic.tar.gz)

설치 지침은 [JEE 패치 설치](/help/release-notes/jee-patch-installer-65.md)를 참조하십시오.

## 외부 브라우저 인증 활성화 {#enable-external-browser-authentication}

이 비디오는 AEM Forms Document Security 서버에서 외부 브라우저 인증을 활성화하는 방법을 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/3492357/)

1. 관리 콘솔에서 **서비스** > **문서 보안** > **구성** > **서버 구성**&#x200B;을 클릭합니다.
1. **Adobe 클라이언트 응용 프로그램에 대한 외부 브라우저에서 확장 인증 허용** 섹션을 찾습니다.
1. 활성화할 각 Adobe 클라이언트 플랫폼에 대한 확인란을 선택합니다.
   * **Adobe Acrobat 및 Reader(64비트) - 데스크톱**
   * **Adobe Acrobat Reader(32비트) - 데스크톱**
1. **확인**&#x200B;을 클릭합니다.

서버 설정 설명은 [서버 구성 설정](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings)을 참조하십시오.

<!--
## Client configuration (Acrobat / Reader) {#client-configuration}

External browser authentication is enabled by default in Acrobat and Reader. No client-side configuration is needed for most deployments. When the server is configured to allow external browser authentication, the client uses it automatically.

To disable external browser authentication on specific client machines (forcing the embedded browser fallback), set the following registry value:

`HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Adobe\Adobe Acrobat\<product_branch>\FeatureLockDown\EDC`

| Setting | Value |
| ------- | ----- |
| Value name | `TPExternalBrowserAuthAdmin` |
| Value type | `REG_DWORD` |
| Value data | `0` (to disable) |

>[!NOTE]
>
> Both the server-side setting and the client-side preference must be enabled for external browser authentication to work. If either is disabled, the client falls back to the embedded browser.
-->

## 인증 {#verification}

이 비디오는 외부 브라우저 인증을 확인하는 방법을 보여 줍니다. Acrobat에서 정책으로 보호된 PDF을 열고 기본 브라우저를 통해 로그인하고 인증 후 문서 잠금 해제를 확인합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3492356/)

1. Document Security 서버를 사용하여 정책으로 보호된 PDF 문서를 만듭니다.
1. Windows 클라이언트 시스템에서 Acrobat Pro 또는 Acrobat Reader에서 보호된 PDF을 엽니다.
1. Acrobat에 동의 대화 상자가 표시됩니다. **로그인**&#x200B;을 클릭합니다.
1. 시스템 기본 브라우저가 IDP 로그인 페이지와 함께 열리는지 확인합니다.
1. 인증 완료.
1. 보호된 문서가 성공적으로 열리는지 확인합니다.

## 문제 해결 {#troubleshooting}

### 시스템 브라우저 대신 포함된 브라우저가 열립니다 {#embedded-browser-opens-instead-of-system-browser}

* 서버에 외부 브라우저 인증이 활성화되어 있는지 확인합니다. [외부 브라우저 인증 사용](#enable-external-browser-authentication)을 참조하세요.
* Acrobat 또는 Reader 버전에서 이 기능을 지원하는지 확인합니다. [Acrobat](#acrobat)을(를) 참조하세요.

### 브라우저에서 인증이 성공하지만 문서가 잠금 해제되지 않음 {#authentication-succeeds-but-document-does-not-unlock}

* Acrobat 또는 Reader이 실행 중이며 방화벽 또는 보안 소프트웨어에서 차단되지 않았는지 확인합니다.
* 문제가 지속되면 Acrobat 또는 Reader 설치를 다시 설치하거나 복구하여 프로토콜 처리기 등록을 복원합니다.

### &quot;로그인할 수 없습니다.&quot; 메시지가 Acrobat에 표시됩니다. {#we-couldnt-sign-you-in-message}

* 사용자가 인증을 완료하는 데 너무 오래 걸렸을 수 있습니다. 다시 시도하십시오.
* 브라우저와 AEM Forms 서버 간의 네트워크 연결을 확인합니다.

### 로그인 페이지에 인증 옵션이 나타나지 않습니다 {#authentication-option-does-not-appear}

* 인증 방법 및 옵션은 AEM Forms 또는 Acrobat이 아닌 IDP에 의해 구성됩니다. IDP가 사용할 인증 방법을 지원하는지 확인합니다.
* 로그인 페이지가 포함된 브라우저가 아닌 시스템 브라우저에 로드되는지 확인합니다.
