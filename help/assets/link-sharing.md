---
title: 링크를 사용하여 자산 공유
description: 자산, 폴더 및 컬렉션을 URL로 공유합니다.
contentOwner: AG
role: Business Practitioner
feature: 링크 공유,자산 관리
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
source-git-commit: 3ec39279d001297dcc11ebd1110bb452de8ca980
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 1%

---

# 링크 {#asset-link-sharing}를 통해 자산 공유

[!DNL Adobe Experience Manager Assets] 자산, 폴더 및 컬렉션을 조직 및 외부 엔티티(파트너 및 공급업체 등)의 멤버와 URL로 공유할 수 있습니다. 링크를 통해 자산을 공유하는 것은 먼저 [!DNL Assets]에 로그인하지 않고도 외부 당사자가 리소스를 사용할 수 있도록 하는 편리한 방법입니다.

>[!PREREQUISITES]
>
>* 링크로 공유할 폴더 또는 자산에 대한 ACL 편집 권한이 필요합니다.
>* 사용자에게 전자 메일을 보내려면 [일 CQ 메일 서비스](#configmailservice)에서 SMTP 서버 세부 사항을 구성합니다.


## 자산 공유 {#share-assets}

사용자와 공유할 자산의 URL을 생성하려면 링크 공유 대화 상자를 사용합니다. 관리자 권한이 있거나 `/var/dam/share` 위치에 읽기 권한이 있는 사용자는 자신과 공유된 링크를 볼 수 있습니다.

1. [!DNL Assets] 사용자 인터페이스에서 링크로 공유할 자산을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 링크 공유]** ![자산 공유 아이콘](assets/do-not-localize/assets_share.png)을 클릭합니다. **[!UICONTROL 공유]**&#x200B;를 클릭한 후 만들 링크는 [!UICONTROL 링크 공유] 필드에 미리 표시됩니다. **[!UICONTROL Submit]**&#x200B;을 클릭하기 전까지는 링크가 아직 만들어지지 않습니다.

   ![링크 공유 대화 상자](assets/Link-sharing-dialog-box.png)

   *그림:링크로 자산을 공유하는 대화 상자*

1. **[!UICONTROL 링크 공유]** 대화 상자의 이메일 주소 상자에 링크를 공유할 사용자의 이메일 ID를 입력합니다. 사용자를 한 명 이상 추가할 수 있습니다.

   ![링크 공유 대화 상자에서 직접 자산에 대한 링크 공유](assets/Asset-Sharing-LinkShareDialog.png)

   *그림:링크 공유 대화 상자에서 직접  [!UICONTROL 자산에 대한 링크] 를 공유합니다.*

   >[!NOTE]
   >
   >조직의 구성원이 아닌 사용자의 이메일 ID를 입력하면 [!UICONTROL 외부 사용자]라는 단어 앞에 사용자의 이메일 ID가 붙습니다.

1. **[!UICONTROL 제목]** 상자에 공유할 자산의 제목을 입력합니다.

1. **[!UICONTROL 메시지]** 상자에 선택적 메시지를 입력합니다.

1. **[!UICONTROL 만료]** 필드에서 링크가 작동하지 않을 만료 날짜 및 시간을 지정합니다. 링크의 기본 만료 시간은 하루입니다.

   ![공유 링크의 만료 날짜 설정](assets/Set-shared-link-expiration.png)

1. 사용자가 표현물과 함께 원본 자산을 다운로드하도록 하려면 **[!UICONTROL 원본 파일 다운로드 허용]**&#x200B;을 선택합니다. 기본적으로 사용자는 링크로 공유하는 자산의 표현물만 다운로드할 수 있습니다.

1. **[!UICONTROL 공유]**&#x200B;를 클릭합니다. 링크가 이메일을 통해 사용자와 공유되는지 확인하는 메시지가 표시됩니다.

1. 공유 자산을 보려면 사용자에게 전송된 이메일의 링크를 클릭합니다. 자산의 미리 보기를 생성하려면 공유 자산을 클릭합니다. 미리 보기를 닫으려면 **[!UICONTROL 뒤로]**&#x200B;를 클릭합니다. 폴더를 공유한 경우 **[!UICONTROL 상위 폴더]**&#x200B;를 클릭하여 상위 폴더로 돌아갑니다.

   ![공유 자산 미리 보기](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] 에서는 지원되는 파일 형식의 자산만 미리  [보기 생성을 지원합니다](/help/assets/assets-formats.md). 다른 MIME 유형이 공유된 경우 자산만 다운로드할 수 있으며 미리 볼 수 없습니다.

1. 공유 자산을 다운로드하려면 도구 모음에서 **[!UICONTROL 선택]**&#x200B;을 클릭하고, 자산을 클릭한 다음, 도구 모음에서 **[!UICONTROL 다운로드]**&#x200B;를 클릭합니다.

   ![공유 자산을 다운로드하는 도구 모음 옵션](assets/chlimage_1-547.png)

1. 링크로 공유한 자산을 보려면 [!DNL Assets] 사용자 인터페이스로 이동하고 [!DNL Experience Manager] 로고를 클릭합니다. **[!UICONTROL 탐색]**&#x200B;을 선택합니다. 탐색 창에서 **[!UICONTROL 공유 링크]**&#x200B;를 선택하여 공유 자산 목록을 표시합니다.

1. 자산 공유를 취소하려면 해당 자산을 선택하고 도구 모음에서 **[!UICONTROL 공유 해제]**&#x200B;를 클릭합니다. 다음은 확인 메시지입니다. 자산의 항목이 목록에서 제거됩니다.

## 일 CQ 메일 서비스 {#configure-day-cq-mail-service} 구성

1. [!DNL Experience Manager] 홈 페이지에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;로 이동합니다.
1. 서비스 목록에서 **[!UICONTROL 일 CQ 메일 서비스]**&#x200B;를 찾습니다.
1. 서비스 옆에 있는 **[!UICONTROL 편집]**&#x200B;을 클릭하고 **[!UICONTROL Day CQ Mail Service]**&#x200B;에 대해 이름에 대해 언급된 세부 사항을 사용하여 다음 매개 변수를 구성합니다.

   * SMTP 서버 호스트 이름:이메일 서버 호스트 이름
   * SMTP 서버 포트:전자 메일 서버 포트
   * SMTP 사용자:이메일 서버 사용자 이름
   * SMTP 암호:이메일 서버 암호

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 최대 데이터 크기 {#configure-maximum-data-size} 구성

링크 공유 기능을 사용하여 공유된 링크에서 자산을 다운로드할 때 [!DNL Experience Manager] 은 저장소에서 자산 계층을 압축한 다음 ZIP 파일에 있는 자산을 반환합니다. 그러나 ZIP 파일로 압축할 수 있는 데이터 양에 제한이 없는 경우 대량의 데이터가 압축되어 JVM에서 메모리 오류가 발생합니다. 이러한 상황으로 인해 시스템을 잠재적 서비스 거부 공격으로부터 보호하려면 구성 관리자에서 **[!UICONTROL 최대 컨텐츠 크기(압축되지 않음)]** CQ DAM Adhoc Asset Share 프록시 서블릿&#x200B;]**에 대한 매개 변수를 사용하여 최대 크기를 구성하십시오.**[!UICONTROL  자산의 압축되지 않은 크기가 구성된 값을 초과하는 경우 자산 다운로드 요청이 거부됩니다. 기본값은 100MB입니다.

1. [!DNL Experience Manager] 로고를 클릭한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;으로 이동합니다.
1. 웹 콘솔에서 **[!UICONTROL 일 CQ DAM 애드혹 자산 공유 프록시 서블릿]** 구성을 찾습니다.
1. 편집 모드에서 **[!UICONTROL 일 CQ DAM 애드혹 자산 공유 프록시 서블릿]** 구성을 열고 **[!UICONTROL 최대 컨텐츠 크기(압축되지 않음)]** 매개 변수의 값을 수정합니다.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 변경 사항을 저장합니다.

## 우수 사례 및 문제 해결 {#best-practices-and-troubleshooting}

* 이름에 공백이 포함된 자산 폴더 또는 컬렉션은 공유되지 않을 수 있습니다.
* 사용자가 공유 자산을 다운로드할 수 없는 경우 [!DNL Experience Manager] 관리자에게 [다운로드 제한](#configure-maximum-data-size)이 무엇인지 문의하십시오.
* 공유 자산에 대한 링크가 있는 이메일을 보낼 수 없거나 다른 사용자가 이메일을 받을 수 없는 경우 [이메일 서비스](#configure-day-cq-mail-service)가 구성되어 있는지 여부를 [!DNL Experience Manager] 관리자에게 문의하십시오.
* 링크 공유 기능을 사용하여 자산을 공유할 수 없는 경우 적절한 권한이 있는지 확인하십시오. [자산 공유](#share-assets)를 참조하십시오.
* 공유 자산이 다른 위치로 이동되면 해당 링크가 작동하지 않습니다. 링크를 다시 만들고 사용자와 다시 공유합니다.

* [!DNL Experience Manager] 작성자 배포의 링크를 외부 엔티티로 공유하려면 링크 공유에 사용되는 다음 URL만(`GET` 요청에만 해당)이 표시되는지 확인하십시오. 보안상의 이유로 다른 URL을 차단합니다.

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`
   [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;에 액세스합니다. **[!UICONTROL Day CQ Link Externalizer]** 구성을 열고 **[!UICONTROL Domains]** 필드에서 다음 속성을 `local`, `author` 및 `publish`에 대해 언급된 값으로 수정합니다. `local` 및 `author` 속성의 경우 각각 로컬 및 작성자 인스턴스의 URL을 제공합니다. 단일 [!DNL Experience Manager] 작성자 인스턴스를 실행하는 경우 `local` 및 `author` 속성에 동일한 값을 사용합니다. 게시 인스턴스의 경우 [!DNL Experience Manager] 게시 인스턴스의 URL을 제공합니다.
