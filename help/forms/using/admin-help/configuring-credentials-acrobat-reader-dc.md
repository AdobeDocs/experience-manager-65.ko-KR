---
title: Acrobat Reader DC 확장에 사용할 자격 증명 구성
description: Acrobat Reader DC 확장에 사용할 자격 증명을 구성하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# Acrobat Reader DC 확장에 사용할 자격 증명 구성{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

PDF 문서에 사용 권한을 적용하려면 Acrobat Reader DC 확장에 대한 유효한 자격 증명으로 AEM 양식을 구성하십시오. AEM Forms를 설치하는 동안 자격 증명이 구성되었을 수 있습니다. 구성 관리자를 실행하는 동안 Acrobat Reader DC 확장 자격 증명을 구성하지 않았거나 새 자격 증명 또는 대체 자격 증명을 가져와야 하는 경우 Trust Store Management 페이지를 사용하여 구성할 수 있습니다.

평가 자격 증명을 사용하는 경우 프로덕션 환경으로 이동할 때 프로덕션 자격 증명으로 교체합니다. 만료된 자격 증명 또는 평가 자격 증명을 업데이트하려면 먼저 이전 Acrobat Reader DC 확장 자격 증명을 삭제하십시오.

자격 증명을 얻는 방법에 대한 자세한 내용은 [AEM 양식(단일 서버) 설치 준비](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf)를 참조하십시오.

Trust Store에 두 개 이상의 Acrobat Reader DC 확장 자격 증명이 포함될 수 있습니다. 이러한 자격 증명 중 하나를 기본 Reader 확장 자격 증명으로 지정합니다. Workbench 사용자가 프로세스 생성 중에 사용할 자격 증명을 결정할 수 없을 때 기본 자격 증명이 사용됩니다. 다음 규칙은 기본 자격 증명에 적용됩니다.

* Acrobat Reader DC 확장 자격 증명을 가져오고 Trust Store에 다른 Acrobat Reader DC 확장 자격 증명이 없는 경우 이 자격 증명이 기본값으로 설정됩니다.
* 기본 옵션을 선택한 상태로 Acrobat Reader DC 확장 자격 증명을 가져오는 경우 기존 기본 자격 증명에서 기본 유형이 제거됩니다. 가져온 자격 증명이 기본값이 됩니다.
* 기본 Acrobat Reader DC 확장 자격 증명을 삭제할 수 없습니다. 기본 자격 증명을 삭제하려면 먼저 다른 자격 증명을 기본값으로 설정합니다. 이 규칙의 예외는 자격 증명이 하나만 있는 경우 기본값이지만 삭제할 수 있다는 것입니다.
* 기본 Acrobat Reader DC 확장 자격 증명을 업데이트할 수 없습니다.

>[!NOTE]
>
>자격 증명을 프로그래밍 방식으로 가져오고 삭제할 수도 있습니다. ([AEM 양식을 사용한 프로그래밍](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ko)을 참조하십시오.)

## Acrobat Reader DC 확장 자격 증명 가져오기 {#import-a-acrobat-reader-dc-extensions-credential}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

1. 관리 콘솔에서 설정 > Trust Store Management > 로컬 자격 증명을 클릭합니다.
1. 가져오기를 클릭하고 Trust Store Type에서 Acrobat Reader DC Extensions Credential 을 선택합니다.
1. (선택 사항) 이 자격 증명이 Acrobat Reader DC 확장과 함께 사용할 기본 자격 증명임을 나타내려면 [기본값]을 선택합니다.
1. 별칭 상자에 자격 증명의 식별자를 입력합니다. 이 식별자는 Acrobat Reader DC 확장에서 자격 증명의 표시 이름으로 사용됩니다. 이 별칭은 AEM forms SDK을 사용하여 프로그래밍 방식으로 자격 증명에 액세스하는 데에도 사용됩니다.

   >[!NOTE]
   >
   >표시 목적으로 별칭 이름은 자동으로 대문자로 변환됩니다. 별칭 이름은 프로세스에서 참조할 때 대소문자를 구분하지 않습니다.

1. 파일 선택 을 클릭하여 자격 증명을 찾고 자격 증명의 암호를 입력한 다음 확인 을 클릭합니다.

   &quot;잘못된 파일 형식 또는 잘못된 암호로 인해 자격 증명을 가져오지 못했습니다.&quot;라는 오류 메시지가 나타나면 암호가 올바른지 확인하십시오.

## Acrobat Reader DC 확장 자격 증명 제거 {#remove-a-acrobat-reader-dc-extensions-credential}

1. 관리 콘솔에서 설정 > Trust Store Management > 로컬 자격 증명을 클릭합니다.
1. 자격 증명을 선택하고 삭제 를 클릭합니다.

## Acrobat Reader DC 확장 자격 증명 바꾸기 {#replace-a-acrobat-reader-dc-extensions-credential}

1. 관리 콘솔에서 설정 > Trust Store Management > 로컬 자격 증명을 클릭합니다.
1. 기존 자격 증명의 별칭을 메모한 다음 선택하고 삭제를 클릭합니다.
1. 완전히 동일한 별칭 이름을 사용하여 새 자격 증명을 가져옵니다.
