---
title: 다중 스레드 파일 변환 활성화
description: 다중 스레드 파일 변환을 활성화하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '896'
ht-degree: 100%

---

# 다중 스레드 파일 변환 활성화 {#enabling-multi-threaded-file-conversions}

PDF Generator를 사용하면 특정 유형의 파일에 대해 다중 스레드 파일 변환을 활성화할 수 있습니다. 다중 스레드 파일 변환은 동시에 여러 변환을 수행할 수 있게 하여 PDF Generator의 성능을 향상합니다.

## OpenOffice, Word, PowerPoint 문서에 대한 다중 스레드 파일 변환 활성화 {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

기본적으로 PDF Generator는 한 번에 하나의 OpenOffice, Microsoft® Word, PowerPoint 문서만 변환할 수 있습니다. 다중 스레드 변환을 활성화하면 PDF Generator가 두 개 이상의 문서를 동시에 변환할 수 있습니다. PDF Generator는 OpenOffice 또는 PDFMaker의 여러 인스턴스를 실행합니다(Word 및 PowerPoint 변환을 수행하는 데 사용됨).

>[!NOTE]
>
>Microsoft® Word 2003 및 PowerPoint 2003에서는 다중 스레드 파일 변환이 지원되지 않습니다. 다중 스레드 파일 변환을 활성화하려면 Microsoft® Word 2007 및 PowerPoint 2007 또는 Microsoft® Word 2010 및 PowerPoint 2010으로 업그레이드하십시오.

>[!NOTE]
>
>Microsoft® Excel, Microsoft® Visio, Microsoft® Project, Microsoft® Publisher에서는 다중 스레드 파일 변환이 지원되지 않습니다.

OpenOffice 또는 PDFMaker의 각 인스턴스는 별도의 사용자 계정을 사용하여 실행됩니다. 추가하는 각 사용자 계정은 Forms 서버 컴퓨터에 대한 관리자 권한이 있는 유효한 사용자여야 합니다. 클러스터링된 환경에서는 동일한 사용자 집합이 클러스터의 모든 노드에 대해 유효해야 합니다.

관리 콘솔의 사용자 계정 페이지에서 다중 스레드 파일 변환에 사용할 사용자 계정을 지정할 수 있습니다. 계정을 추가하고 삭제하거나 계정 암호를 변경할 수 있습니다. Windows Server 2003 또는 Windows Server 2008에서 PDF Generator를 실행하는 경우 관리자 권한이 있는 사용자 계정을 3개 이상 추가합니다.

Windows Server 2003 또는 2008의 OpenOffice, Microsoft® Word, Microsoft® PowerPoint 또는 Linux® 또는 Sun™ Solaris™의 OpenOffice에 사용자를 추가할 때 모든 사용자에 대한 초기 활성화 대화 상자를 닫습니다.

### 프로세스 수준 토큰을 교체할 수 있는 권한 추가 {#add-the-right-to-replace-the-process-level-token}

Windows 운영 체제에서 PDF 변환에 사용되는 관리자 사용자 계정(PDFG 사용자)은 프로세스 수준 토큰 권한을 교체해야 합니다. 이 권한은 그룹 정책 편집기를 사용하여 추가할 수 있습니다.

1. Windows 시작 메뉴에서 실행을 클릭한 후 gpedit.msc를 입력합니다.
1. 로컬 컴퓨터 정책 > 컴퓨터 구성 > Windows 설정 > 보안 설정 > 로컬 정책 > 사용자 권한 할당을 클릭합니다. *프로세스 수준 토큰 교체* 정책을 편집하여 관리자 그룹을 포함합니다.
1. 사용자를 프로세스 수준 토큰 교체 항목에 추가합니다.

### Windows Server 2008의 OpenOffice, Microsoft® Word, Microsoft® PowerPoint에 대한 추가 구성이 필요합니다. {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Windows Server 2008에서 OpenOffice, Microsoft® Word, Microsoft® PowerPoint를 실행하는 경우 추가된 각 사용자에 대해 UAC를 비활성화합니다.

1. 제어판 > 사용자 계정 > 사용자 계정 컨트롤 켜기 또는 끄기를 클릭합니다.
1. &#39;사용자 계정 컨트롤(UAC)을 사용하여 컴퓨터 보호&#39; 상자를 선택 취소하고 확인을 클릭합니다.
1. 컴퓨터를 다시 시작하여 설정을 적용합니다.

### Linux® 또는 Solaris™의 OpenOffice에 필요한 추가 구성 {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. 사용자 계정을 추가합니다. ([사용자 계정 추가](enabling-multi-threaded-file-conversions.md#add-a-user-account)를 참조하십시오.)
1. 다음으로, /etc/sudoers 파일을 변경해야 합니다. 이 파일의 기본 권한은 440입니다. 이 파일의 권한을 쓰기 가능으로 변경합니다.
1. /etc/sudoers 파일에서 Forms 서버를 실행하는 관리자 외의 추가 사용자에 대한 항목을 추가합니다. 예를 들어 lcadm이라는 사용자와 myhost라는 서버로 AEM Forms를 실행하고 user1과 user2를 가장하려는 경우 /etc/sudoers에 다음 항목을 추가합니다.

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   이 구성을 사용하면 lcadm이 암호를 묻지 않고도 &#39;myhost&#39; 호스트에서 &#39;user1&#39; 또는 &#39;user2&#39;로 모든 명령을 실행할 수 있습니다.

   >[!NOTE]
   >
   >&#39;user1&#39;과 &#39;user2&#39;에 시스템 사용자와 PDFG 사용자 역할을 할당했는지 확인하십시오. 사용자에게 PDFG 역할을 할당하려면 [사용자 계정 추가](enabling-multi-threaded-file-conversions.md#add-a-user-account)를 참조하십시오.

1. 또한 /etc/sudoers 파일에서 다음 줄을 찾아 줄의 시작 부분에 숫자 기호(#)를 추가하여 주석 처리합니다.

   ```shell
   Defaults requiretty
   ```

   이 작업을 수행하면 Linux® 사용자를 추가할 수 있습니다.

1. etc/sudoers 파일 권한을 다시 440으로 변경합니다.
1. [사용자 계정 추가](enabling-multi-threaded-file-conversions.md#add-a-user-account)를 통해 추가한 모든 사용자가 Forms 서버에 연결할 수 있도록 허용합니다. 예를 들어 user1이라는 로컬 사용자에게 Forms 서버에 연결할 수 있는 권한을 부여하려면 다음 명령을 사용합니다.

   `xhost +local:user1@`

   자세한 내용은 xhost 명령 설명서를 참조하십시오.

1. 서버를 다시 시작합니다.

>[!NOTE]
>
>OpenOffice는 모든 PDFG 사용자가 액세스할 수 있는 디렉터리 위치에 설치해야 합니다. 이를 확인하려면 PDFG 사용자로 로그인하여 문제 없이 OpenOffice를 실행할 수 있으면 됩니다.

### 사용자 계정 추가 {#add-a-user-account}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

1. 관리 콘솔에서 서비스 > PDF Generator > 사용자 계정을 클릭합니다.
1. 추가를 클릭하고 Forms 서버에 대한 관리 권한이 있는 사용자의 사용자 이름 및 암호를 입력합니다. OpenOffice 사용자를 구성하는 경우 초기 OpenOffice 활성화 대화 상자를 닫습니다.

   >[!NOTE]
   >
   >OpenOffice 사용자를 구성하는 경우 OpenOffice 인스턴스 수는 이 단계에서 지정한 사용자 계정 수보다 클 수 없습니다.

1. Forms 서버를 다시 시작합니다.

### 다중 스레드 파일 변환에 사용되는 목록에서 사용자 제거 {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. 관리 콘솔에서 서비스 > PDF Generator > 사용자 계정을 클릭합니다.
1. 제거할 사용자 옆에 있는 확인란을 클릭하고 삭제를 클릭합니다.
1. 확인 페이지에서 삭제를 클릭합니다.
1. Forms 서버를 다시 시작합니다.

### 계정 암호 변경 {#change-the-password-for-an-account}

1. 관리 콘솔에서 서비스 > PDF Generator > 사용자 계정을 클릭합니다.
1. 사용자 이름을 클릭하고 새 암호를 입력한 후 확인합니다. 이 암호는 사용자의 시스템 암호와 일치해야 합니다.
