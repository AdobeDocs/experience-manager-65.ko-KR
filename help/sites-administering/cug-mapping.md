---
title: AEM 6.5의 사용자 지정 사용자 그룹 매핑
seo-title: Custom User Group Mapping in AEM 6.5
description: AEM에서 사용자 지정 사용자 그룹 매핑이 작동하는 방식을 알아봅니다.
seo-description: Lear how Custom User Group Mapping works in AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Security
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# AEM 6.5의 사용자 지정 사용자 그룹 매핑 {#custom-user-group-mapping-in-aem}

## CUG(사용자 정의 사용자 그룹) 관련 JCR 콘텐츠 비교 {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>이전 AEM 버전</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td><p>속성: cq:cugEnabled</p> <p>노드 유형 선언: N/A, 잔여 속성</p> </td>
   <td><p>승인:</p> <p>노드: rep:CugPolicy 노드 유형의 rep:cugPolicy</p> <p>노드 유형 선언: rep:CugMixin</p> <p> </p> <p> </p> <p> </p> 인증:</p> <p>Mixin 유형: granite:AuthenticationRequired</p> </td>
   <td><p>읽기 액세스를 제한하기 위해 전용 CUG 정책이 대상 노드에 적용됩니다.</p> <p>참고: 정책은 구성된 지원 경로에만 적용할 수 있습니다.</p> <p>rep:cugPolicy 및 rep:CugPolicy 유형이 있는 노드는 보호되며, 일반 JCR API 호출을 사용하여 작성할 수 없습니다. 대신 JCR 액세스 제어 관리를 사용하십시오.</p> <p>다음을 참조하십시오 <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">이 페이지</a> 추가 정보.</p> <p>노드에 인증 요구 사항을 적용하려면 mixin 유형 granite:AuthenticationRequired를 추가하면 됩니다.</p> <p>참고: 구성된 지원 경로 아래에만 적용됩니다.</p> </td>
  </tr>
  <tr>
   <td><p>속성: cq:cugPrincipals</p> <p>노드 유형 선언: NA, 잔여 속성</p> </td>
   <td><p>속성: rep:principalNames</p> <p>노드 유형 선언: rep:CugPolicy</p> </td>
   <td><p>제한된 CUG 아래의 콘텐츠를 읽을 수 있는 해당 보안 주체의 이름이 포함된 속성은 보호되며 일반 JCR API 호출을 사용하여 작성할 수 없습니다. 대신 JCR 액세스 제어 관리를 사용하십시오.</p> <p>다음을 참조하십시오 <a href="https://jackrabbit.apache.org/api/2.12/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.html">이 페이지</a> 구현에 대한 자세한 내용은 를 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td><p>속성: cq:cugLoginPage</p> <p>노드 유형 선언: NA, 잔여 속성</p> </td>
   <td><p>속성: granite:loginPath (선택 사항)</p> <p>노드 유형 선언: granite:AuthenticationRequired</p> </td>
   <td><p>granite:AuthenticationRequired mixin 유형이 정의된 JCR 노드는 대체 로그인 경로를 선택적으로 정의할 수 있습니다.</p> <p>참고: 구성된 지원 경로 아래에만 적용됩니다.</p> </td>
  </tr>
  <tr>
   <td><p>속성: cq:cugRealm</p> <p>노드 유형 선언: NA, 잔여 속성</p> </td>
   <td>NA</td>
   <td>새 구현에서는 더 이상 지원되지 않습니다.</td>
  </tr>
 </tbody>
</table>

## OSGi 서비스 비교 {#comparison-of-osgi-services}

**이전 AEM 버전**

레이블: Adobe Granite CUG(폐쇄형 사용자 그룹) 지원

이름: com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* 라벨 : Apache Jackrabbit Oak CUG 구성

   이름: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

   ConfigurationPolicy = 필수

* 라벨 : Apache Jackrabbit Oak CUG 제외 목록

   이름: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

   ConfigurationPolicy = 필수

* 이름: com.adobe.granite.auth.requirement.impl.RequirementService
* 레이블: Adobe Granite 인증 요구 사항 및 로그인 경로 핸들러

   이름: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler

   ConfigurationPolicy = 필수

**댓글**

* CUG 인증 구성 및 평가 활성화/비활성화.
CUG 인증의 영향을 받지 않아야 하는 주체의 제외 목록을 구성하는 서비스입니다.

   >[!NOTE]
   > 
   >다음과 같은 경우 `CugExcludeImpl` 이(가) 구성되지 않았습니다. `CugConfiguration` 을 기본값으로 되돌립니다.

   특별한 필요가 있는 경우 사용자 지정 CugExclude 구현을 플러그인할 수 있습니다.

* 일치하는 로그인 경로를 LoginSelectorHandler에 노출하는 LoginPathProvider를 구현하는 OSGi 구성 요소입니다. granite:AuthenticationRequired mixin 유형을 사용하여 컨텐츠에 저장된 변경된 인증 요구 사항을 수신하는 관찰자를 등록하는 데 사용되는 RequirementHandler에 대한 필수 참조가 있습니다.
* 인증 요구 사항에 대한 변경 사항을 SlingAuthenticator에 알리는 RequirementHandler를 구현하는 OSGi 구성 요소입니다.

   이 구성 요소에 대한 구성 정책은 REQUIRE이므로 지원되는 경로 집합이 지정된 경우에만 활성화됩니다.

   서비스를 활성화하면 RequirementService가 실행됩니다.

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation in case of special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->
