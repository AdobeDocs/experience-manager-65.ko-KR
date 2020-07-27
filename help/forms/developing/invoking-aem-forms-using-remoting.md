---
title: Remoting을 사용하여 AEM Forms 호출
seo-title: Remoting을 사용하여 AEM Forms 호출
description: 'null'
seo-description: 'null'
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '4593'
ht-degree: 0%

---


# Remoting을 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-remoting}

Workbench에서 만든 프로세스는 Remoting을 사용하여 호출할 수 있습니다. 즉, Flex로 구축한 클라이언트 애플리케이션에서 AEM Forms 프로세스를 호출할 수 있습니다. 이 기능은 데이터 서비스를 기반으로 합니다.

>[!NOTE]
>
>Remoting을 사용할 때는 AEM Forms 서비스와 반대로 Workbench에서 만든 프로세스를 호출하는 것이 좋습니다. 하지만 AEM Forms 서비스를 직접 호출할 수도 있습니다. (AEM Forms 개발자 센터에 있는 Remoting을 사용하여 PDF 문서 암호화를 참조하십시오.)

>[!NOTE]
>
>AEM Forms 서비스가 익명 액세스를 허용하도록 구성되지 않은 경우 Flex 클라이언트의 요청이 웹 브라우저에 문제가 발생합니다. 사용자는 사용자 이름과 암호 자격 증명을 입력해야 합니다.

Remoting을 사용하여 호출할 수 있는 이름 `MyApplication/EncryptDocument`으로 짧은 AEM Forms입니다. 입력 및 출력 값과 같은 이 프로세스에 대한 자세한 내용은 [짧은 기간 프로세스 예를 참조하십시오](/help/forms/developing/aem-forms-processes.md).

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>Flex 애플리케이션을 사용하여 AEM Forms 프로세스를 호출하려면 원격 끝점이 활성화되어 있는지 확인하십시오. 기본적으로 프로세스를 배포할 때 원격 끝점이 활성화됩니다.

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 입력 값으로 전달된 보안되지 않은 PDF 문서를 가져옵니다. 이 작업은 작업을 `SetValue` 기반으로 합니다. 입력 매개 변수의 이름 `inDoc` 과 해당 데이터 유형이 입니다 `document`. ( `document` 데이터 유형은 워크벤치 내에서 사용 가능한 데이터 유형입니다.)
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 작업을 `PasswordEncryptPDF` 기반으로 합니다. 이 프로세스의 출력 값 이름 `outDoc` 은 암호로 암호화된 PDF 문서를 나타냅니다. outDoc의 데이터 유형은 입니다 `document`.
1. 암호로 암호화된 PDF 문서를 로컬 파일 시스템에 PDF 파일로 저장합니다. 이 작업은 작업을 `WriteDocument` 기반으로 합니다.

>[!NOTE]
>
>이 `MyApplication/EncryptDocument` 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제와 함께 작업하려면 Workbench를 `MyApplication/EncryptDocument` 사용하는 프로세스를 만듭니다.

>[!NOTE]
>
>Remoting을 사용하여 오래 지속되는 프로세스를 호출하는 방법에 대한 자세한 내용은 인간 중심 [장기 체류 프로세스 호출을 참조하십시오](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

**참고 항목**

[AEM Forms Flex 라이브러리 파일 포함](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[문서 처리(AEM Forms에 대해 더 이상 사용되지 않음) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Remoting AEM Forms을 사용하여(AEM Forms에 대해 더 이상 사용되지 않음) 안전하지 않은 문서를 전달하여 짧은 기간 동안의 프로세스 호출](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flex로 구축한 클라이언트 애플리케이션 인증](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Remoting을 사용하여 프로세스를 호출하는 보안 문서 전달](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[Remoting을 사용하여 사용자 지정 구성 요소 서비스 호출](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[인간 중심의 오랜 프로세스를 불러일으키는 Flex를 사용하여 구축한 클라이언트 애플리케이션 제작](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[HTTP 토큰을 사용하여 SSO 인증을 수행하는 Flash Builder 애플리케이션 만들기](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

Flex 그래프 컨트롤에 프로세스 데이터를 표시하는 방법에 대한 자세한 내용은 Flex 그래프로 [AEM Forms 프로세스 데이터 표시를 참조하십시오](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html).

>[!NOTE]
>
>*crossdomain.xml 파일을 적절한 위치에 배치해야 합니다. 예를 들어 JBoss에 AEM Forms을 배포한 경우 이 파일을 다음 위치에 배치합니다. &lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war*

## AEM Forms Flex 라이브러리 파일 포함 {#including-the-aem-forms-flex-library-file}

Remoting을 사용하여 프로그래밍 방식으로 AEM Forms 프로세스를 호출하려면 adobe-remoting-provider.swc 파일을 Flex 프로젝트의 클래스 경로에 추가합니다. 이 SWC 파일은 다음 위치에 있습니다.

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   여기서 &lt;*install_directory*>는 AEM Forms이 설치된 디렉토리입니다.

**참고 항목**

[Remoting을 사용하여 AEM Forms 호출(AEM Forms에 대해 더 이상 사용되지 않음) AEM Forms](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[문서 처리(AEM Forms에 대해 더 이상 사용되지 않음) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Remoting AEM Forms을 사용하여(AEM Forms에 대해 더 이상 사용되지 않음) 안전하지 않은 문서를 전달하여 짧은 기간 동안의 프로세스 호출](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flex로 구축한 클라이언트 애플리케이션 인증](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Remoting을 사용하여 문서 처리 {#handling-documents-with-remoting}

AEM Forms에서 사용되는 가장 중요한 비원시 Java 유형 중 하나는 `com.adobe.idp.Document` 클래스입니다. 일반적으로 AEM Forms 작업을 호출하는 데 문서가 필요합니다. 주로 PDF 문서이지만 SWF, HTML, XML 또는 DOC 파일과 같은 다른 문서 유형을 포함할 수 있습니다. (Java [API를 사용하여 AEM Forms 서비스에 데이터 전달을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Flex로 구축한 클라이언트 애플리케이션은 문서를 직접 요청할 수 없습니다. 예를 들어 Adobe Reader를 실행하여 PDF 파일을 만드는 URL을 요청할 수 없습니다. PDF 및 Microsoft Word 문서와 같은 문서 유형에 대한 요청은 URL인 결과를 반환합니다. URL의 컨텐츠를 표시하는 것은 클라이언트의 책임입니다. 문서 관리 서비스는 URL 및 컨텐츠 유형 정보를 생성하는 데 도움이 됩니다. XML 문서에 대한 요청은 그 결과 전체 XML 문서를 반환합니다.

### 문서를 입력 매개 변수로 전달 {#passing-a-document-as-an-input-parameter}

Flex를 사용하여 구축한 클라이언트 응용 프로그램은 문서를 AEM Forms 프로세스에 직접 전달할 수 없습니다. 대신 클라이언트 응용 프로그램은 `mx.rpc.livecycle.DocumentReference` ActionScript 클래스의 인스턴스를 사용하여 인스턴스 `com.adobe.idp.Document` 가 필요한 작업에 입력 매개 변수를 전달합니다. Flex 클라이언트 애플리케이션에는 `DocumentReference` 객체를 설정하는 여러 가지 옵션이 있습니다.

* 문서가 서버에 있고 해당 파일 위치가 알려지면 DocumentReference 개체의 referenceType 속성을 REF_TYPE_FILE로 설정합니다. 다음 예제와 같이 fileRef 속성을 파일 위치로 설정합니다.

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* 문서가 서버에 있고 해당 URL을 알고 있는 경우 DocumentReference 개체의 referenceType 속성을 REF_TYPE_URL로 설정합니다. 다음 예제와 같이 url 속성을 URL로 설정합니다.

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* 클라이언트 응용 프로그램의 텍스트 문자열에서 DocumentReference 개체를 만들려면 DocumentReference 개체의 referenceType 속성을 REF_TYPE_INLINE으로 설정합니다. 다음 예제와 같이 text 속성을 개체에 포함할 텍스트로 설정합니다.

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server’s default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* 문서가 서버에 없으면 원격 업로드 서블릿을 사용하여 문서를 AEM Forms에 업로드합니다. 보안 문서를 업로드하는 기능은 AEM Forms의 새로운 기능입니다. 보안 문서를 업로드할 때 *문서 업로드 응용 프로그램 사용자* 역할을 가진 사용자를 사용해야 합니다. 이 역할이 없으면 보안 문서를 업로드할 수 없습니다. 단일 사인온을 사용하여 보안 문서를 업로드하는 것이 좋습니다. (원격 [을 사용하여 프로세스를 호출하는 보안 문서 전달을 참조하십시오](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).)

>[!NOTE]
안전하지 않은 문서를 업로드하도록 AEM Forms이 구성된 경우 문서 업로드 응용 프로그램 사용자 역할이 없는 사용자를 사용하여 문서를 업로드할 수 있습니다. 사용자는 문서 업로드 권한을 가질 수도 있습니다. 그러나 AEM Forms이 보안 문서만 허용하도록 구성된 경우 사용자에게 문서 업로드 응용 프로그램 사용자 역할 또는 문서 업로드 권한이 있는지 확인하십시오. 보안 및 비보안 [문서를 수락하도록 AEM Forms 구성을 참조하십시오](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).

지정된 업로드 URL에 표준 Flash 업로드 기능을 사용합니다. `https://SERVER:PORT/remoting/lcfileupload`. 그런 다음 유형 입력 매개 변수가 필요한 `DocumentReference` 곳에 개체를 사용할 수 있습니다. 원격 빠른 시작 `Document` 은 원격 업로드 서블릿을 사용하여 PDF 파일을` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }``MyApplication/EncryptDocument`프로세스에 전달합니다. ( [AEM Forms의 경우 더 이상 사용되지 않음) AEM Forms Remoting을 사용하여 안전하지 않은 문서를 전달하여 짧은 기간 동안 지속된 프로세스 호출을 참조하십시오](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

```java
 
private
function startUpload(): void  { 
 fileRef.addEventListener(Event.SELECT, selectHandler); 
 fileRef.addEventListener("uploadCompleteData", completeHandler); 
 try  { 
  var success: Boolean = fileRef.browse(); 
 }  
 catch (error: Error)  { 
  trace("Unable to browse for files."); 
 } 
}   
private
function selectHandler(event: Event): void { 
 var request: URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try  { 
  fileRef.upload(request); 
 }  
 catch (error: Error)  { 
  trace("Unable to upload file."); 
 } 
}  
private
function completeHandler(event: DataEvent): void  { 
 var params: Object = new Object(); 
 var docRef: DocumentReference = new DocumentReference(); 
 docRef.url = event.data as String; 
 docRef.referenceType = DocumentReference.REF_TYPE_URL; 
}
```

원격 빠른 시작 기능은 원격 업로드 서블릿을 사용하여 PDF 파일을 `MyApplication/EncryptDocument`프로세스에 전달합니다. ( [AEM Forms의 경우 더 이상 사용되지 않음) AEM Forms Remoting을 사용하여 안전하지 않은 문서를 전달하여 짧은 기간 동안 지속된 프로세스 호출을 참조하십시오](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

### 클라이언트 애플리케이션으로 문서 다시 전달 {#passing-a-document-back-to-a-client-application}

클라이언트 응용 프로그램은 인스턴스를 출력 매개 변수 `mx.rpc.livecycle.DocumentReference` 로 반환하는 서비스 작업의 `com.adobe.idp.Document` 유형 객체를 받습니다. 클라이언트 응용 프로그램은 Java가 아닌 ActionScript 객체를 다루므로 Java 기반 Document 객체를 다시 Flex 클라이언트로 전달할 수 없습니다. 대신, 서버는 문서에 대한 URL을 생성하여 이 URL을 클라이언트에 다시 전달합니다. 개체의 `DocumentReference``referenceType` 속성은 컨텐츠가 개체에 있는지, 아니면 속성의 URL에서 검색되어야 하는지 `DocumentReference` `DocumentReference.url` 지정합니다. 이 `DocumentReference.contentType` 속성은 문서의 유형을 지정합니다.

**참고 항목**

[Remoting을 사용하여 AEM Forms 호출(AEM Forms에 대해 더 이상 사용되지 않음) AEM Forms](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Flex 라이브러리 파일 포함](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Remoting AEM Forms을 사용하여(AEM Forms에 대해 더 이상 사용되지 않음) 안전하지 않은 문서를 전달하여 짧은 기간 동안의 프로세스 호출](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flex로 구축한 클라이언트 애플리케이션 인증](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Remoting을 사용하여 프로세스를 호출하는 보안 문서 전달](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Remoting을 사용하여 안전하지 않은 문서를 전달하여 짧은 수명 프로세스 호출 {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

Flex로 구축된 애플리케이션에서 AEM Forms 프로세스를 불러오려면 다음 작업을 수행하십시오.

1. 인스턴스를 `mx:RemoteObject` 만듭니다.
1. 인스턴스를 `ChannelSet` 만듭니다.
1. 필수 입력 값을 전달합니다.
1. 반환 값을 처리합니다.

>[!NOTE]
이 섹션에서는 안전하지 않은 문서를 업로드하도록 AEM Forms이 구성된 경우 AEM Forms 프로세스를 불러오고 문서를 업로드하는 방법에 대해 설명합니다. AEM Forms 처리 과정을 불러오고 보안 문서를 업로드하는 방법 및 안전하고 안전하지 않은 문서를 수락하도록 AEM Forms을 구성하는 방법에 대한 자세한 내용은 Remoting을 사용하여 보안 문서 [전달을 참조하십시오](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).

**mx:RemoteObject 인스턴스 만들기**

워크벤치에 생성된 AEM Forms 프로세스를 호출하는 인스턴스를 `mx:RemoteObject` 생성합니다. 인스턴스를 만들려면 `mx:RemoteObject` 다음 값을 지정합니다.

* **id:** 호출할 프로세스를 나타내는 `mx:RemoteObject` 인스턴스의 이름입니다.
* **destination:** 호출할 AEM Forms 프로세스의 이름입니다. 예를 들어 프로세스를 호출하려면 `MyApplication/EncryptDocument` 지정합니다 `MyApplication/EncryptDocument`.
* **result:** 결과를 처리하는 Flex 메서드의 이름입니다.

태그 `mx:RemoteObject` 내에서 프로세스의 호출 메서드 이름을 지정하는 `<mx:method>` 태그를 지정합니다. 일반적으로 Forms 호출 메서드의 이름은 입니다 `invoke`.

다음 코드 예제에서는 프로세스를 호출하는 `mx:RemoteObject` 인스턴스를 `MyApplication/EncryptDocument` 만듭니다.

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**AEM Forms으로 채널 만들기**

클라이언트 응용 프로그램은 다음 ActionScript 예제와 같이 MXML 또는 ActionScript에서 채널을 지정하여 AEM Forms을 호출할 수 있습니다. 채널은 `AMFChannel`, `SecureAMFChannel``HTTPChannel`또는 `SecureHTTPChannel`여야 합니다.

```java
     ...
     private function refresh():void{
         var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("my-amf",
             "https://yourlcserver:8080/remoting/messagebroker/amf"));
         EncryptDocument.setCredentials("administrator", "password");
         EncryptDocument.channelSet = cs;
     }
     ...
```

이전 코드 예제와 같이 인스턴스 `ChannelSet` 를 `mx:RemoteObject` 의 `channelSet` 필드에 할당합니다. 일반적으로 메서드를 호출할 때 정규화된 이름을 지정하지 않고 가져오기 문으로 채널 클래스를 `ChannelSet.addChannel` 가져옵니다.

**입력 값 전달**

Workbench에서 만든 프로세스는 0개 이상의 입력 매개 변수를 사용하고 출력 값을 반환할 수 있습니다. 클라이언트 응용 프로그램은 AEM Forms 프로세스에 속한 매개 변수에 해당하는 필드가 포함된 입력 매개 변수를 `ActionScript` 객체 내에 전달합니다. 이름이 지정된 짧은 프로세스 `MyApplication/EncryptDocument`에는 이름이 지정된 입력 매개 변수가 하나만 필요합니다 `inDoc`. 프로세스에 의해 노출된 작업의 이름 `invoke` (단기 프로세스의 기본 이름)입니다. (AEM Forms [호출을 사용하여(AEM 양식에서 더 이상 사용되지 않음) AEM Forms Remoting을 참조하십시오](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

다음 코드 예제에서는 PDF 문서를 `MyApplication/EncryptDocument` 프로세스에 전달합니다.

```java
     ...
     var params:Object = new Object();
 
     //Document is an instance of DocumentReference
     //that store an unsecured PDF document
     params["inDoc"] = pdfDocument;
 
     // Invoke an operation synchronously:
     EncryptDocument.invoke(params);
     ...
```

이 코드 예에서 `pdfDocument` 는 보안되지 않은 PDF 문서를 포함하는 `DocumentReference` 인스턴스입니다. For information about `DocumentReference`the [Handling documents with (Depreced for AEM forms) Remoting을 참조하십시오](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting).

**서비스의 특정 버전 호출**

호출의 매개 변수 맵에서 매개 변수를 사용하여 특정 버전의 Forms 서비스를 호출할 수 있습니다. `_version` 예를 들어, 서비스의 버전 1.2를 호출하려면 `MyApplication/EncryptDocument` 다음을 수행하십시오.

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

매개 변수 `version` 는 단일 기간이 들어 있는 문자열이어야 합니다. 기간의 왼쪽, 주 버전 및 오른쪽, 부 버전 값은 정수여야 합니다. 이 매개 변수를 지정하지 않으면 헤드 활성 버전이 호출됩니다.

**반환 값 처리**

AEM Forms 프로세스 출력 매개 변수는 다음 예제와 같이 클라이언트 응용 프로그램이 이름별로 특정 매개 변수를 추출하는 ActionScript 객체로 디시리얼라이즈(deserialized)됩니다. (프로세스의 출력 값 `MyApplication/EncryptDocument` 이름이 `outDoc`지정됩니다.)

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**MyApplication/EncryptDocument 프로세스 호출**

다음 단계를 수행하여 `MyApplication/EncryptDocument` 프로세스를 호출할 수 있습니다.

1. ActionScript 또는 MXML을 통해 `mx:RemoteObject` 인스턴스를 만듭니다. mx:RemoteObject 인스턴스 만들기를 참조하십시오.
1. AEM Forms과 통신하고 인스턴스에 연결할 인스턴스를 `ChannelSet` `mx:RemoteObject` 설정합니다. AEM Forms에 채널 만들기를 참조하십시오.
1. 사용자 식별자 값 및 암호를 지정하려면 ChannelSet의 `login` 메서드 또는 서비스 `setCredentials` 메서드를 호출합니다. (Single [Sign-On 사용을 참조하십시오](invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. 인스턴스 `mx.rpc.livecycle.DocumentReference` 를 보안되지 않은 PDF 문서로 채워 `MyApplication/EncryptDocument` 프로세스 전달 ( [문서를 입력 매개 변수로 전달을 참조하십시오](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter).)
1. 인스턴스의 메서드를 호출하여 PDF 문서 `mx:RemoteObject` 를 `invoke` 암호화합니다. 입력 매개 변수 `Object` (보안되지 않은 PDF 문서)가 포함된 PDF를 전달합니다. 입력 값 전달을 참조하십시오.
1. 프로세스에서 반환되는 암호로 암호화된 PDF 문서를 검색합니다. 반환 값 처리를 참조하십시오.

[빠른 시작: Remoting AEM Forms을 사용하여(AEM Forms에 대해 더 이상 사용되지 않음) 안전하지 않은 문서를 전달하여 짧은 기간 동안의 프로세스 호출](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## Flex로 구축한 클라이언트 애플리케이션 인증 {#authenticating-client-applications-built-with-flex}

AEM Forms 사용자 관리자는 중앙 로그인 서비스를 통한 AEM Forms SSO(Single Sign-On), 기본 인증 및 사용자 정의 인증을 포함하여 Flex 애플리케이션에서 원격 요청을 인증할 수 있는 여러 가지 방법이 있습니다. Single Sign-On 또는 익명 액세스가 활성화되지 않은 경우 Remoting 요청은 기본 인증(기본값)이나 사용자 정의 인증을 초래합니다.

기본 인증은 웹 응용 프로그램 컨테이너의 표준 J2EE 기본 인증을 사용합니다. 기본 인증의 경우 HTTP 401 오류로 인해 브라우저 문제가 발생합니다. 즉, RemoteObject를 사용하여 Forms 응용 프로그램에 연결하려고 하지만 Flex 응용 프로그램에서 아직 로그인하지 않은 경우 브라우저에 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다.

사용자 정의 인증의 경우 서버가 클라이언트에 인증을 필요로 한다는 오류를 전송합니다.

>[!NOTE]
HTTP 토큰을 사용한 인증 수행에 대한 자세한 내용은 [HTTP 토큰을 사용하여 SSO 인증을 수행하는 Flash Builder 응용 프로그램 만들기를 참조하십시오](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens).

### 사용자 정의 인증 사용 {#using-custom-authentication}

원격 끝점의 인증 방법을 Basic에서 Custom으로 변경하여 관리 콘솔에서 사용자 정의 인증을 활성화합니다. 사용자 정의 인증을 사용하는 경우 클라이언트 응용 프로그램에서 로그인 `ChannelSet.login` 방법 및 로그아웃하는 `ChannelSet.logout` 방법을 호출합니다.

>[!NOTE]
AEM Forms의 이전 릴리스에서는 메서드를 호출하여 자격 증명을 대상에 `RemoteObject.setCredentials` 전송했습니다. 구성 요소의 서버 연결 첫 번째 시도가 있을 때까지 이 `setCredentials` 메서드는 실제로 자격 증명을 서버에 전달하지 않았습니다. 따라서 구성 요소에서 오류 이벤트를 발생시킨 경우 인증 오류 또는 다른 이유로 인해 오류가 발생했는지 확인할 수 없습니다. 이 `ChannelSet.login` 메서드는 호출 시 서버에 연결하여 인증 문제를 즉시 처리할 수 있습니다. 이 방법을 계속 사용할 수는 있지만 이 방법을 사용하는 것이 `setCredentials` `ChannelSet.login` 좋습니다.

여러 대상은 동일한 채널과 해당 ChannelSet 개체를 사용할 수 있으므로 한 대상에 로그인하면 사용자가 동일한 채널 또는 채널을 사용하는 다른 대상에 로그인됩니다. 두 구성 요소가 동일한 ChannelSet 개체에 다른 자격 증명을 적용하는 경우 마지막으로 적용된 자격 증명이 사용됩니다. 여러 구성 요소가 동일한 인증된 ChannelSet 개체를 사용하는 경우 메서드를 호출하면 모든 구성 요소가 대상에서 `logout` 기록됩니다.

다음 예제에서는 `ChannelSet.login` 및 `ChannelSet.logout` 메서드를 RemoteObject 컨트롤에 사용합니다. 이 응용 프로그램은 다음 작업을 수행합니다.

* 구성 요소에서 사용되는 채널을 나타내는 `ChannelSet` 개체를 `creationComplete` 처리기에 `RemoteObject` 만듭니다
* Button 클릭 이벤트에 대한 응답으로 함수를 호출하여 서버에 `ROLogin` 자격 증명을 전달합니다.
* RemoteObject 구성 요소를 사용하여 Button 클릭 이벤트에 대한 응답으로 문자열을 서버에 보냅니다. 서버는 동일한 문자열을 다시 RemoteObject 구성 요소로 반환합니다.
* RemoteObject 구성 요소의 결과 이벤트를 사용하여 TextArea 컨트롤에 문자열을 표시합니다.
* Button 클릭 이벤트에 대한 응답으로 함수를 호출하여 서버에서 `ROLogout` 로그아웃합니다.

```java
 <?xml version=”1.0”?>
 <!-- security/SecurityConstraintCustom.mxml -->
 <mx:Application xmlns:mx=”https://www.adobe.com/2006/mxml” width=”100%”
     height=”100%” creationComplete=”creationCompleteHandler();”>
 
     <mx:Script>
         <![CDATA[
             import mx.controls.Alert;
             import mx.messaging.config.ServerConfig;
             import mx.rpc.AsyncToken;
             import mx.rpc.AsyncResponder;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import mx.messaging.ChannelSet;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Define an AsyncToken object.
             public var token:AsyncToken;
 
             // Initialize ChannelSet object based on the
             // destination of the RemoteObject component.
             private function creationCompleteHandler():void {
                 if (cs == null)
                 cs = ServerConfig.getChannelSet(remoteObject.destination);
             }
 
             // Login and handle authentication success or failure.
             private function ROLogin():void {
                 // Make sure that the user is not already logged in.
                 if (cs.authenticated == false) {
                     token = cs.login(“sampleuser”, “samplepassword”);
                     // Add result and fault handlers.
                     token.addResponder(new AsyncResponder(LoginResultEvent,
                     LoginFaultEvent));
                 }
             }
 
             // Handle successful login.
             private function LoginResultEvent(event:ResultEvent,
                 token:Object=null):void  {
                     switch(event.result) {
                         case “success”:
                             authenticatedCB.selected = true;
                             break;
                             default:
                     }
                 }
 
                 // Handle login failure.
                 private function LoginFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         switch(event.fault.faultCode) {
                             case “Client.Authentication”:
                                 default:
                                 authenticatedCB.selected = false;
                                 Alert.show(“Login failure: “ + event.fault.faultString);
                     }
                 }
 
                 // Logout and handle success or failure.
                 private function ROLogout():void {
                     // Add result and fault handlers.
                     token = cs.logout();
                     token.addResponder(new
                         AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
                 }
 
                 // Handle successful logout.
                 private function LogoutResultEvent(event:ResultEvent,
                     token:Object=null):void {
                         switch (event.result) {
                             case “success”:
                                 authenticatedCB.selected = false;
                                 break;
                                 default:
                     }
                 }
 
                 // Handle logout failure.
                 private function LogoutFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         Alert.show(“Logout failure: “ + event.fault.faultString);
                 }
                 // Handle message recevied by RemoteObject component.
                 private function resultHandler(event:ResultEvent):void {
                     ta.text += “Server responded: “+ event.result + “\n”;
                 }
 
                 // Handle fault from RemoteObject component.
                 private function faultHandler(event:FaultEvent):void {
                     ta.text += “Received fault: “ + event.fault + “\n”;
                 }
             ]]>
     </mx:Script>
     <mx:HBox>
         <mx:Label text=”Enter a text for the server to echo”/>
         <mx:TextInput id=”ti” text=”Hello World!”/>
         <mx:Button label=”Login”
             click=”ROLogin();”/>
         <mx:Button label=”Echo”
             enabled=”{authenticatedCB.selected}”
             click=”remoteObject.echo(ti.text);”/>
         <mx:Button label=”Logout”
             click=”ROLogout();”/>
         <mx:CheckBox id=”authenticatedCB”
             label=”Authenticated?”
             enabled=”false”/>
     </mx:HBox>
     <mx:TextArea id=”ta” width=”100%” height=”100%”/>
 
     <mx:RemoteObject id=”remoteObject”
         destination=”myDest”
         result=”resultHandler(event);”
         fault=”faultHandler(event);”/>
 </mx:Application>
```

and 메서드 `login` 가 AsyncToken 개체를 `logout` 반환합니다. 결과 이벤트에 대해 이벤트 핸들러를 AsyncToken 개체에 지정하여 성공적인 호출을 처리하고, 장애 이벤트를 처리할 수 있습니다.

### 단일 사인온 사용 {#using-single-sign-on}

AEM Forms 사용자는 여러 AEM Forms 웹 응용 프로그램에 연결하여 작업을 수행할 수 있습니다. 사용자가 웹 애플리케이션 간에 이동할 때 각 웹 애플리케이션에 개별적으로 로그인하도록 하는 것은 효율적이지 않습니다. AEM Forms SSO(Single Sign-On) 메커니즘을 통해 사용자는 한 번 로그인한 다음 모든 AEM Forms 웹 애플리케이션에 액세스할 수 있습니다. AEM Forms 개발자는 AEM Forms과 함께 사용할 클라이언트 애플리케이션을 만들 수 있으므로 단일 사인온 메커니즘을 활용할 수 있어야 합니다.

각 AEM Forms 웹 응용 프로그램은 자체 WAR(Web Archive) 파일로 패키지되어 EAR(Enterprise Archive) 파일의 일부로 패키지됩니다. 응용 프로그램 서버는 다른 웹 응용 프로그램에서 세션 데이터의 공유를 허용하지 않으므로 AEM Forms은 HTTP 쿠키를 사용하여 인증 정보를 저장합니다. 인증 쿠키를 사용하면 사용자는 Forms 응용 프로그램에 로그인한 다음 다른 AEM Forms 웹 응용 프로그램에 연결할 수 있습니다. 이 기술을 단일 사인온이라고 합니다.

AEM Forms 개발자는 클라이언트 애플리케이션을 작성하여 양식 안내선(더 이상 사용되지 않음)의 기능을 확장하고 작업 영역을 사용자 정의합니다. 예를 들어 작업 공간 응용 프로그램에서 프로세스를 시작할 수 있습니다. 그런 다음 클라이언트 응용 프로그램은 원격 끝점을 사용하여 Forms 서비스에서 데이터를 검색합니다.

AEM Forms 서비스가 Remoting을 사용하여(AEM Forms에 대해 더 이상 사용되지 않음) AEM Forms을 호출하면 클라이언트 응용 프로그램이 인증 쿠키를 요청의 일부로 전달합니다. 사용자가 이미 인증을 받았으므로 클라이언트 응용 프로그램에서 AEM Forms 서비스에 연결하는 데 추가 로그인이 필요하지 않습니다.

>[!NOTE]
쿠키가 잘못되었거나 누락된 경우 로그인 페이지로 암시적 리디렉션이 없습니다. 따라서 익명 서비스는 계속 이용할 수 있습니다.

로그인하여 자체적으로 로그아웃하는 클라이언트 응용 프로그램을 작성하여 AEM Forms 단일 사인온 메커니즘을 무시하면 됩니다. Single Sign-On 메커니즘을 무시하면 응용 프로그램에서 기본 인증 또는 사용자 정의 인증을 사용할 수 있습니다.

이 메커니즘은 AEM Forms SSO(Single Sign-On) 메커니즘을 사용하지 않으므로 클라이언트에 인증 쿠키가 기록되지 않습니다. 로그인 자격 증명은 원격 채널의 `ChannelSet` 개체에 저장됩니다. 따라서 동일한 `RemoteObject` 호출을 `ChannelSet` 처리하는 경우 해당 자격 증명의 컨텍스트에서 수행됩니다.

### 단일 사인온 AEM Forms 설정 {#setting-up-single-sign-on-in-aem-forms}

AEM Forms에서 Single Sign-On을 사용하려면 중앙 로그인 서비스가 포함된 양식 워크플로우 구성 요소를 설치합니다. 사용자가 성공적으로 로그인하면 중앙 로그인 서비스는 사용자에게 인증 쿠키를 반환합니다. 이후 Forms 웹 응용 프로그램에 대한 모든 요청에는 쿠키가 포함됩니다. 쿠키가 유효하면 사용자가 인증된 것으로 간주되므로 다시 로그인할 필요가 없습니다.

### Single Sign-On을 사용하는 클라이언트 애플리케이션 쓰기 {#writing-a-client-application-that-uses-single-sign-on}

SSO(Single Sign-On) 방식을 활용하면 클라이언트 애플리케이션을 시작하기 전에 중앙 로그인 서비스를 사용하여 로그인할 수 있습니다. 즉, 클라이언트 응용 프로그램은 브라우저를 통해 로그인하거나 메서드를 호출하여 로그인하지 `ChannelSet.login` 않습니다.

AEM Forms SSO(Single Sign-On) 메커니즘을 사용하는 경우 Remoting 끝점을 구성하여 기본 인증이 아닌 사용자 지정 인증을 사용하십시오. 그렇지 않으면 기본 인증을 사용할 때 인증 오류로 인해 사용자가 보지 않기를 바라는 브라우저 문제가 발생합니다. 대신 응용 프로그램에서 인증 오류를 감지한 다음 사용자가 중앙 로그인 서비스를 사용하여 로그인하도록 알려주는 메시지를 표시합니다.

클라이언트 응용 프로그램은 다음 예제와 같이 구성 요소를 사용하여 원격 끝점을 통해 AEM Forms에 `RemoteObject` 액세스합니다.

```java
 <?xml version="1.0"?>
 <mx:Application
        backgroundColor="#FFFFFF">
 
       <mx:Script>
          <![CDATA[
 
            import mx.controls.Alert;
            import mx.rpc.events.FaultEvent;
 
            // Prompt user to login on a fault.
            private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
         }
          ]]>
       </mx:Script>
 
       <mx:RemoteObject id="srv"
           destination="product"
           fault="faultHandler(event);"/>
 
       <mx:DataGrid
           width="100%" height="100%"
           dataProvider="{srv.getProducts.lastResult}"/>
 
       <mx:Button label="Get Data"
           click="srv.getProducts();"/>
 
 </mx:Application>
```

**Flex 애플리케이션이 실행되는 동안 새로운 사용자로 로그인**

Flex를 사용하여 구축한 애플리케이션에는 AEM Forms 서비스에 대한 모든 요청과 함께 인증 쿠키가 포함되어 있습니다. 성능상의 이유로 AEM Forms은 모든 요청에서 쿠키의 유효성을 검사하지 않습니다. 그러나 AEM Forms은 인증 쿠키가 다른 인증 쿠키로 바뀌는 경우를 감지합니다.

예를 들어 클라이언트 애플리케이션을 시작하고 애플리케이션이 활성 상태인 동안 중앙 로그인 서비스를 사용하여 로그아웃합니다. 그런 다음 다른 사용자로 로그인할 수 있습니다. 다른 사용자로 로그인하면 기존 인증 쿠키가 새 사용자의 인증 쿠키로 바뀝니다.

클라이언트 응용 프로그램의 다음 요청에서 AEM Forms은 쿠키가 변경되었음을 감지하고 사용자를 로그아웃합니다. 따라서 쿠키 변경 후 첫 번째 요청이 실패합니다. 이후의 모든 요청은 새 쿠키의 컨텍스트에서 수행되며 성공합니다.

**로그아웃**

AEM Forms을 로그아웃하고 세션을 무효화하려면 클라이언트 컴퓨터에서 인증 쿠키를 삭제해야 합니다. Single Sign-On의 목적은 사용자가 한 번 로그인하도록 허용하는 것이므로 클라이언트 응용 프로그램이 쿠키를 삭제하도록 원치 않습니다. 이 작업은 사용자를 효과적으로 로그아웃합니다.

따라서 클라이언트 응용 프로그램의 `RemoteObject.logout` 메서드를 호출하면 클라이언트에서 세션이 로그아웃되지 않았다는 오류 메시지가 생성됩니다. 대신 사용자는 중앙 로그인 서비스를 사용하여 인증 쿠키를 로그아웃하고 삭제할 수 있습니다.

**Flex 애플리케이션을 실행하는 동안 로그아웃함**

Flex로 구축한 클라이언트 애플리케이션을 시작하고 중앙 로그인 서비스를 사용하여 로그아웃할 수 있습니다. 로그아웃 프로세스의 일부로 인증 쿠키가 삭제됩니다. 쿠키 없이 또는 잘못된 쿠키로 원격 요청이 수행된 경우 사용자 세션이 무효화됩니다. 이 작업은 실제로 로그아웃 상태입니다. 다음 번에 클라이언트 응용 프로그램이 AEM Forms 서비스에 연결을 시도할 때 사용자에게 로그인 요청이 표시됩니다.

**참고 항목**

[Remoting을 사용하여 AEM Forms 호출(AEM Forms에 대해 더 이상 사용되지 않음) AEM Forms](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[문서 처리(AEM Forms에 대해 더 이상 사용되지 않음) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flex 라이브러리 파일 포함](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Remoting AEM Forms을 사용하여(AEM Forms에 대해 더 이상 사용되지 않음) 안전하지 않은 문서를 전달하여 짧은 기간 동안의 프로세스 호출](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Remoting을 사용하여 프로세스를 호출하는 보안 문서 전달](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Remoting을 사용하여 프로세스를 호출하는 보안 문서 전달 {#passing-secure-documents-to-invoke-processes-using-remoting}

하나 이상의 문서가 필요한 프로세스를 호출할 때 보안 문서를 AEM Forms에 전달할 수 있습니다. 안전한 문서를 전달함으로써 비즈니스 정보와 기밀 문서를 보호합니다. 이 경우 문서는 PDF 문서, XML 문서, Word 문서 등을 참조할 수 있습니다. 보안 문서를 허용하도록 AEM Forms을 구성한 경우 Flex로 작성된 클라이언트 애플리케이션에서 AEM Forms으로 보안 문서를 전달해야 합니다. 보안 및 비보안 [문서를 수락하도록 AEM Forms 구성을 참조하십시오](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).

보안 문서를 전달할 때 Single Sign-On을 사용하고 *문서 업로드 응용 프로그램 사용자* 역할을 가진 AEM Forms 사용자를 지정합니다. 이 역할이 없으면 보안 문서를 업로드할 수 없습니다. 사용자에게 역할을 프로그래밍 방식으로 할당할 수 있습니다. 역할 및 권한 [관리를 참조하십시오](/help/forms/developing/users.md#managing-roles-and-permissions).

>[!NOTE]
새 역할을 만들고 해당 역할의 구성원이 보안 문서를 업로드하도록 하려면 문서 업로드 권한을 지정해야 합니다.

AEM Forms은 업로드 서블릿에 전달된 토큰을 반환하는 이름 `getFileUploadToken` 으로 지정된 작업을 지원합니다. 이 `DocumentReference.constructRequestForUpload` 메서드에는 메서드에서 반환된 토큰과 함께 AEM Forms에 대한 URL이 `LC.FileUploadAuthenticator.getFileUploadToken` 필요합니다. 이 메서드는 업로드 서블릿으로의 호출에 사용되는 `URLRequest` 객체를 반환합니다. 다음 코드는 이 응용 프로그램 논리를 보여 줍니다.

```java
     ...
         private function startUpload():void
         {
             fileRef.addEventListener(Event.SELECT, selectHandler);
             fileRef.addEventListener("uploadCompleteData", completeHandler);
             try
             {
         var success:Boolean = fileRef.browse();
             }
             catch (error:Error)
             {
                 trace("Unable to browse for files.");
             }
 
         }
 
          private function selectHandler(event:Event):void
             {
             var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
             authTokenService.addEventListener("result", authTokenReceived);
             authTokenService.channelSet = cs;
             authTokenService.getFileUploadToken();
             }
 
         private function authTokenReceived(event:ResultEvent):void
             {
             var token:String = event.result as String;
             var request:URLRequest = DocumentReference.constructRequestForUpload("http://localhost:8080", token);
 
             try
             {
           fileRef.upload(request);
             }
             catch (error:Error)
             {
             trace("Unable to upload file.");
             }
             }
 
         private function completeHandler(event:DataEvent):void
         {
 
             var params:Object = new Object();
             var docRef:DocumentReference = new DocumentReference();
             docRef.url = event.data as String;
             docRef.referenceType = DocumentReference.REF_TYPE_URL;
         }
         ...
```

)

### 보안 및 비보안 문서를 수락하도록 AEM Forms 구성 {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

관리 콘솔을 사용하여 Flex 클라이언트 애플리케이션에서 AEM Forms 프로세스로 문서를 전달할 때 문서의 보안 여부를 지정할 수 있습니다. 기본적으로 AEM Forms은 보안 문서를 허용하도록 구성됩니다. 다음 단계를 수행하여 보안 문서를 수락하도록 AEM Forms을 구성할 수 있습니다.

1. 관리 콘솔에 로그인합니다.
1. 설정을 **클릭합니다**.
1. 핵심 **시스템 설정을 클릭합니다.**
1. 구성을 클릭합니다.
1. Flex 애플리케이션에서 비보안 문서 업로드 허용 옵션이 선택되지 않았는지 확인합니다.

>[!NOTE]
비보안 문서를 허용하도록 AEM Forms을 구성하려면 Flex 애플리케이션에서 비보안 문서 업로드 허용 옵션을 선택합니다. 그런 다음 응용 프로그램 또는 서비스를 다시 시작하여 설정이 적용되도록 합니다.

### 빠른 시작: Remoting을 사용하여 보안 문서를 전달하여 짧은 수명 프로세스 호출 {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

다음 코드 예제에서는 `MyApplication/EncryptDocument.`사용자가 로그인해야 PDF 파일을 업로드하고 프로세스를 호출하는 데 사용되는 파일 선택 단추를 클릭할 수 있다고 호출합니다. 즉, 사용자가 인증되면 파일 선택 단추가 활성화됩니다. 다음 그림은 사용자가 인증된 후에 Flex 클라이언트 애플리케이션을 보여 줍니다. 인증된 체크박스가 활성화되었음을 확인합니다.

![uremotelogin](assets/iu_iu_secureremotelogin.png)

보안 문서만 업로드하도록 AEM Forms이 구성되어 있고 사용자에게 *문서 업로드 응용 프로그램 사용자* 역할이 없는 경우 예외가 발생합니다. 사용자에게 이 역할이 있으면 파일이 업로드되고 프로세스가 호출됩니다.

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  xmlns="*"
      creationComplete="initializeChannelSet();">
        <mx:Script>
        <![CDATA[
      import mx.rpc.livecycle.DocumentReference;
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.controls.Alert;
      import mx.rpc.events.FaultEvent;
      import mx.rpc.AsyncResponder;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var docRef:DocumentReference = new DocumentReference();
      private var parentResourcePath:String = "/";
      private var now1:Date;
      private var serverPort:String = "hiro-xp:8080";
 
      // Define a ChannelSet object.
      public var cs:ChannelSet;
 
      // Define an AsyncToken object.
      public var token:AsyncToken;
 
       // Holds information returned from AEM Forms
      [Bindable]
      public var progressList:ArrayCollection = new ArrayCollection();
 
 
      // Handles a successful login
     private function LoginResultEvent(event:ResultEvent,
         token:Object=null):void  {
             switch(event.result) {
                 case "success":
                     authenticatedCB.selected = true;
                     btnFile.enabled = true;
                     btnLogout.enabled = true;
                     btnLogin.enabled = false;
                         break;
                     default:
                 }
             }
 
 
 // Handle login failure.
 private function LoginFaultEvent(event:FaultEvent,
     token:Object=null):void {
     switch(event.fault.faultCode) {
                 case "Client.Authentication":
                         default:
                         authenticatedCB.selected = false;
                         Alert.show("Login failure: " + event.fault.faultString);
                 }
             }
 
 
      // Set up channel set to invoke AEM Forms
      private function initializeChannelSet():void {
        cs = new ChannelSet();
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
        EncryptDocument2.channelSet = cs;
      }
 
     // Call this method to upload the file.
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process.
      private function uploadFile():void {
        fileRef.addEventListener(Event.SELECT, selectHandler);
        fileRef.addEventListener(DataEvent.UPLOAD_COMPLETE_DATA,completeHandler);
        fileRef.browse();
      }
 
      // Gets called for selected file. Does the actual upload via the file upload servlet.
      private function selectHandler(event:Event):void {
              var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
         authTokenService.addEventListener("result", authTokenReceived);
         authTokenService.channelSet = cs;
         authTokenService.getFileUploadToken();
      }
 
     private function authTokenReceived(event:ResultEvent):void
     {
     var token:String = event.result as String;
     var request:URLRequest = DocumentReference.constructRequestForUpload("https://hiro-xp:8080", token);
 
     try
     {
           fileRef.upload(request);
     }
     catch (error:Error)
     {
         trace("Unable to upload file.");
     }
 }
 
      // Called once the file is completely uploaded.
      private function completeHandler(event:DataEvent):void {
 
        // Set the docRef’s url and referenceType parameters
        docRef.url = event.data as String;
        docRef.referenceType=DocumentReference.REF_TYPE_URL;
        executeInvokeProcess();
      }
 
     //This method invokes the EncryptDocument process
      public function executeInvokeProcess():void {
         //Create an Object to store the input value for the EncryptDocument process
           now1 = new Date();
 
         var params:Object = new Object();
         params["inDoc"]=docRef;
 
         // Invoke the EncryptDocument process
         var token:AsyncToken;
         token = EncryptDocument2.invoke(params);
         token.name = name;
      }
 
      // AEM Forms  login method
      private function ROLogin():void {
         // Make sure that the user is not already logged in.
 
         //Get the User and Password
         var userName:String = txtUser.text;
         var pass:String = txtPassword.text;
 
        if (cs.authenticated == false) {
             token = cs.login(userName, pass);
 
         // Add result and fault handlers.
         token.addResponder(new AsyncResponder(LoginResultEvent,    LoginFaultEvent));
                 }
             }
 
      // This method handles a successful process invocation
      public function handleResult(event:ResultEvent):void
      {
            //Retrieve information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var dr:DocumentReference = res["outDoc"] as DocumentReference;
          var now2:Date = new Date();
 
           // These fields map to columns in the DataGrid
          var progObject:Object = new Object();
          progObject.filename = token.name;
          progObject.timing = (now2.time - now1.time).toString();
          progObject.state = "Success";
          progObject.link = "<a href='" + dr.url + "'> open </a>";
          progressList.addItem(progObject);
      }
 
      // Prompt user to login on a fault.
       private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
            }
 
       // AEM Forms  logout method
     private function ROLogout():void {
         // Add result and fault handlers.
         token = cs.logout();
         token.addResponder(new AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
     }
 
     // Handle successful logout.
     private function LogoutResultEvent(event:ResultEvent,
         token:Object=null):void {
         switch (event.result) {
         case "success":
                 authenticatedCB.selected = false;
                 btnFile.enabled = false;
                 btnLogout.enabled = false;
                 btnLogin.enabled = true;
                 break;
                 default:
             }
     }
 
     // Handle logout failure.
     private function LogoutFaultEvent(event:FaultEvent,
             token:Object=null):void {
             Alert.show("Logout failure: " + event.fault.faultString);
     }
 
          private function resultHandler(event:ResultEvent):void {
          // Do anything else here.
          }
        ]]>
 
      </mx:Script>
      <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleResult(event)"/>
      </mx:RemoteObject>
 
       <!--//This consists of what is displayed on the webpage-->
      <mx:Panel id="lcPanel" title="EncryptDocument  (Deprecated for AEM forms) AEM Forms Remoting Example"
           height="25%" width="25%" paddingTop="10" paddingLeft="10" paddingRight="10"
           paddingBottom="10">
         <mx:Label width="100%" color="blue"
                text="Select a PDF file to pass to the EncryptDocument process"/>
        <mx:DataGrid x="10" y="0" width="500" id="idProgress" editable="false"
           dataProvider="{progressList}" height="231" selectable="false" >
          <mx:columns>
            <mx:DataGridColumn headerText="Filename" width="200" dataField="filename" editable="false"/>
            <mx:DataGridColumn headerText="State" width="75" dataField="state" editable="false"/>
            <mx:DataGridColumn headerText="Timing" width="75" dataField="timing" editable="false"/>
            <mx:DataGridColumn headerText="Click to Open" dataField="link" editable="false" >
             <mx:itemRenderer>
                <mx:Component>
                   <mx:Text x="0" y="0" width="100%" htmlText="{data.link}"/>
                </mx:Component>
             </mx:itemRenderer>
            </mx:DataGridColumn>
          </mx:columns>
        </mx:DataGrid>
        <mx:Button label="Select File" click="uploadFile()"  id="btnFile" enabled="false"/>
        <mx:Button label="Login" click="ROLogin();" id="btnLogin"/>
        <mx:Button label="LogOut" click="ROLogout();" enabled="false" id="btnLogout"/>
        <mx:HBox>
         <mx:Label text="User:"/>
         <mx:TextInput id="txtUser" text=""/>
         <mx:Label text="Password:"/>
         <mx:TextInput id="txtPassword" text="" displayAsPassword="true"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
      </mx:Panel>
 </mx:Application>
```

**참고 항목**

[Remoting을 사용하여 AEM Forms 호출(AEM Forms에 대해 더 이상 사용되지 않음) AEM Forms](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[문서 처리(AEM Forms에 대해 더 이상 사용되지 않음) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flex 라이브러리 파일 포함](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Remoting AEM Forms을 사용하여(AEM Forms에 대해 더 이상 사용되지 않음) 안전하지 않은 문서를 전달하여 짧은 기간 동안의 프로세스 호출](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flex로 구축한 클라이언트 애플리케이션 인증](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Remoting을 사용하여 사용자 지정 구성 요소 서비스 호출 {#invoking-custom-component-services-using-remoting}

Remoting을 사용하여 사용자 지정 구성 요소에 있는 서비스를 호출할 수 있습니다. 예를 들어 고객 서비스를 포함하는 은행 구성 요소를 고려합니다. Flex로 작성된 클라이언트 애플리케이션을 사용하여 고객 서비스에 속하는 작업을 호출할 수 있습니다. 이 섹션과 연관된 빠른 시작을 실행하려면 먼저 은행 사용자 지정 구성 요소를 만들어야 합니다.

고객 서비스에서 이름이 지정된 작업을 노출합니다 `createCustomer`. 이 토론은 고객 서비스를 불러오고 고객을 생성하는 Flex 클라이언트 애플리케이션을 만드는 방법에 대해 설명합니다. 이 작업을 수행하려면 새 고객을 나타내는 복잡한 유형 `com.adobe.livecycle.sample.customer.Customer` 의 개체가 필요합니다. 다음 그림은 고객 서비스를 호출하고 새 고객을 생성하는 클라이언트 응용 프로그램을 보여줍니다. 이 `createCustomer` 작업은 고객 식별자 값을 반환합니다. 식별자 값은 [고객 식별자] 텍스트 상자에 표시됩니다.

![u_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

다음 표에는 이 클라이언트 응용 프로그램에 포함된 컨트롤이 나와 있습니다.

<table>
 <thead>
  <tr>
   <th><p>컨트롤 이름</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>txtFirst</p></td>
   <td><p>고객의 이름을 지정합니다. </p></td>
  </tr>
  <tr>
   <td><p>txtLast</p></td>
   <td><p>고객의 성을 지정합니다. </p></td>
  </tr>
  <tr>
   <td><p>txtPhone</p></td>
   <td><p>고객의 전화 번호를 지정합니다.</p></td>
  </tr>
  <tr>
   <td><p>txtStreet</p></td>
   <td><p>고객의 주소 이름을 지정합니다.</p></td>
  </tr>
  <tr>
   <td><p>txtState</p></td>
   <td><p>고객의 상태를 지정합니다. </p></td>
  </tr>
  <tr>
   <td><p>txtZIP</p></td>
   <td><p>고객의 우편 번호를 지정합니다. </p></td>
  </tr>
  <tr>
   <td><p>txtCity</p></td>
   <td><p>고객의 구/군/시를 지정합니다.</p></td>
  </tr>
  <tr>
   <td><p>txtCustId</p></td>
   <td><p>새 계정이 속하는 고객 식별자 값을 지정합니다. 이 텍스트 상자는 고객 서비스 <code>createCustomer</code> 작업의 반환 값으로 채워집니다. </p></td>
  </tr>
 </tbody>
</table>

### AEM Forms의 복잡한 데이터 형식 매핑 {#mapping-aem-forms-complex-data-types}

일부 AEM Forms 작업에는 입력 값으로 복잡한 데이터 유형이 필요합니다. 이러한 복잡한 데이터 유형은 작업에 사용되는 런타임 값을 정의합니다. 예를 들어 고객 서비스 `createCustomer` 의 작업에는 서비스에 필요한 런타임 값이 포함된 `Customer` 인스턴스가 필요합니다. 복잡한 유형이 없으면 고객 서비스는 예외를 throw하고 작업을 수행하지 않습니다.

AEM Forms 서비스를 호출할 때 필요한 AEM Forms 복합 유형에 매핑되는 ActionScript 개체를 만듭니다. 작업에 필요한 각 복잡한 데이터 유형에 대해 별도의 ActionScript 객체를 만듭니다.

ActionScript 클래스에서 `RemoteClass` 메타데이터 태그를 사용하여 AEM Forms 복합 유형에 매핑합니다. 예를 들어 고객 서비스 `createCustomer` 작업을 호출할 때 데이터 유형에 매핑되는 ActionScript 클래스를 `com.adobe.livecycle.sample.customer.Customer` 만듭니다.

고객이라는 다음 ActionScript 클래스는 AEM Forms 데이터 유형에 매핑하는 방법을 보여줍니다 `com.adobe.livecycle.sample.customer.Customer`.

```java
 package customer
 
 {
     [RemoteClass(alias="com.adobe.livecycle.sample.customer.Customer")]
     public class Customer
     {
            public var name:String;
            public var street:String;
            public var city:String;
            public var state:String;
            public var phone:String;
            public var zip:int;
        }
 }
```

AEM Forms 복합 유형의 정규화된 데이터 유형이 별칭 태그에 할당됩니다.

ActionScript 클래스의 필드는 AEM Forms 복합 유형에 속하는 필드와 일치합니다. 고객 ActionScript 클래스에 있는 6개의 필드는 속한 필드와 일치합니다 `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
양식 복합 유형에 속하는 필드 이름을 확인하는 좋은 방법은 웹 브라우저에서 서비스의 WSDL을 보는 것입니다. WSDL은 서비스의 복잡한 유형과 해당 데이터 멤버를 지정합니다. 다음 WSDL은 고객 서비스에 사용됩니다. `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

고객 ActionScript 클래스는 customer라는 패키지에 속합니다. 자체 패키지에 복잡한 AEM Forms 데이터 유형에 매핑되는 모든 ActionScript 클래스를 배치하는 것이 좋습니다. 다음 그림과 같이 Flex 프로젝트의 src 폴더에 폴더를 만들고 폴더에 ActionScript 파일을 배치합니다.

![iu_iu_customeras](assets/iu_iu_customeras.png)

### 빠른 시작: Remoting을 사용하여 고객 사용자 지정 서비스 호출 {#quick-start-invoking-the-customer-custom-service-using-remoting}

다음 코드 예제에서는 고객 서비스를 호출하고 새 고객을 만듭니다. 이 코드 예제를 실행할 때 모든 텍스트 상자를 채워야 합니다. 또한 매핑되는 Customer.as 파일을 만들어야 `com.adobe.livecycle.sample.customer.Customer`합니다.

>[!NOTE]
이 빠른 시작을 실행하기 전에 은행 사용자 지정 구성 요소를 만들고 배포해야 합니다.

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  layout="absolute" backgroundColor="#B1ABAB">
 
 <mx:Script>
            <![CDATA[
 
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.managers.CursorManager;
      import mx.rpc.remoting.mxml.RemoteObject;
 
 
      // Custom class that corresponds to an input to the
      // AEM Forms encryption method
      import customer.Customer;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var parentResourcePath:String = "/";
      private var serverPort:String = "hiro-xp:8080";
      private var now1:Date;
      private var fileName:String;
 
      // Prepares parameters for encryptPDFUsingPassword method call
      public function executeCreateCustomer():void
      {
 
        var cs:ChannelSet= new ChannelSet();
     cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
 
     customerService.setCredentials("administrator", "password");
     customerService.channelSet = cs;
 
     //Create a Customer object required to invoke the Customer service's
     //createCustomer operation
     var myCust:Customer = new Customer();
 
     //Get values from the user of the Flex application
     var fullName:String = txtFirst.text +" "+txtLast.text ;
     var Phone:String = txtPhone.text;
     var Street:String = txtStreet.text;
     var State:String = txtState.text;
     var Zip:int = parseInt(txtZIP.text);
     var City:String = txtCity.text;
 
     //Populate Customer fields
     myCust.name = fullName;
     myCust.phone = Phone;
     myCust.street= Street;
     myCust.state= State;
     myCust.zip = Zip;
     myCust.city = City;
 
     //Invoke the Customer service's createCustomer operation
     var params:Object = new Object();
        params["inCustomer"]=myCust;
     var token:AsyncToken;
        token = customerService.createCustomer(params);
        token.name = name;
      }
 
      private function handleResult(event:ResultEvent):void
      {
          // Retrieve the information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var custId:String = res["CustomerId"] as String;
 
          //Assign to the custId to the text box
          txtCustId.text = custId;
      }
 
 
      private function resultHandler(event:ResultEvent):void
      {
 
      }
            ]]>
 </mx:Script>
 <mx:RemoteObject id="customerService" destination="CustomerService" result="resultHandler(event);">
 <mx:method name="createCustomer" result="handleResult(event)"/>
 </mx:RemoteObject>
 
 
 <mx:Style source="../bank.css"/>
     <mx:Grid>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="New Customer" fontSize="16" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="First Name:" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtFirst"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:Button label="Create Customer" id="btnCreateCustomer" click="executeCreateCustomer()"/>
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Last Name" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtLast"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Phone" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtPhone"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Street" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtStreet"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="State" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtState"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="ZIP" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtZIP"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="City" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCity"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                             <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Customer Identifier" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCustId" editable="false"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                 </mx:Grid>
 </mx:Application>
 
```

**스타일 시트**

이 빠른 시작 부분에는 *bank.css라는 스타일 시트가 포함되어 있습니다*. 다음 코드는 사용되는 스타일 시트를 나타냅니다.

```css
 /* CSS file */
 global
 {
          backgroundGradientAlphas: 1.0, 1.0;
          backgroundGradientColors: #525152,#525152;
          borderColor: #424444;
          verticalAlign: middle;
          color: #FFFFFF;
          font-size:12;
          font-weight:normal;
 }
 
 ApplicationControlBar
 {
          fillAlphas: 1.0, 1.0;
          fillColors: #393839, #393839;
 }
 
 .textField
 {
          backgroundColor: #393839;
          background-disabled-color: #636563;
 }
 
 
 .button
 {
          fillColors: #636563, #424242;
 }
 
 .dropdownMenu
 {
          backgroundColor: #DDDDDD;
          fillColors: #636563, #393839;
          alternatingItemColors: #888888, #999999;
 }
 
 .questionLabel
 {
 
 }
 
 ToolTip
 {
        backgroundColor: black;
        backgroundAlpha: 1.0;
        cornerRadius: 0;
        color: white;
 }
 
 DateChooser
 {
        cornerRadius: 0; /* pixels */
        headerColors: black, black;
        borderColor: black;
        themeColor: black;
        todayColor: red;
        todayStyleName: myTodayStyleName;
        headerStyleName: myHeaderStyleName;
        weekDayStyleName: myWeekDayStyleName;
        dropShadowEnabled: true;
 }
 
 .myTodayStyleName
 {
        color: white;
 }
 
 .myWeekDayStyleName
 {
        fontWeight: normal;
 }
 
 .myHeaderStyleName
 {
        color: red;
        fontSize: 16;
        fontWeight: bold;
 }
```

**참고 항목**

[Remoting을 사용하여 AEM Forms 호출(AEM Forms에 대해 더 이상 사용되지 않음) AEM Forms](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[문서 처리(AEM Forms에 대해 더 이상 사용되지 않음) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flex 라이브러리 파일 포함](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Remoting AEM Forms을 사용하여(AEM Forms에 대해 더 이상 사용되지 않음) 안전하지 않은 문서를 전달하여 짧은 기간 동안의 프로세스 호출](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flex로 구축한 클라이언트 애플리케이션 인증](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Remoting을 사용하여 프로세스를 호출하는 보안 문서 전달](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
