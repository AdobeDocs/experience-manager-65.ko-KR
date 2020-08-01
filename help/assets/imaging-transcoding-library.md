---
title: 이미징 코드 변환 라이브러리
description: 인코딩, 트랜스코딩, 이미지 리샘플링, 이미지 크기 조정 등 핵심 이미지 처리 기능을 수행할 수 있는 이미지 처리 솔루션인 Adobe의 이미징 트랜스코딩 라이브러리를 구성 및 사용하는 방법을 살펴볼 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 1%

---


# 이미징 코드 변환 라이브러리 {#imaging-transcoding-library}

Adobe의 이미징 트랜스코딩 라이브러리는 다음과 같은 핵심 이미지 처리 기능을 수행할 수 있는 독점적인 이미지 처리 솔루션입니다.

* 인코딩
* 트랜스코딩(지원되는 포맷 변환)
* PS 및 인텔 IPP 알고리즘 사용 이미지 리샘플링
* 비트 심도 및 색상 프로파일 유지
* JPEG 품질 압축
* 이미지 크기 조정

이미징 트랜스코딩 라이브러리는 CMYK -Alpha를 제외한 모든 알파 지원과 CMYK를 지원합니다.

Imaging Transcoding Library는 다양한 파일 포맷과 프로파일을 지원할 뿐만 아니라 성능, 확장성 및 품질 측면에서 다른 타사 솔루션에 비해 상당한 이점을 제공합니다. 다음은 이미징 트랜스코딩 라이브러리를 사용할 때 얻을 수 있는 몇 가지 주요 이점입니다.

* **파일 크기 또는 해상도로 크기 조정**: 크기 조절은 기본적으로 파일을 디코딩하는 동안 이미지 트랜스코딩 라이브러리를 재지정하는 특허 기능을 통해 이루어집니다. 이러한 기능을 통해 런타임 메모리 사용이 항상 최적의 상태로 유지되며 파일 크기나 해상도의 메가픽셀을 증가시키는 이차 기능이 아닙니다. 이미징 트랜스코딩 라이브러리는 더 큰 고해상도(더 높은 메가픽셀 포함) 파일을 처리할 수 있습니다. ImageMagick과 같은 타사 도구는 이러한 파일을 처리하는 동안 큰 파일 및 충돌을 처리할 수 없습니다.
* **Photoshop 품질 압축 및 크기 조정 알고리즘**: 다운샘플링 품질(매끄러움, 샤프 및 자동 쌍입방) 및 압축 품질 측면에서 업계 표준과 일관성을 유지할 수 있습니다. Imaging Transcoding Library는 입력 이미지의 품질 요소를 추가로 평가하고 출력 이미지에 적합한 테이블과 품질 설정을 지능적으로 사용합니다. 이 기능을 사용하면 시각적 품질을 저해하지 않고도 최적의 크기의 파일을 제작할 수 있습니다.
* **높은 처리량:** 응답 시간은 낮고 처리량은 ImageMagick보다 일관되게 높습니다. 따라서 이미징 트랜스코딩 라이브러리는 사용자의 대기 시간과 호스팅 비용을 줄일 수 있습니다.
* **동시 로드를 사용하여 더 높은 비율 조정:** 이미징 트랜스코딩 라이브러리는 동시 로드 조건에서 최적으로 수행됩니다. It provides high throughput with optimum CPU performance, memory usage, and low response time, which helps the cost of hosting.

## Supported platforms {#supported-platforms}

이미징 트랜스코딩 라이브러리는 RHEL 7 및 CentOS 7 배포에만 사용할 수 있습니다.

>[!NOTE]
>
>Mac OS 및 기타 *nix 배포(예: Debian 및 Ubuntu)는 지원되지 않습니다.

## 사용량 {#usage}

이미징 트랜스코딩 라이브러리의 명령줄 인수에는 다음이 포함될 수 있습니다.

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

매개 변수에 대해 다음 옵션을 구성할 수 `-resize` 있습니다.

* `X`: 유사한 [!DNL Experience Manager]작업 예: -resize 319.
* `WxH`: 예를 들어 종횡비는 유지되지 않습니다 `-resize 319x319`.
* `Wx`: 너비를 수정하고 종횡비를 유지하면서 높이를 계산합니다. 예 `-resize 319x`.
* `xH`: 높이를 수정하고 종횡비를 유지하면서 너비를 계산합니다. 예 `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 이미징 트랜스코딩 라이브러리 구성 {#configuring-imaging-transcoding-library}

ITL 처리를 구성하려면 구성 파일을 만들고 워크플로를 업데이트하여 실행합니다.

### 압축을 푼 번들에 대한 구성 파일 만들기 {#create-conf-file}

라이브러리를 구성하려면 다음 단계를 사용하여 라이브러리를 나타내는 CONF 파일을 생성합니다. 관리자 또는 루트 권한이 필요합니다.

1. 소프트웨어 배포에서 [이미징 트랜스코딩 라이브러리 패키지를 다운로드하고](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) 패키지 관리자를 사용하여 설치합니다. 그 패키지는 [!DNL Experience Manager] 6.5와 호환된다.

1. 의 번들 ID에 대해 알려면 웹 콘솔 `com.day.cq.dam.cq-dam-switchengine`에 로그인하고 OSGi **[!UICONTROL > 번들을]** 클릭합니다 ****. 또는 번들 콘솔을 열려면 `https://[aem_server:[port]/system/console/bundles/` URL에 액세스하십시오. 번들 `com.day.cq.dam.cq-dam-switchengine` 및 해당 ID를 찾습니다.

1. 번들 ID를 사용하여 폴더 이름이 구성되는 명령을 사용하여 폴더를 확인하여 필요한 모든 라이브러리 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`가 추출되는지 확인합니다. 예를 들어 번들 id가 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` 인 경우 이 명령을 사용합니다 `588`.

1. 라이브러리에 `SWitchEngineLibs.conf` 연결할 파일을 만듭니다.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 명령 `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` 을 사용하여 conf 파일에 경로를 `cat SWitchEngineLibs.conf` 추가합니다.

1. 명령을 실행하여 필요한 링크 및 캐시를 `ldconfig` 만듭니다.

1. 시작하는 데 사용되는 계정에서 [!DNL Experience Manager]파일 `.bash_profile` 을 편집합니다. 다음을 추가하여 `LD_LIBRARY_PATH` 추가합니다.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. 경로 값이 로 설정되어 있는지 확인하려면 `.`command를 `echo $LD_LIBRARY_PATH` 사용합니다. 출력물은 그냥 `.`됩니다 값이 로 설정되지 않은 경우 세션 `.`을 다시 시작합니다.

### DAM [!UICONTROL 자산 업데이트 워크플로우] 구성 {#configure-dam-asset-update-workflow}

이미지 처리에 라이브러리를 사용하도록 [!UICONTROL DAM 자산] 업데이트 워크플로우를 업데이트합니다.

1. 사용자 [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > 워크플로우 **[!UICONTROL > 모델]** 을 **[!UICONTROL 선택합니다]**.

1. 워크플로우 **[!UICONTROL 모델]** 페이지에서 **[!UICONTROL DAM 자산]** 업데이트 워크플로우 모델을 편집 모드로 엽니다.

1. [축소판 **[!UICONTROL 처리] 워크플로우]** 프로세스 단계를 엽니다. [축소판 **** ] 탭에서 [MIME 유형 건너뛰기] **[!UICONTROL 목록에서 기본 축소판 생성 프로세스를 건너뛸 MIME 유형을]** 추가합니다.
예를 들어 이미징 트랜스코딩 라이브러리를 사용하여 TIFF 이미지에 대한 축소판을 만들려면 [MIME 유형 건너뛰기] `image/tiff` 필드 **[!UICONTROL 에서 지정합니다]** .

1. [ **[!UICONTROL 웹 사용 이미지]** ] 탭에서 [건너뛰기 목록]에서 기본 웹 변환 생성 프로세스를 건너뛸 MIME 유형을 **[!UICONTROL 추가합니다]**. 예를 들어, 위 단계에서 MIME 유형 `image/tiff` 을 생략한 경우 건너뛰기 목록 `image/tiff` 에 추가합니다.

1. EPS **[!UICONTROL 축소판(ImageMagick에서 제공)]** 단계를 열고 **[!UICONTROL 인수]** 탭으로 이동합니다. [ **[!UICONTROL MIME 유형]** ] 목록에서 이미징 트랜스코딩 라이브러리를 처리할 MIME 형식을 추가합니다. 예를 들어, 위 단계 `image/tiff` 에서 MIME 유형을 건너뛰었을 경우 `image/jpeg` MIME 유형 **** 목록에 추가하십시오.

1. 기본 명령이 있을 경우 기본 명령을 제거합니다.

1. 사이드 패널과 단계 목록에서 SWitchEngine 핸들러를 **[!UICONTROL 추가합니다]**.

1. 사용자 지정 요구 사항에 따라 [!UICONTROL SwitchEngine 핸들러에] 명령을 추가합니다. 요구 사항에 맞게 지정한 명령의 매개 변수를 조정합니다. 예를 들어 JPEG 이미지의 색상 프로파일을 보존하려면 명령(Commands) **[!UICONTROL 목록에 다음 명령을]** 추가합니다.

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![천하](assets/chlimage_1-199.png)

1. (선택 사항) 하나의 명령을 사용하여 중간 변환에서 축소판을 생성합니다. 중간 변환은 정적 및 웹 변환을 생성하는 소스 역할을 합니다. 이 방법은 이전 방법보다 빠릅니다. 그러나 이 방법을 사용하면 사용자 정의 매개 변수를 축소판에 적용할 수 없습니다.

   ![천하](assets/chlimage_1-200.png)

1. 웹 변환을 생성하려면 **[!UICONTROL 웹 사용 이미지]** 탭에서 매개 변수를 구성하십시오.

1. 업데이트된 [!UICONTROL DAM 자산 업데이트 워크플로우] 모델을 동기화합니다. 워크플로우를 저장합니다.

구성을 확인하고 TIFF 이미지를 업로드하고 error.log 파일을 모니터링합니다. 다음에 대한 언급 `INFO` 메시지가 표시됩니다 `SwitchEngineHandlingProcess execute: executing command line`. 로그에 생성된 표현물이 언급됩니다. 워크플로우가 완료되면 에서 새 변환을 볼 수 있습니다 [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [지원되는 MIME 형식 아티클](assets-formats.md#supported-image-transcoding-library)

