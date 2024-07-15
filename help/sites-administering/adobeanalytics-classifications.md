---
title: Adobe 분류
description: Adobe 분류를 사용하여 분류 데이터를 Adobe Analytics으로 내보내는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 5%

---

# Adobe 분류{#adobe-classifications}

Adobe 분류는 예약된 방식으로 분류 데이터를 [Adobe Analytics](/help/sites-administering/adobeanalytics.md)(으)로 내보냅니다. 내보내기가 **com.adobe.cq.scheduled.exporter.Exporter**&#x200B;의 구현입니다.

이를 구성하는 방법:

1. **탐색**&#x200B;을 사용하여 **도구**, **Cloud Service**, **기존 Cloud Service**&#x200B;을 선택하십시오.
1. **Adobe Analytics**(으)로 스크롤한 다음 **구성 표시**&#x200B;를 선택합니다.
1. Adobe Analytics 구성 옆에 있는 **[+]** 링크를 클릭합니다.

1. **프레임워크 만들기** 대화 상자에서:

   * **제목**&#x200B;을 지정합니다.
   * 저장소에 프레임워크 세부 정보를 저장하는 노드에 대해 **이름**&#x200B;을(를) 지정할 수도 있습니다.
   * **Adobe Analytics 분류** 선택

   **만들기**&#x200B;를 클릭합니다.

   ![프레임워크 만들기 대화 상자](assets/aa-25.png)

1. 편집할 수 있는 **분류 설정** 대화 상자가 열립니다.

   ![분류 설정 대화 상자](assets/aa-classifications-settings.png)

   속성에는 다음이 포함됩니다.

   | **필드** | **설명** |
   |---|---|
   | 활성화됨 | Adobe 분류 설정을 활성화하려면 **예**&#x200B;를 선택하십시오. |
   | 충돌 시 덮어쓰기 | 데이터 충돌을 덮어쓰려면 **예**&#x200B;를 선택하십시오. 기본적으로 **아니요**(으)로 설정됩니다. |
   | 삭제가 처리되었습니다 | **예**(으)로 설정하면 처리된 노드를 내보낸 후 삭제합니다. 기본값은 **False**&#x200B;입니다. |
   | 작업 내보내기 설명 | Adobe 분류 작업에 대한 설명을 입력합니다. |
   | 알림 전자 메일 | Adobe 분류 알림에 대한 이메일 주소를 입력합니다. |
   | 보고서 세트 | 가져오기 작업을 실행할 보고서 세트를 입력합니다. |
   | 데이터 세트 | 가져오기 작업을 실행할 데이터 세트 관계 ID를 입력합니다. |
   | 변환자 | 드롭다운 메뉴에서 변환기 구현을 선택합니다. |
   | 데이터 소스 | 데이터 컨테이너의 경로로 이동합니다. |
   | 일정 내보내기 | 내보내기 일정을 선택합니다. 기본값은 30분마다입니다. |

1. 설정을 저장하려면 **확인**&#x200B;을 클릭하세요.

## 페이지 크기 수정 {#modifying-page-size}

레코드는 페이지에서 처리됩니다. 기본적으로 Adobe 분류는 페이지 크기가 1000인 페이지를 만듭니다.

Adobe 분류의 25000에 따라 페이지 크기가 최대 한도로 설정될 수 있으며 Felix 콘솔에서 수정할 수 있습니다. 내보내는 동안 Adobe 분류는 소스 노드를 잠궈 동시 수정을 방지합니다. 내보내기 후, 오류 시 또는 세션이 닫히면 노드 잠금이 해제됩니다.

페이지 크기를 변경하려면:

1. **https://&lt;host>:&lt;port>/system/console/configMgr**&#x200B;의 OSGI 콘솔로 이동하고 **AEM 분류 내보내기 Adobe**&#x200B;을 선택합니다.

   ![aa-26](assets/aa-26.png)

1. 필요에 따라 **페이지 크기 내보내기**&#x200B;를 업데이트한 다음 **저장**&#x200B;을 클릭합니다.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Adobe 분류는 이전에 SAINT 익스포터라고 했습니다.

내보내기는 변환기(Transformer)를 사용하여 내보내기 데이터를 특정 형식으로 변환할 수 있습니다. Adobe 분류의 경우 변환기 인터페이스를 구현하는 하위 인터페이스 `SAINTTransformer<String[]>`이(가) 제공되었습니다. 이 인터페이스는 데이터 형식을 SAINT API에서 사용하는 `String[]`(으)로 제한하고 선택할 해당 서비스를 찾는 마커 인터페이스를 제공하는 데 사용됩니다.

기본 구현 SAINTDefaultTransformer에서 내보내기 소스의 하위 리소스는 속성 이름을 키로 사용하고 속성 값을 값으로 사용하는 레코드로 처리됩니다. **Key** 열은 첫 번째 열로 자동으로 추가됩니다. 해당 값은 노드 이름이 됩니다. 네임스페이스가 지정된 속성(`:` 포함)은 무시됩니다.

*노드 구조:*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * Product = 내 제품 이름(문자열)
      * 가격 = 120.90 (문자열)
      * 크기 = M (문자열)
      * Color = black (문자열)
      * Color^Code = 101 (String)

**SAINT 헤더 및 레코드:**

| **키** | **제품** | **가격** | **크기** | **색상** | **색상^코드** |
|---|---|---|---|---|---|
| 1 | 내 제품 이름 | 120.90 | 월 | black | 101 |

속성에는 다음이 포함됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성 경로</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>변환자</td>
   <td>SAINTransformer 구현의 클래스 이름</td>
  </tr>
  <tr>
   <td>이메일</td>
   <td>알림 이메일 주소.</td>
  </tr>
  <tr>
   <td>보고서 세트</td>
   <td>가져오기 작업을 실행할 보고서 세트 ID. </td>
  </tr>
  <tr>
   <td>데이터 세트</td>
   <td>가져오기 작업을 실행할 데이터 세트 관계 ID. </td>
  </tr>
  <tr>
   <td>설명</td>
   <td>작업 설명. <br /> </td>
  </tr>
  <tr>
   <td>덮어쓰기</td>
   <td>데이터 충돌을 덮어쓰는 플래그. 기본값은 <strong>false</strong>입니다.</td>
  </tr>
  <tr>
   <td>체크디비전</td>
   <td>보고서 세트의 호환성을 확인하는 플래그. 기본값은 <strong>true</strong>입니다.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>내보내기 후 처리된 노드를 삭제하는 플래그. 기본값은 <strong>false</strong>입니다.</td>
  </tr>
 </tbody>
</table>

## Adobe 분류 내보내기 자동화 {#automating-adobe-classifications-export}

고유한 워크플로우를 만들 수 있으므로 새 가져오기에서 워크플로우를 시작하여 적절하고 올바르게 구조화된 데이터를 **/var/export/**&#x200B;에 만들어 Adobe 분류로 내보낼 수 있습니다.
