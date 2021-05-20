---
title: AEM Forms 프로세스 이해
seo-title: AEM Forms 프로세스 이해
description: AEM Forms 프로세스 이해
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
role: Developer
exl-id: 434ac316-8a01-43a6-844b-1b792f60fa21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# AEM Forms 프로세스 이해 {#understanding-aem-forms-processes}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

일반적인 사용 사례는 AEM Forms 서비스 세트가 단일 문서에서 작동하는 것입니다. Workbench를 사용하여 프로세스를 만들어 서비스 컨테이너에 요청을 보낼 수 있습니다. 프로세스는 자동화하려는 비즈니스 프로세스를 나타냅니다. 프로세스 만들기에 대한 내용은 [Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용을 참조하십시오.

프로세스가 활성화되면 서비스가 되고 다른 서비스처럼 호출할 수 있습니다. 암호화 서비스와 같은 표준 서비스와 프로세스에서 시작된 서비스 간의 한 가지 차이점은 암호화 서비스가 많은 작업을 수행하는 하나의 작업을 가지고 있다는 것입니다. 반면 표준 서비스에는 여러 가지 작업이 있습니다. 각 작업은 일반적으로 문서에 정책을 적용하거나 문서를 암호화하는 등 하나의 작업을 수행합니다.

프로세스는 수명이 짧거나 오래 걸릴 수 있습니다. 단기 프로세스는 이 프로세스가 호출된 동일한 실행 스레드에서 동기적으로 수행되는 작업입니다. 단기 작업은 클라이언트 응용 프로그램이 메서드를 호출하고 반환 값을 기다리는 대부분의 프로그래밍 언어에서 발견되는 표준 동작과 비슷합니다.

그러나 다음과 같은 요인으로 인해 프로세스를 동기식으로 완료할 수 없는 상황이 있습니다.

* 프로세스는 상당한 시간에 걸쳐 있을 수 있습니다.
* 프로세스는 조직의 경계를 확장할 수 있습니다.
* 프로세스를 완료하려면 외부 입력이 필요합니다. 예를 들어 부재 중인 관리자에게 양식이 전송되는 상황을 고려해 보십시오. 이 경우 관리자가 양식을 반환하고 채울 때까지 프로세스가 완료되지 않습니다.

   이러한 유형의 프로세스를 장기 처리 과정이라고 합니다. 장기간 프로세스가 비동기식으로 수행되므로 시스템이 리소스 권한으로 상호 작용하고 작업을 추적하고 모니터링할 수 있습니다. 긴 기간 프로세스가 호출되면 AEM Forms은 긴 기간 프로세스 상태를 추적하는 레코드의 일부로 호출 식별자 값을 만듭니다. 레코드가 AEM Forms 데이터베이스에 저장됩니다. 더 이상 필요하지 않은 긴 기간 프로세스 레코드를 삭제할 수 있습니다.

>[!NOTE]
>
>AEM Forms은 단기 프로세스가 호출될 때 레코드를 만들지 않습니다.

호출 식별자 값을 사용하여 긴 기간 프로세스의 상태를 추적할 수 있습니다. 예를 들어 프로세스 호출 식별자 값을 사용하여 실행 중인 프로세스 인스턴스 종료와 같은 프로세스 관리자 작업을 수행할 수 있습니다.

**단기 프로세스 예**

다음 그림은 *MyApplication/EncryptDocument*&#x200B;라는 짧은 기간의 프로세스의 예입니다.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 이 프로세스를 호출하는 방법에 대해 설명하는 코드 예제를 따라 하려면 Workbench를 사용하여 `MyApplication/EncryptDocument` 프로세스를 만듭니다. ([Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용 을 참조하십시오.)

이 단기 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 입력 값으로 전달되는 비보안 PDF 문서를 가져옵니다.
1. 암호로 PDF 문서를 암호화합니다. 이 프로세스에 대한 입력 매개 변수의 이름은 `inDoc`이고 데이터 유형은 문서입니다.
1. 암호로 암호화된 PDF 문서를 PDF 파일로 로컬 파일 시스템에 저장합니다. 이 프로세스는 암호화된 PDF 문서를 출력 값으로 반환합니다. 이 프로세스에 대한 출력 매개 변수의 이름은 `outDoc`이고 데이터 유형은 문서입니다.

   이 프로세스는 이 프로세스가 호출된 동일한 실행 스레드에서 동기적으로 완료됩니다. 이 단기 프로세스의 이름은 `MyApplication/EncryptDocument`이고 해당 작업은 `invoke`입니다.

   >[!NOTE]
   >
   >일반적으로 단기 프로세스는 세 가지 이상의 작업으로 구성됩니다. 워크벤치를 사용하여 프로세스를 만듭니다. ([Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용 을 참조하십시오.)

   *AEM*&#x200B;형식을 사용한 프로그래밍에서 이 단기 프로세스를 프로그래밍 방식으로 호출할 수 있는 다음과 같은 방법을 설명합니다.

   * [AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (Flex 응용 프로그램 사용)을 사용하여 비보안 문서를 전달하여 단기 프로세스를 호출합니다
   * [Invocation API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) (Java Invocation API)를 사용하여 단기 프로세스 호출
   * [Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) (웹 서비스 예제)
   * [MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) (웹 서비스 예제)
   * [SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) (웹 서비스 예제)
   * [HTTP를 통해 BLOB 데이터를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) (웹 서비스 예제)
   * [DIME를 사용하여 AEM Forms을 호출하는](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) (웹 서비스 예)
   * [REST를 사용하여 MyApplication/EncryptDocument 프로세스를 호출하는 중](/help/forms/developing/invoking-aem-forms-using-rest.md)

**장기간 프로세스 예**

다음 그림은 장기간 프로세스의 예입니다.

이 프로세스는 지원자가 대출 양식을 제출할 때 호출됩니다. 대출 담당 직원이 대출 요청을 승인하거나 거부하기 전까지는 그 과정이 완료되지 않는다. 이 긴 기간 프로세스의 이름은 *FirstAppSolution/PreLoanProcess*&#x200B;이며 해당 작업은 `invoke_Async`입니다. 이 프로세스는 비동기식으로 호출해야 합니다. 이 오래 지속되는 프로세스를 프로그래밍 방식으로 호출하는 방법에 대한 자세한 내용은 [인간 중심의 장기 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)을 참조하십시오.

>[!NOTE]
>
>이 프로세스는 [첫 번째 AEM Forms 응용 프로그램 만들기](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)에 지정된 자습서에 따라 만들 수 있습니다.
