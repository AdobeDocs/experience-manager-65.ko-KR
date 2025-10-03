---
title: Acrobat Reader DC 확장 프로그램에서 사용할 자격 증명 구성
description: Acrobat Reader DC 확장 프로그램에서 사용할 자격 증명을 구성하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '558'
ht-degree: 100%

---

# Acrobat Reader DC 확장 프로그램에서 사용할 자격 증명 구성{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

PDF 문서에 사용 권한을 적용하려면 Acrobat Reader DC 확장 프로그램에 유효한 자격 증명으로 AEM Forms를 구성합니다. AEM Forms를 설치하는 동안 자격 증명이 구성되었을 수 있습니다. 구성 관리자를 실행하는 동안 Acrobat Reader DC 확장 프로그램 자격 증명을 구성하지 않았거나 새 자격 증명 또는 교체 자격 증명을 가져와야 하는 경우 Trust Store 관리 페이지에서 해당 작업을 수행할 수 있습니다.

평가 자격 증명을 사용하는 경우 프로덕션 환경으로 전환할 때 프로덕션 자격 증명으로 바꿉니다. 만료된 자격 증명 또는 평가 자격 증명을 업데이트하려면 먼저 기존 Acrobat Reader DC 확장 프로그램 자격 증명을 삭제하십시오.

자격 증명 획득에 대한 자세한 내용은 [AEM Forms(단일 서버) 설치 준비](https://helpx.adobe.com/kr/pdf/aem-forms/6-3/prepare-install-single-server.pdf)를 참조하십시오.

Trust Store에는 두 개 이상의 Acrobat Reader DC 확장 프로그램 자격 증명이 포함될 수 있습니다. 해당 자격 증명 중 하나를 기본 Reader 확장 프로그램 자격 증명으로 지정합니다. 기본 자격 증명은 워크벤치 사용자가 프로세스 생성 중에 어떤 자격 증명을 사용해야 할지를 결정할 수 없는 경우에 사용됩니다. 다음 규칙은 기본 자격 증명에 적용됩니다.

* Acrobat Reader DC 확장 프로그램 자격 증명을 가져오고 Trust Store에 다른 Acrobat Reader DC 확장 프로그램 자격 증명이 없으면 해당 자격 증명이 기본값으로 설정됩니다.
* 기본 옵션을 선택하여 Acrobat Reader DC 확장 프로그램 자격 증명을 가져오면 기존 기본 자격 증명에서 기본 유형이 제거되고 가져온 자격 증명이 기본값이 됩니다.
* 기본 Acrobat Reader DC 확장 프로그램 자격 증명은 삭제할 수 없습니다. 기본 자격 증명을 삭제하려면 먼저 다른 자격 증명을 기본값으로 설정하십시오. 이 규칙은 자격 증명이 하나뿐인 경우 기본값이더라도 삭제할 수 있다는 예외가 있습니다.
* 기본 Acrobat Reader DC 확장 프로그램 자격 증명은 업데이트할 수 없습니다.

>[!NOTE]
>
>자격 증명을 프로그래밍 방식으로 가져오거나 삭제할 수도 있습니다. ([AEM Forms를 사용한 프로그래밍](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html)을 참조하십시오.)

## Acrobat Reader DC 확장 프로그램 자격 증명 가져오기 {#import-a-acrobat-reader-dc-extensions-credential}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

1. 관리 콘솔에서 설정 > Trust Store 관리 > 로컬 자격 증명을 클릭합니다.
1. 가져오기를 클릭하고 Trust Store 유형에서 Acrobat Reader DC 확장 프로그램 자격 증명을 선택합니다.
1. (선택 사항) 이 자격 증명이 Acrobat Reader DC 확장 프로그램에서 사용할 기본 자격 증명임을 나타내려면 기본값을 선택합니다.
1. 별칭 상자에 자격 증명에 대한 식별자를 입력합니다. 이 식별자는 Acrobat Reader DC 확장 프로그램에서 자격 증명의 표시 이름으로 사용됩니다. 이 별칭은 AEM Forms SDK를 사용하여 자격 증명에 프로그래밍 방식으로 액세스하는 데에도 사용됩니다.

   >[!NOTE]
   >
   >별칭은 표시 목적에 따라 대문자로 자동 변환됩니다. 프로세스에서 별칭을 참조할 때는 대소문자를 구분하지 않습니다.

1. 파일 선택을 클릭하여 자격 증명을 찾고 자격 증명의 암호를 입력한 후 확인을 클릭합니다.

   “잘못된 파일 형식 또는 잘못된 암호로 인해 자격 증명을 가져오지 못했습니다.”라는 오류 메시지가 나타나면 암호가 유효한지 확인합니다.

## Acrobat Reader DC 확장 프로그램 자격 증명 제거 {#remove-a-acrobat-reader-dc-extensions-credential}

1. 관리 콘솔에서 설정 > Trust Store 관리 > 로컬 자격 증명을 클릭합니다.
1. 자격 증명을 선택하고 삭제를 클릭합니다.

## Acrobat Reader DC 확장 프로그램 자격 증명 교체 {#replace-a-acrobat-reader-dc-extensions-credential}

1. 관리 콘솔에서 설정 > Trust Store 관리 > 로컬 자격 증명을 클릭합니다.
1. 기존 자격 증명의 별칭을 기록한 후 해당 별칭을 선택하고 삭제를 클릭합니다.
1. 정확히 동일한 별칭 이름을 사용하여 새 자격 증명을 가져옵니다.
