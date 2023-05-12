---
title: Adobe InDesign에 대한 배치 전용 표현물 생성
description: Experience Manager Assets 워크플로우 및 ImageMagick를 사용하여 신규 및 기존 자산의 FPO 변환을 생성합니다.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---

# Adobe InDesign에 대한 배치 전용 표현물 생성 {#fpo-renditions}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=en) |
| AEM 6.5 | 이 문서 |

Experience Manager에서 Adobe InDesign 문서로 대규모 자산을 배치하는 경우 크리에이티브 전문가가 해당 자산이 끝나면 상당한 시간을 기다려야 합니다 [자산 배치](https://helpx.adobe.com/indesign/using/placing-graphics.html). 한편 InDesign 사용이 차단되었습니다. 따라서 크리에이티브 플로우가 중단되고 사용자 경험에 부정적인 영향을 줍니다. Adobe을 사용하면 InDesign 문서에 작은 크기의 렌디션을 일시적으로 배치할 수 있습니다. 최종 출력이 필요한 경우(예: 인쇄 및 게시 워크플로우) 원래 전체 해상도 자산은 임시 변환을 백그라운드로 대체합니다. 백그라운드에서 이러한 비동기 업데이트를 통해 디자인 프로세스의 속도를 높여 생산성을 높이고 크리에이티브 프로세스를 방해하지 않습니다.

Adobe Experience Manager(AEM)은 배치에만 사용되는 표현물(FPO)을 제공합니다. 이러한 FPO 변환은 파일 크기가 작지만 동일한 종횡비입니다. 자산에 FPO 변환을 사용할 수 없는 경우 Adobe InDesign에서는 대신 원본 자산을 사용합니다. 이 대체 메커니즘을 사용하면 크리에이티브 워크플로우가 중단 없이 진행됩니다.

## FPO 변환을 생성하는 방법 {#approach-to-generate-fpo-renditions}

Experience Manager을 사용하면 많은 방법으로 FPO 변환을 생성하는 데 사용할 수 있는 이미지를 처리할 수 있습니다. 가장 일반적인 두 가지 방법은 내장 Experience Manager 워크플로우를 사용하고 ImageMagick를 사용하는 것입니다. 이 두 가지 방법을 사용하여 새로 업로드한 자산과 Experience Manager에 있는 자산의 렌디션 생성을 구성합니다.

ImageMagick를 사용하여 FPO 변환을 생성하기 위해 를 포함하여 이미지를 처리할 수 있습니다. 원본 이미지의 PPI가 72보다 큰 경우 표현물의 픽셀 크기가 비례적으로 축소됩니다. 자세한 내용은 [Experience Manager Assets에서 작동하도록 ImageMagick 설치 및 구성](best-practices-for-imagemagick.md).

|  | Experience Manager의 내장된 워크플로우 사용 | ImageMagick 워크플로우 사용 | 비고 |
|--- |--- |---|--- |
| 새 자산의 경우 | FPO 변환 활성화([도움말](#generate-renditions-of-new-assets-using-aem-workflow)) | Experience Manager 워크플로우에서 ImageMagick 명령줄 추가([도움말](#generate-renditions-of-new-assets-using-imagemagick)) | Experience Manager은 업로드할 때마다 DAM 자산 업데이트 워크플로우를 실행합니다. |
| 기존 자산의 경우 | 새로운 전용 Experience Manager 워크플로우에서 FPO 표현물 활성화([도움말](#generate-renditions-of-existing-assets-using-aem-workflow)) | 새로운 전용 Experience Manager 워크플로우에 ImageMagick 명령줄 추가([도움말](#generate-renditions-of-existing-assets-using-imagemagick)) | 기존 자산의 FPO 표현물은 요청 시 또는 대량으로 만들 수 있습니다. |

>[!CAUTION]
>
>기본 워크플로우의 사본을 수정하여 변환을 생성하는 워크플로우를 만듭니다. 따라서 Experience Manager 업데이트 시(예: 새 서비스 팩 설치) 변경 사항을 덮어쓰지 않습니다.

## Experience Manager 워크플로우를 사용하여 새 자산의 표현물 생성 {#generate-renditions-of-new-assets-using-aem-workflow}

다음은 표현물 생성을 사용하도록 DAM 자산 업데이트 워크플로우 모델을 구성하는 절차입니다.

1. 클릭 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**. 선택 **[!UICONTROL DAM 자산 업데이트]** 모델 및 클릭 **[!UICONTROL 편집]**.

1. 선택 **[!UICONTROL 프로세스 축소판]** 단계와 클릭 **[!UICONTROL 구성]**.

1. 클릭 **[!UICONTROL FPO 표현물]** 탭. 선택 **[!UICONTROL FPO 변환 생성 활성화]**.

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. 조정 **[!UICONTROL 품질]** 추가 또는 수정 **[!UICONTROL 서식 목록]** 값을 필요한 값으로 채우는 방법을 설명합니다. 기본적으로 FPO 변환을 생성할 MIME 유형 목록은 pjpeg, jpeg, jpg, gif, png, x-png 및 tiff입니다. 클릭 **[!UICONTROL 완료]**.

   >[!NOTE]
   >
   >파일 형식 JPEG, GIF, PNG, TIFF, PSD 및 BMP에 대해 렌디션 생성이 지원됩니다.

1. 변경 사항을 활성화하려면 **[!UICONTROL 동기화]**.

>[!NOTE]
>
>한 쪽의 1280픽셀보다 큰 이미지는 FPO 표현물의 픽셀 크기를 유지하지 않습니다.

## ImageMagick를 사용하여 새 자산의 렌디션 생성 {#generate-renditions-of-new-assets-using-imagemagick}

Experience Manager에서 새 자산이 업로드되면 DAM 자산 업데이트 워크플로우가 실행됩니다. ImageMagick를 사용하여 새로 업로드한 자산의 렌디션을 처리하려면 워크플로우 모델에 새 명령을 추가합니다.

1. 클릭 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**.

1. 선택 **[!UICONTROL DAM 자산 업데이트]** 모델 및 클릭 **[!UICONTROL 편집]**.

1. 클릭 **[!UICONTROL 사이드 패널 전환]** 왼쪽 위 모서리에서 명령줄 단계를 검색합니다.

1. 을(를) 드래그합니다. **[!UICONTROL 명령줄]** 단계를 수행한 후 앞에 추가합니다 **[!UICONTROL 프로세스 축소판]** 단계.

1. 선택 **[!UICONTROL 명령줄]** 단계와 클릭 **[!UICONTROL 구성]**.

1. 원하는 정보를 사용자 지정으로 추가합니다 **[!UICONTROL 제목]** 및 **[!UICONTROL 설명]**. 예를 들어 FPO 변환(ImageMagick에서 제공)이 있습니다.

1. 에서 **[!UICONTROL 인수]** 탭, 관련 추가 **[!UICONTROL Mime 유형]** 명령을 적용할 파일 형식 목록을 제공합니다.

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. 에서 **[!UICONTROL 인수]** 탭, **[!UICONTROL 명령]** 섹션에서 관련 ImageMagick 명령을 추가하여 FPO 변환을 생성합니다.

   다음은 JPEG 포맷으로 FPO 변환을 생성하여 72PPI로 다운샘플링한 10% 품질 설정으로 생성하고 출력을 병합하여 다중 레이어 Adobe Photoshop 파일을 처리하는 예제 명령입니다.

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. 변경 사항을 활성화하려면 **[!UICONTROL 동기화]**.

ImageMagick 명령줄 기능에 대한 자세한 내용은 [https://imagemagick.org](https://imagemagick.org).

## Experience Manager 워크플로우를 사용하여 기존 자산의 표현물 생성 {#generate-renditions-of-existing-assets-using-aem-workflow}

Experience Manager 워크플로우를 사용하여 기존 자산의 FPO 변환을 생성하려면 내장 FPO 표현물 옵션을 사용하는 전용 워크플로우 모델을 만듭니다.

1. 클릭 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**.

1. 모델을 만들려면 **[!UICONTROL 만들기]** > **[!UICONTROL 모델 만들기]**.

1. 의미 있는 추가 **[!UICONTROL 제목]** 및 **[!UICONTROL 이름]**.

1. 모델을 선택하고 를 클릭합니다 **[!UICONTROL 편집]**. 클릭 **[!UICONTROL 페이지 정보]** > **[!UICONTROL 속성 열기]**&#x200B;를 선택한 다음 을 선택합니다. **[!UICONTROL 임시 워크플로우]**. 확장성 및 성능이 향상됩니다.

1. 클릭 **[!UICONTROL 저장]** 및 **[!UICONTROL 닫기]**.

1. 클릭 **[!UICONTROL 사이드 패널 전환]** 왼쪽 위 모서리에서 프로세스 축소판 단계를 검색합니다.

1. 선택 **[!UICONTROL 프로세스 축소판]** 을(를) 클릭합니다. **[!UICONTROL 구성]**. 다음을 수행합니다 [Experience Manager 워크플로우를 사용하여 새 자산의 렌디션을 생성하는 구성](#generate-renditions-of-new-assets-using-aem-workflow).

1. 변경 사항을 활성화하려면 **[!UICONTROL 동기화]**.


## ImageMagick를 사용하여 기존 자산의 렌디션 생성 {#generate-renditions-of-existing-assets-using-imagemagick}

ImageMagick 처리 기능을 사용하여 기존 자산의 FPO 렌디션을 생성하려면 ImageMagick 명령줄 을 사용하는 전용 워크플로우 모델을 만들어야 합니다.

1. 1단계부터 3단계까지 [Experience Manager 워크플로우를 사용하여 기존 자산의 렌디션을 생성하는 구성](#generate-renditions-of-existing-assets-using-aem-workflow) 섹션을 참조하십시오.

1. 4단계에서 8단계로 진행합니다 [imageMagick를 사용하여 새 자산의 렌디션을 생성하는 구성](#generate-renditions-of-new-assets-using-imagemagick) 섹션을 참조하십시오.


## FPO 표현물 보기 {#view-fpo-renditions}

워크플로우가 완료된 후 생성된 FPO 표현물을 확인할 수 있습니다. Experience Manager Assets 사용자 인터페이스에서 자산을 클릭하여 큰 미리 보기를 엽니다. 왼쪽 레일을 열고 표현물 을 선택합니다. 또는 키보드 단축키를 사용합니다 `Alt + 3` 미리 보기가 열려 있을 때.

클릭 **[!UICONTROL FPO 표현물]** 미리 보기를 로드하려면 다음을 수행하십시오. 선택적으로 변환을 마우스 오른쪽 단추로 클릭하고 파일 시스템에 저장할 수 있습니다.

![rendition_list](assets/rendition_list.png)


## 팁 및 제한 사항 {#tips-limitations}

* ImageMagick 기반 구성을 사용하려면 Experience Manager과 동일한 시스템에 ImageMagick를 설치합니다.
* 많은 자산 또는 전체 리포지토리의 FPO 변환을 생성하려면 낮은 트래픽 기간 동안 워크플로우를 계획하고 실행합니다. 많은 자산에 대해 FPO 변환을 생성하는 것은 리소스가 많이 사용되므로 Experience Manager 서버에서 충분한 처리 능력과 메모리를 사용할 수 있어야 합니다.
* 성능 및 확장성을 보려면 [ImageMagick 미세 조정](performance-tuning-guidelines.md).
* 자산의 일반 명령줄 처리에 대해서는 [자산을 처리하는 명령줄 핸들러](media-handlers.md).
