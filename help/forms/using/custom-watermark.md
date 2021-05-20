---
title: 문자 PDF 미리 보기의 사용자 지정 워터마크
seo-title: 문자 PDF 미리 보기의 사용자 지정 워터마크
description: 편지 PDF 미리 보기에서 사용자 정의 워터마크를 만드는 방법을 알아봅니다.
seo-description: 편지 PDF 미리 보기에서 사용자 정의 워터마크를 만드는 방법을 알아봅니다.
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
feature: 서신 관리
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# 문자 PDF 미리 보기{#custom-watermark-in-letter-pdf-preview}의 사용자 지정 워터마크

## 개요 {#overview}

서신 작성 UI에서 에이전트 사용자는 전자 메일이나 인쇄와 같이 사후 처리로 전송되는 최종 형태를 미리 봅니다.

조직에서 이 데이터를 무단 사용하지 않도록 미리 보기 PDF에 워터마크를 지정할 수 있습니다. 기본 워터마크는 PDF에 나타나는 &quot;미리 보기&quot;입니다.

미리 보기 PDF에서 워터마크를 활성화하려면 https://&#39;[서버]:[포트]&#39;/system/console/configMgr에서 **[!UICONTROL 미리 보기 중 워터마크]** 적용 옵션을 선택합니다.****

![기본 워터마크](assets/default-watermark.png)

다음 단계를 사용하여 워터마크의 텍스트와 모양을 사용자 정의할 수 있습니다.

## 서신 작성 UI {#customizewatermark-}에서 PDF 미리 보기에서 워터마크 사용자 정의

1. `https://'[server]:[port]'/[ContextPath]/crx/de`(으)로 이동하여 관리자로 로그인합니다.
1. apps 폴더에서 libs 폴더의 미리 보기 워터마크 폴더와 유사한 경로/구조를 사용하여 **[!UICONTROL 미리 보기 워터마크]**&#x200B;라는 폴더를 만듭니다.

   1. 다음 경로에서 **미리 보기 워터마크** 폴더를 마우스 오른쪽 단추로 클릭하고 **오버레이 노드**&#x200B;를 선택합니다.

      `/libs/fd/cm/configFiles/previewwatermark`

   1. 오버레이 노드 대화 상자에 다음 값이 있는지 확인합니다.

      **경로:** /libs/fd/cm/configFiles/previewwatermark

      **오버레이 위치:** /apps/

      **일치 노드 유형:** 선택됨

      >[!NOTE]
      >
      >/libs 분기에서 변경하지 마십시오. 이 분기는 사용자가 변경할 때마다 변경되므로 변경한 내용이 손실될 수 있습니다.
      >
      >    
      >    
      >    * 인스턴스에서 업그레이드
      >    * 핫픽스 적용
      >    * 기능 팩 설치


   1. **확인**&#x200B;을 클릭한 다음 **모두 저장**&#x200B;을 클릭합니다. **[!UICONTROL 미리 보기 워터마크]** 폴더가 지정된 경로에 생성됩니다.



1. ddx 파일을 &quot;/libs/fd/cm/configFiles/previewwatermark&quot; 폴더에서 &quot;/apps/fd/cm/configFiles/previewwatermark&quot; 폴더로 복사하여 붙여넣고 **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.
1. /apps/fd/cm/configFiles/previewwatermark/ 아래의 ddx 파일에서 원하는 대로 변경합니다.

   ```xml
   <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
    <PDF result="output.pdf">
     <PDF source="input.pdf"/>
           <Watermark opacity="15%" rotation="45">
            <StyledText>
                     <p font-family="Georgia" font-size="70pt" color="black" font-weight="bold">
                         PREVIEW
                    </p>
            </StyledText>
           </Watermark>
    </PDF>
   </DDX>
   ```

   워터마크 모양, 텍스트 및 정렬 사용자 지정에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) 문서에서 워터마크 및 배경 추가 및 제거를 참조하십시오.

   >[!NOTE]
   >
   >ddx 파일에서 결과 및 소스에 대한 참조가 output.pdf 및 input.pdf에 변경되지 않은 채로 유지됩니다. 파일 ddx의 이름도 변경할 수 없습니다.

1. **모두 저장**&#x200B;을 클릭합니다.
