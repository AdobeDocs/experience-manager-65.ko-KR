---
title: Adobe 분류
seo-title: Adobe 분류
description: Adobe 분류에 대해 알아보십시오.
seo-description: Adobe 분류에 대해 알아보십시오.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
translation-type: tm+mt
source-git-commit: 4456b5366387c27810c407d6ac9e6c17fc290269
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 6%

---


# Adobe 분류{#adobe-classifications}

Adobe 분류은 분류 데이터를 예약된 방식으로 [Adobe Analytics](/help/sites-administering/adobeanalytics.md)로 내보냅니다. 내보내기는 **com.adobe.cq.scheduled.exporter.Exporter**&#x200B;의 구현입니다.

이를 구성하려면:

1. **내비게이션**&#x200B;을 사용하여 **도구**, **Cloud Services**&#x200B;을 선택한 다음 **기존 Cloud Services**&#x200B;을 선택합니다.
1. **Adobe Analytics**&#x200B;로 스크롤하고 **구성 표시**&#x200B;를 선택합니다.
1. Adobe Analytics 구성 옆에 있는 **[+]** 링크를 클릭합니다.

1. **프레임워크 만들기** 대화 상자에서 다음을 수행합니다.

   * **제목**&#x200B;을 지정합니다.
   * 원할 경우 저장소에 프레임워크 세부 사항을 저장하는 노드에 대해 **이름**&#x200B;을 지정할 수 있습니다.
   * **Adobe Analytics 분류** 선택

   **만들기**&#x200B;를 클릭합니다.

   ![프레임워크 만들기 대화 상자](assets/aa-25.png)

1. 편집을 위해 **분류 설정** 대화 상자가 열립니다.

   ![분류 설정 대화 상자](assets/aa-classifications-settings.png)

   속성에는 다음이 포함됩니다.

   | **필드** | **설명** |
   |---|---|
   | 활성화됨 | Adobe 분류 설정을 활성화하려면 **예**&#x200B;를 선택합니다. |
   | 충돌 시 덮어쓰기 | 데이터 충돌을 덮어쓰려면 **예**&#x200B;를 선택합니다. 기본적으로 이 값은 **No**&#x200B;로 설정됩니다. |
   | 삭제가 처리되었습니다 | **Yes**&#x200B;로 설정하면 처리된 노드를 내보낸 후 삭제합니다. 기본값은 **False**&#x200B;입니다. |
   | 작업 내보내기 설명 | Adobe 분류 작업에 대한 설명을 입력합니다. |
   | 알림 이메일 | Adobe 분류 알림에 대한 이메일 주소를 입력합니다. |
   | 보고서 세트 | 가져오기 작업을 실행할 보고서 세트를 입력합니다. |
   | 데이터 세트 | 가져오기 작업을 실행할 데이터 집합 관계 ID를 입력합니다. |
   | 변환자 | 드롭다운 메뉴에서 변환기 구현을 선택합니다. |
   | 데이터 소스 | 데이터 컨테이너의 경로로 이동합니다. |
   | 일정 내보내기 | 내보내기 일정을 선택합니다. 기본값은 30분마다 있습니다. |

1. 설정을 저장하려면 **확인**&#x200B;을 클릭합니다.

## 페이지 크기 수정 {#modifying-page-size}

레코드는 페이지에서 처리됩니다. 기본적으로 Adobe 분류은 페이지 크기가 1000인 페이지를 만듭니다.

페이지 크기는 Adobe 분류에서 정의당 최대 25,000개이며 Felix 콘솔에서 수정할 수 있습니다. 내보내는 동안 Adobe 분류은 소스 노드를 잠가 동시 수정을 방지합니다. 내보내기 후, 오류 시 또는 세션이 닫힌 후 노드의 잠금이 해제됩니다.

페이지 크기를 변경하려면:

1. **https://&lt;호스트>:&lt;포트>/system/console/configMgr**&#x200B;의 OSGI 콘솔로 이동하고 **Adobe AEM 분류 내보내기**&#x200B;를 선택합니다.

   ![aa-26](assets/aa-26.png)

1. **페이지 크기 내보내기**&#x200B;를 필요에 따라 업데이트한 다음 **저장**&#x200B;을 클릭합니다.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Adobe 분류은 이전에 SAINT 내보내기라고도 했습니다.

내보내기 프로그램은 Transformer를 사용하여 내보내기 데이터를 특정 형식으로 변형할 수 있습니다. Adobe 분류의 경우 Transformer 인터페이스를 구현하는 하위 인터페이스 `SAINTTransformer<String[]>`가 제공되었습니다. 이 인터페이스는 데이터 유형을 SAINT API에서 사용하는 `String[]`으로 제한하고 마커 인터페이스를 사용하여 선택할 서비스를 찾습니다.

기본 구현 SAINTDefaultTransformer에서 내보내기 소스의 자식 리소스는 속성 이름을 키와 속성 값으로 포함하는 레코드로 처리됩니다. **키** 열은 첫 번째 열로 자동으로 추가됩니다. 이 값은 노드 이름이 됩니다. 이름 지정된 속성(`:` 포함)은 무시됩니다.

*노드 구조:*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * 제품 = 내 제품 이름(문자열)
      * 가격 = 120.90 (문자열)
      * 크기 = M(문자열)
      * 색상 = 검정(문자열)
      * 색상^코드 = 101(문자열)

**SAINT 헤더 및 레코드:**

| **키** | **제품** | **가격** | **크기** | **색상** | **색상^코드** |
|---|---|---|---|---|---|
| 1 | 내 제품 이름 | 120.90 | M | black | 101년 |

속성에는 다음이 포함됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성 경로</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>변압기</td>
   <td>SAINTTrans전 구현의 클래스 이름</td>
  </tr>
  <tr>
   <td>이메일</td>
   <td>알림 이메일 주소입니다.</td>
  </tr>
  <tr>
   <td>reportsuites</td>
   <td>보고서 세트 ID를 사용하여 가져오기 작업을 실행합니다. </td>
  </tr>
  <tr>
   <td>데이터 집합</td>
   <td>가져오기 작업을 실행할 데이터 집합 관계 ID입니다. </td>
  </tr>
  <tr>
   <td>설명</td>
   <td>작업 설명입니다.<br /> </td>
  </tr>
  <tr>
   <td>덮어쓰기</td>
   <td>데이터 충돌을 덮어쓸 플래그. 기본값은 <strong>false</strong>입니다.</td>
  </tr>
  <tr>
   <td>checkdification</td>
   <td>호환성이 있는지 보고서 세트를 확인하는 플래그. 기본값은 <strong>true</strong>입니다.</td>
  </tr>
  <tr>
   <td>deletered</td>
   <td>내보내기 후 처리된 노드를 삭제하는 플래그. 기본값은 <strong>false</strong>입니다.</td>
  </tr>
 </tbody>
</table>

## Adobe 분류 내보내기 자동화 {#automating-adobe-classifications-export}

고유한 워크플로우를 만들 수 있으므로 새 가져오기를 통해 **/var/export/**&#x200B;에서 적절하고 올바르게 구조화된 데이터를 만드는 워크플로우를 실행할 수 있으므로 Adobe 분류으로 내보낼 수 있습니다.
