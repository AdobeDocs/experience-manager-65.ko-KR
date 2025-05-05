---
title: 표현물로 XMP 원본에 쓰기
description: XMP 원본에 쓰기 기능이 에셋에 대한 메타데이터 변경 사항을 에셋의 모든 또는 특정 변환에 전파하는 방법을 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 6%

---

# 표현물로 XMP 원본에 쓰기 {#xmp-writeback-to-renditions}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=ko) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Experience Manager Assets]의 이 XMP 원본에 쓰기 기능은 메타데이터 변경 내용을 원본 자산의 렌디션에 복제합니다. Assets 내에서 또는 에셋을 업로드하는 동안 에셋의 메타데이터를 변경하면 변경 사항이 에셋 계층의 메타데이터 노드에 처음 저장됩니다.

XMP 원본에 쓰기 기능을 사용하면 메타데이터 변경 내용을 에셋의 모든 또는 특정 표현물로 전파할 수 있습니다. 이 기능은 등록된 네임스페이스를 사용하는 메타데이터 속성만 다시 씁니다. 즉, 이름이 `dc:title`인 속성은 다시 기록되지만 이름이 `mytitle`인 속성은 기록되지 않습니다.

제목이 `Classic Leather`인 자산의 [!UICONTROL Title] 속성을 `Nylon`(으)로 수정하는 시나리오를 생각해 보십시오.

![메타데이터](assets/metadata.png)

이 경우 [!DNL Experience Manager Assets]은(는) 자산 계층 구조에 저장된 자산 메타데이터의 `dc:title` 매개 변수에 **[!UICONTROL Title]** 속성의 변경 내용을 저장합니다.

![metadata_stored](assets/metadata_stored.png)

그러나 [!DNL Experience Manager Assets]은(는) 메타데이터 변경 내용을 에셋 렌디션에 자동으로 전파하지 않습니다. [XMP 원본에 쓰기 활성화 방법](#enable-xmp-writeback)을 참조하세요.

## XMP 원본에 쓰기 활성화 {#enable-xmp-writeback}

에셋을 업로드할 때 메타데이터 변경 사항을 에셋의 렌디션에 전파하려면 Configuration Manager에서 **[!UICONTROL Adobe CQ DAM Rendition Maker]** 구성을 수정합니다.

1. 구성 관리자를 열려면 `https://[aem_server]:[port]/system/console/configMgr`에 액세스하십시오.
1. **[!UICONTROL Adobe CQ DAM Rendition Maker]** 구성을 엽니다.
1. **[!UICONTROL XMP 전파]** 옵션을 선택한 다음 변경 내용을 저장합니다.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 특정 표현물에 대한 XMP 원본에 쓰기 활성화 {#enabling-xmp-writeback-for-specific-renditions}

XMP 쓰기 저장(Writeback) 기능을 통해 메타데이터 변경 내용을 전파하여 렌디션을 선택하려면 이러한 렌디션을 [!UICONTROL DAM 메타데이터 쓰기 저장(WriteBack)] 워크플로의 XMP 쓰기 저장 프로세스 워크플로 단계에 지정합니다. 기본적으로 이 단계는 원본 렌디션으로 구성됩니다.

XMP 원본에 쓰기 기능이 메타데이터를 렌디션 썸네일 140.100.png 및 319.319.png로 전파하도록 하려면 다음 단계를 수행하십시오.

1. Experience Manager 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**(으)로 이동합니다.
1. 모델 페이지에서 **[!UICONTROL DAM 메타데이터 원본에 쓰기]** 워크플로 모델을 엽니다.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. [!UICONTROL 단계 속성] 대화 상자에서 **[!UICONTROL 프로세스]** 탭을 클릭합니다.
1. **인수** 상자에서 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`을(를) 추가하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   ![step_properties](assets/step_properties.png)

1. 변경 사항을 저장합니다.
1. 새 특성이 있는 [!DNL Dynamic Media] 이미지의 피라미드 TIFF 렌디션을 다시 생성하려면 [!UICONTROL DAM 메타데이터 원본에 쓰기] 워크플로에 **[!UICONTROL Dynamic Media 프로세스 이미지 Assets]** 단계를 추가하십시오.

   PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. 워크플로우를 저장합니다.

메타데이터 변경 사항은 에셋의 렌디션 thumbnail.140.100.png 및 thumbnail.319.319.png에 전파되며 나머지는 전파되지 않습니다.

>[!NOTE]
>
>64비트 Linux의 XMP 원본에 쓰기 문제는 [64비트 RedHat Linux에서 XMP 원본에 쓰기 기능을 활성화하는 방법](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)을 참조하십시오.
>
>지원되는 플랫폼에 대해서는 [XMP 메타데이터 다시 쓰기 필수 구성 요소](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)를 참조하십시오.

## XMP 메타데이터 필터링 {#filtering-xmp-metadata}

[!DNL Experience Manager Assets]은(는) 에셋 바이너리에서 읽고 에셋을 수집할 때 JCR에 저장되는 XMP 메타데이터에 대한 속성/노드의 차단 목록 및 허용 목록 필터링을 모두 지원합니다.

차단 목록을 사용하여 필터링하면 제외를 위해 지정된 속성을 제외한 모든 XMP 메타데이터 속성을 가져올 수 있습니다. 그러나 엄청난 양의 XMP 메타데이터가 있는 INDD 파일과 같은 에셋 유형(예: 10,000개의 속성이 있는 1000개의 노드)의 경우 필터링할 노드 이름을 항상 미리 알고 있는 것은 아닙니다. 차단 목록을 사용하여 필터링하면 XMP 메타데이터가 많은 자산을 가져올 수 있으므로 [!DNL Experience Manager] 배포에 안정성 문제가 발생할 수 있습니다(예: 모니터링 큐 차단).

허용 목록을 통한 XMP 메타데이터 필터링은 가져올 XMP 속성을 정의할 수 있도록 하여 이 문제를 해결합니다. 이렇게 하면 다른 모든 또는 알 수 없는 XMP 속성이 무시됩니다. 이전 버전과의 호환성을 위해 차단 목록을 사용하는 필터에 이러한 속성 중 일부를 추가할 수 있습니다.

>[!NOTE]
>
>필터링은 자산 바이너리의 XMP 소스에서 파생된 속성에만 작동합니다. EXIF 및 IPTC 포맷과 같이 비XMP 소스에서 파생된 속성의 경우 필터링이 작동하지 않습니다. 예를 들어 에셋 생성 날짜는 EXIF TIFF의 이름이 `CreateDate`인 속성에 저장됩니다. Experience Manager은 이 값을 `exif:DateTimeOriginal`(이)라는 메타데이터 필드에 저장합니다. 소스가 비 XMP 소스이므로 이 속성에서는 필터링이 작동하지 않습니다.

1. 구성 관리자를 열려면 `https://[aem_server]:[port]/system/console/configMgr`에 액세스하십시오.
1. **[!UICONTROL Adobe CQ DAM XmpFilter]** 구성을 엽니다.
1. 허용 목록의 필터링을 적용하려면 **[!UICONTROL XMP 속성에 허용 목록 적용]**&#x200B;을 선택하고 **[!UICONTROL XMP 필터링에 허용된 XML 이름]** 상자에서 가져올 속성을 지정합니다.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 허용 목록을 통해 필터링을 적용한 후 차단된 XMP 속성을 필터링하려면 **[!UICONTROL XMP 필터링을 위해 차단된 XML 이름]** 상자에 해당 속성을 지정합니다.

   >[!NOTE]
   >
   >기본적으로 **[!UICONTROL XMP 속성에 차단 목록 적용]** 옵션이 선택되어 있습니다. 즉, 차단 목록을 사용한 필터링은 기본적으로 활성화되어 있습니다. 이러한 필터링을 비활성화하려면 **[!UICONTROL XMP 속성에 차단 목록 적용]** 옵션 선택을 취소하십시오.

1. 변경 사항을 저장합니다.
