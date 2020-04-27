---
title: AEM Assets에서 작동하도록 ImageMagick 설치 및 구성
description: ImageMagick 소프트웨어에 대한 자세한 내용, 설치 방법, 명령줄 프로세스 단계 설정, 이미지 축소판 편집, 작성 및 생성 방법 등을 살펴볼 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 31234518537ca4a0b7ff36e8d52a3b7b1b8fe4f7

---


# AEM Assets에서 작동하도록 ImageMagick 설치 및 구성{#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick은 비트맵 이미지를 생성, 편집, 구성 또는 변환할 수 있는 소프트웨어 플러그인입니다. PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF 및 SVG를 비롯한 다양한 형식(200개 이상)으로 이미지를 읽고 쓸 수 있습니다. ImageMagick을 사용하여 이미지 크기 조정, 대칭 이동, 회전, 왜곡, 기울이기 및 변형 또한 ImageMagick을 사용하여 이미지 색상을 조정하거나 다양한 특수 효과를 적용하거나 텍스트, 선, 다각형, 타원 및 곡선을 그릴 수 있습니다.

명령줄에서 Adobe Experience Manager(AEM) 미디어 핸들러를 사용하여 ImageMagick을 통해 이미지를 처리합니다. ImageMagick을 사용하여 다양한 파일 포맷으로 작업하려면 [에셋 파일 포맷 우수 사례를](/help/assets/assets-file-format-best-practices.md)참조하십시오. 지원되는 모든 파일 포맷에 대해 알아보려면 [자산 지원 형식을](/help/assets/assets-formats.md)참조하십시오.

ImageMagick을 사용하여 대용량 파일을 처리하려면 일반적인 메모리 요구 사항보다 높은 수치, IM 정책에 필요한 잠재적 변경 사항 및 성능에 대한 전반적인 영향을 고려하십시오. 메모리 요구 사항은 해상도, 비트 심도, 색상 프로파일 및 파일 포맷과 같은 다양한 요인에 따라 달라집니다. ImageMagick을 사용하여 매우 큰 파일을 처리하려면 AEM 서버를 적절하게 벤치마킹하십시오. 유용한 리소스는 마지막에 제공됩니다.

>[!NOTE]
>
>AMS(Adobe Managed Services)에서 AEM을 사용하는 경우 고해상도 PSD 또는 PSB 파섹 파일을 많이 처리하려는 경우 Adobe 고객 지원 센터에 문의하십시오. Adobe Experience Manager는 3000 x 23000픽셀이 넘는 매우 고해상도 PSB 파일을 처리하지 못할 수 있습니다.

## ImageMagick 설치 {#installing-imagemagick}

다양한 운영 체제에서 ImageMagic 설치 파일을 사용할 수 있습니다. 운영 체제에 적합한 버전을 사용하십시오.

1. 운영 체제에 적합한 [ImageMagick 설치 파일을](https://www.imagemagick.org/script/download.php) 다운로드합니다.
1. AEM 서버를 호스팅하는 디스크에 ImageMagick을 설치하려면 설치 파일을 실행합니다.

1. 경로 환경 변수를 ImageMagic 설치 디렉토리로 설정합니다.
1. 설치가 성공적인지 확인하려면 `identify -version` 명령을 실행합니다.

## 명령줄 프로세스 단계 설정 {#set-up-the-command-line-process-step}

특정 사용 사례에 대해 명령줄 프로세스 단계를 설정할 수 있습니다. AEM 서버에 JPEG 이미지 파일을 추가할 때마다 뒤집힌 이미지 및 축소판(140x100, 48x48, 319x319 및 1280x1280)을 생성하려면 다음 단계를 수행하십시오 `/content/dam` .

1. AEM 서버에서 워크플로우 콘솔(`https://[aem_server]:[port]/workflow`)로 이동하여 DAM 자산 **[!UICONTROL 업데이트 워크플로우 모델을]** 엽니다.
1. DAM 자산 **[!UICONTROL 업데이트]** 워크플로우 모델에서 EPS **[!UICONTROL 축소판(ImageMagick 제공)]** 단계를 엽니다.
1. 인수 **[!UICONTROL 탭에서]** MIME 유형 `image/jpeg` 목록에 **[!UICONTROL 추가합니다]** .

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. 명령 **[!UICONTROL 상자에]** 다음 명령을 입력합니다.

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. 생성된 **[!UICONTROL 변환 삭제]** 및 웹 변환 **[!UICONTROL 생성 플래그를]** 선택합니다.

   ![select_flags](assets/select_flags.png)

1. [웹 **[!UICONTROL 사용 이미지]** ] 탭에서 1280x1280픽셀의 변환 세부 사항을 지정합니다. 또한 Mimetype `image/jpeg` 상자에 **[!UICONTROL 지정합니다]** .

   ![web_enabled_image](assets/web_enabled_image.png)

1. **[!UICONTROL 확인]**&#x200B;을 클릭하여 변경 사항을 저장합니다.

   >[!NOTE]
   >
   >Windows SE와 같은 특정 Windows 버전 `convert` 명령은 Windows 설치의 일부인 기본 `convert` 유틸리티와 충돌하므로 실행할 수 없습니다. 이 경우 ImageMagick 유틸리티의 전체 경로를 언급하십시오. 예를 들어,
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. [ **[!UICONTROL 프로세스 축소판]** ] 단계를 열고 [MIME 유형 건너뛰기] `image/jpeg` 아래에 **[!UICONTROL MIME 유형을 추가합니다]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. 웹 **[!UICONTROL 사용 이미지]** 탭에서 목록 `image/jpeg` 건너뛰기 아래에 MIME 유형을 **[!UICONTROL 추가합니다]**. **[!UICONTROL 확인]**&#x200B;을 클릭하여 변경 사항을 저장합니다.

   ![web_enabled](assets/web_enabled.png)

1. 워크플로우를 저장합니다.
1. ImageMagic에서 이미지를 제대로 처리할 수 있는지 확인하려면 JPG 이미지를 AEM 자산에 업로드하십시오. 역진행 이미지와 표현물이 생성되는지 확인합니다.

## 보안 취약점 완화 {#mitigating-security-vulnerabilities}

이미지를 처리하기 위해 ImageMagick을 사용하는 것과 관련된 여러 가지 보안 취약점이 있습니다. 예를 들어 사용자가 제출한 이미지를 처리하는 경우 RCE(원격 코드 실행)가 발생할 위험이 있습니다.

또한 다양한 이미지 처리 플러그인은 ImageMagick 라이브러리에 따라 달라지며 PHP의 이미지, Ruby의 빠른 이미지 및 페이퍼클립, nodejs의 이미지 클릭 등을 포함합니다.

ImageMagick 또는 영향을 받는 라이브러리를 사용하는 경우, Adobe에서는 다음 작업 중 하나 이상을 수행하여 알려진 취약점을 완화하는 것이 좋습니다(하지만 둘 다 가능).

1. 모든 이미지 파일이 처리를 위해 ImageMagick으로 보내기 전에 지원하는 이미지 파일 유형에 해당하는 예상 [&quot;매직 바이트&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) 로 시작하는지 확인합니다.
1. 정책 파일을 사용하여 취약한 ImageMagick 코드를 비활성화합니다. ImageMagick에 대한 글로벌 정책은 에서 찾을 수 `/etc/ImageMagick`있습니다.
