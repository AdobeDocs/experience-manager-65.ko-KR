---
title: Acrobat Reader DC 확장에서 사용할 자격 증명 구성
seo-title: Acrobat Reader DC 확장에서 사용할 자격 증명 구성
description: Acrobat Reader DC 확장에서 사용할 자격 증명을 구성하는 방법을 알아봅니다.
seo-description: Acrobat Reader DC 확장에서 사용할 자격 증명을 구성하는 방법을 알아봅니다.
uuid: 9210e6c9-6f5c-402d-b355-b104cdffd5eb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5bb32fb1-4b6e-412f-aa16-f60db9dcaba1
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Acrobat Reader DC 확장에서 사용할 자격 증명 구성{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

PDF 문서에 사용 권한을 적용하려면 Acrobat Reader DC 확장에 대한 유효한 자격 증명으로 AEM 양식을 구성합니다. AEM Forms 설치 중에 자격 증명이 구성되었을 수 있습니다. Configuration Manager를 실행하는 동안 Acrobat Reader DC 확장 자격 증명을 구성하지 않았거나 새 자격 증명 또는 교체 자격 증명을 가져와야 하는 경우 저장소 관리 페이지에서 이 작업을 수행할 수 있습니다.

평가 자격 증명을 사용하는 경우 프로덕션 환경으로 이동할 때 프로덕션 자격 증명으로 바꿉니다. 만료 또는 평가 자격 증명을 업데이트하려면 먼저 이전 Acrobat Reader DC 확장 자격 증명을 삭제하십시오.

자격 증명을 가져오는 방법에 대한 자세한 내용은 [AEM Forms 설치 준비(단일 서버)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)를 참조하십시오.

트러스트 저장소에 둘 이상의 Acrobat Reader DC 확장 자격 증명이 포함될 수 있습니다. 이러한 자격 증명 중 하나를 기본 Reader 확장 자격 증명으로 지정해야 합니다. 기본 자격 증명은 Workbench 사용자가 프로세스 생성 중에 사용할 자격 증명을 결정할 수 없을 때 사용됩니다. 이러한 규칙은 기본 자격 증명에 적용됩니다.

* Acrobat Reader DC 확장 자격 증명을 가져오고 트러스트 저장소에 다른 Acrobat Reader DC 확장 자격 증명이 포함되어 있지 않으면 기본값으로 설정됩니다.
* 기본값 옵션을 선택한 상태로 Acrobat Reader DC 확장 자격 증명을 가져오는 경우 기존 기본 자격 증명에서 기본 유형이 제거됩니다. 가져온 자격 증명이 기본값이 됩니다.
* 기본 Acrobat Reader DC 확장 자격 증명은 삭제할 수 없습니다. 기본 자격 증명을 삭제하려면 먼저 다른 자격 증명을 기본값으로 설정합니다. 이 규칙의 예외는 자격 증명이 하나만 있으면 기본값이지만 삭제할 수 있습니다.
* 기본 Acrobat Reader DC 확장 자격 증명은 업데이트할 수 없습니다.

>[!NOTE]
>
>자격 증명을 프로그래밍 방식으로 가져오고 삭제할 수도 있습니다. ([AEM Forms로 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63)을 참조하십시오.)

## Acrobat Reader DC 확장 자격 증명 {#import-a-acrobat-reader-dc-extensions-credential} 가져오기

1. 관리 콘솔에서 설정 > 신뢰 저장소 관리 > 로컬 자격 증명을 클릭합니다.
1. 가져오기를 클릭하고 Trust Store 유형에서 Acrobat Reader DC 확장 자격 증명을 선택합니다.
1. (선택 사항) 이 자격 증명이 Acrobat Reader DC 확장에서 사용할 기본 자격 증명임을 나타내려면 기본값 을 선택합니다.
1. 별칭 상자에 자격 증명의 식별자를 입력합니다. 이 식별자는 Acrobat Reader DC 확장에서 자격 증명의 표시 이름으로 사용됩니다. 이 별칭은 AEM Forms SDK를 사용하여 프로그래밍 방식으로 자격 증명에 액세스하는 데에도 사용됩니다.

   >[!NOTE]
   >
   >표시 목적으로 별칭 이름이 자동으로 대문자로 변환됩니다. 프로세스에서 별칭 이름을 참조할 때는 별칭 이름을 대/소문자를 구분하지 않습니다.

1. 파일 선택 을 클릭하여 자격 증명을 찾고 자격 증명의 암호를 입력한 다음 확인을 클릭합니다.

   &quot;잘못된 파일 형식 또는 잘못된 암호로 인해 자격 증명을 가져오지 못했습니다&quot;라는 오류 메시지가 나타나면 암호가 유효한지 확인하십시오.

## Acrobat Reader DC 확장 자격 증명 {#remove-a-acrobat-reader-dc-extensions-credential} 제거

1. 관리 콘솔에서 설정 > 신뢰 저장소 관리 > 로컬 자격 증명을 클릭합니다.
1. 자격 증명을 선택하고 삭제를 클릭합니다.

## Acrobat Reader DC 확장 자격 증명 {#replace-a-acrobat-reader-dc-extensions-credential} 바꾸기

1. 관리 콘솔에서 설정 > 신뢰 저장소 관리 > 로컬 자격 증명을 클릭합니다.
1. 기존 자격 증명의 별칭을 기록한 다음 해당 별칭을 선택하고 삭제를 누릅니다.
1. 동일한 별칭 이름을 사용하여 새 자격 증명을 가져옵니다.
