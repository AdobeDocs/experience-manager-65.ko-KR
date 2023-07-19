---
title: Adobe InDesign에 대한 배치 전용 렌디션 생성
description: Experience Manager Assets 워크플로 및 ImageMagick을 사용하여 새 에셋과 기존 에셋의 FPO 렌디션을 생성합니다.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
hide: true
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 1%

---

# Adobe InDesign에 대한 배치 전용 렌디션 생성 {#fpo-renditions}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=en) |
| AEM 6.5 | 이 문서 |

Experience Manager에서 Adobe InDesign 문서로 대형 에셋을 배치할 때 크리에이티브 전문가는 상당한 시간을 기다려야 합니다 [자산 배치](https://helpx.adobe.com/indesign/using/placing-graphics.html). 한편, 사용자는 InDesign 사용이 차단된다. 이는 크리에이티브 흐름을 방해하고 사용자 경험에 부정적인 영향을 미칩니다. Adobe을 사용하면 InDesign 문서에 작은 크기의 렌디션을 임시로 배치할 수 있습니다. 인쇄 및 게시 워크플로와 같이 최종 출력이 필요한 경우 원본 전체 해상도 에셋이 배경의 임시 렌디션을 대체합니다. 백그라운드에서 이 비동기식 업데이트는 디자인 프로세스를 가속화하여 생산성을 높이고 크리에이티브 프로세스를 방해하지 않습니다.

Adobe Experience Manager(AEM)는 배치에만 사용되는 변환(FPO)을 제공합니다. 이러한 FPO 렌디션은 파일 크기는 작지만 종횡비가 동일합니다. 에셋에 FPO 렌디션을 사용할 수 없는 경우 Adobe InDesign은 원본 에셋을 대신 사용합니다. 이 대체 메커니즘을 사용하면 크리에이티브 워크플로우가 중단 없이 진행될 수 있습니다.

## FPO 표현물 생성 방법 {#approach-to-generate-fpo-renditions}

Experience Manager을 사용하면 FPO 표현물을 생성하는 데 사용할 수 있는 이미지를 처리하는 다양한 방법을 사용할 수 있습니다. 가장 일반적인 두 가지 방법은 내장 Experience Manager 워크플로우를 사용하는 것과 ImageMagick을 사용하는 것입니다. 이 두 가지 방법을 사용하여 새로 업로드한 에셋과 Experience Manager에 있는 에셋의 렌디션 생성을 구성합니다.

ImageMagick을 사용하여 FPO 표현물 생성을 비롯한 이미지를 처리할 수 있습니다. 이러한 렌디션은 다운샘플링됩니다. 즉, 원본 이미지의 PPI가 72보다 큰 경우 렌디션의 픽셀 치수가 비례적으로 줄어듭니다. 다음을 참조하십시오 [Experience Manager Assets에서 작동하도록 ImageMagick 설치 및 구성](best-practices-for-imagemagick.md).

|  | Experience Manager의 내장 워크플로우 사용 | ImageMagick 워크플로우 사용 | 비고 |
|--- |--- |---|--- |
| 새 자산용 | FPO 렌디션 활성화([도움말](#generate-renditions-of-new-assets-using-aem-workflow)) | Experience Manager 워크플로에서 ImageMagick 명령줄 추가([도움말](#generate-renditions-of-new-assets-using-imagemagick)) | Experience Manager은 모든 업로드에 대해 DAM 자산 업데이트 워크플로우를 실행합니다. |
| 기존 자산의 경우 | 새로운 전용 Experience Manager 워크플로우에서 FPO 렌디션 활성화([도움말](#generate-renditions-of-existing-assets-using-aem-workflow)) | 새로운 전용 Experience Manager 워크플로우에 ImageMagick 명령줄 추가([도움말](#generate-renditions-of-existing-assets-using-imagemagick)) | 기존 에셋의 FPO 렌디션은 온디맨드 또는 대량으로 작성할 수 있습니다. |

>[!CAUTION]
>
>기본 워크플로우의 사본을 수정하여 렌디션을 생성할 워크플로우를 만듭니다. 이는 Experience Manager 업데이트 시, 예를 들어 새 서비스 팩을 설치하여 변경 사항을 덮어쓰는 것을 방지합니다.

## Experience Manager 워크플로우를 사용하여 새 에셋의 렌디션 생성 {#generate-renditions-of-new-assets-using-aem-workflow}

렌디션을 생성할 수 있도록 DAM 자산 업데이트 워크플로우 모델을 구성하는 단계는 다음과 같습니다.

1. 클릭 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**. 선택 **[!UICONTROL DAM 자산 업데이트]** 모델 및 클릭 **[!UICONTROL 편집]**.

1. 선택 **[!UICONTROL 프로세스 썸네일]** 단계 및 클릭 **[!UICONTROL 구성]**.

1. 클릭 **[!UICONTROL FPO 렌디션]** 탭. 선택 **[!UICONTROL FPO 렌디션 만들기 활성화]**.

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. 조정 **[!UICONTROL 품질]** 및 추가 또는 수정 **[!UICONTROL 목록 서식]** 값을 입력해야 합니다. 기본적으로 FPO 렌디션을 생성하는 MIME 유형 목록은 pjpeg, jpeg, jpg, gif, png, x-png 및 tiff입니다. **[!UICONTROL 완료]**&#x200B;를 클릭합니다.

   >[!NOTE]
   >
   >렌디션 생성은 JPEG, GIF, PNG, TIFF, PSD 및 BMP 파일 유형에 대해 지원됩니다.

1. 변경 사항을 활성화하려면 **[!UICONTROL 동기화]**.

>[!NOTE]
>
>한쪽에 있는 1280픽셀보다 큰 이미지는 FPO 렌디션의 픽셀 치수를 유지하지 않습니다.

## ImageMagick을 사용하여 새 자산의 렌디션 생성 {#generate-renditions-of-new-assets-using-imagemagick}

Experience Manager에서 DAM 자산 업데이트 워크플로우는 새 자산이 업로드될 때 실행됩니다. ImageMagick을 사용하여 새로 업로드한 자산의 렌디션을 처리하려면 워크플로우 모델에 새 명령을 추가합니다.

1. 클릭 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**.

1. 선택 **[!UICONTROL DAM 자산 업데이트]** 모델 및 클릭 **[!UICONTROL 편집]**.

1. 클릭 **[!UICONTROL 사이드 패널 전환]** 왼쪽 상단 모서리에서 명령줄 단계를 검색합니다.

1. 드래그 **[!UICONTROL 명령줄]** 단계 및 다음 항목 앞에 추가 **[!UICONTROL 프로세스 썸네일]** 단계.

1. 선택 **[!UICONTROL 명령줄]** 단계 및 클릭 **[!UICONTROL 구성]**.

1. 원하는 정보를 사용자 정의로 추가 **[!UICONTROL 제목]** 및 **[!UICONTROL 설명]**. 예를 들어 FPO 렌디션(ImageMagick 제공)입니다.

1. 다음에서 **[!UICONTROL 인수]** 탭, 관련 항목 추가 **[!UICONTROL Mime 유형]** 명령을 적용할 파일 형식 목록을 제공합니다.

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. 다음에서 **[!UICONTROL 인수]** 탭, **[!UICONTROL 명령]** 섹션에서 관련 ImageMagick 명령을 추가하여 FPO 렌디션을 생성합니다.

   다음은 JPEG 형식으로 FPO 렌디션을 생성하고 10% 품질 설정에서 72PPI로 다운샘플링한 다음 출력을 병합하여 다중 계층 Adobe Photoshop 파일을 처리하는 예제 명령입니다.

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. 변경 사항을 활성화하려면 **[!UICONTROL 동기화]**.

ImageMagick 명령줄 기능에 대한 자세한 내용은 [https://imagemagick.org](https://imagemagick.org).

## Experience Manager 워크플로우를 사용하여 기존 에셋의 렌디션 생성 {#generate-renditions-of-existing-assets-using-aem-workflow}

Experience Manager 워크플로우를 사용하여 기존 에셋의 FPO 렌디션을 생성하려면 내장 FPO 렌디션 옵션을 사용하는 전용 워크플로우 모델을 만듭니다.

1. 클릭 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**.

1. 모델을 만들려면 **[!UICONTROL 만들기]** > **[!UICONTROL 모델 만들기]**.

1. 의미 있는 항목 추가 **[!UICONTROL 제목]** 및 **[!UICONTROL 이름]**.

1. 모델을 선택하고 **[!UICONTROL 편집]**. 클릭 **[!UICONTROL 페이지 정보]** > **[!UICONTROL 속성 열기]**&#x200B;을 선택한 다음 을 선택합니다 **[!UICONTROL 임시 워크플로우]**. 따라서 확장성과 성능이 향상됩니다.

1. 클릭 **[!UICONTROL 저장]** 및 **[!UICONTROL 닫기]**.

1. 클릭 **[!UICONTROL 사이드 패널 전환]** 왼쪽 상단 모서리에서 프로세스 썸네일 단계를 검색합니다.

1. 선택 **[!UICONTROL 프로세스 썸네일]** 및 클릭 **[!UICONTROL 구성]**. 다음 [Experience Manager 워크플로우를 사용하여 새 자산의 렌디션을 생성하는 구성](#generate-renditions-of-new-assets-using-aem-workflow).

1. 변경 사항을 활성화하려면 **[!UICONTROL 동기화]**.


## ImageMagick을 사용하여 기존 에셋의 렌디션 생성 {#generate-renditions-of-existing-assets-using-imagemagick}

ImageMagick 처리 기능을 사용하여 기존 에셋의 FPO 렌디션을 생성하려면 ImageMagick 명령줄을 사용하여 전용 워크플로 모델을 만듭니다.

1. 에서 1단계부터 3단계까지 수행 [Experience Manager 워크플로우를 사용하여 기존 에셋의 렌디션을 생성하는 구성](#generate-renditions-of-existing-assets-using-aem-workflow) 섹션.

1. 에서 4단계부터 8단계까지 수행 [ImageMagick을 사용하여 새 자산의 렌디션을 생성하는 구성](#generate-renditions-of-new-assets-using-imagemagick) 섹션.


## FPO 표현물 보기 {#view-fpo-renditions}

워크플로우가 완료된 후 생성된 FPO 렌디션을 확인할 수 있습니다. Experience Manager Assets 사용자 인터페이스에서 에셋을 클릭하여 큰 미리 보기를 엽니다. 왼쪽 레일을 열고 렌디션을 선택합니다. 또는 키보드 단축키를 사용합니다 `Alt + 3` 미리보기가 열려 있는 경우.

클릭 **[!UICONTROL FPO 렌디션]** 미리보기를 로드합니다. 필요한 경우 렌디션을 마우스 오른쪽 버튼으로 클릭하고 파일 시스템에 저장할 수 있습니다.

![rendition_list](assets/rendition_list.png)


## 팁 및 제한 사항 {#tips-limitations}

* ImageMagick 기반 구성을 사용하려면 Experience Manager과 동일한 컴퓨터에 ImageMagick을 설치합니다.
* 많은 에셋 또는 전체 저장소의 FPO 렌디션을 생성하려면 트래픽이 적은 기간 동안 워크플로우를 계획 및 실행합니다. 많은 자산에 대해 FPO 렌디션을 생성하는 것은 리소스를 많이 사용하는 작업이며 Experience Manager 서버에는 충분한 처리 능력과 사용 가능한 메모리가 있어야 합니다.
* 성능 및 확장성에 대한 자세한 내용은 [ImageMagick 미세 조정](performance-tuning-guidelines.md).
* 에셋의 일반 명령줄 처리에 대한 자세한 내용은 [자산을 처리하는 명령줄 핸들러](media-handlers.md).
