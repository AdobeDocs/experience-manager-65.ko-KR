---
title: 공유 에셋에 대한 URL 생성
description: 이 문서에서는 AEM 자산 내에서 자산, 폴더 및 컬렉션을 외부 당사자에게 URL로 공유하는 방법에 대해 설명합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 링크를 통해 에셋 공유 {#asset-link-sharing}

AEM(Adobe Experience Manager) 자산을 사용하면 자산, 폴더 및 컬렉션을 조직 구성원 및 파트너, 벤더를 비롯한 외부 엔티티와 URL로 공유할 수 있습니다. 링크를 통해 자산을 공유하는 것은 AEM 자산에 먼저 로그인하지 않고도 외부 당사자가 리소스를 사용할 수 있도록 하는 편리한 방법입니다.

>[!NOTE]
>
>링크로 공유할 폴더 또는 자산에 대해 ACL 편집 권한이 필요합니다.

## 자산 공유 {#sharelink}

사용자와 공유할 에셋의 URL을 생성하려면 링크 공유 대화 상자를 사용합니다. 관리자 권한이 있거나 읽기 권한이 있는 사용자는 `/var/dam/share` 해당 사용자와 공유된 링크를 볼 수 있습니다.

>[!NOTE]
>
>사용자와 링크를 공유하기 전에 요일 CQ 메일 서비스가 구성되어 있는지 확인합니다. 먼저 일 CQ 메일 서비스를 [구성하지 않고 링크를 공유하려고 하면 오류가 발생합니다](/help/assets/link-sharing.md#configmailservice).

1. 자산 사용자 인터페이스에서 링크로 공유할 자산을 선택합니다.
1. 도구 모음에서 공유 링크 **[!UICONTROL 자산_공유를]** 클릭/탭합니다 ![](assets/assets_share.png).

   [링크 공유] 필드에 자산 링크가 자동으로 **[!UICONTROL 만들어집니다]** . 이 링크를 복사하고 사용자와 공유합니다. 링크의 기본 만료 시간은 하루입니다.

   ![링크 공유 대화 상자](assets/Link-sharing-dialog-box.png)

   *그림:에셋을 링크로 공유하는 대화 상자*

   또는 이 절차의 3-7단계를 수행하여 이메일 수신자를 추가하고 링크의 만료 시간을 구성한 다음 대화 상자에서 보냅니다.

   >[!NOTE]
   >
   >AEM 작성자 인스턴스의 링크를 외부 엔티티에 공유하려면 `GET` 요청에 대해서만 다음 URL(링크 공유에 사용)만 표시해야 합니다. 다른 URL을 차단하여 AEM 작성자의 보안을 보장합니다.
   >
   >* http://&lt;aem_server>:&lt;port>/linkshare.html
   * http://&lt;aem_server>:&lt;port>/linksharepreview.html
   * http://&lt;aem_server>:&lt;port>/linkexpired.html


   >[!NOTE]
   공유 에셋이 다른 위치로 이동하면 해당 링크가 작동하지 않습니다. 링크를 다시 만들고 사용자와 다시 공유합니다.

1. AEM 인터페이스에서 도구 > **[!UICONTROL 작업]** > **[!UICONTROL 웹]** 콘솔에 **[!UICONTROL 액세스합니다]**.

1. 요일 **[!UICONTROL CQ 링크 외부라이저]** 구성을 열고 도메인 **[!UICONTROL 필드에서 다음]** 속성을 `local`, `author`및 에 대해 언급된 값으로 수정합니다 `publish`. 및 `local` `author` 속성에 대해 로컬 및 작성자 인스턴스의 URL을 각각 제공합니다. 단일 Experience Manager 작성자 인스턴스를 실행하는 경우 `local` 및 `author` 속성 모두 동일한 값을 갖습니다. 예를 `publish`들어 Experience Manager 게시 인스턴스에 대한 URL을 제공합니다.

1. [링크 공유] **[!UICONTROL 대화 상자의]** 이메일 주소 상자에 링크를 공유할 사용자의 이메일 ID를 입력합니다. 여러 사용자와 링크를 공유할 수도 있습니다.

   사용자가 조직의 구성원인 경우 입력 영역 아래 목록에 표시되는 제안된 이메일 ID에서 사용자의 이메일 ID를 선택합니다. 외부 사용자의 경우 전체 이메일 ID를 입력한 다음 목록에서 선택합니다.

   사용자에게 보낼 이메일을 활성화하려면 요일 CQ 메일 서비스에서 SMTP 서버 [세부 사항을 구성합니다](#configmailservice).

   ![링크 공유 대화 상자에서 바로 에셋에 대한 링크 공유](assets/Asset-Sharing-LinkShareDialog.png)

   *그림:링크 공유 대화 상자에서 바로 에셋에 대한[!UICONTROL 링크를 공유할 수]있습니다.*

   >[!NOTE]
   조직의 구성원이 아닌 사용자의 이메일 ID를 입력하면 외부 [!UICONTROL 사용자라는] 단어가 사용자의 이메일 ID로 접두사로 추가됩니다.

1. 제목 **[!UICONTROL 필드에]** 공유할 자산의 제목을 입력합니다.

1. 메시지 **[!UICONTROL 필드에]** 선택적 메시지를 입력합니다.

1. 만료 **[!UICONTROL 필드에서]** 날짜 선택기를 사용하여 링크의 만료 날짜 및 시간을 지정합니다. 기본적으로 만료 날짜는 링크를 공유하는 날짜로부터 일주일 동안 설정됩니다.

   ![공유 링크의 만료 날짜 설정](assets/Set-shared-link-expiration.png)

1. 사용자가 변환과 함께 원본 이미지를 다운로드할 수 있도록 하려면 원본 파일 **[!UICONTROL 다운로드 허용을 선택합니다]**.

   >[!NOTE]
   기본적으로 사용자는 링크로 공유하는 자산의 표현물만 다운로드할 수 있습니다.

1. **[!UICONTROL 공유]**&#x200B;를 클릭합니다. 링크가 이메일을 통해 사용자와 공유됨을 확인하는 메시지가 표시됩니다.
1. 공유 자산을 보려면 사용자에게 전송되는 이메일의 링크를 클릭/탭합니다. 공유 자산은 Adobe Marketing Cloud **[!UICONTROL 페이지에 표시됩니다]** .

   ![chlimage_1-260](assets/chlimage_1-545.png)

   목록 보기로 전환하려면 도구 모음에서 레이아웃 옵션을 클릭/탭합니다.

1. 자산의 미리 보기를 생성하려면 공유 자산을 클릭/탭합니다. 미리 보기를 닫고 Marketing Cloud **[!UICONTROL 페이지로 돌아가려면]** 도구 모음에서 뒤로를 클릭/ **[!UICONTROL 탭합니다]** . 폴더를 공유한 경우 상위 폴더를 클릭/탭하여 **[!UICONTROL 상위]** 폴더로 돌아갑니다.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   AEM 파섹JPG, PNG, GIF, BMP, INDD, PDF 및 PPT입니다. 다른 MIME 유형의 자산만 다운로드할 수 있습니다.

1. 공유 자산을 다운로드하려면 **[!UICONTROL 도구 모음에서 선택을]** 누르고 자산을 클릭/탭한 다음 도구 **[!UICONTROL 모음에서 다운로드를 클릭/탭]** 탭합니다.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. 공유한 자산을 링크로 보려면 자산 UI로 이동하고 Experience Manager 로고를 누릅니다. 목록에서 **[!UICONTROL 내비게이션을]** 선택하여 탐색 창을 표시합니다.
1. 탐색 창에서 공유 **[!UICONTROL 링크를]** 선택하여 공유 에셋 목록을 표시합니다.
1. 자산 공유를 취소하려면 자산을 선택하고 도구 모음에서 **[!UICONTROL 공유]** 해제를 탭/클릭합니다. 확인 메시지는 다음과 같습니다. 자산의 항목이 목록에서 제거됩니다.

## 일 CQ 메일 서비스 구성 {#configmailservice}

1. Experience Manager 홈 페이지에서 도구 > 작업 **** > **[!UICONTROL 웹]** 콘솔로 **[!UICONTROL 이동합니다]**.
1. 서비스 목록에서 Day CQ Mail **[!UICONTROL Service를 찾습니다]**.
1. 서비스 **[!UICONTROL 옆에]** 있는 편집을 누르고, 이름에 대해 **[!UICONTROL 명시된 세부 사항과 함께 Day CQ Mail Service에 대해]** 다음 매개 변수를 구성합니다.

   * SMTP 서버 호스트 이름:이메일 서버 호스트 이름
   * SMTP 서버 포트:이메일 서버 포트
   * SMTP 사용자:이메일 서버 사용자 이름
   * SMTP 암호:이메일 서버 암호
   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Click/tap **[!UICONTROL Save]**.

## 최대 데이터 크기 구성 {#maxdatasize}

링크 공유 기능을 사용하여 공유된 링크에서 자산을 다운로드할 때 AEM은 저장소에서 자산 계층을 압축한 다음 ZIP 파일로 자산을 반환합니다. 그러나 ZIP 파일에서 압축할 수 있는 데이터 양에 제한이 없는 경우 엄청난 양의 데이터가 압축되어 JVM에서 메모리 오류가 발생합니다. 이러한 상황에서 시스템을 잠재적 서비스 거부 공격으로부터 보호하려면 Configuration Manager의 일 CQ DAM Adhoc **[!UICONTROL Asset Share 프록시 서블릿에 대한 최대 컨텐트 크기(비압축)]** 매개 변수를 [!UICONTROL 사용하여 최대 크기를] 구성합니다. 자산의 압축되지 않은 크기가 구성된 값을 초과하는 경우 자산 다운로드 요청이 거부됩니다. 기본값은 100MB입니다.

1. AEM 로고를 클릭/탭한 다음 도구 > **[!UICONTROL 작업]** > **[!UICONTROL 웹]** 콘솔로 **[!UICONTROL 이동합니다]**.
1. 웹 콘솔에서 CQ DAM Adhoc **[!UICONTROL Asset Share 프록시 서블릿 구성을 찾습니다]** .
1. 편집 **[!UICONTROL 모드에서 일 CQ DAM 애드혹 자산 공유 프록시]** 서블릿 구성을 열고 최대 컨텐트 크기(압축되지 않은) **** 매개 변수의 값을 수정합니다.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 변경 사항을 저장합니다.

## Best practices and troubleshooting {#bestpractices}

* 이름에 공백이 포함된 자산 폴더 또는 컬렉션은 공유되지 않을 수 있습니다.
* 사용자가 공유 자산을 다운로드할 수 없는 경우 AEM 관리자에게 [다운로드 제한이](#maxdatasize) 무엇인지 확인하십시오.
* 공유 자산에 대한 링크가 포함된 이메일을 보낼 수 없거나 다른 사용자가 이메일을 받을 수 없는 경우 [이메일 서비스가](#configmailservice) 구성되었는지 여부를 AEM 관리자에게 문의하십시오.
* 링크 공유 기능을 사용하여 자산을 공유할 수 없는 경우 적절한 권한이 있는지 확인하십시오. 자산 [공유를 참조하십시오](#sharelink).
