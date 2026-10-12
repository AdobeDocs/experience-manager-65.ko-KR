---
title: C2PA 메타데이터 [!DNL Experience Manager Assets]
description: '[!DNL Experience Manager Assets]이(가) 업로드된 에셋에서 C2PA 메타데이터를 감지하고 사용자 인터페이스에 플래그를 지정하고 일반 AI 에셋에 대해 생성한 렌디션에 서명하는 방법을 알아봅니다.'
role: User, Admin, Developer
feature: Asset Management, Metadata, Renditions, Workflow, Asset Processing
solution: Experience Manager, Experience Manager Assets
source-git-commit: f47205896ed512deadb4d31acbfe0fafa18515e7
workflow-type: tm+mt
source-wordcount: '2585'
ht-degree: 6%
---

# [!DNL Experience Manager Assets]의 C2PA 메타데이터 {#c2pa-metadata}

브랜드는 콘텐츠 투명성, AI 공개, 에셋 변조 방지에 그 어느 때보다 더 큰 관심을 기울이고 있습니다. Adobe의 Content Authenticity Initiative(CAI)는 [Coalition for Content Provenance and Authenticity](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html)&#x200B;(C2PA) 기술 표준을 준수하는 도구를 빌드합니다. 변조가 명백한 새로운 종류의 메타데이터인 C2PA 메타데이터는 시청자가 콘텐츠 계보를 이해하고 브랜드 자산의 무결성을 확인하는 데 도움이 됩니다. 여기에는 디지털 에셋의 기록에 대한 인사이트를 제공하는 다양한 출처의 데이터가 포함될 수 있습니다.

이 정보에는 다음 내용이 포함됩니다.

* **발급자 또는 서명자:** 자산의 디지털 서명을 발급한 엔터티 또는 회사에 대한 정보입니다.
* **문제 날짜:** C2PA 메타데이터가 에셋에 적용된 날짜입니다.
* **프로세스:** 에셋에 대한 편집 또는 수정 사항의 기록입니다.
* **디바이스 세부 정보:** 에셋을 만들거나 편집하는 데 사용되는 앱 또는 장치 관련 정보입니다.
* **AI 도구 사용됨:** 생성 AI를 사용하여 에셋을 편집하거나 만든 경우 사용된 모델의 이름이 포함됩니다.
* **기타 관련 정보:** 자산의 내역에 대한 추가 컨텍스트를 제공하는 추가 데이터입니다.

에셋의 기록에 대한 자세한 내용은 [확인](https://contentcredentials.org/verify)을 참조하세요.

[!DNL Adobe Experience Manager Assets]은(는) 에셋을 업로드하거나 업데이트할 때 C2PA 메타데이터를 감지하고 [!DNL Assets] 사용자 인터페이스에서 해당 에셋에 플래그를 지정하고 [!DNL Experience Manager]이(가) 생성하는 변환에서 Gen AI 공개를 그대로 유지합니다. [!DNL Experience Manager]이(가) 썸네일, 웹 렌디션, 워터마크가 지정된 복사본 또는 비디오 변환 코드와 같은 Gen AI 에셋의 렌디션을 만들거나 수정할 때마다 [!DNL Experience Manager]은(는) 원본 에셋을 상위로 참조하는 새 C2PA 메타데이터를 사용하여 해당 렌디션에 서명합니다. 다운로드, 게시 또는 공유하는 렌디션은 출처를 유지합니다.

## 사전 요구 사항 {#Prerequisites}

C2PA 메타데이터 지원에는 [!DNL Adobe Experience Manager] 6.5 서비스 팩이 필요합니다. 서비스 팩 6.5.25.0에서 [AEM 6.5 SP25 - C2PA GenAI 규정 준수 핫픽스](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-ASSETS-75868-SP25-1.0.zip)를 설치하십시오.

## 지원되는 형식 및 플랫폼 {#supported-formats}

### 형식 {#formats}

[!DNL Experience Manager]은(는) [C2PA 사양](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html)이 포함된 매니페스트에 대해 지원하는 형식으로 변환에 서명합니다.

| 유형 | 형식 | MIME 유형 |
|---|---|---|
| 이미지 | JPEG, PNG, GIF, TIFF, DNG, WebP, JPEG XL, AVIF, HEIC/HEIF, SVG | `image/jpeg`, `image/png`, `image/gif`, `image/tiff`, `image/x-adobe-dng`, `image/webp`, `image/jxl`, `image/avif`, `image/heic`, `image/heif`, `image/svg+xml` |
| 비디오 | MP4, MOV, AVI | `video/mp4`, `video/quicktime`, `video/x-msvideo` |
| 오디오 | MP3, M4A, WAV, FLAC | `audio/mpeg`, `audio/mp4`, `audio/wav`, `audio/flac` |

[!DNL Experience Manager]은(는) `image/jpg`, `image/pjpeg`, `image/x-png` 및 `video/mov`과(와) 같은 일반적인 별칭도 인식합니다. [!DNL Experience Manager]은(는) 파일 형식과 관계없이 업로드된 모든 에셋에서 매니페스트를 확인합니다. PSD 또는 EPS과 같은 다른 형식의 렌디션은 서명되지 않습니다.

### 플랫폼 {#platforms}

C2PA 메타데이터 지원은 `cq-dam-core` 번들 내에 제공되는 기본 C2PA 구성 요소를 사용하며, 지원되는 플랫폼마다 빌드가 하나씩 있습니다. 서비스가 시작되면 [!DNL Experience Manager]이(가) 플랫폼의 빌드(`adobe_c2patool` 또는 Windows의 `adobe_c2patool.exe`)를 번들의 개인 데이터 폴더로 추출하여 SHA-256 체크섬을 확인하고 별도의 프로세스로 실행합니다. 아무 것도 설치하거나 `PATH`을(를) 변경할 필요가 없습니다.

| 운영 체제 | 아키텍처 |
|---|---|
| Linux(glibc 2.28 이상(Red Hat Enterprise Linux 8 포함) | `x86_64`, `aarch64` |
| macOS | `x86_64`, `aarch64`(Apple 실리콘) |
| Windows | `x86_64` |

이 기능은 [!DNL Adobe Managed Services] 및 온-프레미스 배포에서 동일하게 작동합니다. [!DNL Experience Manager] 프로세스에서 이 실행 파일을 시작할 수 있는지 확인하십시오. `noexec`개의 탑재, 바이러스 백신 또는 끝점 보안 소프트웨어를 사용하는 경우 `crx-quickstart` 폴더에서 `adobe_c2patool`을(를) 실행할 수 있도록 허용합니다. 그렇지 않으면 C2PA 메타데이터 지원을 시작할 수 없습니다.

## C2PA 메타데이터의 작동 방식 {#how-c2pa-metadata-works}

C2PA 메타데이터 지원에는 에셋이 업로드되거나 업데이트될 때 검색과 [!DNL Experience Manager]이(가) 렌디션을 생성하거나 수정할 때마다 다시 서명이라는 두 가지 부분이 있습니다.

### 워크플로우 구성 {#workflow}

[C2PA 메타데이터 감지](#detect)에 표시된 **[!UICONTROL C2PA 자격 증명 감지]** 단계는 기본 **[!UICONTROL DAM 자산 업데이트]** 워크플로 모델의 일부입니다. 해당 모델의 사용자 정의 사본을 사용하는 경우 단계를 직접 추가합니다.

1. [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**(으)로 이동한 다음 ![편집 아이콘](assets/edit.svg) **[!UICONTROL 편집]** 모드로 모델을 엽니다.
1. 렌디션을 생성하기 전에 **[!UICONTROL 메타데이터 프로세서]** 다음에 **[!UICONTROL C2PA 자격 증명 감지]** 단계를 추가하십시오.
1. **[!UICONTROL 동기화]**&#x200B;를 선택하여 모델을 저장합니다.

렌디션 단계는 에셋에서 검색이 이미 실행된 경우에만 출력에 서명합니다. 이후에 검색이 실행되면 워크플로우가 다시 실행될 때까지 해당 렌디션에 서명이 없습니다.

### C2PA 메타데이터 감지 {#detect}

**[!UICONTROL DAM 자산 업데이트]** 워크플로에는 아래 그림과 같이 **[!UICONTROL 메타데이터 프로세서]** 단계 이후에 실행되는 **[!UICONTROL C2PA 자격 증명 감지]** 단계가 포함되어 있습니다. 에셋의 원본 바이너리를 읽고 에셋의 메타데이터 노드 `jcr:content/metadata`에 결과를 기록합니다.

![워크플로](assets/workflow.png)

다음 표에는 C2PA 메타데이터 워크플로의 주요 메타데이터 속성이 나열되어 있습니다.

| 속성 | 유형 | 설명 |
|---|---|---|
| `dam:hasC2PAManifest` | `boolean` | 원본 바이너리에 포함된 C2PA 매니페스트가 있는 경우 `true`. 항상 쓰여져 있습니다. |
| `dam:isAiGenerated` | `boolean` | 매니페스트에서 자산을 Gen AI 레이블 지정 범위에 넣는 경우 `true`입니다. 매니페스트가 있을 때만 기록됩니다. |
| `dam:c2paValidationState` | `string` | 매니페스트의 유효성 검사 상태를 설명합니다. `TRUSTED`, `VALID`, `INVALID` 또는 `UNKNOWN`. 매니페스트가 있을 때만 기록됩니다. |

매니페스트가 있으면 [!DNL Experience Manager]에서 매니페스트를 `c2pa-manifest.json` 렌디션(`application/json`)으로 저장합니다.

원본 에셋을 매니페스트가 없는 바이너리로 바꾸면 다음 워크플로우 실행에서 `dam:hasC2PAManifest`을(를) `false`(으)로 설정하고 `dam:isAiGenerated`, `dam:c2paValidationState` 및 `c2pa-manifest.json` 렌디션을 제거합니다.

>[!NOTE]
>
>검색 실패는 에셋 수집을 차단하지 않습니다. 매니페스트 읽기 시간이 초과되거나 실패하면 [!DNL Experience Manager]은(는) 오류를 기록하고, 메타데이터는 변경되지 않은 상태로 두며, 나머지 워크플로우에서는 계속됩니다.

### [!DNL Assets] 사용자 인터페이스에서 C2PA 메타데이터 보기 {#view-c2pa-metadata}

C2PA 메타데이터를 전달하는 Assets은 [!DNL Assets] 사용자 인터페이스에 **cr**(C2PA 메타데이터) 배지를 표시합니다. **[!UICONTROL Assets]** > **[!UICONTROL 파일]**(으)로 이동하여 왼쪽 아래 모서리에 있는 배지를 찾습니다.

* **[!UICONTROL 카드 보기]**&#x200B;의 자산 축소판입니다.
* **[!UICONTROL 열 보기]**&#x200B;의 자산 축소판입니다. 썸네일을 표시할 자산을 선택합니다.
* 에셋 세부 사항 페이지의 미리보기 영역입니다.

다음 그림에 표시된 **cr** 배지는 자산에 C2PA 메타데이터가 포함되어 있는지 여부를 나타냅니다. 매니페스트 자체를 표시하지 않습니다. 전체 매니페스트를 보려면 자산을 다운로드하고 [확인](https://contentcredentials.org/verify)에서 여세요.

![cr 배지](assets/cr.png)

[!DNL Experience Manager]은(는) 검색된 매니페스트를 에셋에서 `c2pa-manifest.json` 렌디션으로 저장합니다. 이 렌디션은 내부에 있습니다. 자산 세부 정보 페이지의 **[!UICONTROL 렌디션]** 패널 또는 렌디션 선택기에 나타나지 않습니다.

### 렌디션 서명 {#sign-renditions}

렌디션은 새 바이너리이므로 원본 에셋에 포함된 매니페스트에서 이를 다루지 않습니다. 일반 AI 공개를 그대로 유지하기 위해 [!DNL Experience Manager]은(는) 적격한 모든 렌디션을 생성하는 프로세스의 마지막 단계로 서명합니다. 새로운 C2PA 메타데이터:

* 원본 자산을 **부모** 성분으로 참조합니다.
* C2PA 작업 `c2pa.resized`, `c2pa.transcoded` 또는 `c2pa.edited` 중 하나로 원본 에셋에서 렌디션이 파생된 방식을 기록합니다.
* `Adobe Experience Manager`을(를) 소프트웨어 에이전트로 지정합니다.

[!DNL Experience Manager]은(는) 다음 항목이 모두 `true`인 경우에만 렌디션에 서명합니다.

* 원본 자산에 `dam:isAiGenerated`이(가) `true`(으)로 설정되어 있습니다. 매니페스트를 포함하지만 AI를 통해 생성되지 않은 Assets에 여전히 **cr** 배지가 표시되지만 [!DNL Experience Manager]은(는) 렌디션을 다시 서명하지 않습니다.
* 원본 매니페스트를 읽을 수 있으며 유효성 검사 상태가 `INVALID`이(가) 아닙니다. [!DNL Experience Manager]은(는) 에셋이 변경된 후 유효성 검사가 실패한 매니페스트에 새 서명을 연결하지 않습니다.
* 렌디션 형식은 포함된 C2PA 매니페스트를 지원합니다. 자세한 내용은 [지원되는 형식](#supported-formats)을 참조하세요. [!DNL Experience Manager]에서 지원되지 않는 형식을 오류 없이 건너뜁니다.

[C2PA 메타데이터 감지](#detect)에 표시된 **[!UICONTROL DAM 자산 업데이트 워크플로우 완료]** 워크플로우의 다음 단계는 출력에 서명합니다.

| 워크플로 단계 | 렌디션 서명됨 | C2PA 작업 기록됨 |
|---|---|---|
| **[!UICONTROL 축소판 처리]** | 썸네일 표현물과 웹 사용 이미지 | 형식이 변경되면 `c2pa.resized` 및 `c2pa.transcoded`입니다. |
| **[!UICONTROL EPS 썸네일(ImageMagick 제공)]** | 기본 출력, 파생된 썸네일 및 웹 표현물. | `c2pa.resized`, `c2pa.transcoded` 또는 `c2pa.edited` |
| **[!UICONTROL FFmpeg 썸네일]** | 비디오 포스터 프레임 및 축소판 | `c2pa.resized` 및 `c2pa.transcoded` |
| **[!UICONTROL FFmpeg 코드 변환]** | 비디오 인코딩. | `c2pa.transcoded` |
| **[!UICONTROL PDF/AI 이미지 미리 보기 렌디션 래스터화]** | 렌디션 미리 보기. (`cqdam.preview.png`) | `c2pa.transcoded` |

다음 워크플로우 프로세스는 **[!UICONTROL DAM 자산 업데이트 워크플로우 완료]** 워크플로우, 다른 워크플로우 또는 사용자 지정 워크플로우 모델에서 이 프로세스를 사용할 때 출력에 서명합니다. [C2PA 메타데이터 감지](#detect)와 같이 워크플로 단계의 **[!UICONTROL 축소판 처리]** 목록에서 축소판을 선택하십시오.

| 워크플로우 프로세스 | 렌디션 서명됨 | C2PA 작업 기록됨 |
|---|---|---|
| **[!UICONTROL 축소판 만들기]** | 축소판 표현물. | 형식이 변경되면 `c2pa.resized` 및 `c2pa.transcoded`입니다. |
| **[!UICONTROL 웹 사용 이미지 만들기]** | 웹 표현물. | 형식이 변경되면 `c2pa.resized` 및 `c2pa.transcoded`입니다. |
| **[!UICONTROL 명령줄]**(예: [!DNL ImageMagick] 포함) | 기본 출력, 파생된 썸네일 및 웹 표현물. | `c2pa.resized`, `c2pa.transcoded` 또는 `c2pa.edited` |
| **[!UICONTROL 이미지 워터마크 프로세스]** | 워터마크가 지정된 렌디션 또는 워터마크가 적용될 때의 원본 렌디션입니다. 자세한 내용은 [자산을 워터마크 지정](/help/assets/watermarking.md)을 참조하십시오. | `c2pa.edited` |
| **[!UICONTROL 비디오 스토리보드 만들기]** | 스토리보드 키 프레임. | `c2pa.transcoded` |
| **[!UICONTROL XMP 원본에 쓰기]** | 메타데이터가 다시 작성된 후의 원본 렌디션입니다. 자세한 내용은 [변환에 대한 XMP 원본에 쓰기](/help/assets/xmp-writeback.md)를 참조하십시오. | `c2pa.edited` |

### XMP 원본에 쓰기 저장(writeback) 중에 원본 이진 파일 보호 {#xmp-writeback}

XMP 원본에 쓰기 기능은 포함된 매니페스트를 깨뜨리는 원본 바이너리를 다시 작성합니다. `dam:hasC2PAManifest`이(가) `true`(으)로 설정된 자산의 경우 [!DNL Experience Manager]은(는) **[!UICONTROL DAM 메타데이터 원본에 쓰기]** 워크플로의 **[!UICONTROL XMP 원본에 쓰기 프로세스]** 단계의 동작을 다음과 같이 변경합니다.

* **일반 AI 자산**(`dam:isAiGenerated`은(는) `true`임): [!DNL Experience Manager]이(가) XMP을 쓴 다음 원본에 다시 쓰기 전 바이너리를 상위로 사용하여 원본 바이너리에 다시 서명합니다. 쓰기 저장과 새 서명을 함께 저장합니다. 재서명이 실패하면 두 단계를 모두 삭제하고 실패합니다.
* **매니페스트를 포함하는 다른 자산**: [!DNL Experience Manager]이(가) XMP 원본에 쓰기 작업을 건너뛰고 이유를 기록합니다. 원본 이진과 매니페스트는 변경되지 않습니다.

### 서명 모드 {#signing-mode}

[!DNL Experience Manager]은(는) 렌디션을 생성하는 인스턴스에서 자체 생성한 임시 자체 서명된 인증서를 사용하여 렌디션에 로컬로 서명합니다. 서명에는 네트워크 액세스가 필요하지 않으며 인증서 또는 개인 키 구성이 필요하지 않습니다.

>[!NOTE]
>
>고유한 서명 인증서를 구성할 수 없습니다. [확인](https://contentcredentials.org/verify)과 같은 유효성 검사기는 표현물의 Gen AI 공개 및 원본에 대한 링크를 보여주지만 조직을 서명자로 식별하지는 않습니다.

## C2PA 메타데이터 구성 {#configure}

C2PA 메타데이터 지원은 기본적으로 활성화되어 있습니다. 설치하거나 구성할 필요가 없습니다.

### OSGi 구성 {#osgi-configuration}

기본 구성을 변경하려면 아래 그림과 같이 구성 관리자에서 **[!UICONTROL 일 CQ DAM C2PA 서비스]**(PID `com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl`)를 `https://[aem_server]:[port]/system/console/configMgr`에 구성하거나 프로젝트에 OSGi 구성을 추가합니다. 자세한 내용은 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오.

![OSGi 구성](assets/OSGi.png)

아래 표에는 프로젝트의 OSGi 구성 속성이 나와 있습니다.

| 속성 | 구성 관리자의 이름 | 기본값 | 설명 |
|---|---|---|---|
| `enabled` | **[!UICONTROL 사용]** | `true` | C2PA 메타데이터 지원을 켜거나 끕니다. [!DNL Experience Manager]을(를) 해제하면 매니페스트가 검색되지 않고 렌디션에 서명되지 않습니다. |
| `timeoutMillis` | **[!UICONTROL CLI 시간 초과(ms)]** | `30000` | [!DNL Experience Manager]이(가) 시간 초과로 처리되기 전에 파일에서 단일 읽기 또는 서명 작업을 기다리는 최대 시간(밀리초)을 지정합니다. 큰 비디오 또는 고해상도 이미지 파일에 대해 이 값을 높입니다. |

예를 들어 `/apps/<your-project>/config/com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl.config`에서 OSGi 구성을 추가합니다.

```text
enabled=B"true"
timeoutMillis=L"60000"
```

### C2PA 메타데이터 지원 해제 {#disable}

[OSGi 구성](#osgi-configuration)에 표시된 **[!UICONTROL 일 CQ DAM C2PA 서비스]** 구성에서 **[!UICONTROL 활성화됨]** 옵션을 비활성화한 다음 변경 사항을 저장합니다. 변경 사항은 재시작 없이 즉시 적용됩니다.

* [C2PA 메타데이터 검색](#detect)에 표시된 **[!UICONTROL C2PA 자격 증명 검색]** 단계가 작동하지 않습니다.
* 워크플로 단계는 서명하지 않고 렌디션을 만듭니다.
* 이전에 처리된 Assets은 `dam:hasC2PAManifest` 속성을 유지하고 **cr** 배지를 표시합니다.

>[!CAUTION]
>
>**[!UICONTROL 사용]** 옵션을 사용하지 않도록 설정한 후에는 일반 AI 에셋 렌디션에 C2PA 메타데이터가 없습니다. 일반 AI 공개 규정을 준수하려면 **[!UICONTROL 사용]** 옵션을 활성화하십시오.

## 처리 파이프라인 사용자 정의 {#customize}

**[!UICONTROL DAM 자산 업데이트]**&#x200B;에서 단계를 추가, 제거 또는 순서를 변경하고 Gen AI 공개를 그대로 유지하려면 다음 규칙을 따르십시오.

* **먼저 검색 실행.** 렌디션을 만들거나 수정하는 모든 단계를 **[!UICONTROL C2PA 자격 증명 감지]**&#x200B;를 먼저 하세요.
* **마지막으로 서명** 서명 후 바이너리를 변경하면 서명이 무효화됩니다. 렌디션에 서명한 단계 후에는 렌디션을 수정하는 단계를 실행하지 마십시오.
* **서명하는 단계를 사용합니다.** [렌디션 서명](#sign-renditions)에 나열된 기본 제공 단계는 출력에 서명합니다. **[!UICONTROL 명령줄]** 프로세스 이외의 다른 프로세스를 통해 실행하는 사용자 지정 단계 및 타사 도구는 서명을 명시적으로 추가하지 않는 한 해당 출력에 서명하지 않습니다. 자세한 내용은 [미디어 핸들러 및 워크플로우를 사용하여 에셋 처리](/help/assets/media-handlers.md)를 참조하십시오.
* **[!UICONTROL XMP 원본에 쓰기]** 및 **[!UICONTROL 이미지 워터마킹 프로세스]**&#x200B;와 같이 단계를 다시 서명하지 않는 한 **원본을 제대로 수정하지 마십시오**.

### 사용자 지정 워크플로 단계에서 렌디션에 서명 {#custom-step}

렌디션을 생성하는 사용자 지정 워크플로 단계는 `com.day.cq.dam.api.c2pa.C2PASigner` OSGi 서비스를 통해 서명할 수 있습니다. 기본 제공 단계와 동일한 자격 규칙을 적용하지만 대신 결과를 `C2PASigningOutcome`(으)로 보고합니다.

```java
import java.util.Collections;

import org.osgi.service.component.annotations.Reference;
import org.osgi.service.component.annotations.ReferenceCardinality;
import org.osgi.service.component.annotations.ReferencePolicy;

import com.day.cq.dam.api.Asset;
import com.day.cq.dam.api.Rendition;
import com.day.cq.dam.api.c2pa.C2PAAction;
import com.day.cq.dam.api.c2pa.C2PAConstants;
import com.day.cq.dam.api.c2pa.C2PASigner;
import com.day.cq.dam.api.c2pa.C2PASigningOutcome;

// Inside your WorkflowProcess implementation:

@Reference(cardinality = ReferenceCardinality.OPTIONAL, policy = ReferencePolicy.DYNAMIC)
private volatile C2PASigner c2paSigner;

private void signRendition(Asset asset, Rendition rendition) {
    C2PASigner signer = c2paSigner;
    if (signer == null) {
        return;
    }
    C2PASigningOutcome outcome = signer.signIfEligible(asset, rendition,
            Collections.singletonList(
                    new C2PAAction(C2PAConstants.ACTION_RESIZED, C2PAConstants.SOFTWARE_AGENT, null)));
    if (outcome == C2PASigningOutcome.FAILED) {
        // Log, retry, or alert an operator.
    }
}
```

단계 변환이 완료된 후에만 `signIfEligible`을(를) 호출합니다. OSGi 서비스는 아래 표에 나열된 메서드를 제공합니다.

| 메서드 | 사용 대상 |
|---|---|
| `signIfEligible(Asset, Rendition, List<C2PAAction>)` | 소스 자산을 상위로 하여 새 렌디션에 서명합니다. |
| `signIfEligible(Asset, Map<Rendition, List<C2PAAction>>)` | 동일한 에셋에서 파생된 여러 렌디션에 서명합니다. 이 메서드는 소스 매니페스트를 한 번 읽습니다. |
| `captureResignState(Asset)` | 단계에서 원본 에셋을 수정하기 전에 원본 에셋의 이미지를 가져옵니다. 이 메서드는 자산이 적격하지 않은 경우 `null`을(를) 반환합니다. |
| `resign(Asset, Rendition, List<C2PAAction>)` | 즉석 변경 후 이미지를 상위로 하여 원본 에셋에 다시 서명합니다. |
| `discardResignState(Rendition)` | 예를 들어, 변경하지 못했기 때문에 사용할 수 없지만 찍은 이미지를 배치합니다. |

`C2PASigningOutcome`의 값은 아래 표에 나와 있습니다.

| 결과 | 설명 |
|---|---|
| `SIGNED` | [!DNL Experience Manager] 님이 변환에 서명했습니다. |
| `SKIPPED_SOURCE_NOT_AI_GENERATED` | 소스 에셋은 AI가 생성한 에셋으로 플래그가 지정되지 않습니다. |
| `SKIPPED_FORMAT_NOT_ELIGIBLE` | 렌디션 형식이 포함된 C2PA 매니페스트를 지원하지 않습니다. |
| `SKIPPED_MANIFEST_UNREADABLE` | [!DNL Experience Manager]이(가) 원본 에셋에서 매니페스트를 찾을 수 없습니다. |
| `SKIPPED_MANIFEST_NOT_VALID` | 소스 매니페스트의 유효성을 검사하지 못했습니다. |
| `SKIPPED_SERVICE_UNAVAILABLE` | C2PA 메타데이터 지원이 꺼져 있거나 사용할 수 없습니다. |
| `FAILED` | 소스 매니페스트를 읽거나 렌디션에 서명하지 못했습니다. |

고가의 렌디션을 생성하기 전에 자격 조건을 확인하려면 `C2PASupportedFormats.isEligible(...)`을(를) 호출하십시오.

## 문제 해결 {#troubleshooting}

문제를 해결할 때 **[!UICONTROL Apache Sling Logger 구성]**&#x200B;에서 다음 로거를 `DEBUG`(으)로 설정하십시오.

* `com.day.cq.dam.core.impl.c2pa`: 기본 C2PA 구성 요소 추출, 매니페스트 읽기 및 서명
* `com.day.cq.dam.core.process.DetectC2PACredentialProcess`: 검색.

| 증상 | 가능한 원인 | 해결 방법 |
|---|---|---|
| **cr** 배지를 표시하는 자산이 없습니다. | C2PA 메타데이터 지원이 꺼져 있거나 워크플로우 모델에 검색 단계가 포함되어 있지 않습니다. | **[!UICONTROL Enabled]**&#x200B;이(가) **[!UICONTROL 일 CQ DAM C2PA 서비스]** 구성에 활성화되어 있고 **[!UICONTROL DAM 자산 업데이트]** 모델에 **[!UICONTROL C2PA 자격 증명 감지]**&#x200B;가 포함되어 있는지 확인하십시오. |
| 알고 있는 자산에는 매니페스트가 있지만 배지가 없습니다. | 기능을 사용하기 전에 에셋이 업로드되었습니다. | 에셋에서 **[!UICONTROL DAM 에셋 업데이트]** 워크플로우를 다시 실행합니다(예: **[!UICONTROL 타임라인]** > **[!UICONTROL 워크플로우 시작]**). |
| 서비스가 시작되지 않습니다. 오류 로그에서 `adobe_c2patool`을(를) 실행 파일로 추출 또는 표시할 수 없다고 보고합니다. | 운영 체제 또는 아키텍처에 대한 바이너리가 없거나 파일 시스템이 실행 파일을 차단합니다. | 지원되는 플랫폼을 사용합니다. [!DNL Experience Manager] 프로세스에서 해당 `crx-quickstart` 폴더의 실행 파일을 실행할 수 있도록 허용합니다. |
| 오류 로그가 `GLIBC_2.xx not found`을(를) 보고합니다. | Linux 호스트는 2.28 이전 버전의 glibc를 실행합니다. | 호스트 운영 체제를 업그레이드합니다. |
| 감지 또는 서명 시간이 초과되었습니다. | 큰 파일은 기본 시간 제한인 30초보다 오래 걸립니다. | **[!UICONTROL CLI 시간 초과(ms)]**&#x200B;를 발생시킵니다. |
| Gen AI 에셋의 렌디션은 서명되지 않습니다. | 형식이 지원되지 않거나, 매니페스트가 `INVALID`이거나, 렌디션 단계 후 검색이 실행되었습니다. | `dam:c2paValidationState` 및 렌디션 형식을 확인하십시오. 렌디션 단계 이전에 **[!UICONTROL C2PA 자격 증명 감지]**&#x200B;를 이동하십시오. |
| XMP 원본에 쓰기 는 자산을 업데이트하지 않습니다. | 에셋이 매니페스트를 전달하지만 AI를 통해 생성되지 않으므로 [!DNL Experience Manager]이(가) 원본 에셋을 변경하지 않고 유지합니다. | 이는 예상되는 비헤이비어입니다. 자세한 내용은 [XMP 원본에 쓰기 저장 중 원본 보호](#xmp-writeback)를 참조하십시오. |

## 제한 사항 {#limitations}

* [!DNL Assets] 사용자 인터페이스에서는 C2PA 메타데이터가 있는지 여부만 표시합니다. 매니페스트 세부 정보에 대한 패널이 없습니다.
* [!DNL Experience Manager] AI를 통해 생성된 자산에 대해서만 렌디션에 다시 서명합니다. 매니페스트를 전달하는 다른 에셋의 렌디션은 C2PA 메타데이터 없이 만들어집니다.
* [!DNL Experience Manager]이(가) 자동 서명된 임시 인증서를 사용하여 서명합니다. 사용자 지정 또는 조직 특정 서명 인증서는 지원되지 않습니다.


>[!MORELIKETHIS]
>
>*  [!DNL Experience Manager as a Cloud Service]&#x200B;[&#128279;](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/assets-view/c2pa-metadata-assets-view)의 Assets 보기에서 C2PA 메타데이터
>* [C2PA 메타데이터 위치 [!DNL Experience Manager Assets Essentials]](https://experienceleague.adobe.com/ko/docs/experience-manager-assets-essentials/help/content-credentials)
>* [C2PA 메타데이터 위치 [!DNL Dynamic Media]](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/c2pa-metadata)
>* [변환에 대한 XMP 원본에 쓰기](/help/assets/xmp-writeback.md)
>* [자산을 워터마크 지정](/help/assets/watermarking.md)
>* [Content Authenticity Initiative](https://contentauthenticity.org/)
>* [확인](https://contentcredentials.org/verify)
