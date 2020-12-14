---
title: 3D 자산 미리 보기
description: 3D 자산을 미리 보는 방법 학습
contentOwner: Rick Brough
docset: aem65
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 11%

---


# AEM{#previewing-3d-assets-aem}에서 3D 자산 미리 보기

Adobe Experience Manager은 제작 프로세스의 일환으로 3D 자산의 업로드, 전달 및 대화형 미리 보기를 지원합니다.

대화형 3D 뷰어는 AEM의 자산 세부 사항 페이지에서 사용할 수 있습니다. 이 뷰어에는 3D 자산을 궤도를 따라 이동하고, 확대/축소하고, 패닝할 수 있는 대화형 카메라 컨트롤 컬렉션이 포함되어 있습니다.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## AEM {#supported-3d-previewing-assets}에서 3D 미리 보기에 지원되는 형식

대화형 3D 미리 보기는 다음 파일 형식을 지원합니다.

| 3D 파일 확장명 | 파일 형식 | MIME 유형 | 메모 |
|---|---|---|---|
| GLB | 이진 GL 전송 | model/gltf-binary |  |
| GLTF | GL 전송 형식 | model/gltf+json | 아래의 **참고**&#x200B;을 참조하십시오. |
| OBJ | WaveFront 3D 개체 파일 | application/x-tgif |  |
| STL | 입체사진 | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | 통합 전용 지원;미리 보기를 사용할 수 없습니다. |
| USDZ | 범용 장면 설명 Zip 아카이브 | model/vnd.usdz+zip | 통합 전용 지원;미리 보기를 사용할 수 없습니다. |

**참고**:재질이 gLTF 모델의 미리 보기에서 렌더링되지 않는 경우 이름이 적절하게 지정되고 모델과 동일한 루트 폴더의  `textures` 폴더에 있는지 확인합니다. 이러한 폴더는 다음과 같습니다.

    자산(폴더)
    model.
    gltfmodel.
    binteexits (폴더)
    material_0_baseColor.
    jpegmaterial_0_normal.jpeg

## AEM{#performance-3d-previewing-assets}에서 3D 자산을 미리 볼 때의 성능 고려 사항

자산 세부 사항 보기 페이지에서 3D 자산을 여는 데 걸리는 시간은 대역폭, 이미지 복잡도 및 서버에 대한 지연 시간 등 여러 요인에 따라 다릅니다.

또한 카메라를 대화형으로 조작할 때는 워크스테이션, 노트북 또는 모바일 터치 장치와 같은 클라이언트 컴퓨터의 기능도 중요합니다. 그래픽 성능이 좋은 강력한 시스템에서는 대화형 3D 보기 환경이 좀 더 원활하고 유용할 수 있습니다.

**AEM에서 3D 자산을 미리 보려면**

1. 3D 자산을 AEM에 업로드했는지 확인합니다.
[3D 미리 보기](#supported-3d-previewing-assets) 및 [자산 업로드](/help/assets/manage-assets.md#uploading-assets)를 참조하십시오.
1. AEM의 **[!UICONTROL 탐색]** 페이지에서 **[!UICONTROL 자산 > 파일을 탭합니다.]**

   ![탐색 페이지](/help/assets/assets-dm/navigation-assets.png)

1. 페이지의 오른쪽 위 모서리 근처에 있는 보기 드롭다운 목록에서 **[!UICONTROL 카드 보기]**&#x200B;를 탭한 다음 미리 보려는 3D 자산으로 이동합니다.

   ![3D 카드 선택](/help/assets/assets-dm/3d-card-select.png)
   _카드 보기에서 미리 보려는 3D 자산의 카드를 누릅니다._

1. 3D 자산의 카드를 탭하여 자산 세부 사항 보기 페이지에서 엽니다.

   ![인터랙티브한 3D 미리 보기](/help/assets/assets-dm/3d-preview.png)
   _자산 세부 사항 보기 페이지에서 3D 자산의 대화형 미리 보기입니다._
1. 3D 자산에 대한 자산 세부 사항 보기 페이지에서 다음 중 하나를 수행합니다.
   * **카메라** 회전 - 3D 장면과 개체 주위로 보기를 선회합니다.
      * _마우스_:마우스 왼쪽 단추를 클릭하고 드래그합니다.
      * _터치 스크린_:한 손가락을 누른 상태에서 드래그합니다.
   * **카메라** 팬—보기 왼쪽, 오른쪽, 위쪽 또는 아래쪽으로 이동합니다.
      * _마우스_:마우스 오른쪽 단추를 클릭하고 드래그합니다.
      * _터치 스크린_:두 손가락을 누른 상태에서 드래그합니다.
   * **카메라** 확대 - 3D 장면 영역 확대 및 밖으로 카메라를 확대할 수 있습니다.
      * _마우스_:스크롤 휠입니다.
      * _터치 스크린_:두 손가락을 꼬집다.
   * **카메라** 다시 입력 - 3D 장면의 개체 지점에 맞게 카메라를 다시 입력합니다.
      * _마우스_:두 번 클릭합니다.
      * _터치 스크린_:두 번 누릅니다.
   * **재설정** - 페이지의 오른쪽 아래 모서리 근처에 있는 재설정 아이콘을 눌러 보기 대상 포인트를 3D 자산의 중심으로 복원합니다. 또한 재설정을 수행하면 카메라가 더 가깝거나 더 멀리 이동되어 자산이 전체적으로 적절한 보기 크기로 표시됩니다.
   * **전체 화면 모드** - 전체 화면 모드로 전환하려면 페이지의 오른쪽 아래에 있는 전체 화면 아이콘을 누릅니다.

1. 완료되면 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL Close.]**
