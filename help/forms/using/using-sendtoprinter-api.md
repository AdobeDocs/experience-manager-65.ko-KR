---
title: sendToPrinter API 사용
description: sendToPrinter 서비스를 사용하여 문서를 프린터로 보냅니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services
source-git-commit: 744cfcee691ea71f33cd56509f65d4f640d4c6e3
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 14%

---

# sendToPrinter API 사용 {#using-the-sendtoprinter-api}

## 개요 {#overview}

AEM Forms에서 SendToPrinter 서비스를 사용하여 문서를 프린터로 보낼 수 있습니다. SendToPrinter 서비스는 다음과 같은 인쇄 액세스 메커니즘을 지원합니다.

* **직접 접근 가능한 프린터** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **간접 액세스 가능 프린터** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

  문서를 프린터로 보낼 때 다음 인쇄 프로토콜 중 하나를 지정합니다.

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**다이렉트 IP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **공유 프린터** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIF**: 출력 서비스가 CIF(Common Internet File System) 인쇄 프로토콜을 지원합니다.

## SendToPrinter 서비스 사용 {#using-sendtoprinter-service}

아래 표에는 다음이 나와 있습니다.

* 다양한 프로토콜에 사용할 printerName 또는 printServer에 대한 정보입니다.
* 프린터가 프린터 서버 URI와 프린터의 이름 조합의 다양한 조합에 대해 반환하는 값 또는 예외

| 프로토콜(액세스 메커니즘) | 인쇄 서버 URI(PrinterSpec.printServer) | 프린터 이름(PrinterSpec.printerName) | 결과 |
|--- |--- |--- |--- |
| SharedPrinter | 임의 | 비어 있음 | 예외: 필수 인수 sPrinterName은 비워 둘 수 없습니다. |
| SharedPrinter | 임의 | 잘못됨 | 프린터를 찾을 수 없다는 예외가 나타납니다. |
| SharedPrinter | 임의 | 유효 | 인쇄 작업이 완료되었습니다. |
| LPD | 비어 있음 | 임의 | 필수 인수 sPrintServerUri를 비워 둘 수 없다는 예외가 발생했습니다. |
| LPD | 잘못됨 | 비어 있음 | 필수 인수 sPrinterName을 비워 둘 수 없다는 예외가 발생했습니다. |
| LPD | 잘못됨 | 비어 있지 않음 | sPrintServerUri를 찾을 수 없다는 예외가 발생했습니다. |
| LPD | 유효 | 잘못됨 | 프린터를 찾을 수 없다는 예외 사항입니다. |
| LPD | 유효 | 유효 | 인쇄 작업이 정상적으로 완료되었습니다. |
| CUPS | 비어 있음 | 임의 | 필수 인수 sPrintServerUri를 비워 둘 수 없다는 예외가 발생했습니다. |
| CUPS | 잘못됨 | 임의 | 프린터를 찾을 수 없다는 예외 사항입니다. |
| CUPS | 유효 | 임의 | 인쇄 작업이 완료되었습니다. |
| DirectIP | 비어 있음 | 임의 | 필수 인수 sPrintServerUri를 비워 둘 수 없다는 예외가 발생했습니다. |
| DirectIP | 잘못됨 | 임의 | 프린터를 찾을 수 없다는 예외 사항입니다. |
| DirectIP | 유효 | 임의 | 인쇄 작업이 완료되었습니다. |
| CIFS | 유효 | 비어 있음 | 인쇄 작업이 완료되었습니다. |
| CIFS | 잘못됨 | 임의 | CIF을 사용하여 인쇄하는 도중 알 수 없는 오류가 발생했습니다. |
| CIFS | 비어 있음 | 임의 | 필수 인수 sPrintServerUri를 비워 둘 수 없다는 예외가 발생했습니다. |

## 인증 지원 {#authentication-support}

인증은 CIF 인쇄에만 지원됩니다. 인증하려면 PrinterSpec에 사용자 이름/암호/도메인을 입력합니다. 다음 단계를 수행하여 AEM Granite CyprtoSupport 서비스를 사용하여 암호를 암호화할 수 있습니다.

1. https://으로 이동&lt;server>:&lt;port>/system/console.

1. 다음으로 이동 **[!UICONTROL 기본]** > **[!UICONTROL 암호화 지원]**.

1. 일반 텍스트를 입력하고 **[!UICONTROL Protect]**.
