---
title: 3D 자산 미리보기
description: Experience Manager에서 3D 에셋을 미리 보는 방법에 대해 알아봅니다.
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: User
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 9%

---

# Adobe Experience Manager에서 3D 자산 미리 보기 {#previewing-3d-assets-aem}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/previewing-3d-assets.html?lang=ko) |
| AEM 6.5 | 이 문서 |

Experience Manager은 작성 프로세스의 일부로 3D 에셋의 업로드, 전달 및 대화형 미리 보기를 지원합니다.

대화형 3D 뷰어는 Experience Manager의 에셋 세부 사항 페이지에서 사용할 수 있습니다. 이 뷰어에는 3D 자산을 궤도를 따라 이동하고, 확대/축소하고, 패닝할 수 있는 대화형 카메라 컨트롤 컬렉션이 포함되어 있습니다.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Experience Manager에서 3D 미리 보기에 대해 지원되는 형식 {#supported-3d-previewing-assets}

대화형 3D 미리보기는 다음 파일 형식을 지원합니다.

| 3D 파일 확장명 | 파일 포맷 | MIME 유형 | 메모 |
|---|---|---|---|
| GLB | 이진 GL 전송 | model/gltf-binary | |
| GLTF | GL 전송 형식 | model/gltf+json | 아래의 **참고**&#x200B;을 참조하세요. |
| OBJ | WaveFront 3D 개체 파일 | application/x-tgif | |
| STL | 스테레오리소그래피 | application/vnd.ms-pki.stl | |
| DN | Adobe Dimension | model/x-adobe-dn | 수집만 지원합니다. 미리 보기를 사용할 수 없습니다. |
| USDZ | 범용 장면 설명 Zip 아카이브 | model/vnd.usdz+zip | 수집만 지원합니다. 미리 보기를 사용할 수 없습니다. |

>[!NOTE]
>
>gLTF 모델의 미리 보기에서 자재가 렌더링되지 않는 경우 다음과 같이 이름이 올바르게 지정되었는지 확인하고 모델과 동일한 루트 폴더의 `textures` 폴더에서 이름이 지정되었는지 확인하십시오.

    자산(폴더)
    model.gltf
    model.bin
    텍스처(폴더)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Experience Manager에서 3D 에셋을 미리 볼 때 성능 고려 사항{#performance-3d-previewing-assets}

에셋 세부 사항 보기 페이지에서 3D 에셋을 여는 데 걸리는 시간은 대역폭, 이미지 복잡성 및 서버 대기 시간 등 여러 요인에 따라 다릅니다.

또한 클라이언트 컴퓨터의 기능(워크스테이션, 노트북 또는 모바일 터치 장치 등)도 상호 작용 방식으로 카메라를 조작할 때 고려해야 할 사항입니다. 우수한 그래픽 기능을 갖춘 합리적으로 강력한 시스템은 대화형 3D 시청 환경을 더 유연하고 더 유리하게 만들 수 있습니다.

**Experience Manager에서 3D 자산을 미리 보려면:**

1. 3D 자산을 Experience Manager에 업로드했는지 확인합니다.
[3D 미리 보기에 대해 지원되는 형식](#supported-3d-previewing-assets) 및 [Assets 업로드](/help/assets/manage-assets.md#uploading-assets)를 참조하십시오.
1. **[!UICONTROL Experience Manager Assets]** 페이지에서 **[!UICONTROL 탐색]** > **[!UICONTROL 파일]**&#x200B;을 선택합니다.

   ![탐색 페이지](/help/assets/assets-dm/navigation-assets.png)

1. 페이지의 오른쪽 상단 모서리 근처에서 보기 드롭다운 목록에서 **[!UICONTROL 카드 보기]**&#x200B;를 선택한 다음 미리 보려는 3D 자산으로 이동합니다.

   ![3D 카드 선택](/help/assets/assets-dm/3d-card-select.png)
   _카드 보기에서 미리 보려는 3D 자산의 카드를 선택합니다._

1. 3D 에셋의 카드를 선택합니다.

   ![대화형 3D 미리 보기](/help/assets/assets-dm/3d-preview.png)
   _자산 세부 정보 보기 페이지에서 3D 자산의 대화형 미리 보기._
1. 3D 자산에 대한 자산 세부 사항 보기 페이지에서 다음 중 하나를 수행합니다.

   | 보기 | 설명 | 마우스 동작 | 터치 스크린 동작 |
   | --- | --- | --- | --- |
   | **카메라 돌리기** | 3D 장면 및 개체 주위로 보기를 궤도 회전합니다. | 마우스 왼쪽 단추를 클릭하고 드래그합니다. | 한 손가락으로 + 드래그. |
   | **카메라 패닝** | 보기를 왼쪽, 오른쪽, 위쪽 또는 아래쪽으로 회전합니다. | 마우스 오른쪽 단추를 클릭하고 드래그하십시오. | 두 손가락으로 + 드래그. |
   | **카메라 확대/축소** | 3D 장면의 영역 안과 밖으로 이동합니다. | 스크롤 휠입니다. | 손가락 두 개 조입니다. |
   | **카메라를 다시 가운데로** | 카메라를 3D 장면의 개체에 있는 점에 다시 가운데로 맞춥니다. | 두 번 클릭합니다. | 두 번 선택합니다. |
   | **재설정** | 페이지의 오른쪽 하단 모서리 근처에서 재설정 아이콘을 선택하여 보기 대상 지점을 3D 에셋의 가운데로 복원합니다. 또한 재설정을 사용하면 카메라를 더 가깝게 또는 더 멀리 이동하여 에셋을 전체적으로 적절한 보기 크기로 표시할 수 있습니다. |   |   |
   | **전체 화면 모드** | 전체 화면 모드로 전환하려면 페이지의 오른쪽 아래 모서리에서 전체 화면 아이콘을 선택합니다. |   |   |

1. 완료되면 페이지의 오른쪽 상단 근처에서 **[!UICONTROL 닫기]**&#x200B;를 선택합니다.
