---
title: PDF 생성에서 WorkBench로 많은 PDF을 인쇄하지 못했습니다.
description: 고객이 WorkBench를 통해 구현된 서비스를 통해 많은 수의 PDF을 생성하면 인쇄 서비스가 실패합니다.
source-git-commit: 9cdf22918f08fe505c3efd0ce43235e3442165d5
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# PDF 생성이 WorkBench를 통해 많은 PDF을 인쇄하지 못했습니다. {#PDF-generation-fails-to-print-a-large-number-of-PDFs-via-WorkBench}

## 문제 {#issue}

고객이 WorkBench를 통해 구현된 서비스를 통해 많은 PDF을 생성하는 경우. 메모리가 부족하여 서비스가 실패합니다. 오류는 다음과 같이 표시됩니다.

`ALC-OUT-002-013: XMLFormFactory, PAexecute failure: "0: Out of Memory"`

<!-- Attached is a simplified template (BollatoRiservatiLandscape_table_simple.xdp) that simulates the problem.
Using the Designer, if we associate the template "BollatoRiservatiLandscape_table_semplice.xdp" with the XML file "BollatoRiservati.xml" during the generation of the pdf, the process comes to occupy 1.6 Gb of RAM. On the server side, with the complete template, the pdf generation process breaks down, occupying 2 GB of RAM.-->

인쇄 요청의 최대 페이지 수가 Windows에서 약 1000페이지로 제한되기 때문입니다. 인쇄 출력이 생성될 때 템플릿과 데이터를 메모리에 로드해야 하고 결과 레이아웃이 메모리에 빌드됩니다. 이는 최종 산출물의 크기에 한계가 있다는 것을 의미한다. 인쇄 출력을 생성하는 프로세스는 32비트 작업이므로 Windows에서는 2GB의 RAM으로 제한됩니다 <!--and 4 GB on UNIX-->.

## 적용 대상 {#applies-to}

솔루션은 AEM Forms에 적용됩니다 <!--JEE Server and AEM Forms on OSGi Server--> x86_win32 XMLFM용

## 솔루션 {#solution}

메모리 사용에 영향을 주는 가장 큰 요소는 양식의 데이터 양입니다. 그러나 메모리 사용에 영향을 덜 미치는 폼 디자인에는 다른 요인이 있습니다. 이러한 요소를 알고 있으면 더 큰 인쇄 출력을 위한 양식을 디자인할 수 있습니다. 다음 섹션은 메모리 풋프린트에 영향을 주는 요소를 우선 순위가 지정된 순서로 나타냅니다.

### 영향 요소 {#impact-factor}

**높음**

1. **선택 하위 양식** - 선택 하위 양식 세트는 조건문을 사용하여 세트 내에서 특정 하위 양식의 표시를 사용자 정의할 수 있는 하위 양식 세트 객체의 변형입니다.
1. **캡션 대신 정적 텍스트 사용** - 거의 모든 필드에서 캡션이 제공되므로 캡션으로 추가 정적 텍스트 대신 해당 텍스트를 사용해야 합니다.
1. 사용 **리치 텍스트 형식(RTF)** 가능한한.

**평균**

메모리 사용을 개선하는 데 도움이 되도록 양식 템플릿을 디자인하는 동안 고려해야 할 추가 요소:

1. 필드에 레이블을 지정하는 정적 텍스트를 사용하지 마십시오. 대신 텍스트 필드에서 캡션을 사용합니다.
2. 직사각형, 선, 물체, 표를 너무 많이 사용하지 마세요.
3. 가능하면 RichText 및 Choice 하위 양식을 사용하지 마십시오.
4. 하위 양식 및 중첩된 하위 양식을 과도하게 사용하지 마십시오.

### 데이터 크기 제한 {#data-size-limitations}

최대 프로세스 메모리에 의해 제한되므로 프로세스에서 사용하는 메모리는 데이터 파일의 크기에만 의존하지 않습니다. 양식 디자인과 매우 밀접하게 연결되어 있으며, 양식에서 병합되는 데이터의 실제 양에 어느 정도 관련되어 있습니다.

양식에 작은 데이터가 있는 작은 노드가 많으면 프로세스에 큰 데이터가 있는 노드가 적은 양식보다 더 많은 메모리가 소모되고(따라서 메모리 부족 속도가 더 빠름),

읽기 [아래 부록](#appendix) 자세한 내용은 테스트 결과가 인쇄 양식(태그가 지정되지 않은 PDF)을 기반으로 하는 경우를 참조하십시오. 태그된 PDF 프로세스 메모리 요구 사항을 사용하면 증가합니다. 또한 양식의 필드 수에 따라 다릅니다. 대략적으로 프로세스 메모리 요구 사항은 태그가 지정되지 않은 PDF의 1.5배를 약간 초과합니다.

### 대화형 Forms {#interactive-forms}

대화형 필드가 다시 렌더링될 때 대화형 양식이 Forms 인쇄보다 더 많은 메모리를 사용합니다. 수행된 테스트에서 메모리 소비는 인쇄 양식에 비해 대략 1.5배만큼 증가했으며 이들은 정적 대화형 양식이었다.

### 이미지 형식 {#image-formats}

Adobe은 특정 이미지 형식을 권장하지 않습니다. 하지만 PNG(Portable Network Graphics)와 같은 작은 이미지 크기를 갖는 것이 좋습니다. 크기가 수백 MegaBytes로 다양한 고해상도의 이미지를 사용하는 것도 바람직하지 않습니다. 또한 압축 해제 시 크기가 수백 MB의 데이터로 확장되는 압축 이미지를 사용하는 것은 바람직하지 않습니다.

### 부록 {#appendix}

**표 예제**

간단한 테이블과 복잡한 테이블에 대한 페이지 수와 데이터 크기를 보여 주는 테이블의 다른 변형이 아래에 표시되어 있습니다.

1. 5000페이지의 PDF이 생성되는 단일 열의 테이블, 데이터 파일 크기는 24MB 및 30K 레코드입니다.

   ![table_single_column](/help/forms/using/assets/table_single_column.png)

1. 800페이지의 PDF이 생성되고 데이터 파일 크기가 4.6MB 및 20K 레코드인 작은 열이 많은 표입니다.
   ![table_many_small_columns](/help/forms/using/assets/table_many_small_columns.png)

1. 작은 열이 많지만 더 큰 xmlTag 이름이 사용되었기 때문에 더 큰 데이터 파일이 있는 테이블입니다.
여기서, 모든 것은 이전과 동일하지만 xml 태그 이름이 크게 만들어져 실제 유효 데이터가 증가하지 않고 데이터 파일 크기가 증가합니다. (따라서) 최종 결과(상한)는 거의 동일합니다. 데이터 파일 크기가 4.6MB에서 44.6MB로 증가했지만, 800페이지의 PDF이 생성되며 데이터 파일 크기는 44.6MB 및 20K 레코드입니다.

   ![table_bigger_xml_tagname](/help/forms/using/assets/table_bigger_xml_tagname.png)

따라서 데이터 파일 크기에 대한 일반적인 상한을 두는 것은 어렵습니다. 각 양식은 고유하므로 메모리 소모는 양식마다 다릅니다.