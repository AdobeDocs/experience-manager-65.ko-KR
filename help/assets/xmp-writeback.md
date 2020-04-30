---
title: 표현물로 XMP 원본에 쓰기
description: XMP 원본에 쓰기 기능을 사용하여 자산의 메타데이터 변경 내용을 자산의 모든 표현물 또는 특정 표현물에 전파하는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 표현물로 XMP 원본에 쓰기 {#xmp-writeback-to-renditions}

의 XMP 원본에 쓰기 기능은 자산 메타데이터 변경 사항을 자산의 표현물에 [!DNL Adobe Experience Manager Assets] 복제합니다. 자산 내에서 또는 자산을 업로드하는 동안 자산에 대한 메타데이터를 변경하면 변경 [!DNL Experience Manager Assets] 사항은 처음에 CRXDe의 자산 노드 내에 저장됩니다. XMP 원본에 쓰기 기능은 메타데이터 변경 내용을 자산의 모든 또는 특정 표현물에 전파합니다.

제목이 [!UICONTROL 있는 자산의 제목] 속성을 수정하는 시나리오를 `Classic Leather` 고려하십시오 `Nylon`.

![메타데이터](assets/metadata.png)

이 경우, [!DNL Experience Manager Assets] 에서는 **[!UICONTROL 자산 계층에 저장된 자산 메타데이터의]** 매개 변수에 Title `dc:title` 속성에 대한 변경 사항을 저장합니다.

![metadata_stored](assets/metadata_stored.png)

하지만, 메타데이터 변경 사항을 자산의 변환에 자동으로 전파하지는 [!DNL Experience Manager Assets] 않습니다.

XMP 원본에 쓰기 기능을 사용하면 메타데이터 변경 내용을 자산의 모든 표현물 또는 특정 표현물에 전파할 수 있습니다. 하지만 변경 사항은 자산 계층의 메타데이터 노드 아래에 저장되지 않습니다. 대신 이 기능에는 변환의 바이너리 파일에 변경 사항이 포함됩니다.

## XMP 원본에 쓰기 활성화 {#enabling-xmp-writeback}

업로드 시 메타데이터 변경 사항이 자산의 변환에 전파되도록 하려면 Configuration Manager에서 **[!UICONTROL Adobe CQ DAM Rendition Maker]** 구성을 수정합니다.

1. Configuration Manager를 열려면 에 `https://[aem_server]:[port]/system/console/configMgr`액세스하십시오.
1. Adobe CQ **[!UICONTROL DAM Rendition Maker 구성을]** 엽니다.
1. **[!UICONTROL XMP 전파[!UICONTROL **] 옵션을 선택한 다음 변경 내용을 저장합니다.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 특정 변환에 대해 XMP 원본에 쓰기 활성화 {#enabling-xmp-writeback-for-specific-renditions}

XMP 원본에 쓰기 기능을 사용하여 메타데이터 변경 내용을 일부 변환에 전파하려면 이러한 변환을 DAM 메타데이터 다시 쓰기 워크플로우의 XMP 원본에 [!UICONTROL 쓰기 프로세스 워크플로우 단계에 지정합니다] . 기본적으로 이 단계는 원래 변환으로 구성됩니다.

XMP 원본에 쓰기 기능을 사용하여 변환 축소판 140.100.png 및 319.319.png에 메타데이터를 전파하려면 다음 단계를 수행하십시오.

1. Experience Manager 인터페이스에서 도구 > 워크플로우 **[!UICONTROL >]** 모델로 **[!UICONTROL 이동합니다]******.
1. 모델(Models) 페이지에서 DAM 메타데이터 **[!UICONTROL 원본에]** 쓰기 워크플로우 모델을 엽니다.
1. DAM 메타데이터 **[!UICONTROL 원본에]** 쓰기 **[!UICONTROL 속성 페이지에서 XMP]** 쓰기 프로세스 단계를엽니다.
1. 단계 [!UICONTROL 속성] 대화 상자에서 프로세스 **[!UICONTROL 탭을 클릭합니다]** .
1. 인수 **상자에서** 추가한 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`다음 확인을 탭/ **클릭합니다**.

   ![step_properties](assets/step_properties.png)

1. 변경 사항을 저장합니다.
1. 새로운 속성을 사용하여 이미지에 대한 피라미드 TIFF 변환을 다시 생성하려면 Dynamic Media Process [!DNL Dynamic Media] Image Assets **[!UICONTROL 단계를 DAM 메타데이터 작성]** 워크플로우에 [!UICONTROL 추가하십시오] .

   PTIFF 변환은 Dynamic Media Hybrid 구현에서만 로컬에 만들어지고 저장됩니다.

1. 워크플로우를 저장합니다.

메타데이터 변경 사항이 변환 변환 축소판으로 전파됩니다.140.100.png 및 thumbnail.319.319.png로 전달되며 다른 항목은 전파되지 않습니다.

>[!NOTE]
>
>64비트 Linux의 XMP 쓰기 저장(writeback) 문제는 64 [비트 RedHat Linux에서 XMP 다시 쓰기를 활성화하는 방법을 참조하십시오](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>지원되는 플랫폼에 대한 자세한 내용은 XMP [메타데이터 쓰기 되돌림 사전 요구 사항을](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)참조하십시오.

## XMP 메타데이터 필터링 {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] 자산 이진에서 읽고 자산을 인제스트할 때 JCR에 저장되는 XMP 메타데이터에 대한 속성/노드의 블랙 리스트 및 화이트 리스트 필터링을 모두 지원합니다.

블랙 필터링을 사용하면 제외에 지정된 속성을 제외한 모든 XMP 메타데이터 속성을 가져올 수 있습니다. 그러나 XMP 메타데이터가 많은 INDD 파일(예: 10,000개의 속성이 있는 1000개의 노드)과 같은 에셋 유형의 경우 필터링할 노드 이름이 항상 미리 알려지는 것은 아닙니다. 블랙 리스트 필터링을 통해 많은 XMP 메타데이터가 있는 많은 자산을 가져올 수 있는 경우 Experience Manager 배포는 중단된 관측 대기열과 같은 안정성 문제를 일으킬 수 있습니다.

XMP 메타데이터를 화이트 리스트 필터링하면 가져올 XMP 속성을 정의할 수 있어 이 문제를 해결합니다. 이렇게 하면 기타/알 수 없는 XMP 속성이 무시됩니다. 이전 버전과의 호환성을 위해 이러한 속성 중 일부를 블랙 리스트 필터에 추가할 수 있습니다.

>[!NOTE]
>
>필터링은 자산 바이너리의 XMP 소스에서 파생된 속성에만 작동합니다. EXIF 및 IPTC 포맷과 같이 XMP 소스가 아닌 소스에서 파생된 속성의 경우 필터링이 작동하지 않습니다. 예를 들어 에셋 작성 날짜는 EXIF TIFF `CreateDate` 에서 명명된 속성에 저장됩니다. Experience Manager는 이 값을 이름이 `exif:DateTimeOriginal`지정된 메타데이터 필드에 저장합니다. 소스가 XMP 소스가 아니므로 이 속성에서는 필터링이 작동하지 않습니다.

1. Configuration Manager를 열려면 에 `https://[aem_server]:[port]/system/console/configMgr`액세스하십시오.
1. Adobe CQ **[!UICONTROL DAM XmpFilter 구성을]** 엽니다.
1. 화이트 리스트 필터링을 적용하려면 [XMP **[!UICONTROL 속성에 화이트리스트 적용]**]을 선택하고 [XMP 필터링을 **[!UICONTROL 위한 화이트리스트 XML]** 이름] 상자에서 가져올 속성을 지정합니다.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 화이트리스트 필터링을 적용한 후 블랙리스트에 추가된 XMP 속성을 필터링하려면 XMP 필터링을 **** 위해 블랙리스트에 추가된 XML 이름 상자에서 지정합니다.

   >[!NOTE]
   >
   >[ **[!UICONTROL XMP 속성에 블랙 리스트 적용]** ] 옵션은 기본적으로 선택되어 있습니다. 다시 말해 블랙 리스트 필터링은 기본적으로 활성화되어 있습니다. 블랙 리스트 필터링을 비활성화하려면 [XMP 속성에 **[!UICONTROL 블랙 리스트 적용] 옵션을 선택]** 취소합니다.

1. 변경 사항을 저장합니다.
