---
title: HTML5 양식에서 스크리블 서명 사용
seo-title: Using Scribble Signature in HTML5 forms
description: 터치 장치에서 HTML5 양식이 점점 더 많이 사용되고 있으며, 한 가지 일반적인 요구 사항은 서명을 지원하는 것입니다. 모바일 장치에서 문서에 서명하는 것은 모바일 장치에서 일반적으로 사용되는 양식 서명 방법이 되고 있습니다.
seo-description: HTML5 forms are increasingly used on touch devices, and one common requirement is to support signatures. Signing documents on mobile devices is becoming an accepted way of signing forms on mobile devices.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
feature: Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# HTML5 양식에서 스크리블 서명 사용{#using-scribble-signature-in-html-forms}

터치 장치에서 HTML5 양식이 점점 더 사용되고 있으며, 한 가지 일반적인 요구 사항은 서명을 지원하는 것입니다. 모바일 장치에서 문서 작성(스타일러스 또는 손가락으로 쓰기)은 허용되는 양식 서명 방법이 되고 있습니다. 이제 HTML5 forms 및 Forms Designer에서 양식에 스크리블 서명 필드를 지정할 수 있습니다. 브라우저에서 양식을 렌더링하면 스타일러스, 마우스 또는 터치를 사용하여 이러한 필드에 서명할 수 있습니다.

## 스크리블 서명 필드를 사용하여 양식을 디자인하는 방법 {#how-to-design-a-form-using-scribble-signature-field}

1. Forms 디자이너에서 양식을 엽니다.
1. 페이지에 서명 스크리블 필드를 드래그하여 놓습니다.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >Forms Designer에서 선택한 필드의 Dimension은 필드를 렌더링할 때 반영됩니다. 그러나 렌더링된 서명 상자의 차원은 Forms 디자이너에 지정된 차원이 아니라 필드의 종횡비를 기반으로 계산됩니다.

1. 서명 스크리블 필드를 구성합니다.

   서명 스크리블 필드는 기본적으로 iPad에서 서명 프로세스 중에 지리적 위치 정보를 필수로 표시합니다(다른 장치에서는 선택 사항). 이 기본 동작은 `geoLocMandatoryOnIpad` 속성을 사용합니다. 이 속성은 서명 스크리블 필드에 추가 항목으로 표시됩니다. 수정하는 단계는 다음과 같습니다.

   1. 양식에서 서명 스크리블 필드를 선택합니다.
   1. 을(를) 선택합니다 **XML 소스** 탭.

      >[!NOTE]
      >
      >XML 소스 탭을 열려면 **보기** > **XML 소스**.

   1. 을(를) 찾습니다 `<ui>` 태그를에서 지정합니다. `<field>` 태그를 지정하고 소스 코드를 다음과 같이 수정합니다.

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. 을(를) 선택합니다 **디자인 보기** 탭. 확인 상자에서 **예**.
   1. 양식을 저장합니다.

1. 지원되는 장치/데스크탑 브라우저에서 양식을 렌더링합니다.

## 스크리블 서명과 인터페이스 {#interfacing-with-the-scribble-signatures}

### 서명 {#signing}

양식에 서명 스크리블 필드를 추가하고 렌더링하면 해당 필드를 클릭하거나 탭하면 대화 상자가 열립니다. 사용자는 점선 사각형에 의해 지정된 그리기 영역에 마우스, 손가락 또는 스타일러스를 사용하여 서명을 휘갈겨쓸 수 있다.

![지리적 위치](assets/geolocation.png)

**A.** 브러시 **B.** 지우개 **C.** 지리적 위치 **D.** 지리적 위치 정보

### 지리적 태깅 {#geo-tagging}

스크리블을 만들 때 지리적 위치 아이콘을 클릭하면 지리적 위치 및 시간 정보가 필드에 포함됩니다.

>[!NOTE]
iPad에서는 기본적으로 지리적 위치 정보를 포함해야 합니다.

iPad에서 지리적 위치 아이콘은 기본적으로 표시되지 않으며, 클릭하면 지리적 위치 정보가 자동으로 포함됩니다 **확인**.

iPad의 경우 다음 값을 수정하여 이 설정을 변경할 수 있습니다. `geoLocManadatoryOnIpad` 매개 변수 대상 `0`를 입력합니다.

* 지리적 위치 정보가 필수이면 사용자는 줄어든 그리기 영역이 표시됩니다. 사용자가 클릭하면 지리적 위치 텍스트가 추가됩니다 **확인** 아이콘을 클릭합니다.
* 다른 경우에는 사용자에게 완전한 단점이 제공됩니다. 사용자가 지리적 위치 정보를 포함하도록 선택하는 경우 지리적 위치 텍스트를 수용하도록 이 영역의 크기가 조정됩니다.

### 서명 지우기 {#clearing-a-signature}

이 기능을 사용하는 동안 사용자는 **지우개** 아이콘을 클릭하여 필드를 지우고 다시 시작합니다. 지리적 위치 정보가 추가되면 지워집니다.

### 서명 저장 {#saving-a-signature}

클릭 **확인** 아이콘은 스크리블을 필드에 이미지로 저장합니다. 추가적인 처리를 위해 이미지와 값을 서버에 제출할 수 있습니다. 사용자가 **확인**&#x200B;이렇게 하면 스크리블 파일이 잠깁니다. 스크리블 위젯을 사용하여 서명을 다시 편집할 수 없습니다.

스크리블 필드를 탭하거나 클릭하면 대화 상자가 읽기 전용 모드로 열립니다.

![3](assets/3.png)

### 펜 크기 선택 {#selecting-pen-size}

을(를) 클릭합니다. **브러시** 사용 가능한 펜 크기 목록을 표시하는 아이콘 해당 펜을 사용하려면 펜 크기를 클릭하거나 탭합니다.

### 양식에서 서명 삭제 {#delete-signatures-from-the-form}

양식에서 서명을 삭제하려면

* (모바일 장치) 서명 필드를 길게 누르고 확인 대화 상자에서 **예**.
* (데스크톱) 서명 필드를 마우스로 가리킨 다음 **취소** 아이콘을 클릭하고 확인 대화 상자에서 **예**.
