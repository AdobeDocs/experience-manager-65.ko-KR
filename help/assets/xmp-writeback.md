---
title: 표현물로 XMP 원본에 쓰기
description: XMP 원본에 쓰기 기능이 에셋에 대한 메타데이터 변경 사항을 에셋의 모든 또는 특정 변환에 전파하는 방법을 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 6%

---

# 표현물로 XMP 원본에 쓰기 {#xmp-writeback-to-renditions}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 | 이 문서 |

의 이 XMP 원본에 쓰기 기능 [!DNL Adobe Experience Manager Assets] 메타데이터 변경 사항을 원본 에셋의 렌디션에 복제합니다. Assets 내에서 또는 에셋을 업로드하는 동안 에셋의 메타데이터를 변경하면 변경 사항이 에셋 계층의 메타데이터 노드에 처음 저장됩니다.

XMP 원본에 쓰기 기능을 사용하면 메타데이터 변경 내용을 에셋의 모든 또는 특정 표현물로 전파할 수 있습니다. 이 기능은 를 사용하는 메타데이터 속성만 기록합니다. `jcr` 네임스페이스, 즉 `dc:title` 은(는) 다시 기록되지만 라는 속성이 있습니다. `mytitle` 아님.

을 수정하는 시나리오를 고려하십시오. [!UICONTROL 제목] 제목이 있는 자산의 속성 `Classic Leather` 끝 `Nylon`.

![메타데이터](assets/metadata.png)

이 경우 [!DNL Experience Manager Assets] 의 변경 사항을 **[!UICONTROL 제목]** 의 속성 `dc:title` 에셋 계층에 저장된 에셋 메타데이터의 매개 변수.

![metadata_stored](assets/metadata_stored.png)

그러나 [!DNL Experience Manager Assets] 는 메타데이터 변경 사항을 에셋 렌디션에 자동으로 전파하지 않습니다. 다음을 참조하십시오 [XMP 원본에 쓰기 활성화 방법](#enable-xmp-writeback).

## XMP 원본에 쓰기 활성화 {#enable-xmp-writeback}

메타데이터 변경 사항을 업로드할 때 에셋의 렌디션에 전파하려면 를 수정합니다 **[!UICONTROL Adobe CQ DAM 렌디션 작성기]** 구성 관리자에서 구성합니다.

1. Configuration Manager를 열려면 `https://[aem_server]:[port]/system/console/configMgr`.
1. 를 엽니다. **[!UICONTROL Adobe CQ DAM 렌디션 작성기]** 구성.
1. 다음 항목 선택 **[!UICONTROL XMP 전파]** 옵션을 선택한 다음 변경 사항을 저장합니다.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 특정 표현물에 대한 XMP 원본에 쓰기 활성화 {#enabling-xmp-writeback-for-specific-renditions}

XMP 쓰기 저장(Writeback) 기능이 메타데이터 변경 사항을 전파하여 렌디션을 선택하도록 하려면 다음 렌디션을 XMP 쓰기 저장(Writeback) 프로세스 워크플로 단계에 지정합니다 [!UICONTROL DAM 메타데이터 WriteBack] 워크플로입니다. 기본적으로 이 단계는 원본 렌디션으로 구성됩니다.

XMP 원본에 쓰기 기능이 메타데이터를 렌디션 썸네일 140.100.png 및 319.319.png로 전파하도록 하려면 다음 단계를 수행하십시오.

1. Experience Manager 인터페이스에서 다음 위치로 이동합니다 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**.
1. Models 페이지에서 를 엽니다. **[!UICONTROL DAM 메타데이터 원본에 쓰기]** 워크플로우 모델.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. 다음에서 [!UICONTROL 단계 속성] 대화 상자에서 **[!UICONTROL 프로세스]** 탭.
1. 다음에서 **인수** 상자, 추가 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, 및 클릭 **[!UICONTROL 확인]**.

   ![step_properties](assets/step_properties.png)

1. 변경 사항을 저장합니다.
1. 피라미드형 TIFF 렌디션 재생성하기 [!DNL Dynamic Media] 새 특성이 있는 이미지에 **[!UICONTROL Dynamic Media 이미지 자산 처리]** 로 이동 [!UICONTROL DAM 메타데이터 원본에 쓰기] 워크플로입니다.

   PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. 워크플로우를 저장합니다.

메타데이터 변경 사항은 에셋의 렌디션 thumbnail.140.100.png 및 thumbnail.319.319.png에 전파되며 나머지는 전파되지 않습니다.

>[!NOTE]
>
>64비트 Linux의 XMP 원본에 쓰기 문제는 다음을 참조하십시오. [64비트 RedHat Linux에서 XMP 다시 쓰기를 활성화하는 방법](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>지원되는 플랫폼에 대해서는 다음을 참조하십시오. [XMP 메타데이터 쓰기 되돌리기 사전 요구 사항](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## XMP 메타데이터 필터링 {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] 는 에셋 바이너리에서 읽고 에셋을 수집할 때 JCR에 저장되는 XMP 메타데이터에 대한 속성/노드의 차단 목록 및 허용 목록 필터링을 모두 지원합니다.

차단 목록을 사용하여 필터링하면 제외를 위해 지정된 속성을 제외한 모든 XMP 메타데이터 속성을 가져올 수 있습니다. 그러나 엄청난 양의 XMP 메타데이터가 있는 INDD 파일과 같은 에셋 유형(예: 10,000개의 속성이 있는 1000개의 노드)의 경우 필터링할 노드 이름을 항상 미리 알고 있는 것은 아닙니다. 차단 목록을 사용하여 필터링하면 많은 XMP 메타데이터가 있는 많은 에셋을 가져올 수 있습니다. [!DNL Experience Manager] 배포에 안정성 문제가 발생할 수 있습니다(예: 모니터링 큐 차단).

허용 목록을 통한 XMP 메타데이터 필터링은 가져올 XMP 속성을 정의할 수 있도록 하여 이 문제를 해결합니다. 이렇게 하면 다른 모든 또는 알 수 없는 XMP 속성이 무시됩니다. 이전 버전과의 호환성을 위해 차단 목록을 사용하는 필터에 이러한 속성 중 일부를 추가할 수 있습니다.

>[!NOTE]
>
>필터링은 자산 바이너리의 XMP 소스에서 파생된 속성에만 작동합니다. EXIF 및 IPTC 포맷과 같이 비XMP 소스에서 파생된 속성의 경우 필터링이 작동하지 않습니다. 예를 들어 에셋 생성 날짜는 라는 속성에 저장됩니다. `CreateDate` EXIF TIFF. Experience Manager은 이름이 인 메타데이터 필드에 이 값을 저장합니다. `exif:DateTimeOriginal`. 소스가 비 XMP 소스이므로 이 속성에서는 필터링이 작동하지 않습니다.

1. Configuration Manager를 열려면 `https://[aem_server]:[port]/system/console/configMgr`.
1. 를 엽니다. **[!UICONTROL Adobe CQ DAM XmpFilter]** 구성.
1. 허용 목록을 통해 필터링을 적용하려면 다음을 선택합니다. **[!UICONTROL XMP 속성에 허용 목록에 추가하다 적용]**&#x200B;을 클릭하고 가져올 속성을 지정합니다. **[!UICONTROL XMP 필터링에 허용된 XML 이름]** 상자.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 허용 목록을 통해 필터링을 적용한 후 차단된 XMP 속성을 필터링하려면 **[!UICONTROL XMP 필터링을 위해 차단된 XML 이름]** 상자.

   >[!NOTE]
   >
   >다음 **[!UICONTROL XMP 속성에 차단 목록에 추가하다 적용]** 기본적으로 옵션이 선택되어 있습니다. 즉, 차단 목록을 사용한 필터링은 기본적으로 활성화되어 있습니다. 이러한 필터링을 비활성화하려면 선택을 취소합니다 **[!UICONTROL XMP 속성에 차단 목록에 추가하다 적용]** 옵션을 선택합니다.

1. 변경 사항을 저장합니다.
