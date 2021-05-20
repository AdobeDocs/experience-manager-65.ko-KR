---
title: 웹 사이트 구조 설정
seo-title: 웹 사이트 구조 설정
description: 디렉토리 설정
seo-description: 디렉토리 설정
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 웹 사이트 구조 설정 {#setup-website-structure}

웹 사이트를 설정하려면 아래 지침에 따라 다음 위치에서 만들 폴더를 설명합니다.

* `/apps/an-scf-sandbox`

   사용자 정의 응용 프로그램 및 템플릿이 상주하는 위치입니다.

* `/etc/designs/an-scf-sandbox`

   다운로드 가능한 디자인 요소가 있는 위치입니다.

* `/content/an-scf-sandbox`

   여기에서 다운로드 가능한 웹 페이지가 있습니다.

이 자습서의 코드는 애플리케이션, 디자인 및 컨텐츠에 대해 동일한 기본 폴더 이름을 사용합니다. 웹 사이트의 다른 이름을 선택하는 경우 항상 `an-scf-sandbox` 을 선택한 이름으로 바꾸십시오.

>[!NOTE]
>
>이름 정보:
>
>* CRXDE에 표시되는 이름은 주소 지정 가능한 컨텐츠의 경로를 형성하는 노드 이름입니다.
>* 노드 이름에는 공백을 포함할 수 있지만 URI에서 사용할 경우 공간을 &#39;%20&#39; 또는 &#39;+&#39; 중 하나로 인코딩해야 합니다.
>* 노드 이름은 하이픈 및 밑줄을 포함할 수 있지만 Java 파일 내에서 패키지 이름으로 참조할 때 인코딩해야 합니다. 하이픈과 밑줄은 모두 밑줄 및 유니코드 값을 사용하여 이스케이프됩니다.

   >
   >   
   * 하이픈은 &#39;_002d&#39;가 됩니다.
   >   * 밑줄이 &#39;_005f&#39;가 됨


## 응용 프로그램 디렉토리(/apps) {#setup-the-application-directory-apps} 설정

저장소의 /apps 디렉토리에는 /content 디렉토리에서 제공되는 페이지의 동작 및 렌더링을 구현하는 코드가 포함되어 있습니다.

/apps 디렉토리는 보호되며 /content 및 /etc/designs 디렉토리처럼 공개적으로 액세스할 수 없습니다.

1. `/apps/an-scf-sandbox` 폴더를 만듭니다.

   탐색기 창에서 **[!UICONTROL CRXDE Lite]** 사용

   1. `/apps` 폴더를 선택합니다.
   1. **[!UICONTROL 만들기]**... 를 마우스 오른쪽 단추로 클릭하거나 **[!UICONTROL 만들기...]** 메뉴.
   1. **[!UICONTROL 폴더 만들기.. 를 선택합니다.]**.
   1. **[!UICONTROL 폴더 만들기]** 대화 상자에서 `an-scf-sandbox`를 입력합니다.
   1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

1. **[!UICONTROL components]** 하위 폴더를 만듭니다.

   1. `/apps/an-scf-sandbox` 폴더를 선택합니다.
   1. **[!UICONTROL 만들기 > 폴더 만들기]**&#x200B;를 클릭합니다.
   1. **[!UICONTROL 폴더 만들기]** 대화 상자에서 **[!UICONTROL 구성 요소]**&#x200B;를 입력합니다.
   1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

1. **[!UICONTROL templates]** 하위 폴더를 만듭니다.

   1. `/apps/an-scf-sandbox` 폴더를 선택합니다.
   1. **[!UICONTROL 만들기 > 폴더 만들기]**&#x200B;를 클릭합니다.
   1. **[!UICONTROL 폴더 만들기]** 대화 상자에서 **[!UICONTROL 템플릿]**&#x200B;을 입력합니다.
   1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
   1. `/apps/an-scf-sandbox`을(를) 다시 선택합니다.
   1. **[!UICONTROL 모두 저장]**&#x200B;을 선택합니다.

   편집 프로세스와 마찬가지로 자주 저장합니다. 데이터 입력 문제가 발생하는 경우 로그인 시간이 초과되었거나 이전 편집 내용을 저장해야 하기 때문일 수 있습니다.

1. 이제 CRXDE Lite의 탐색기 창의 구조는 다음과 같아야 합니다.

   ![crxde-template](assets/crxde-template.png)

## 디자인 디렉토리(/etc/designs) {#setup-the-design-directory-etc-designs} 설정

/etc/designs 디렉토리에는 페이지 컨텐츠와 함께 다운로드할 이미지, 스크립트 및 스타일시트가 포함되어 있습니다.

1. 클래식 UI에서 디자이너 도구를 사용하려면 [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin)로 이동합니다.

   참고:CRXDE Lite을 사용하여 `cq:Page` 유형의 노드를 만드는 경우 액세스 제어 및 복제가 페이지에 대한 기본 설정으로 설정되지 않습니다.

1. 탐색기 창에서 **[!UICONTROL 디자인]** 폴더를 선택한 다음 **[!UICONTROL 새]** > **[!UICONTROL 새 페이지]**&#x200B;를 클릭합니다.

   다음을 입력합니다.

   * 제목:**[!UICONTROL SCF 샌드박스]**
   * 이름:**[!UICONTROL an-scf-sandbox]**
   * **[!UICONTROL 디자인 페이지 템플릿]** 선택

   **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

   ![디자인 템플릿](assets/design-template.png)

1. &quot;SCF Sandbox&quot; 폴더가 나타나지 않으면 탐색기 창을 새로 고칩니다.

1. CRXDE Lite(http:// localhost:4502/crx/de)로 돌아가서 /etc/designs를 확장하여 &quot;an-scf-sandbox&quot;라는 노드를 확인합니다.

   CRXDE의 오른쪽 아래 창에서 속성 탭, 액세스 제어 탭 및 복제 탭을 보고 디자인 페이지 템플릿을 사용하여 정의된 내용을 확인할 수 있습니다.

   ![crxde-configure-template](assets/crxde-configure-template.png)

## 컨텐츠 디렉토리(/content) {#setup-the-content-directory-content} 설정

저장소의 /content 디렉토리는 웹 사이트 컨텐츠가 있는 위치입니다. /content 아래의 경로는 브라우저 요청에 대한 URL의 경로를 구성합니다.

** 초기 애플리케이션 [의 일부로 ](initial-app.md#createthepagetemplate) 페이지 템플릿이 작성되면 템플릿을 기반으로 초기 페이지 컨텐츠를 만들 수 있습니다..  [**⇒**](initial-app.md)
