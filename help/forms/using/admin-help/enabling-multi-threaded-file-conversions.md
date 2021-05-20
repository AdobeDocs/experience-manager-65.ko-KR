---
title: 다중 스레드 파일 변환 활성화
seo-title: 다중 스레드 파일 변환 활성화
description: 다중 스레드 파일 변환을 활성화하는 방법을 알아봅니다.
seo-description: 다중 스레드 파일 변환을 활성화하는 방법을 알아봅니다.
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
feature: PDF 생성기
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# 다중 스레드 파일 변환 활성화 {#enabling-multi-threaded-file-conversions}

PDF Generator는 특정 유형의 파일에 대해 멀티스레드 파일 변환을 활성화하는 기능을 제공합니다. 다중 스레드 파일 변환은 PDF 생성기가 동시에 여러 전환을 수행할 수 있도록 하여 성능을 향상시킵니다.

## OpenOffice, Word 및 PowerPoint 문서에 대해 다중 스레드 파일 변환을 사용하도록 설정 {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

기본적으로 PDF 생성기는 한 번에 하나의 OpenOffice, Microsoft Word 또는 PowerPoint 문서만 변환할 수 있습니다. 다중 스레드 변환을 사용할 경우 PDF 생성기는 두 개 이상의 문서를 동시에 변환할 수 있습니다. PDF 생성기는 OpenOffice 또는 PDFMaker의 여러 인스턴스를 실행합니다(Word 및 PowerPoint 변환을 수행하는 데 사용됨).

>[!NOTE]
>
>다중 스레드 파일 변환은 Microsoft Word 2003 및 PowerPoint 2003에서 지원되지 않습니다. 다중 스레드 파일 변환을 사용하려면 Microsoft Word 2007 및 PowerPoint 2007 또는 Microsoft Word 2010 및 PowerPoint 2010으로 업그레이드하십시오.

>[!NOTE]
>
>다중 스레드 파일 변환은 Microsoft Excel, Microsoft Visio, Microsoft Project 또는 Microsoft Publisher에서 지원되지 않습니다.

OpenOffice 또는 PDFMaker의 각 인스턴스는 별도의 사용자 계정을 사용하여 실행됩니다. 추가하는 각 사용자 계정은 Forms 서버 컴퓨터에 대한 관리 권한이 있는 유효한 사용자여야 합니다. 클러스터형 환경에서는 클러스터의 모든 노드에 대해 동일한 사용자 세트가 유효해야 합니다.

관리 콘솔의 사용자 계정 페이지에서 다중 스레드 파일 변환에 사용할 사용자 계정을 지정할 수 있습니다. 계정을 추가하거나, 삭제하거나, 계정 암호를 변경할 수 있습니다. Windows Server 2003 또는 Windows Server 2008에서 PDF 생성기를 실행 중인 경우 관리자 권한이 있는 사용자 계정을 3개 이상 추가합니다.

Windows Server 2003 또는 2008의 OpenOffice, Microsoft Word, Microsoft PowerPoint 또는 Linux 또는 Sun™ Solaris™의 OpenOffice용 사용자를 추가할 때 모든 사용자의 초기 활성화 대화 상자를 닫습니다.

### 프로세스 수준 토큰 {#add-the-right-to-replace-the-process-level-token}을 바꿀 권한을 추가합니다.

Windows 운영 체제에서 PDF 변환에 사용되는 관리자 사용자 계정(PDFG 사용자)은 프로세스 수준 토큰 권한을 바꿔야 합니다. 그룹 정책 편집기를 사용하여 이 권한을 추가할 수 있습니다.

1. Windows 시작 메뉴에서 실행 을 클릭한 다음 gppedit.msc를 입력합니다.
1. 로컬 컴퓨터 정책 > 컴퓨터 구성 > Windows 설정 > 보안 설정 > 로컬 정책 > 사용자 권한 할당을 클릭합니다. Administrators 그룹을 포함하려면 *프로세스 수준 토큰* 정책을 편집합니다.
1. 프로세스 수준 토큰 바꾸기 항목에 사용자를 추가합니다.

### Windows Server 2008의 OpenOffice, Microsoft Word 및 Microsoft PowerPoint에 필요한 추가 구성 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Windows Server 2008에서 OpenOffice, Microsoft Word 또는 Microsoft PowerPoint를 실행 중인 경우 추가한 각 사용자에 대해 UAC를 사용하지 않도록 설정합니다.

1. Campaign 컨트롤 패널 > 사용자 계정 > 사용자 계정 제어 설정 또는 해제를 클릭합니다.
1. &quot;Use User Account Control (UAC) to help your computer(사용자 계정 컨트롤 사용)&quot; 상자를 선택 취소하고 [확인]을 클릭합니다.
1. 설정을 적용하려면 컴퓨터를 다시 시작하십시오.

### Linux 또는 Solaris 기반 OpenOffice에 필요한 추가 구성 {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. 사용자 계정을 추가합니다. ([사용자 계정 추가](enabling-multi-threaded-file-conversions.md#add-a-user-account)를 참조하십시오.)
1. 그런 다음 /etc/sudoers 파일을 변경합니다. 이 파일의 기본 권한은 440입니다. 이 파일에 대한 권한을 쓰기 가능으로 변경합니다.
1. /etc/sudoers 파일에 추가 사용자(forms 서버를 실행하는 관리자 제외)에 대한 항목을 추가합니다. 예를 들어, lcadm이라는 사용자로 AEM Forms를 실행하고 myhost라는 서버를 실행하는 경우 user1 및 user2를 가장하려면 다음 항목을 /etc/sudoers에 추가합니다.

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   이 구성을 통해 lcadm은 암호를 확인하지 않고 &#39;myhost&#39; 호스트의 모든 명령을 &#39;user1&#39; 또는 &#39;user2&#39;로 실행할 수 있습니다.

   >[!NOTE]
   >
   >시스템 사용자 및 PDFG 사용자 역할을 &#39;user1&#39; 및 &#39;user2&#39;에 할당했는지 확인합니다. 사용자에게 PDFG 역할을 할당하려면 [사용자 계정 추가](enabling-multi-threaded-file-conversions.md#add-a-user-account)를 참조하십시오

1. 또한 /etc/sudoers 파일에서 줄 시작 부분에 숫자 기호(#)를 추가하여 이 줄을 찾아 주석을 답니다.

   ```shell
   Defaults requiretty
   ```

   Linux 사용자를 추가할 수 있습니다.

1. etc/users 파일에 대한 권한을 다시 440으로 변경합니다.
1. [사용자 계정 추가](enabling-multi-threaded-file-conversions.md#add-a-user-account)를 통해 추가한 모든 사용자가 Forms 서버에 연결할 수 있도록 합니다. 예를 들어, user1이라는 로컬 사용자가 Forms 서버에 연결할 수 있는 권한을 부여하려면 다음 명령을 사용하십시오

   `xhost +local:user1@`

   자세한 내용은 xhost 명령 설명서를 참조하십시오.

1. 서버를 다시 시작합니다.

>[!NOTE]
>
>모든 PDFG 사용자가 액세스할 수 있는 디렉터리 위치에 OpenOffice를 설치해야 합니다. PDFG 사용자로 로그인하고 문제 없이 OpenOffice를 시작할 수 있는지 확인하여 이를 확인할 수 있습니다.

### 사용자 계정 추가 {#add-a-user-account}

1. 관리 콘솔에서 서비스 > PDF Generator > 사용자 계정을 클릭합니다.
1. 추가를 클릭하고 forms 서버에 대한 관리 권한이 있는 사용자의 사용자 이름과 암호를 입력합니다. OpenOffice에 대한 사용자를 구성하는 경우 초기 OpenOffice 활성화 대화 상자를 닫습니다.

   >[!NOTE]
   >
   >OpenOffice에 대한 사용자를 구성하는 경우 OpenOffice 인스턴스 수는 이 단계에서 지정한 사용자 계정 수보다 클 수 없습니다.

1. Forms 서버를 다시 시작합니다.

### 다중 스레드 파일 변환에 사용되는 목록에서 사용자를 제거합니다. {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. 관리 콘솔에서 서비스 > PDF Generator > 사용자 계정을 클릭합니다.
1. 제거할 사용자 옆에 있는 확인란을 클릭하고 삭제를 클릭합니다.
1. 확인 페이지에서 삭제를 클릭합니다.
1. Forms 서버를 다시 시작합니다.

### 계정 {#change-the-password-for-an-account} 암호 변경

1. 관리 콘솔에서 서비스 > PDF Generator > 사용자 계정을 클릭합니다.
1. 사용자 이름을 클릭하고 새 암호를 입력하고 확인합니다. 이 암호는 사용자의 시스템 암호와 일치해야 합니다.
