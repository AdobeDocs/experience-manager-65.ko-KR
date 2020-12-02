---
title: sendToPrinter API 사용
seo-title: sendToPrinter API 사용
description: sendToPrinter 서비스를 사용하여 문서를 프린터로 보냅니다.
seo-description: sendToPrinter 서비스를 사용하여 문서를 프린터로 보냅니다.
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 13%

---


# sendToPrinter API {#using-the-sendtoprinter-api} 사용

## 개요 {#overview}

AEM Forms에서는 SendToPrinter 서비스를 사용하여 문서를 프린터로 전송할 수 있습니다. SendToPrinter 서비스는 다음과 같은 인쇄 액세스 메커니즘을 지원합니다.

* **직접 액세스 가능한 프린터** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **간접 액세스 가능한 프린터** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   문서를 프린터로 보낼 때 다음과 같은 인쇄 프로토콜 중 하나를 지정합니다.

   * **컵** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**:출력 서비스는 CIFS(Common Internet File System) 인쇄 프로토콜을 지원합니다.

## SendToPrinter 서비스 {#using-sendtoprinter-service} 사용

아래 표는 다음과 같습니다.

* 다양한 프로토콜에 사용할 printerName 또는 printServer에 대한 정보입니다.
* 프린터 서버 URI와 프린터 이름의 다양한 조합에 대해 프린터가 반환하는 값 또는 예외

| 프로토콜(액세스 메커니즘) | 인쇄 서버 URI(PrinterSpec.printServer) | 프린터 이름(PrinterSpec.printerName) | 결과 |
|--- |--- |--- |--- |
| SharedPrinter | 임의 | 비어 있음 | 예외:필수 인수 sPrinterName은 비워 둘 수 없습니다. |
| SharedPrinter | 임의 | 잘못됨 | 프린터를 찾을 수 없다는 예외가 있습니다. |
| SharedPrinter | 임의 | 유효 | 성공적인 인쇄 작업 |
| LPD | 비어 있음 | 임의 | 필수 인수 sPrintServerUri를 비워 둘 수 없다는 예외를 제외하고, |
| LPD | 잘못됨 | 비어 있음 | 필수 인수 sPrinterName을 비워 둘 수 없다는 예외를 나타냅니다. |
| LPD | 잘못됨 | 비어 있지 않음 | sPrintServerUri를 찾을 수 없다는 예외 |
| LPD | 유효 | 잘못됨 | 프린터를 찾을 수 없다는 예외 사항. |
| LPD | 유효 | 유효 | 성공적인 인쇄 작업 |
| CUPS | 비어 있음 | 임의 | 필수 인수 sPrintServerUri를 비워 둘 수 없다는 예외를 제외하고, |
| 컵 | 잘못됨 | 임의 | 프린터를 찾을 수 없다는 예외 사항. |
| 컵 | 유효 | 임의 | 성공적인 인쇄 작업 |
| DirectIP | 비어 있음 | 임의 | 필수 인수 sPrintServerUri를 비워 둘 수 없다는 예외를 제외하고, |
| DirectIP | 잘못됨 | 임의 | 프린터를 찾을 수 없다는 예외 사항. |
| DirectIP | 유효 | 임의 | 성공적인 인쇄 작업 |
| CIFS | 유효 | 비어 있음 | 성공적인 인쇄 작업 |
| CIFS | 잘못됨 | 임의 | CIFS를 사용하여 인쇄하는 동안 알 수 없는 오류가 발생했습니다. |
| CIFS | 비어 있음 | 임의 | 필수 인수 sPrintServerUri를 비워 둘 수 없다는 예외를 제외하고, |

## 인증 지원 {#authentication-support}

인증은 CIFS 인쇄에만 지원됩니다. 인증하려면 PrinterSpec에 사용자 이름/암호/도메인을 입력합니다. 다음 단계를 수행하여 AEM Granite CyprtoSupport Service를 사용하여 암호를 암호화할 수 있습니다.

1. https://&lt;server>:&lt;port>/system/console로 이동합니다.

1. **[!UICONTROL Main]** > **[!UICONTROL Crypto 지원]**&#x200B;으로 이동합니다.

1. 일반 텍스트를 입력하고 **[!UICONTROL Protect]**&#x200B;을 클릭합니다.

