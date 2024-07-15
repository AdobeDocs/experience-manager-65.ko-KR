---
title: "자습서: AEM Forms에서 양식 데이터 모델 만들기"
description: 대화형 커뮤니케이션용 양식 데이터 모델 만들기
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: c8a6037c-46bd-4058-8314-61cb925ba5a8
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2684'
ht-degree: 0%

---

# 자습서: AEM Forms에서 양식 데이터 모델 만들기{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

이 자습서는 [첫 번째 대화형 통신 만들기](/help/forms/using/create-your-first-interactive-communication.md) 시리즈의 단계입니다. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하려면 연대순으로 시리즈를 따르는 것이 좋습니다.

## 튜토리얼 기본 정보 {#about-the-tutorial}

AEM Forms 데이터 통합 모듈을 사용하면 AEM 사용자 프로필, RESTful 웹 서비스, SOAP 기반 웹 서비스, OData 서비스 및 관계형 데이터베이스와 같은 서로 다른 백엔드 데이터 소스에서 양식 데이터 모델을 만들 수 있습니다. 양식 데이터 모델에서 데이터 모델 개체 및 서비스를 구성하고 적응형 양식과 연결할 수 있습니다. 적응형 양식 필드는 데이터 모델 개체 속성에 바인딩됩니다. 이 서비스를 사용하면 적응형 양식을 미리 채우고 제출된 양식 데이터를 데이터 모델 개체에 다시 쓸 수 있습니다.

양식 데이터 통합 및 양식 데이터 모델에 대한 자세한 내용은 [AEM Forms 데이터 통합](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)을 참조하십시오.

이 자습서에서는 양식 데이터 모델을 대화형 통신과 준비, 만들기, 구성 및 연결하는 단계를 안내합니다. 이 자습서를 마치면 다음을 수행할 수 있습니다.

* [데이터베이스 설정](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [MySQL 데이터베이스를 데이터 소스로 구성](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [양식 데이터 모델 만들기](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [양식 데이터 모델 구성](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [양식 데이터 모델 테스트](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

양식 데이터 모델은 다음과 유사합니다.

![양식 데이터 모델](assets/form_data_model_callouts_new.png)

**A.** 구성된 데이터 원본 **B.** 데이터 원본 스키마 **C.** 사용 가능한 서비스 **D.** 데이터 모델 개체 **E.** 구성된 서비스

## 사전 요구 사항 {#prerequisites}

시작하기 전에 다음을 확인하십시오.

* [데이터베이스 설정](../../forms/using/create-form-data-model0.md#step-set-up-the-database) 섹션에 명시된 샘플 데이터가 있는 MySQL 데이터베이스입니다.
* [JDBC 데이터베이스 드라이버 번들](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)에 설명된 대로 MySQL JDBC 드라이버용 OSGi 번들

## 1단계: 데이터베이스 설정 {#step-set-up-the-database}

대화형 통신을 만들려면 데이터베이스가 필수적입니다. 이 자습서에서는 데이터베이스를 사용하여 대화형 통신의 양식 데이터 모델 및 지속성 기능을 표시합니다. 고객, 청구서 및 호출 테이블을 포함하는 데이터베이스를 설정합니다.
다음 이미지는 customer 테이블에 대한 샘플 데이터를 보여 줍니다.

![sample_data_cust](assets/sample_data_cust.png)

다음 DDL 문을 사용하여 데이터베이스에 **customer** 테이블을 만듭니다.

```sql
CREATE TABLE `customer` (
   `mobilenum` int(11) NOT NULL,
   `name` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `alternatemobilenumber` int(11) DEFAULT NULL,
   `relationshipnumber` int(11) DEFAULT NULL,
   `customerplan` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`mobilenum`),
   UNIQUE KEY `mobilenum_UNIQUE` (`mobilenum`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

다음 DDL 문을 사용하여 데이터베이스에 **bills** 테이블을 만듭니다.

```sql
CREATE TABLE `bills` (
   `billplan` varchar(45) NOT NULL,
   `latepayment` decimal(4,2) NOT NULL,
   `monthlycharges` decimal(4,2) NOT NULL,
   `billdate` date NOT NULL,
   `billperiod` varchar(45) NOT NULL,
   `prevbal` decimal(4,2) NOT NULL,
   `callcharges` decimal(4,2) NOT NULL,
   `confcallcharges` decimal(4,2) NOT NULL,
   `smscharges` decimal(4,2) NOT NULL,
   `internetcharges` decimal(4,2) NOT NULL,
   `roamingnational` decimal(4,2) NOT NULL,
   `roamingintnl` decimal(4,2) NOT NULL,
   `vas` decimal(4,2) NOT NULL,
   `discounts` decimal(4,2) NOT NULL,
   `tax` decimal(4,2) NOT NULL,
   PRIMARY KEY (`billplan`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

다음 DDL 문을 사용하여 데이터베이스에 **calls** 테이블을 만듭니다.

```sql
CREATE TABLE `calls` (
   `mobilenum` int(11) DEFAULT NULL,
   `calldate` date DEFAULT NULL,
   `calltime` varchar(45) DEFAULT NULL,
   `callnumber` int(11) DEFAULT NULL,
   `callduration` varchar(45) DEFAULT NULL,
   `callcharges` decimal(4,2) DEFAULT NULL,
   `calltype` varchar(45) DEFAULT NULL
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

**호출** 테이블에는 통화 날짜, 통화 시간, 통화 번호, 통화 시간, 통화 요금 등 통화 정보가 포함되어 있습니다. **customer** 테이블이 모바일 번호(mobileenum) 필드를 사용하여 호출 테이블에 연결되어 있습니다. **customer** 표에 나열된 각 휴대폰 번호에 대해 **calls** 표에 여러 레코드가 있습니다. 예를 들어 **호출** 테이블을 참조하여 **1457892541** 휴대폰 번호에 대한 통화 정보를 검색할 수 있습니다.

**청구서** 테이블에는 청구서 날짜, 청구서 기간, 월별 청구서 및 전화 요금 등 청구서 세부 정보가 포함되어 있습니다. **customer** 테이블은 청구서 계획 필드를 사용하여 **청구서** 테이블에 연결되어 있습니다. **customer** 테이블에 각 고객과 연결된 플랜이 있습니다. **청구서** 표에는 모든 기존 플랜에 대한 가격 정보가 포함되어 있습니다. 예를 들어 **고객** 테이블에서 **Sarah**&#x200B;에 대한 플랜 세부 정보를 검색하고 해당 세부 정보를 사용하여 **청구서** 테이블에서 가격 세부 정보를 검색할 수 있습니다.

## 2단계: MySQL 데이터베이스를 데이터 소스로 구성 {#step-configure-mysql-database-as-data-source}

다양한 유형의 데이터 소스를 구성하여 양식 데이터 모델을 만들 수 있습니다. 이 자습서에서는 샘플 데이터로 구성되고 채워진 MySQL 데이터베이스를 구성합니다. 지원되는 다른 데이터 원본 및 구성 방법에 대한 자세한 내용은 [AEM Forms 데이터 통합](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)을 참조하세요.

다음을 수행하여 MySQL 데이터베이스를 구성합니다.

1. MySQL 데이터베이스용 JDBC 드라이버를 OSGi 번들로 설치합니다.

   1. AEM Forms 작성자 인스턴스에 관리자로 로그인하고 AEM 웹 콘솔 번들로 이동합니다. 기본 URL은 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)입니다.
   1. **설치/업데이트**&#x200B;를 선택하십시오. **번들 업로드/설치** 대화 상자가 나타납니다.

   1. **파일 선택**&#x200B;을 선택하여 MySQL JDBC 드라이버 OSGi 번들을 찾아 선택합니다. **번들 시작** 및 **패키지 새로 고침**&#x200B;을 선택하고 **설치** 또는 **업데이트**&#x200B;를 선택합니다. MySQL에 대한 Oracle 공사의 JDBC 드라이버가 활성화되어 있는지 확인합니다. 드라이버가 설치되었습니다.

1. MySQL 데이터베이스를 데이터 소스로 구성:

   1. [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)의 AEM 웹 콘솔로 이동합니다.
   1. **Apache Sling 연결의 풀링된 데이터 원본** 구성을 찾습니다. 을(를) 선택하여 편집 모드로 구성을 엽니다.
   1. 구성 대화 상자에서 다음 세부 사항을 지정합니다.

      * **데이터 원본 이름:** 모든 이름을 지정할 수 있습니다. 예를 들어 **MySQL**&#x200B;을(를) 지정합니다.

      * **DataSource 서비스 속성 이름**: DataSource 이름이 포함된 서비스 속성의 이름을 지정하십시오. 데이터 소스 인스턴스를 OSGi 서비스로 등록하는 동안 지정됩니다. 예: **datasource.name**.

      * **JDBC 드라이버 클래스**: JDBC 드라이버의 Java 클래스 이름을 지정합니다. MySQL 데이터베이스의 경우 **com.mysql.jdbc.Driver**&#x200B;를 지정하십시오.

      * **JDBC 연결 URI**: 데이터베이스의 연결 URL을 지정합니다. 포트 3306 및 스키마 텔레카에서 실행되는 MySQL 데이터베이스의 경우 URL은 `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`입니다.
      * 데이터베이스의 **사용자 이름:** 사용자 이름. JDBC 드라이버가 데이터베이스와의 연결을 설정할 수 있도록 해야 합니다.
      * 데이터베이스의 **암호:** 암호입니다. JDBC 드라이버가 데이터베이스와의 연결을 설정할 수 있도록 해야 합니다.
      * **차입 시 테스트:** **차입 시 테스트** 옵션을 활성화합니다.

      * **반환 시 테스트:** **반환 시 테스트** 옵션을 활성화합니다.

      * **유효성 검사 쿼리:** SQL SELECT 쿼리를 지정하여 풀에서의 연결을 검증하십시오. 쿼리는 하나 이상의 행을 반환해야 합니다. 예를 들어 **고객에서 &#42;을(를) 선택**&#x200B;합니다.

      * **트랜잭션 격리**: 값을 **READ_COMMITTED**(으)로 설정합니다.

   다른 속성은 기본 [값](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html)을 사용하고 **저장**&#x200B;을 선택하세요.

   다음과 유사한 구성이 만들어집니다.

   ![Apache 구성](assets/apache_configuration_new.png)

## 3단계: 양식 데이터 모델 만들기 {#step-create-form-data-model}

AEM Forms은 구성된 데이터 소스에서 [양식 데이터 모드를 만들기](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)할 수 있는 직관적인 사용자 인터페이스를 제공합니다. 양식 데이터 모델에서 여러 데이터 소스를 사용할 수 있습니다. 이 자습서의 사용 사례에서는 MySQL을 데이터 소스로 사용합니다.

양식 데이터 모델을 만들려면 다음을 수행하십시오.

1. AEM 작성자 인스턴스에서 **Forms** > **데이터 통합**&#x200B;으로 이동합니다.
1. **만들기** > **양식 데이터 모델**&#x200B;을(를) 선택합니다.
1. 양식 데이터 모델 만들기 마법사에서 양식 데이터 모델에 대해 **name**&#x200B;을(를) 지정합니다. 예: **FDM_Create_First_IC**. **다음**&#x200B;을 선택합니다.
1. 데이터 소스 선택 화면에 구성된 모든 데이터 소스가 나열됩니다. **MySQL** 데이터 원본을 선택하고 **만들기**&#x200B;를 선택합니다.

   ![MYSQL 데이터 원본](assets/fdm_mysql_data_source_new.png)

1. **완료**&#x200B;를 클릭합니다. **FDM_Create_First_IC** 양식 데이터 모델이 만들어집니다.

## 4단계: 양식 데이터 모델 구성 {#step-configure-form-data-model}

양식 데이터 모델 구성에는 다음이 포함됩니다.

* [데이터 모델 개체 및 서비스 추가](#add-data-model-objects-and-services)
* [데이터 모델 객체에 대해 계산된 하위 등록 정보 생성](#create-computed-child-properties-for-data-model-object)
* [데이터 모델 개체 간 연결 추가](#add-associations-between-data-model-objects)
* [데이터 모델 개체 속성 편집](#edit-data-model-object-properties)
* [데이터 모델 개체에 대한 서비스 구성](#configure-services)

### 데이터 모델 개체 및 서비스 추가 {#add-data-model-objects-and-services}

1. AEM 작성자 인스턴스에서 **Forms** > **데이터 통합**&#x200B;으로 이동합니다. 기본 URL은 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)입니다.
1. 이전에 만든 **FDM_Create_First_IC** 양식 데이터 모델이 여기에 나열됩니다. 선택한 다음 **편집**&#x200B;을 선택합니다.

   선택한 데이터 원본 **MySQL**&#x200B;이(가) **데이터 원본** 창에 표시됩니다.

   FDM에 대한 ![MYSQL 데이터 소스](assets/mysql_fdm_new.png)

1. **MySQL** 데이터 원본 트리를 확장합니다. **teleca** 스키마에서 다음 데이터 모델 개체 및 서비스를 선택하십시오.

   * **데이터 모델 개체**:

      * 청구서
      * 호출
      * 고객

   * **서비스:**

      * get
      * 업데이트

   선택한 데이터 모델 개체 및 서비스를 양식 데이터 모델에 추가하려면 **선택한 항목 추가**&#x200B;를 선택하십시오.

   ![데이터 모델 개체 서비스 선택](assets/select_data_model_object_services_new.png)

   BOM, 호출 및 고객 데이터 모델 개체는 **모델** 탭의 오른쪽 창에 표시됩니다. 가져오기 및 업데이트 서비스가 **서비스** 탭에 표시됩니다.

   ![데이터 모델 개체](assets/data_model_objects_new.png)

### 데이터 모델 개체에 대해 계산된 하위 속성 만들기 {#create-computed-child-properties-for-data-model-object}

계산된 등록 정보는 규칙이나 표현식을 기반으로 값이 계산되는 등록 정보입니다. 규칙을 사용하여 계산된 속성의 값을 리터럴 문자열, 숫자, 수학 표현식의 결과 또는 양식 데이터 모델의 다른 속성 값으로 설정할 수 있습니다.

사용 사례에 따라 다음 수식을 사용하여 **bills** 데이터 모델 개체에 **usageccharges** 자식 계산 속성을 만듭니다.

* 사용 요금 = 통화 요금 + 전화 회의 통화 요금 + SMS 요금 + 모바일 인터넷 요금 + 로밍 국가 + 로밍 국제 + VAS (이러한 모든 속성은 청구서 데이터 모델 개체에 있음)
**usagecharges** 하위 계산 속성에 대한 자세한 내용은 [대화형 통신 계획](/help/forms/using/planning-interactive-communications.md)을 참조하십시오.

다음 단계를 실행하여 BOM 데이터 모델 객체에 대해 계산된 1차 하위 구성요소 등록 정보를 생성합니다.

1. **청구서** 데이터 모델 개체 위쪽에 있는 확인란을 선택하여 선택하고 **자식 속성 만들기**&#x200B;를 선택합니다.
1. **자식 속성 만들기** 창에서:

   1. **usagecharges**&#x200B;을(를) 자식 속성 이름으로 입력하십시오.
   1. **계산됨**&#x200B;을(를) 사용하도록 설정합니다.
   1. **Float**&#x200B;을(를) 유형으로 선택하고 **완료**&#x200B;을(를) 선택하여 하위 속성을 **청구서** 데이터 모델 개체에 추가합니다.

   ![자식 속성 만들기](assets/create_child_property_new.png)

1. **규칙 편집**&#x200B;을 선택하여 규칙 편집기를 엽니다.
1. **만들기**&#x200B;를 선택합니다. **값 설정** 규칙 창이 열립니다.
1. 옵션 선택 드롭다운에서 **수학 식**&#x200B;을 선택합니다.

   ![사용 요금 규칙 편집기](assets/usage_charges_rule_editor_new.png)

1. 수식에서 각각 **callcharges** 및 **confcallcharges**&#x200B;을(를) 첫 번째 및 두 번째 개체로 선택합니다. **plus**&#x200B;을(를) 연산자로 선택합니다. 수학 식 내에서 선택하고 **식 확장**&#x200B;을 선택하여 **smscharges**, **internetcharges**, **roamingnational**, **roamingninnl** 및 **vas** 개체를 식에 추가합니다.

   다음 이미지는 규칙 편집기의 수학 표현식을 보여 줍니다.

   ![사용 요금 규칙](assets/usage_charges_rule_all_new.png)

1. **완료**&#x200B;를 선택합니다. 규칙이 규칙 편집기에서 만들어집니다.
1. **닫기**&#x200B;를 선택하여 규칙 편집기 창을 닫습니다.

### 데이터 모델 개체 간 연결 추가 {#add-associations-between-data-model-objects}

데이터 모델 개체가 정의되면 개체 간에 연결을 작성할 수 있습니다. 연결은 일대일 또는 일대다일 수 있습니다. 예를 들어 한 직원에 여러 개의 종속 항목이 연결되어 있을 수 있습니다. 일대다 연결이라고 하며 연결된 데이터 모델 개체를 연결하는 선에 1:n으로 표시됩니다. 그러나 연관이 지정된 직원 ID에 대해 고유한 직원 이름을 반환하는 경우 이를 일대일 연관이라고 합니다.

데이터 소스의 연관된 데이터 모델 객체를 양식 데이터 모델에 추가하면 해당 연관이 유지되어 화살표 선으로 연결된 상태로 표시됩니다.

사용 사례에 따라 데이터 모델 개체 간에 다음과 같은 연결을 만듭니다.

| 연결 | 데이터 모델 개체 |
|---|---|
| 1:n | customer:calls(여러 번의 호출이 월별 청구서에서 고객과 연결될 수 있음) |
| 1:1 | 고객:청구서(한 개의 청구서가 특정 달의 고객과 연관되어 있음) |

데이터 모델 개체 간의 연결을 만들려면 다음 단계를 수행하십시오.

1. **고객** 데이터 모델 개체 위쪽에 있는 확인란을 선택하여 선택하고 **연결 추가**&#x200B;를 선택합니다. **연결 추가** 속성 창이 열립니다.
1. **연결 추가** 창에서:

   * 연결의 제목을 지정합니다. 선택 필드입니다.
   * **Type** 드롭다운 목록에서 **일대다**&#x200B;을(를) 선택합니다.

   * **모델 개체** 드롭다운 목록에서 **호출**&#x200B;을(를) 선택합니다.

   * **서비스** 드롭다운 목록에서 **get**&#x200B;을(를) 선택합니다.

   * 속성을 사용하여 **고객** 데이터 모델 개체를 **호출** 데이터 모델 개체에 연결하려면 **추가**&#x200B;를 선택하십시오. 사용 사례에 따라 호출 데이터 모델 개체는 고객 데이터 모델 개체의 모바일 번호 속성에 연결되어 있어야 합니다. **인수 추가** 대화 상자가 열립니다.

   ![연결 추가](assets/add_association_new.png)

1. **인수 추가** 대화 상자에서 다음 작업을 수행합니다.

   * **이름** 드롭다운 목록에서 **mobileenum**을(를) 선택합니다. 모바일 번호 속성은 고객이 사용할 수 있고 데이터 모델 개체를 호출하는 공통 속성입니다. 따라서 이 데이터 모델은 고객과 호출 데이터 모델 개체 간의 연결을 만드는 데 사용됩니다.
고객 데이터 모델 개체에서 사용할 수 있는 각 모바일 번호에 대해 호출 테이블에서 사용할 수 있는 여러 호출 레코드가 있습니다.

   * 인수에 대한 선택적 제목 및 설명을 지정합니다.
   * **바인딩 대상** 드롭다운 목록에서 **고객**&#x200B;을(를) 선택합니다.

   * **바인딩 값** 드롭다운 목록에서 **mobileenum**&#x200B;을(를) 선택합니다.

   * **추가**&#x200B;를 선택합니다.

   ![인수에 대한 연결 추가](assets/add_association_argument_new.png)

   mobileenum 속성은 **인수** 섹션에 표시됩니다.

   ![인수 연결 추가](assets/add_argument_association_new.png)

1. 고객과 호출 데이터 모델 개체 간에 1:n 연결을 만들려면 **완료**&#x200B;를 선택하십시오.

   고객과 호출 데이터 모델 객체 간의 연관을 생성했으면 고객과 청구서 데이터 모델 객체 간의 1:1 연관을 생성합니다.

1. **고객** 데이터 모델 개체 위쪽에 있는 확인란을 선택하여 선택하고 **연결 추가**&#x200B;를 선택합니다. **연결 추가** 속성 창이 열립니다.
1. **연결 추가** 창에서:

   * 연결의 제목을 지정합니다. 선택 필드입니다.
   * **유형** 드롭다운 목록에서 **일대일**&#x200B;을(를) 선택합니다.

   * **모델 개체** 드롭다운 목록에서 **청구서**&#x200B;을(를) 선택하십시오.

   * **서비스** 드롭다운 목록에서 **get**&#x200B;을(를) 선택합니다. BOM 테이블의 기본 키인 **billplan** 속성은 **인수** 섹션에서 이미 사용할 수 있습니다.
BOM 및 고객 데이터 모델 개체는 각각 BOM(청구서) 및 customerplan(고객) 속성을 사용하여 연결됩니다. 이러한 속성 사이에 바인딩을 만들어 MySQL 데이터베이스에서 사용 가능한 고객에 대한 계획 세부 정보를 검색합니다.

   * **바인딩 대상** 드롭다운 목록에서 **고객**&#x200B;을(를) 선택합니다.

   * **바인딩 값** 드롭다운 목록에서 **customerplan** 선택

   * **완료**&#x200B;를 선택하여 billplan과 customerplan 속성 간에 바인딩을 만듭니다.

   ![고객 청구서에 대한 연결 추가](assets/add_association_customer_bills_new.png)

   다음 이미지는 데이터 모델 개체와 이들 개체 간의 연결을 만드는 데 사용된 속성 간의 연결을 보여 줍니다.

   ![fdm_associations](assets/fdm_associations.gif)

### 데이터 모델 개체 속성 편집 {#edit-data-model-object-properties}

고객과 다른 데이터 모델 개체 간의 연결을 만든 후 고객 속성을 편집하여 데이터 모델 개체에서 데이터를 검색할 기준 속성을 정의합니다. 사용 사례에 따라 모바일 번호는 고객 데이터 모델 개체에서 데이터를 검색하는 속성으로 사용됩니다.

1. **customer** 데이터 모델 개체 위쪽에 있는 확인란을 선택하여 선택하고 **속성 편집**&#x200B;을 선택합니다. **속성 편집** 창이 열립니다.
1. **customer**&#x200B;을(를) **최상위 수준 모델 개체**(으)로 지정하십시오.
1. **서비스 읽기** 드롭다운 목록에서 **get**&#x200B;을(를) 선택합니다.
1. **인수** 섹션에서:

   * **바인딩 대상** 드롭다운 목록에서 **요청 특성**&#x200B;을(를) 선택합니다.

   * **mobileenum**&#x200B;을(를) 바인딩 값으로 지정합니다.

1. **쓰기** 서비스 드롭다운 목록에서 **업데이트**&#x200B;를 선택합니다.
1. **인수** 섹션에서:

   * **mobileenum** 속성의 경우 **바인딩 대상** 드롭다운 목록에서 **고객**&#x200B;을 선택합니다.

   * **바인딩 값** 드롭다운 목록에서 **mobileenum**&#x200B;을(를) 선택합니다.

1. 속성을 저장하려면 **완료**&#x200B;를 선택하십시오.

   ![서비스 구성](assets/configure_services_customer_new.png)

1. **호출** 데이터 모델 개체 위쪽에 있는 확인란을 선택하여 선택하고 **속성 편집**&#x200B;을 선택합니다. **속성 편집** 창이 열립니다.
1. **호출** 데이터 모델 개체에 대해 **최상위 수준 모델 개체**&#x200B;를 사용하지 않도록 설정하십시오.
1. **완료**&#x200B;를 선택합니다.

   **bills** 데이터 모델 개체에 대한 속성을 구성하려면 8~10단계를 반복합니다.

### 서비스 구성 {#configure-services}

1. **서비스** 탭으로 이동합니다.
1. **get** 서비스를 선택하고 **속성 편집**&#x200B;을 선택합니다. **속성 편집** 창이 열립니다.
1. **속성 편집** 창에서:

   * 선택적 제목 및 설명을 입력합니다.
   * **출력 모델 개체** 드롭다운 목록에서 **고객**&#x200B;을(를) 선택하십시오.

   * 속성을 저장하려면 **완료**&#x200B;를 선택하십시오.

   ![속성 편집](assets/edit_properties_get_details_new.png)

1. **업데이트** 서비스를 선택하고 **속성 편집**&#x200B;을 선택합니다. **속성 편집** 창이 열립니다.
1. **속성 편집** 창에서:

   * 선택적 제목 및 설명을 입력합니다.
   * **입력 모델 개체** 드롭다운 목록에서 **고객**&#x200B;을(를) 선택하십시오.

   * **완료**&#x200B;를 선택합니다.
   * 양식 데이터 모델을 저장하려면 **저장**&#x200B;을(를) 선택하십시오.

   ![서비스 속성 업데이트](assets/update_service_properties_new.png)

## 5단계: 양식 데이터 모델 및 서비스 테스트 {#step-test-form-data-model-and-services}

데이터 모델 개체 및 서비스를 테스트하여 양식 데이터 모델이 올바르게 구성되었는지 확인할 수 있습니다.

테스트를 실행하려면 다음을 수행하십시오.

1. **모델** 탭으로 이동하여 **고객** 데이터 모델 개체를 선택하고 **테스트 모델 개체**&#x200B;를 선택합니다.
1. **테스트 양식 데이터 모델** 창의 **모델/서비스 선택** 드롭다운 목록에서 **모델 개체 읽기**&#x200B;를 선택합니다.
1. **입력** 섹션에서 구성된 MySQL 데이터베이스에 있는 **mobileenum** 속성의 값을 지정하고 **테스트**&#x200B;를 선택합니다.

   지정된 mobileenum 속성과 연결된 고객 세부 정보를 가져와서 아래와 같이 출력 섹션에 표시합니다. 대화 상자를 닫습니다.

   ![데이터 모델 테스트](assets/test_data_model_new.png)

1. **서비스** 탭으로 이동합니다.
1. **get** 서비스를 선택하고 **테스트 서비스를 선택하십시오.**
1. **입력** 섹션에서 구성된 MySQL 데이터베이스에 있는 **mobileenum** 속성의 값을 지정하고 **테스트**&#x200B;를 선택합니다.

   지정된 mobileenum 속성과 연결된 고객 세부 정보를 가져와서 아래와 같이 출력 섹션에 표시합니다. 대화 상자를 닫습니다.

   ![테스트 서비스](assets/test_service_new.png)

### 샘플 데이터 편집 및 저장 {#edit-and-save-sample-data}

양식 데이터 모델 편집기를 사용하면 양식 데이터 모델에서 계산된 속성을 포함한 모든 데이터 모델 개체 속성에 대한 샘플 데이터를 생성할 수 있습니다. 각 속성에 대해 구성된 데이터 유형을 준수하는 무작위 값 세트입니다. 또한 샘플 데이터를 재생성하더라도 보존되는 데이터를 편집하고 저장할 수 있습니다.

샘플 데이터를 생성, 편집 및 저장하려면 다음을 수행합니다.

1. 양식 데이터 모델 페이지에서 **샘플 데이터 편집**&#x200B;을 선택합니다. 샘플 데이터 편집 창에서 샘플 데이터를 생성하고 표시합니다.

   ![샘플 데이터 편집](assets/edit_sample_data_new.png)

1. **샘플 데이터 편집** 창에서 필요에 따라 데이터를 편집하고 **저장**&#x200B;을 선택합니다. 창을 닫습니다.
