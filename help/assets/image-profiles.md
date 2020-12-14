---
title: Dynamic Media 이미지 프로필
description: 언샵 마스크, 스마트 자르기 또는 스마트 견본 또는 두 가지 모두에 대한 설정이 포함된 이미지 프로필을 만든 다음 이미지 에셋 폴더에 프로필을 적용합니다.
uuid: 9049fab9-d2be-4118-8684-ce58f3c8c16a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 4f9301db-edf8-480b-886c-b5e8fca5bf5c
translation-type: tm+mt
source-git-commit: 10dae6e9f49e93d2f4923cee754c1d23d9d4b25e
workflow-type: tm+mt
source-wordcount: '2760'
ht-degree: 4%

---


# Dynamic Media 이미지 프로필 {#image-profiles}

이미지를 업로드할 때 폴더에 이미지 프로필을 적용하여 업로드 시 이미지를 자동으로 자를 수 있습니다.

>[!NOTE]
>
>스마트 자르기는 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.

>[!IMPORTANT]
>
>이미지 프로필은 PDF, 애니메이션 GIF 또는 INDD(Adobe InDesign) 파일에는 적용되지 않습니다.

## 자르기 옵션 {#crop-options}

<!-- CQDOC-16069 for paragraph directly below -->

스마트 자르기 좌표는 종횡비에 따라 다릅니다. 즉, 이미지 프로필의 다양한 스마트 자르기 설정의 경우 종횡비가 이미지 프로필의 추가된 크기에 대해 동일하면 동일한 종횡비가 다이내믹 미디어로 전송됩니다. 이로 인해 Adobe에서는 동일한 자르기 영역을 사용하는 것이 좋습니다. 이렇게 하면 이미지 프로필에 사용된 다른 차원에 영향을 주지 않습니다.

생성하는 각 스마트 자르기 생성에는 추가 처리가 필요합니다. 예를 들어 5개 이상의 스마트 자르기 종횡비를 추가하면 자산 처리 속도가 느려질 수 있습니다. 또한 시스템에서 로드가 증가할 수 있습니다. 폴더 수준에서 스마트 자르기를 적용할 수 있으므로 Adobe은 필요한 폴더 *에만*&#x200B;을(를) 사용할 것을 권장합니다.

선택할 수 있는 이미지 자르기 옵션이 2개 있습니다. 또한 색상 및 이미지 견본 생성을 자동화하는 옵션이 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>옵션</strong></td>
   <td><strong>사용 시기</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>픽셀 자르기</td>
   <td>차원만을 기준으로 이미지를 벌크 잘라냅니다.</td>
   <td><p>이 옵션을 사용하려면 [자르기 옵션] 드롭다운 목록에서 <strong>픽셀 자르기</strong>를 선택합니다.</p> <p>이미지의 양쪽에서 자르려면 이미지의 측면 또는 양쪽에서 자를 픽셀 수를 입력합니다. 이미지 파일의 ppi(인치당 픽셀 수) 설정에 따라 이미지의 크기가 잘립니다.</p> <p>이미지 프로필 픽셀 자르기는 다음 방식으로 렌더링됩니다.<br /> </p>
    <ul>
     <li>값은 위쪽, 아래쪽, 왼쪽 및 오른쪽입니다.</li>
     <li>왼쪽 상단은 0,0으로 간주되며 픽셀 자르기는 여기에서 계산됩니다.</li>
     <li>자르기 시작 지점:왼쪽은 X이고 위쪽은 Y</li>
     <li>수평 계산:원본 이미지의 가로 픽셀 치수에서 [왼쪽]을 뺀 다음 [오른쪽]을 뺀 것입니다.</li>
     <li>수직 계산:세로 픽셀 높이를 위쪽에서 마이너스(-)한 다음, 아래쪽을 마이너스(-)합니다.</li>
    </ul> <p>예를 들어 4000 x 3000픽셀 이미지를 가지고 있다고 가정합니다. 값을 사용합니다.위쪽=250, 아래쪽=500, 왼쪽=300, 오른쪽=700.</p> <p>왼쪽 위(300,250)에서 (4000-300-700, 3000-250-500 또는 3000,2250)의 칠 공간을 사용하여 자릅니다.</p> </td>
  </tr>
  <tr>
   <td>스마트 자르기</td>
   <td>시각적 초점에 따라 이미지를 대량으로 자릅니다.</td>
   <td><p>스마트 자르기는 Adobe Sensei의 강력한 인공 지능을 사용하여 일괄 이미지 자르기를 신속하게 자동화합니다. 스마트 자르기는 화면 크기와 상관없이 원하는 관심 영역을 캡처하기 위해 이미지의 초점을 자동으로 감지하고 잘라냅니다.</p> <p>스마트 자르기를 사용하려면 자르기 옵션 드롭다운 목록에서 <strong>스마트 자르기</strong>를 선택한 다음 응답형 이미지 자르기 오른쪽에 있는 기능을 활성화(켜기)합니다.</p> <p>[큰], [보통] 및 [작은]의 기본 중단점 크기는 일반적으로 대부분의 이미지가 모바일 및 태블릿 장치, 데스크톱 및 배너에서 사용되는 전체 크기 범위를 포함합니다. 원하는 경우 [큰], [보통] 및 [작은]의 기본 이름을 편집할 수 있습니다.</p> <p>중단점을 더 추가하려면 <strong>자르기 추가</strong>;자르기를 삭제하려면 [휴지통] 아이콘을 클릭합니다.</p> </td>
  </tr>
  <tr>
   <td>색상 및 이미지 견본</td>
   <td>각 이미지에 대한 이미지 견본을 일괄 생성합니다.</td>
   <td><p><strong>참고</strong>:스마트 견본은 Dynamic Media Classic에서 지원되지 않습니다.</p> <p>색상 또는 텍스처를 보여주는 제품 이미지에서 고품질 색상 견본을 자동으로 찾아 생성할 수 있습니다.</p> <p>색상 및 이미지 견본을 사용하려면 자르기 옵션 드롭다운 목록에서 <strong>스마트 자르기</strong>를 선택한 다음 색상 및 이미지 견본 오른쪽에 있는 기능을 활성화(켜기)합니다. [폭] 및 [높이] 텍스트 상자에 픽셀 값을 입력합니다.</p> <p>모든 이미지 자르기는 [변환] 레일에서 사용할 수 있지만 견본은 URL 복사 기능을 통해서만 사용됩니다. 고유한 보기 구성 요소를 사용하여 사이트의 견본을 렌더링해야 합니다. 캐러셀 배너는 예외입니다. Dynamic Media은 캐러셀 배너에 사용된 견본에 대한 보기 구성 요소를 제공합니다.)</p> <p><strong>이미지 견본 사용</strong></p> <p>이미지 색상 견본의 URL은 간단합니다. 이것은 다음과 같습니다.</p> <p><code>/is/image/company/&lt;asset_name&gt;:Swatch</code></p> <p>여기서 <code>:Swatch</code>은(는) 자산 요청에 추가됩니다.</p> <p><strong>색상 견본 사용</strong></p> <p>색상 견본을 사용하려면 다음을 사용하여 <code>req=userdata</code> 요청을 수행합니다.</p> <p><code>/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata</code></p> <p>예를 들어 다음은 Dynamic Media Classic의 견본 에셋입니다.</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch</code></p> <p>견본 에셋의 해당 <code>req=userdata</code> URL은 다음과 같습니다.</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata</code></p> <p><code>req=userdata</code> 응답은 다음과 같습니다.</p> <p><code class="code">SmartCropDef=Swatch
       SmartCropHeight=200.0
       SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200
       SmartCropType=Swatch
       SmartCropWidth=200.0
       SmartSwatchColor=0xA56DB2</code></p> <p>다음 각 URL 예제와 같이 XML 또는 JSON 형식으로 <code>req=userdata</code> 응답을 요청할 수도 있습니다.</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml</code></p><p><code>SmartSwatchColor</code></p><p></p></td></tr></tbody></table>

## 언샵 마스크 {#unsharp-mask}

**[!UICONTROL 언샵 마스크]**&#x200B;를 사용하여 최종 다운샘플링된 이미지에 대해 선명하게 하기 필터 효과를 미세 조정합니다. 효과의 강도, 효과의 반경(픽셀 단위로 측정됨) 및 무시될 대비 임계값을 제어할 수 있습니다. 이 효과는 Adobe Photoshop의 &quot;언샵 마스크&quot; 필터와 동일한 옵션을 사용합니다.

>[!NOTE]
>
>언샵 마스크는 50% 이상 다운샘플링된 PTIFF(피라미드형 tiff) 내의 축소된 변환에만 적용됩니다. 즉, 축소판과 같은 작은 크기의 변환이 변경되고 언샵 마스크가 표시되는 반면, PTIFF 내에서 가장 큰 크기의 변환은 언샵 마스크의 영향을 받지 않습니다.

**[!UICONTROL 언샵 마스크]**&#x200B;에는 다음 필터링 옵션이 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>옵션</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>양</td>
   <td>가장자리 픽셀에 적용된 대비 양을 제어합니다. 기본값은 1.75입니다. 고해상도 이미지의 경우 최대 5까지 늘릴 수 있습니다. 양을 필터 강도 측정으로 생각해 보십시오. 범위는 0-5입니다.</td>
  </tr>
  <tr>
   <td>반경</td>
   <td>선명하게 하기가 적용되는 가장자리 픽셀 주위의 픽셀 수를 결정합니다. 고대비 이미지의 경우 1~2를 입력합니다. 작은 값은 가장자리 픽셀만 선명하게 하고 큰 값은 넓은 폭의 픽셀을 선명하게 합니다. 정확한 값은 이미지의 크기에 따라 다릅니다. 기본값은 0.2입니다. 범위는 0-250입니다.</td>
  </tr>
  <tr>
   <td>임계값</td>
   <td><p>언샵 마스크 필터를 적용할 때 무시할 대비 범위를 결정합니다.즉, 이 옵션은 가장자리 픽셀로 간주하여 선명하게 하기 전에 선명하게 된 픽셀이 주위 영역과 얼마나 달라야 하는지를 결정합니다. 노이즈를 표시하지 않으려면 0-255 사이의 값을 실험해 봅니다.</p> </td>
  </tr>
 </tbody>
</table>

선명하게 하기는 [이미지 선명하게 하기](/help/assets/assets/s7_sharpening_images.pdf)에 설명되어 있습니다.

## Dynamic Media 이미지 프로필 만들기 {#creating-image-profiles}

다른 자산 유형에 대한 고급 처리 매개 변수를 정의하려면 [자산 처리 구성](config-dms7.md#configuring-asset-processing)을 참조하십시오.

메타데이터, 이미지 및 비디오 처리를 위한 프로필[을 참조하십시오.](processing-profiles.md)

처리 프로필 사용[에 대한 디지털 자산 구성을 위한 우수 사례를 참조하십시오.](/help/assets/organize-assets.md)

**Dynamic Media 이미지 프로필을 만들려면**

1. AEM 로고를 누르고 **[!UICONTROL 도구 > 자산 > 이미지 프로필로 이동합니다.]**
1. **[!UICONTROL 만들기]**&#x200B;를 눌러 새 이미지 프로필을 추가합니다.
1. 프로파일 이름과 언샵 마스크, 자르기 또는 견본 또는 둘 다에 대한 값을 입력합니다.

   의도한 목적에 맞는 프로필 이름을 사용하는 것이 도움이 될 수 있습니다. 예를 들어 견본만 생성하는 프로파일을 만들려면(즉, 스마트 자르기가 비활성화(꺼짐)되고 색상 및 이미지 견본이 활성화(켜짐)되면 프로파일 이름 &quot;스마트 견본&quot;을 사용할 수 있습니다.

   [스마트 자르기 및 스마트 견본 옵션](#crop-options) 및 [언샵 마스크](#unsharp-mask)도 참조하십시오.

   ![자르기](assets/crop.png)

1. **[!UICONTROL 저장을 누릅니다.]** 새로 만든 프로필이 사용 가능한 프로필 목록에 나타납니다.

## Dynamic Media 이미지 프로필 편집 또는 삭제 {#editing-or-deleting-image-profiles}

1. AEM 로고를 누르고 **[!UICONTROL 도구 > 자산 > 이미지 프로필로 이동합니다.]**
1. 편집하거나 제거할 이미지 프로필을 선택합니다. 편집하려면 **[!UICONTROL 이미지 처리 프로필 편집을 선택합니다.]** 제거하려면 [이미지 처리 프로필  **[!UICONTROL 삭제]를 선택합니다.]**

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 편집하는 경우 변경 내용을 저장합니다. 삭제하는 경우 프로필을 제거할 것인지 확인합니다.

## 폴더 {#applying-an-image-profile-to-folders}에 Dynamic Media 이미지 프로필 적용

이미지 프로필을 폴더에 할당하면 모든 하위 폴더는 해당 상위 폴더의 프로필을 자동으로 상속합니다. 즉, 하나의 이미지 프로필만 폴더에 할당할 수 있습니다. 따라서 에셋을 업로드, 저장, 사용 및 보관하는 폴더 구조를 주의 깊게 고려합니다.

폴더에 다른 이미지 프로필을 할당하면 새 프로필이 이전 프로필을 무시합니다. 이전 기존 폴더 자산은 변경되지 않습니다. 새 프로필이 나중에 폴더에 추가되는 자산에 적용됩니다.

프로필이 할당된 폴더는 카드에 나타나는 프로필의 이름으로 사용자 인터페이스에 표시됩니다.

<!-- When you add smart crop to an existing image profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

특정 폴더에 이미지 프로필을 적용하거나 모든 자산에 전체적으로 적용할 수 있습니다.

나중에 변경한 기존 이미지 프로필이 이미 있는 폴더의 에셋을 다시 처리할 수 있습니다. [폴더의 자산에 대한 처리 프로필을 편집한 후 재처리](processing-profiles.md#reprocessing-assets)를 참조하십시오.

### 특정 폴더 {#applying-image-profiles-to-specific-folders}에 Dynamic Media 이미지 프로필 적용

**[!UICONTROL 도구]** 메뉴 내에서 또는 폴더에 있는 경우 **[!UICONTROL 속성에서 이미지 프로필을 폴더에 적용할 수 있습니다.]** 이 섹션에서는 두 가지 방법으로 폴더에 이미지 프로필을 적용하는 방법을 설명합니다.

프로파일이 이미 할당된 폴더가 폴더 이름 바로 아래에 프로파일 이름이 표시되어 표시됩니다.

나중에 변경한 기존 비디오 프로필이 이미 있는 폴더의 에셋을 다시 처리할 수 있습니다. [폴더의 자산에 대한 처리 프로필을 편집한 후 재처리](processing-profiles.md#reprocessing-assets)를 참조하십시오.

#### 프로필 사용자 인터페이스 {#applying-image-profiles-to-folders-from-profiles-user-interface}의 폴더에 Dynamic Media 이미지 프로필 적용

1. AEM 로고를 누르고 **[!UICONTROL 도구 > 자산 > 이미지 프로필로 이동합니다.]**
1. 폴더 또는 여러 폴더에 적용할 이미지 프로필을 선택합니다.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. **[!UICONTROL 폴더에 처리 프로필 적용]**&#x200B;을 누르고 새로 업로드된 자산을 받는 데 사용할 폴더 또는 여러 폴더를 선택하고 **[!UICONTROL 적용을 탭/클릭합니다.]** 프로파일이 이미 할당된 폴더가 폴더 이름 바로 아래에 프로파일 이름이 표시되어 표시됩니다.

#### 속성 {#applying-image-profiles-to-folders-from-properties}의 폴더에 Dynamic Media 이미지 프로필 적용

1. AEM 로고를 누르고 **[!UICONTROL 자산]**&#x200B;으로 이동한 다음 이미지 프로필을 적용할 폴더로 이동합니다.
1. 폴더에서 확인 표시를 눌러 선택한 다음 **[!UICONTROL 속성을 누릅니다.]**
1. **[!UICONTROL 이미지 프로필]** 탭을 누릅니다. **[!UICONTROL 프로필 이름]** 드롭다운 목록에서 프로필을 선택한 다음 **[!UICONTROL 저장 및 닫기를 탭합니다.]** 프로파일이 이미 할당된 폴더가 폴더 이름 바로 아래에 프로파일 이름이 표시되어 표시됩니다.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Dynamic Media 이미지 프로필을 전역적으로 적용 {#applying-an-image-profile-globally}

프로필을 폴더에 적용하는 것 외에도 하나의 프로필을 전역적으로 적용할 수 있으므로 모든 폴더의 AEM 자산에 업로드된 콘텐트에 선택한 프로필이 적용되도록 할 수 있습니다.

나중에 변경한 기존 비디오 프로필이 이미 있는 폴더의 에셋을 다시 처리할 수 있습니다. [폴더의 자산에 대한 처리 프로필을 편집한 후 재처리](processing-profiles.md#reprocessing-assets)를 참조하십시오.

**Dynamic Media 이미지 프로필을 전체적으로 적용하려면 다음을 수행하십시오**.

1. 다음 중 하나를 수행하십시오.

   * `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam`으로 이동하여 적절한 프로필을 적용하고 **[!UICONTROL 저장을 탭합니다.]**

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * 다음 노드로 CRXDE Lite으로 이동합니다.`/content/dam/jcr:content`.

      `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` 속성을 추가하고 **[!UICONTROL 모두 저장을 탭합니다.]**

      ![configure_image_profiles](assets/configure_image_profiles.png)

## 단일 이미지 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}의 스마트 자르기 또는 스마트 견본 편집

>[!NOTE]
>
>스마트 자르기는 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.

이미지의 스마트 자르기 창을 수동으로 재정렬하거나 크기를 조정하여 초점을 세부적으로 조정할 수 있습니다.

스마트 자르기를 편집하고 저장하면 특정 이미지의 자르기를 사용하는 모든 영역에 변경 내용이 전파됩니다.

필요한 경우 스마트 자르기를 다시 실행하여 추가 자르기를 다시 생성할 수 있습니다.

자세한 내용은 [여러 이미지의 스마트 자르기 또는 스마트 견본 편집](#editing-the-smart-crop-or-smart-swatch-of-multiple-images)을 참조하십시오.

**단일 이미지의 스마트 자르기 또는 스마트 견본을 편집하려면 다음을 수행하십시오**.

1. AEM 로고를 누르고 **[!UICONTROL 자산]**&#x200B;으로 이동한 다음 스마트 자르기 또는 스마트 견본 이미지 프로필이 적용된 폴더로 이동합니다.

1. 폴더를 눌러 컨텐츠를 엽니다.
1. 조정할 스마트 자르기 또는 스마트 견본의 이미지를 누릅니다.
1. 도구 모음에서 **[!UICONTROL 스마트 자르기]**&#x200B;를 누릅니다.

1. 다음 중 하나를 수행합니다.

   * 페이지의 오른쪽 위 모서리 근처에 있는 슬라이더 막대를 왼쪽이나 오른쪽으로 드래그하여 이미지 표시를 각각 늘리거나 줄입니다.
   * 이미지에서 모서리 핸들을 드래그하여 자르기 또는 견본의 보기 가능한 영역의 크기를 조정합니다.
   * 이미지에서 상자/견본을 새 위치로 드래그합니다. 이미지 견본만 편집할 수 있습니다.색상 견본은 정적입니다.
   * 이미지 위에 있는 **[!UICONTROL 되돌리기]**&#x200B;를 눌러 모든 편집 내용을 실행 취소하고 원래 자르기나 견본을 복원합니다.

1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 저장]**&#x200B;을 탭한 다음 **[!UICONTROL 닫기]**&#x200B;를 탭하여 자산 폴더로 돌아갑니다.

## 여러 이미지의 스마트 자르기 또는 스마트 견본 편집 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

스마트 자르기를 포함하는 이미지 프로필을 폴더에 적용하면 해당 폴더의 모든 이미지에 자르기가 적용됩니다. 원하는 경우 여러 이미지의 스마트 자르기 창을 수동으로 *다시 정렬하거나 크기를 조정하여 초점을 더 세분화할 수 있습니다.*

스마트 자르기를 편집하고 저장하면 특정 이미지의 자르기를 사용하는 모든 영역에 변경 내용이 전파됩니다.

필요한 경우 스마트 자르기를 다시 실행하여 추가 자르기를 다시 생성할 수 있습니다.

**여러 이미지의 스마트 자르기 또는 스마트 견본을 편집하려면 다음을 수행하십시오**.

1. AEM 로고를 누르고 **[!UICONTROL 자산]**&#x200B;으로 이동한 다음 스마트 자르기 또는 스마트 견본 이미지 프로필이 적용된 폴더로 이동합니다.
1. 폴더에서 **[!UICONTROL 추가 작업]**(...) 아이콘을 누른 다음 **[!UICONTROL 스마트 자르기.]**

1. **[!UICONTROL 스마트 자르기 편집]** 페이지에서 다음 중 하나를 수행합니다.

   * 페이지에서 이미지의 보기 크기를 조정합니다.

      중단점 이름 드롭다운 목록 오른쪽에 있는 슬라이더 막대를 왼쪽 또는 오른쪽으로 드래그하여 볼 수 있는 이미지 표시 크기를 변경합니다.

      ![edit_smart_crops-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 중단점 이름을 기준으로 볼 수 있는 이미지 목록을 필터링합니다. 아래 예에서, 이미지는 중단점 이름 &quot;보통&quot;에 대해 필터링됩니다.

      페이지의 오른쪽 위 모서리 근처에 있는 드롭다운 목록에서 표시되는 이미지를 필터링할 중단점 이름을 선택합니다. (위의 이미지를 참조하십시오.)

      ![edit_smart_crops-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 스마트 자르기 상자의 크기를 조정합니다. 다음 중 하나를 수행합니다.

      * 이미지에 스마트 자르기 또는 스마트 색상 견본만 있는 경우 자르기 상자의 모퉁이 핸들을 드래그하여 자르기의 표시 가능한 영역의 크기를 조정합니다.
      * 이미지에 스마트 자르기 및 스마트 색상 견본이 모두 있는 경우 자르기 상자의 모퉁이 핸들을 드래그하여 자르기의 보기 가능한 영역의 크기를 조정합니다. 또는 이미지 아래에 있는 스마트 견본(색상 견본은 정적임)을 탭하거나 클릭한 다음 자르기 상자의 모퉁이 핸들을 드래그하여 견본의 표시 가능한 영역의 크기를 조정합니다.

      ![이미지의 스마트 자르기 크기 조정](assets/edit_smart_crops-resize.png)

   * 스마트 자르기 상자를 이동합니다. 다음 중 하나를 수행합니다.

      * 이미지에 스마트 자르기 또는 스마트 색상 견본만 있으면 자르기 상자를 새 위치로 드래그합니다.
      * 이미지에 스마트 자르기 및 스마트 색상 견본이 모두 있으면 스마트 자르기 상자를 새 위치로 드래그합니다. 또는 이미지 아래의 스마트 색상 견본을 탭하거나 클릭한 다음(색상 견본은 정적임) 스마트 견본 자르기 상자를 새로운 위치로 드래그합니다.

      ![edit_smart_crops-move](assets/edit_smart_crops-move.png)

   * 모든 편집 내용을 실행 취소하고 원본 스마트 자르기 또는 스마트 견본을 복원할 수 있습니다(현재 편집 세션에만 적용).

      이미지 위의 **[!UICONTROL 되돌리기]**&#x200B;를 누릅니다.

      ![edit_smart_crops-revert](assets/edit_smart_crops-revert.png)



1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 저장을 탭합니다.]** 그런 다음  **** 닫기를 탭하여 자산 폴더로 돌아갑니다.

## {#removing-an-image-profile-from-folders} 폴더에서 이미지 프로필 제거

폴더에서 이미지 프로필을 제거하면 모든 하위 폴더는 해당 상위 폴더에서 자동으로 프로필 제거를 상속합니다. 그러나 폴더 내에서 발생한 파일 처리는 그대로 유지됩니다.

**[!UICONTROL 도구]** 메뉴 내에서 또는 폴더에 있는 경우 **[!UICONTROL 속성에서 이미지 프로필을 제거할 수 있습니다.]** 이 섹션에서는 두 가지 방법으로 폴더에서 이미지 프로필을 제거하는 방법에 대해 설명합니다.

### 프로필 사용자 인터페이스 {#removing-image-profiles-from-folders-via-profiles-user-interface}을(를) 통해 폴더에서 Dynamic Media 이미지 프로필 제거

1. AEM 로고를 누르고 **[!UICONTROL 도구 > 자산 > 이미지 프로필로 이동합니다.]**
1. 폴더 또는 여러 폴더에서 제거할 이미지 프로필을 선택합니다.
1. **[!UICONTROL 폴더에서 처리 프로필 제거]**&#x200B;를 누르고 프로필을 제거할 폴더 또는 여러 폴더를 선택하고 **[!UICONTROL 제거를 누릅니다.]**

   이름이 폴더 이름 아래에 더 이상 나타나지 않으므로 이미지 프로필이 폴더에 더 이상 적용되지 않음을 확인할 수 있습니다.

### {#removing-image-profiles-from-folders-via-properties} 속성을 통해 폴더에서 Dynamic Media 이미지 프로필 제거

1. AEM 로고를 누르고 **[!UICONTROL 자산]**&#x200B;으로 이동한 다음 이미지 프로필을 제거할 폴더로 이동합니다.
1. 폴더에서 확인 표시를 눌러 선택한 다음 **[!UICONTROL 속성을 누릅니다.]**
1. **[!UICONTROL 이미지 프로필]** 탭을 선택합니다.
1. **[!UICONTROL 프로필 이름]** 드롭다운 목록에서 **[!UICONTROL 없음]**&#x200B;을 선택한 다음 **[!UICONTROL 저장 및 닫기를 탭합니다.]**

   프로파일이 이미 할당된 폴더가 폴더 이름 바로 아래에 프로파일 이름이 표시되어 표시됩니다.
