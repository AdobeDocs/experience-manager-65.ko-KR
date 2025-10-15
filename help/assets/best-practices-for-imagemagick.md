---
title: ImageMagick 설치 및 구성
description: ImageMagick 소프트웨어, 설치 방법, 명령줄 프로세스 단계 설정 및 이를 사용하여 이미지의 썸네일을 편집, 작성 및 생성하는 방법에 대해 알아봅니다.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools
exl-id: 6c149d31-1e64-4d29-a32a-58bd69e9fa98
solution: Experience Manager, Experience Manager Assets
source-git-commit: f8588ef353bd08b41202350072728d80ee51f565
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 0%

---

# [!DNL Experience Manager Assets]에서 작동하도록 ImageMagick 설치 및 구성 {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick은 비트맵 이미지를 작성, 편집, 작성 또는 변환하는 소프트웨어 플러그인입니다. PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF, SVG 등 다양한 형식(200개 이상)으로 이미지를 읽고 쓸 수 있습니다. ImageMagick을 사용하여 이미지의 크기 조정, 뒤집기, 대칭복사, 회전, 왜곡, 기울이기 및 변형을 수행할 수 있습니다. ImageMagick를 사용하여 이미지 색상을 조정하거나 다양한 특수 효과를 적용하거나 텍스트, 선, 다각형, 타원 및 곡선을 그릴 수도 있습니다.

명령줄에서 [!DNL Adobe Experience Manager] 미디어 핸들러를 사용하여 ImageMagick을 통해 이미지를 처리합니다. ImageMagick를 사용하여 다양한 파일 형식을 사용하려면 [Assets 파일 형식 모범 사례](/help/assets/assets-file-format-best-practices.md)를 참조하세요. 지원되는 모든 파일 형식에 대해 알아보려면 [Assets 지원 형식](/help/assets/assets-formats.md)을 참조하세요.

ImageMagick을 사용하여 대용량 파일을 처리하려면 일반적인 메모리 요구 사항, IM 정책에 필요한 잠재적인 변경 사항 및 성능에 미치는 전반적인 영향을 고려하십시오. 메모리 요구 사항은 해상도, 비트 깊이, 색상 프로파일 및 파일 형식과 같은 다양한 요소에 따라 다릅니다. ImageMagick을 사용하여 대용량 파일을 처리하려면 [!DNL Experience Manager] 서버를 올바르게 벤치마킹하십시오. 유용한 리소스는 마지막에 제공됩니다.

>[!NOTE]
>
>[!DNL Experience Manager]&#x200B;(AMS)에서 [!DNL Adobe Managed Services]을(를) 사용 중인 경우 고해상도 PSD 또는 PSB 파일을 많이 처리하려면 Adobe 고객 지원 센터에 문의하십시오. [!DNL Experience Manager]은(는) 30000 x 23000 픽셀보다 큰 고해상도 PSB 파일을 처리하지 못할 수 있습니다.

## ImageMagick 설치 {#installing-imagemagick}

ImageMagic 설치 파일의 여러 버전은 다양한 운영 체제에서 사용할 수 있습니다. 운영 체제에 적합한 버전을 사용합니다.

1. 운영 체제에 적합한 ImageMagick 설치 파일(`https://www.imagemagick.org/script/download.php website`)을 다운로드합니다.
1. [!DNL Experience Manager] 서버를 호스팅하는 디스크에 ImageMagick을 설치하려면 설치 파일을 실행하십시오.

1. 경로 환경 변수를 ImageMagic 설치 디렉토리로 설정합니다.
1. 설치가 성공했는지 확인하려면 `identify -version` 명령을 실행하십시오.

## 명령줄 프로세스 단계 설정 {#set-up-the-command-line-process-step}

특정 사용 사례에 대한 명령줄 프로세스 단계를 설정할 수 있습니다. `/content/dam` 서버의 [!DNL Experience Manager]에 JPEG 이미지 파일을 추가할 때마다 뒤집힌 이미지 및 썸네일(140x100, 48x48, 319x319 및 1280x1280)을 생성하려면 다음 단계를 수행하십시오.

1. [!DNL Experience Manager] 서버에서 워크플로 콘솔(`https://[aem_server]:[port]/workflow`)로 이동하여 **[!UICONTROL DAM 자산 업데이트]** 워크플로 모델을 엽니다.
1. **[!UICONTROL DAM 자산 업데이트]** 워크플로우 모델에서 **[!UICONTROL EPS 썸네일(ImageMagick 제공)]** 단계를 엽니다.
1. **[!UICONTROL 인수 탭]**&#x200B;에서 `image/jpeg`MIME 형식&#x200B;**[!UICONTROL 목록에]**&#x200B;을(를) 추가하십시오.

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. **[!UICONTROL 명령]** 상자에 다음 명령을 입력합니다.

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. **[!UICONTROL 생성된 렌디션 삭제]** 및 **[!UICONTROL 웹 렌디션 생성]** 플래그를 선택합니다.

   ![select_flags](assets/select_flags.png)

1. **[!UICONTROL 웹 사용 이미지]** 탭에서 1280x1280 픽셀 크기의 렌디션에 대한 세부 정보를 지정합니다. 또한 `image/jpeg`Mimetype **[!UICONTROL 상자에]**&#x200B;을(를) 지정하십시오.

   ![web_enabled_image](assets/web_enabled_image.png)

1. **[!UICONTROL 확인]**&#x200B;을 클릭하여 변경 내용을 저장합니다.

   >[!NOTE]
   >
   >`convert` 명령은 Windows 설치의 일부인 기본 `convert` 유틸리티와 충돌하므로 특정 Windows 버전(예: Windows SE)에서 실행되지 않을 수 있습니다. 이 경우 ImageMagick 유틸리티의 전체 경로를 언급하십시오. 예를 들어, 을 지정합니다.
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. **[!UICONTROL 썸네일 처리]** 단계를 열고 `image/jpeg`MIME 유형 건너뛰기&#x200B;**[!UICONTROL 에 MIME 유형]**&#x200B;을(를) 추가합니다.

   ![skip_mime_types](assets/skip_mime_types.png)

1. **[!UICONTROL 웹 사용 이미지]** 탭의 `image/jpeg`목록 건너뛰기&#x200B;**[!UICONTROL 아래에 MIME 형식]**&#x200B;을(를) 추가하십시오. **[!UICONTROL 확인]**&#x200B;을 클릭하여 변경 내용을 저장합니다.

   ![web_enabled](assets/web_enabled.png)

1. 워크플로우를 저장합니다.

1. 올바른 처리를 확인하려면 JPG 이미지를 [!DNL Assets]에 업로드하십시오. 처리가 완료되면 뒤집힌 이미지와 표현물이 생성되는지 확인합니다.

## 보안 취약성 완화 {#mitigating-security-vulnerabilities}

ImageMagick을 사용하여 이미지를 처리하는 것과 관련된 여러 보안 취약점이 있습니다. 예를 들어 사용자가 제출한 이미지를 처리하면 RCE(원격 코드 실행)가 발생합니다.

또한 PHP의 이미지, Ruby의 이미지 및 paperclip, nodejs의 이미지magick 등 다양한 이미지 처리 플러그인은 ImageMagick 라이브러리에 따라 다릅니다.

Adobe ImageMagick 또는 영향을 받는 라이브러리를 사용하는 경우 다음 작업 중 하나 이상(하지만 둘 다)을 수행하여 알려진 취약성을 완화하는 것이 좋습니다.

1. 모든 이미지 파일이 처리를 위해 ImageMagick에 보내기 전에 지원하는 이미지 파일 형식에 해당하는 예상 [&quot;매직 바이트&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures)&#x200B;(으)로 시작하는지 확인하십시오.
1. 정책 파일을 사용하여 취약한 ImageMagick 코드를 비활성화합니다. ImageMagick에 대한 전역 정책이 `/etc/ImageMagick`에 있습니다.
