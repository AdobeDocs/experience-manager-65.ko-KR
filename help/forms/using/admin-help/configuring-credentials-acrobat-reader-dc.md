---
title: Acrobat Reader DC 익스텐션에서 사용할 자격 증명 구성
seo-title: Acrobat Reader DC 익스텐션에서 사용할 자격 증명 구성
description: Acrobat Reader DC 익스텐션에서 사용할 자격 증명을 구성하는 방법을 알아봅니다.
seo-description: Acrobat Reader DC 익스텐션에서 사용할 자격 증명을 구성하는 방법을 알아봅니다.
uuid: 9210e6c9-6f5c-402d-b355-b104cdffd5eb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5bb32fb1-4b6e-412f-aa16-f60db9dcaba1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Acrobat Reader DC 확장{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}에 사용할 자격 증명 구성

PDF 문서에 사용 권한을 적용하려면 Acrobat Reader DC 익스텐션에 대한 유효한 자격 증명으로 AEM 양식을 구성합니다. AEM 양식을 설치하는 동안 자격 증명이 구성되었을 수 있습니다. Configuration Manager를 실행하는 동안 Acrobat Reader DC 확장 자격 증명을 구성하지 않았거나 새 자격 증명 또는 교체 자격 증명을 가져와야 하는 경우 Trust Store 관리 페이지를 사용하여 이 자격 증명을 구성할 수 있습니다.

평가판 자격 증명을 사용하는 경우 프로덕션 환경으로 이동할 때 프로덕션 자격 증명으로 교체하십시오. 만료된 자격 증명 또는 평가 자격 증명을 업데이트하려면 먼저 이전 Acrobat Reader DC 확장 자격 증명을 삭제합니다.

자격 증명을 얻는 방법에 대한 자세한 내용은 [AEM 양식 설치 준비(단일 서버)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)를 참조하십시오.

Trust Store에 둘 이상의 Acrobat Reader DC 확장 자격 증명이 포함될 수 있습니다. 이러한 자격 증명 중 하나를 기본 Reader 확장 자격 증명으로 지정해야 합니다. 기본 자격 증명은 워크벤치 사용자가 프로세스 생성 중에 사용할 자격 증명을 확인할 수 없을 때 사용됩니다. 이러한 규칙은 기본 자격 증명에 적용됩니다.

* Acrobat Reader DC 확장 자격 증명을 가져오고 Trust Store에 다른 Acrobat Reader DC 확장 자격 증명이 없는 경우 기본적으로 설정됩니다.
* [기본값] 옵션을 선택한 상태로 Acrobat Reader DC 확장 자격 증명을 가져오는 경우 기본 유형은 기존 기본 자격 증명에서 제거됩니다. 가져온 자격 증명이 기본값이 됩니다.
* 기본 Acrobat Reader DC 확장 자격 증명은 삭제할 수 없습니다. 기본 자격 증명을 삭제하려면 먼저 다른 자격 증명을 기본값으로 설정합니다. 이 규칙의 예외는 자격 증명이 하나만 있으면 기본값이지만 삭제할 수 있다는 것입니다.
* 기본 Acrobat Reader DC 확장 자격 증명을 업데이트할 수 없습니다.

>[!NOTE]
>
>자격 증명을 프로그래밍 방식으로 가져오거나 삭제할 수도 있습니다. (AEM 양식[을 사용하여 프로그래밍 참조)](https://www.adobe.com/go/learn_aemforms_programming_63)

## Acrobat Reader DC 확장 자격 증명 가져오기 {#import-a-acrobat-reader-dc-extensions-credential}

1. 관리 콘솔에서 설정 > 트러스트 저장소 관리 > 로컬 자격 증명을 클릭합니다.
1. [가져오기]를 클릭하고 [신뢰 저장소 유형]에서 [Acrobat Reader DC 확장 자격 증명]을 선택합니다.
1. (선택 사항) 이 자격 증명이 Acrobat Reader DC 확장 프로그램에 사용할 기본 자격 증명임을 나타내려면 [기본값]을 선택합니다.
1. 별칭 상자에 자격 증명의 식별자를 입력합니다. 이 식별자는 Acrobat Reader DC 확장명의 자격 증명을 위한 표시 이름으로 사용됩니다. 이 별칭은 AEM 양식 SDK를 사용하여 프로그래밍 방식으로 자격 증명에 액세스하는 데에도 사용됩니다.

   >[!NOTE]
   >
   >표시 목적으로 별칭 이름이 자동으로 대문자로 변환됩니다. 프로세스에서 별칭 이름을 참조할 때는 별칭 이름에 대/소문자를 구분하지 않습니다.

1. [파일 선택]을 클릭하여 자격 증명을 찾고 자격 증명의 암호를 입력한 다음 [확인]을 클릭합니다.

   &quot;잘못된 파일 형식 또는 잘못된 암호로 인해 자격 증명을 가져오지 못했습니다&quot; 오류 메시지가 표시되는 경우 암호가 올바른지 확인하십시오.

## Acrobat Reader DC 확장 자격 증명 제거 {#remove-a-acrobat-reader-dc-extensions-credential}

1. 관리 콘솔에서 설정 > 트러스트 저장소 관리 > 로컬 자격 증명을 클릭합니다.
1. 자격 증명을 선택하고 [삭제]를 클릭합니다.

## Acrobat Reader DC 확장 자격 증명 {#replace-a-acrobat-reader-dc-extensions-credential} 교체

1. 관리 콘솔에서 설정 > 트러스트 저장소 관리 > 로컬 자격 증명을 클릭합니다.
1. 기존 자격 증명의 별칭을 기록한 다음 해당 별칭을 선택하고 [삭제]를 클릭합니다.
1. 동일한 별칭 이름을 사용하여 새 자격 증명을 가져옵니다.

