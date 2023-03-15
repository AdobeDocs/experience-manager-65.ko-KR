---
title: 사용자로 등록
seo-title: Registering as a User
description: 사용자 조직의 외부에 있더라도 Document Security 사용자로부터 받은 정책 보호 문서를 사용하는 방법에 대해 알아봅니다.
seo-description: Learn how you can use policy-protected documents that you receive from an document security user, even if you are external to the user’s organization.
uuid: 4648b358-f545-434f-a3b2-2937e961dc64
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: 26e11ef4-9f8f-4b0b-b035-a498fd7d65ef
feature: Document Security
exl-id: 320d8fa4-e200-4993-b018-a9718cddc5c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 6%

---

# 사용자로 등록 {#registering-as-a-user}

사용자 조직의 외부에 있는 경우에도 document security 사용자로부터 받은 정책으로 보호된 문서를 사용할 수 있습니다. 정책으로 보호된 문서를 사용하려면 문서 보안에 등록해야 합니다. 이전에 등록 초대를 받지 않은 경우 다음 이벤트가 발생하면 document security에서 등록 프로세스를 시작합니다.

* 정책으로 보호된 문서를 보내려는 문서 보안 사용자가 귀하를 정책에 추가합니다.
* Document Security 관리자가 계정을 만듭니다.

   계정을 등록하고 활성화한 후에는 정책을 통해 사용할 권한이 있는 정책으로 보호된 문서를 사용할 수 있습니다. Document Security 관리자가 초대된 사용자에 대해 이러한 기능을 활성화하는 경우 다음 작업을 수행할 권한이 있을 수 있습니다.

* document security 정책을 사용하여 Protect 문서.
* 문서에 적용할 수 있는 나만의 사용자 정책을 만듭니다.
* 다른 외부 사용자를 정책에 추가하여 정책으로 보호된 문서를 사용하도록 초대합니다.

   또한 등록 시 다른 정책으로 보호된 문서를 사용하기 위해 다시 등록할 필요가 없습니다. 정책 관리자가 계정을 비활성화하거나 삭제할 때까지 계정은 활성 상태로 유지됩니다.

>[!NOTE]
>
>정책으로 보호된 문서를 받았지만 등록 이메일 초대를 받지 못한 경우 자세한 내용은 문서를 보낸 사람에게 문의하십시오.

## 초대된 사용자로 등록 {#register-as-an-invited-user}

초대받은 사용자이고 document security에서 이메일 등록 메시지를 받은 경우 메시지의 URL을 사용하여 온라인 등록 페이지를 열어 등록할 수 있습니다. 등록하면 계정 활성화에 대한 두 번째 알림을 받게 됩니다.

1. Document Security 등록 이메일을 엽니다. 메시지에 포함된 URL은 문서 보안의 외부 사용자 등록 페이지에 대한 링크입니다.
1. URL을 클릭하거나 복사하여 브라우저에 붙여넣습니다. 외부 사용자 등록 페이지가 표시됩니다.
1. 해당 상자에 이름, 전화 번호, 주소, 조직 및 암호를 입력한 다음 암호 확인 상자에 암호를 다시 입력합니다. 아무 8자의 조합이 암호가 될 수 있습니다.
1. 저장을 클릭합니다. 이메일에 활성화 이메일 메시지가 있는지 확인하라는 감사 메시지가 나타납니다. 이제 등록 프로세스를 완료하려면 계정을 활성화해야 합니다.

## 초대된 사용자 계정 활성화 {#activate-your-invited-user-account}

등록하면 Document Security가 활성화 이메일을 보냅니다. 메시지의 URL을 사용하여 계정을 활성화해야 합니다. 그런 다음 document security에 로그인하여 액세스 권한이 있는 정책으로 보호된 문서를 사용할 수 있습니다. 관리자가 외부 사용자를 위해 활성화하는 기능에 따라 정책을 만들고, 문서에 정책을 적용하고, 다른 외부 사용자를 정책에 추가할 수 있는 권한이 있을 수 있습니다.

관리자가 계정을 비활성화하거나 삭제할 때까지 귀하의 계정은 활성 상태로 유지됩니다.

1. Document Security 등록 확인 이메일을 엽니다.
1. 메시지에 나타나는 URL을 클릭합니다. 문서 보안 활성화 페이지가 표시됩니다.
1. 로그인 페이지로 이동하려면 여기를 클릭하십시오 .
1. 사용자 이름 상자에 document security에 등록한 이메일 주소를 입력합니다. 이 이메일 주소는 기본 문서 보안 사용자 이름입니다.
1. 암호 상자에 등록할 때 생성한 암호를 입력한 다음 로그인을 클릭합니다.

## 암호 재설정 {#reset-your-password}

암호를 잊어버린 경우 정책 관리자가 암호를 재설정할 수 있습니다. 암호를 재설정하면 임시 암호를 사용하여 로그인할 수 있도록 초대하는 이메일이 생성됩니다. 그런 다음 새 암호를 만들 수 있습니다.

새 암호를 받기 위해 Document Security 관리자에게 연락하는 방법에 대한 자세한 내용은 등록 초대를 받은 조직의 활성화 이메일 알림 또는 기타 알림을 참조하십시오.

1. 새 암호가 필요하다고 정책 관리자에게 알립니다.
1. 문서 보안 암호 이메일을 수신하면 열고 새 임시 암호를 가져옵니다.
1. 새 임시 암호를 사용하여 문서 보안에 로그인합니다.
1. 페이지의 오른쪽 위 모서리에 있는 옵션 을 클릭합니다. [외부 사용자] 페이지가 표시됩니다.
1. 암호 변경 을 선택하고 이전 암호 상자에 임시 암호를 입력합니다.
1. 새 암호 상자에 새 암호를 입력한 다음 암호 확인 상자에 다시 입력합니다.
