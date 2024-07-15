---
title: 이미징 코드 변환 라이브러리
description: 인코딩, 코드 변환, 이미지 리샘플링 및 이미지 크기 조정을 비롯한 핵심 이미지 처리 기능을 수행할 수 있는 이미지 처리 솔루션인 Adobe의 이미징 코드 변환 라이브러리를 구성하고 사용하는 방법에 대해 알아봅니다.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# 이미징 코드 변환 라이브러리 {#imaging-transcoding-library}

Adobe Imaging Transcoding Library는 다음을 포함한 핵심 이미지 처리 기능을 수행할 수 있는 독점 이미지 처리 솔루션입니다.

* 인코딩
* 코드 변환(지원되는 형식 변환)
* PS 및 인텔 IPP 알고리즘을 사용한 이미지 리샘플링
* 비트 심도 및 색상 프로파일 보존
* JPEG 품질 압축
* 이미지 크기 조정

이미징 코드 변환 라이브러리는 CMYK -Alpha을 제외하고 CMYK 지원 및 전체 알파 지원을 제공합니다.

이미징 코드 변환 라이브러리는 다양한 파일 형식 및 프로필을 지원할 뿐만 아니라 성능, 확장성 및 품질과 관련하여 다른 타사 솔루션에 비해 상당한 이점을 제공합니다. 다음은 이미징 코드 변환 라이브러리를 사용할 때 얻을 수 있는 몇 가지 주요 이점입니다.

* **파일 크기 또는 해상도가 증가하면서 크기 조절**: 크기 조절은 주로 파일을 디코딩하는 동안 크기를 다시 조정할 수 있는 이미징 코드 변환 라이브러리의 특허 받은 기능을 통해 이루어집니다. 이 기능은 런타임 메모리 사용이 항상 최적이고 파일 크기 또는 해상도 메가픽셀을 증가시키는 2차 함수가 아님을 보장합니다. 이미징 코드 변환 라이브러리는 더 큰 고해상도(더 높은 메가픽셀 포함) 파일을 처리할 수 있습니다. ImageMagick와 같은 타사 도구는 대용량 파일을 처리할 수 없으며 이러한 파일을 처리하는 동안 충돌이 발생합니다.
* **Photoshop 품질 압축 및 크기 조정 알고리즘**: 다운 샘플링(매끄러움, 선명함 및 자동 바이큐빅) 품질 및 압축 품질 측면에서 업계 표준과 일치합니다. 이미징 코드 변환 라이브러리는 입력 이미지의 품질 요인을 추가로 평가하고 출력 이미지에 대한 최적의 테이블 및 품질 설정을 지능적으로 사용합니다. 이 기능은 시각적 품질을 손상시키지 않고 최적의 크기를 갖는 파일을 생성합니다.
* **높은 처리량:** 응답 시간이 짧고 처리량이 ImageMagick보다 일관되게 높습니다. 따라서 이미징 코드 변환 라이브러리는 사용자의 대기 시간과 호스팅 비용을 줄여야 합니다.
* **동시 부하로 더 잘 확장:** 이미징 코드 변환 라이브러리는 동시 부하 조건에서 최적으로 수행됩니다. 최적의 CPU 성능, 메모리 사용량, 낮은 응답 시간으로 높은 처리량을 제공하여 호스팅 비용을 절감하는 데 도움이 됩니다.

## 지원되는 플랫폼 {#supported-platforms}

이미징 코드 변환 라이브러리는 RHEL 7 및 CentOS 7 배포판에서만 사용할 수 있습니다.

>[!NOTE]
>
>Mac OS 및 기타 *nix 배포(예: Debian 및 Ubuntu)는 지원되지 않습니다.

## 사용 {#usage}

이미징 코드 변환 라이브러리의 명령줄 인수에는 다음 항목이 포함될 수 있습니다.

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth '4' is automatically converted to '8'
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

`-resize` 매개 변수에 대해 다음 옵션을 구성할 수 있습니다.

* `X`: [!DNL Experience Manager]과(와) 유사하게 작동합니다. 예를 들어 -resize 319를 사용합니다.
* `WxH`: 종횡비가 유지되지 않습니다(예: `-resize 319x319`).
* `Wx`: 너비를 수정하고 종횡비를 유지하면서 높이를 계산합니다. 예: `-resize 319x`
* `xH`: 높이를 수정하고 종횡비를 유지하면서 너비를 계산합니다. 예: `-resize x319`

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 이미징 코드 변환 라이브러리 구성 {#configuring-imaging-transcoding-library}

ITL 처리를 구성하려면 구성 파일을 만들고 이를 실행할 워크플로우를 업데이트합니다.

### 추출된 번들에 대한 구성 파일 만들기 {#create-conf-file}

라이브러리를 구성하려면 다음 단계를 사용하여 라이브러리를 나타내는 CONF 파일을 만듭니다. 관리자 또는 루트 권한이 필요합니다.

1. 소프트웨어 배포에서 [이미징 코드 변환 라이브러리 패키지](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg)를 다운로드하고 패키지 관리자를 사용하여 설치하십시오. 패키지가 [!DNL Experience Manager] 6.5와(과) 호환됩니다.

1. `com.day.cq.dam.cq-dam-switchengine`의 번들 ID를 확인하려면 웹 콘솔에 로그인하고 **[!UICONTROL OSGi]** > **[!UICONTROL 번들]**&#x200B;을(를) 클릭합니다. 또는 번들 콘솔을 열려면 `https://[aem_server:[port]/system/console/bundles/` URL에 액세스합니다. `com.day.cq.dam.cq-dam-switchengine` 번들 및 해당 ID를 찾습니다.

1. `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` 명령을 사용하여 폴더를 확인하여 필요한 모든 라이브러리가 추출되었는지 확인하십시오. 여기서 폴더 이름은 번들 ID를 사용하여 생성됩니다. 예를 들어 번들 ID가 `588`인 경우 명령은 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/`입니다.

1. 라이브러리에 연결할 `SWitchEngineLibs.conf` 파일을 만듭니다.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. `cat SWitchEngineLibs.conf` 명령을 사용하여 conf 파일에 `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` 경로를 추가하십시오.

1. `ldconfig` 명령을 실행하여 필요한 링크와 캐시를 만듭니다.

1. [!DNL Experience Manager]을(를) 시작하는 데 사용되는 계정에서 `.bash_profile` 파일을 편집하세요. 다음을 추가하여 `LD_LIBRARY_PATH`을(를) 추가합니다.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. 경로의 값이 `.`(으)로 설정되었는지 확인하려면 `echo $LD_LIBRARY_PATH` 명령을 사용하십시오. 출력은 `.`이어야 합니다. 값이 `.`(으)로 설정되지 않은 경우 세션을 다시 시작합니다.

### [!UICONTROL DAM 자산 업데이트] 워크플로 구성 {#configure-dam-asset-update-workflow}

이미지 처리에 라이브러리를 사용하도록 [!UICONTROL DAM 자산 업데이트] 워크플로우를 업데이트합니다.

1. [!DNL Experience Manager] 사용자 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**&#x200B;을(를) 선택합니다.

1. **[!UICONTROL 워크플로 모델]** 페이지에서 편집 모드로 **[!UICONTROL DAM 자산 업데이트]** 워크플로 모델을 엽니다.

1. **[!UICONTROL 프로세스 썸네일]** 워크플로우 프로세스 단계를 엽니다. **[!UICONTROL 썸네일]** 탭의 **[!UICONTROL MIME 유형 건너뛰기]** 목록에서 기본 썸네일 생성 프로세스를 건너뛸 MIME 유형을 추가합니다.
예를 들어 이미징 코드 변환 라이브러리를 사용하여 TIFF 이미지에 대한 썸네일을 만들려면 **[!UICONTROL MIME 유형 건너뛰기]** 필드에 `image/tiff`을(를) 지정하십시오.

1. **[!UICONTROL 웹 사용 이미지]** 탭에서 **[!UICONTROL 목록 건너뛰기]**&#x200B;에서 기본 웹 렌디션 생성 프로세스를 건너뛸 MIME 형식을 추가합니다. 예를 들어 위 단계에서 MIME 유형 `image/tiff`을(를) 건너뛰었다면 `image/tiff`을(를) 건너뛰기 목록에 추가하십시오.

1. **[!UICONTROL EPS 썸네일(ImageMagick 제공)]** 단계를 열고 **[!UICONTROL 인수]** 탭으로 이동합니다. **[!UICONTROL MIME 형식]** 목록에서 이미징 코드 변환 라이브러리에서 처리할 MIME 형식을 추가합니다. 예를 들어 위 단계에서 MIME 유형 `image/tiff`을(를) 건너뛰었다면 **[!UICONTROL MIME 유형]** 목록에 `image/jpeg`을(를) 추가하십시오.

1. 기본 명령이 있는 경우 제거합니다.

1. 사이드 패널을 전환하고 단계 목록에서 **[!UICONTROL SWitchEngine 처리기]**&#x200B;를 추가합니다.

1. 사용자 지정 요구 사항에 따라 [!UICONTROL SwitchEngine 처리기]에 명령을 추가합니다. 요구 사항을 충족하도록 지정하는 명령의 매개변수를 조정합니다. 예를 들어 JPEG 이미지의 색 프로필을 유지하려면 **[!UICONTROL 명령]** 목록에 다음 명령을 추가합니다.

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![chlimage](assets/chlimage_1-199.png)

1. (선택 사항) 단일 명령을 사용하여 중간 렌디션에서 썸네일을 생성합니다. 중간 렌디션은 정적 렌디션과 웹 렌디션을 생성하는 소스 역할을 합니다. 이 방법은 이전 방법보다 빠릅니다. 그러나 이 방법을 사용하여 사용자 지정 매개 변수를 썸네일에 적용할 수는 없습니다.

   ![chlimage](assets/chlimage_1-200.png)

1. 웹 변환을 생성하려면 **[!UICONTROL 웹 사용 이미지]** 탭에서 매개 변수를 구성하십시오.

1. 업데이트된 [!UICONTROL DAM 자산 업데이트] 워크플로우 모델을 동기화합니다. 워크플로우를 저장합니다.

구성을 확인하려면 TIFF 이미지를 업로드하고 error.log 파일을 모니터링합니다. `SwitchEngineHandlingProcess execute: executing command line`을(를) 언급한 `INFO`개의 메시지가 표시됩니다. 로그에는 생성된 렌디션이 언급됩니다. 워크플로가 완료되면 [!DNL Experience Manager]에서 새 변환을 볼 수 있습니다.

>[!MORELIKETHIS]
>
>* [지원되는 MIME 유형 문서](assets-formats.md#supported-image-transcoding-library)
