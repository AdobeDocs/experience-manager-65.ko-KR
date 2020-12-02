---
title: 자산 번역 우수 사례
description: 번역된 다양한 버전을 동기화하고 번역 워크플로우를 간소화하기 위한 효율적인 자산 관리를 위한 모범 사례
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 3%

---


# 자산 번역 우수 사례 {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] 다국어 워크플로우를 지원하므로 디지털 자산에 대한 바이너리, 메타데이터 및 태그를 여러 개의 로캘로 변환하고 번역된 에셋을 관리할 수 있습니다. 자세한 내용은 [다국어 자산](multilingual-assets.md)을 참조하십시오.

번역 워크플로우를 실행하기 전에 다른 번역 버전이 동기화되도록 자산을 효율적으로 관리하기 위해 자산의 [언어 사본](preparing-assets-for-translation.md)을 만듭니다.

자산 또는 자산 그룹의 언어 사본은 유사한 컨텐츠 계층 구조를 가진 언어 동기(또는 동일 언어의 자산 버전)입니다.

각 언어 사본은 독립적인 자산입니다. 따라서 자산을 여러 로캘로 변환하면 CRX 저장소의 크기가 크게 늘어날 수 있습니다. 예를 들어 10GB의 자산을 두 언어로 번역할 경우 저장소 크기가 약 20GB(각 언어당 10GB)로 늘어날 수 있습니다.

자산 바이너리는 메타데이터 및 태그와 비교하여 훨씬 더 큰 저장 공간을 차지합니다. 따라서 메타데이터 및 태그를 번역하는 것이 목적으로만 사용되는 경우 이진 파일을 변환하지 마십시오. 다른 로케일로 번역된 메타데이터 및 태그와 연관시키기 위해 저장소에 있는 이진 파일의 원본 복사본을 유지할 수 있습니다. 여러 번역된 버전 대신 바이너리의 단일 복사본을 유지 관리하면 저장소 크기에 미치는 영향을 최소화할 수 있습니다.

파일 데이터 저장소 및 Amazon S3 데이터 저장소는 이러한 시나리오에 가장 적합한 저장소 인프라를 제공합니다. 이러한 저장소 저장소에는 여러 로케일에서 메타데이터 및 태그로 공유할 수 있는 자산 이진 파일(변환 포함)의 단일 사본이 저장됩니다. 따라서 자산 언어 사본을 만들고 메타데이터와 태그를 번역해도 저장소 크기에 영향을 주지 않습니다.

또한 두 가지 워크플로우 및 번역 통합 프레임워크에 대해 몇 가지 구성 변경을 수행하여 프로세스를 더욱 간소화할 수 있습니다.

1. 다음 중 하나를 수행하십시오.

   * [파일 데이터 저장소 설정](/help/sites-deploying/data-store-config.md)
   * [Amazon S3 데이터 저장소 설정](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. [!UICONTROL 마지막으로 수정한 날짜 설정] 워크플로우를 활성화합니다.

   [!UICONTROL DAM MetaData Writeback] 워크플로우는 자산의 마지막 수정 날짜를 구성합니다. 2단계에서 이 워크플로를 비활성화했으므로 [!DNL Assets]은(는) 더 이상 마지막으로 수정한 자산의 날짜를 최신 상태로 유지할 수 없습니다. 따라서 *마지막으로 수정한 날짜 설정* 워크플로우를 활성화하여 마지막으로 수정한 자산의 날짜가 최신 상태인지 확인합니다. 마지막으로 수정한 날짜가 지난 자산은 오류를 초래할 수 있습니다.

1. [자산 이진 파일 ](/help/sites-administering/tc-tic.md) 변환을 중지하도록 번역 통합 프레임워크를 구성합니다. [!UICONTROL 자산] 탭에서 **[!UICONTROL 자산 번역]** 옵션을 선택 취소하여 자산 바이너리의 번역을 중지합니다.
1. [다국어 자산 워크플로우](multilingual-assets.md)를 사용하여 자산 메타데이터/태그를 변환합니다.
