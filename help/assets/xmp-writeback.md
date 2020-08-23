---
title: 표현물로 XMP 원본에 쓰기
description: XMP 원본에 쓰기 기능이 자산의 메타데이터 변경 내용을 자산의 모든 표현물 또는 특정 표현물에 전달하는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 2%

---


# 표현물로 XMP 원본에 쓰기 {#xmp-writeback-to-renditions}

XMP writeback 기능은 자산 메타데이터 변경 사항을 자산의 변환에 [!DNL Adobe Experience Manager Assets] 복제합니다. 자산을 업로드하는 동안 [!DNL Experience Manager Assets] 또는 내부에서 자산의 메타데이터를 변경하면 변경 내용은 처음에 CRXDe의 자산 노드 내에 저장됩니다. XMP 원본에 쓰기 기능은 메타데이터 변경 사항을 자산의 모든 또는 특정 표현물에 전파합니다.

제목이 있는 자산의 [!UICONTROL 제목] 속성을 수정하는 시나리오 `Classic Leather` 를 `Nylon`고려하십시오.

![메타데이터](assets/metadata.png)

이 경우, [!DNL Experience Manager Assets] 제목 **[!UICONTROL 속성]** 변경 사항을 자산 계층 `dc:title` 에 저장된 자산 메타데이터의 매개 변수에 저장합니다.

![metadata_stored](assets/metadata_stored.png)

하지만, 메타데이터 변경 사항을 자산의 변환에 자동으로 전파하지는 [!DNL Experience Manager Assets] 않습니다.

XMP 원본에 쓰기 기능을 사용하면 메타데이터 변경 내용을 자산의 모든 표현물 또는 특정 표현물에 전파할 수 있습니다. 하지만 변경 사항은 자산 계층의 메타데이터 노드 아래에 저장되지 않습니다. 대신 이 기능에는 변환에 대한 바이너리 파일의 변경 사항이 포함됩니다.

## XMP writeback 사용 {#enabling-xmp-writeback}

업로드 시 메타데이터 변경 사항이 자산의 변환에 전파되도록 하려면 Configuration Manager에서 **[!UICONTROL Adobe CQ DAM Rendition Maker]** 구성을 수정하십시오.

1. 구성 관리자를 열려면 액세스 `https://[aem_server]:[port]/system/console/configMgr`를 참조하십시오.
1. **[!UICONTROL Adobe CQ DAM Rendition Maker]** 구성을 엽니다.
1. XMP **[!UICONTROL 전달]** 옵션을 선택한 다음 변경 내용을 저장합니다.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 특정 변환에 대해 XMP 쓰기 저장 활성화 {#enabling-xmp-writeback-for-specific-renditions}

XMP 원본에 쓰기 기능이 메타데이터 변경 사항을 선택하여 표현물을 선택할 수 있도록 하려면 이러한 표현물을 [!UICONTROL DAM 메타데이터 쓰기 되돌리기 워크플로우의 XMP 쓰기 처리 워크플로우 단계에 지정합니다] . 기본적으로 이 단계는 원래 변환으로 구성됩니다.

XMP 원본에 쓰기 기능이 메타데이터를 변환 축소판 140.100.png 및 319.319.png에 전파하려면 다음 단계를 수행하십시오.

1. Experience Manager 인터페이스에서 **[!UICONTROL 도구]** > 워크플로우 **[!UICONTROL > 모델]** 으로 **[!UICONTROL 이동합니다]**.
1. 모델 페이지에서 **[!UICONTROL DAM 메타데이터 쓰기]** 워크플로우 모델을 엽니다.
1. DAM **[!UICONTROL 메타데이터 원본에 쓰기]** 속성 페이지에서 **[!UICONTROL XMP 쓰기]** 처리 단계를 엽니다.
1. 단계 [!UICONTROL 속성] 대화 상자에서 프로세스 **[!UICONTROL 탭을]** 클릭합니다.
1. [ **인수** ] 상자에서 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`을 추가한 다음 **확인을 클릭합니다**.

   ![step_properties](assets/step_properties.png)

1. 변경 사항을 저장합니다.
1. 새로운 속성을 사용하여 이미지의 피라미드형 TIFF 표현물을 재생성하려면 [!DNL Dynamic Media] DAM 메타데이터 작성 **[!UICONTROL 워크플로우에]** 다이내믹 미디어 프로세스 이미지 자산 [!UICONTROL 단계를] 추가하십시오.

   PTIFF 변환은 Dynamic Media Hybrid 구현에서만 로컬로 만들어지고 저장됩니다.

1. 워크플로우를 저장합니다.

메타데이터 변경 사항이 변환 축소판 그림 140.100.png 및 thumbnail.319.319.png로 전파되며 다른 항목은 전파되지 않습니다.

>[!NOTE]
>
>64비트 Linux의 XMP 쓰기 저장(writeback) 문제 [의 경우 64비트 RedHat Linux에서 XMP 쓰기 되돌리기 사용 방법을 참조하십시오](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>지원되는 플랫폼에 대해서는 [XMP 메타데이터 쓰기 되돌림 사전 요구 사항을 참조하십시오](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## XMP 메타데이터 필터링 {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] 자산 이진에서 읽고 자산을 인제스트할 때 JCR에 저장되는 XMP 메타데이터에 대한 속성/노드의 차단 목록 및 허용 목록 필터링을 모두 지원합니다.

차단 목록을 사용하여 필터링하면 제외에 지정된 속성을 제외한 모든 XMP 메타데이터 속성을 가져올 수 있습니다. 하지만 대량의 XMP 메타데이터가 있는 INDD 파일(예: 1000개의 노드 및 10,000개의 속성)과 같은 에셋 유형의 경우 필터링할 노드 이름이 미리 알려지는 것은 아닙니다. 차단 목록을 사용하여 필터링하면 많은 XMP 메타데이터가 있는 많은 자산을 가져올 수 있는 경우, 배포에는 안정성 문제(예: 끊어진 관측 큐)가 발생할 수 [!DNL Experience Manager] 있습니다.

허용 목록을 통해 XMP 메타데이터를 필터링하면 가져올 XMP 속성을 정의할 수 있어 이 문제가 해결됩니다. 이렇게 하면 기타 또는 알 수 없는 XMP 속성이 무시됩니다. 이전 버전과의 호환성을 위해 차단 목록을 사용하는 필터에 이러한 속성 중 일부를 추가할 수 있습니다.

>[!NOTE]
>
>필터링은 자산 바이너리의 XMP 소스에서 파생된 속성에만 작동합니다. EXIF 및 IPTC 포맷과 같이 XMP이 아닌 소스에서 파생된 속성의 경우 필터링이 작동하지 않습니다. 예를 들어 에셋 작성 날짜는 EXIF TIFF에 명명된 속성 `CreateDate` 에 저장됩니다. Experience Manager은 이 값을 이름이 지정된 메타데이터 필드에 저장합니다 `exif:DateTimeOriginal`. 소스는 XMP이 아닌 소스입니다. 이 속성에서는 필터링이 기능이 작동하지 않습니다.

1. 구성 관리자를 열려면 액세스 `https://[aem_server]:[port]/system/console/configMgr`를 참조하십시오.
1. Adobe CQ **[!UICONTROL DAM XmpFilter 구성을]** 엽니다.
1. 허용 목록을 통해 필터링을 적용하려면 XMP 속성에 **[!UICONTROL 허용 목록에 추가하다 적용을 선택하고 XMP 필터링을 위해 허용된 XML 이름]**&#x200B;상자에서 가져올 속성을 **[!UICONTROL 지정합니다]** .

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 허용 목록을 통한 필터링을 적용한 후 차단된 XMP 속성을 필터링하려면 XMP용 **[!UICONTROL 차단된 XML 이름 필터링]** 상자에 해당 속성을 지정합니다.

   >[!NOTE]
   >
   >XMP 속성에 **[!UICONTROL 차단 목록에 추가하다 적용]** 옵션이 기본적으로 선택되어 있습니다. 즉, 차단 목록을 사용한 필터링은 기본적으로 활성화되어 있습니다. 이러한 필터링을 비활성화하려면 [XMP 속성에 **[!UICONTROL 차단 목록에 추가하다 적용] 옵션을 선택 취소합니다]** .

1. 변경 사항을 저장합니다.
