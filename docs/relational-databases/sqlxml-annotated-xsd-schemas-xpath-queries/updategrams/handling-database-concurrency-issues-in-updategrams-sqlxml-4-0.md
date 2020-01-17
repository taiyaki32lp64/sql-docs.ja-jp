---
title: アップデートグラムでのデータベースの同時実行に関する問題 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- <before> block
- low concurrency protection
- database concurrency [SQLXML]
- timestamp column [SQLXML]
- updategrams [SQLXML], database concurrency
- high concurrency protection [SQLXML]
- optimistic concurrency control
- concurrency [SQLXML]
- intermediate concurrency protection [SQLXML]
ms.assetid: d4b908d1-b25b-4ad9-8478-9cd882e8c44e
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eb77a6499472d116ad3b30028ce1566b68b81122
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241287"
---
# <a name="handling-database-concurrency-issues-in-updategrams-sqlxml-40"></a>アップデートグラムでのデータベース コンカレンシーに関する問題への対応 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  アップデートグラムは、他のデータベースの更新メカニズムと同様に、マルチサーバー環境での同時実行更新に対応しています。 アップデートグラムではオプティミスティック コンカレンシーが使用されます。この機能では、更新するデータがデータベースからの読み取り後に他のユーザー アプリケーションによって変更され邸内事を確認するために、選択フィールド データの比較がスナップショットとして使用されます。 アップデートグラムでは、これらのスナップショット値がアップデートグラムの** \<before>** ブロックに含まれています。 アップデートグラムでは、データベースを更新する前に、更新プログラムが** \<** 有効であることを確認するために、データベース内の現在の値に対して before>block に指定されている値をチェックします。  
  
 アップデートグラムでは、オプティミスティック コンカレンシーによる保護を低 (なし)、中、高の 3 レベルで使用できます。 必要な保護レベルを適用するには、アップデートグラムで適切に指定する必要があります。  
  
## <a name="lowest-level-of-protection"></a>最低レベルの保護  
 このレベルでは、最後のデータベースの読み取り後に行われたその他の更新を無視して更新操作を実行します。 このような場合は、 ** \<before>** block で主キー列のみを指定してレコードを識別し、更新** \<後**の情報を after>ブロックに指定します。  
  
 たとえば次のアップデートグラムでは、以前の電話番号に関係なく、新しい連絡先の電話番号として正しい番号を設定できます。 ** \<Before>** block によって、主キー列 (ContactID) のみが指定されていることに注意してください。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="intermediate-level-of-protection"></a>中レベルの保護  
 この保護レベルでは、トランザクションで読み取ったレコードが他のトランザクションによって変更されていないことを確認するため、アップデートグラムにおいて、更新するデータの現在の値とデータベース列の値が比較されます。  
  
 この保護レベルを取得するには、主キー列と更新する列を [ ** \<before>** block] で指定します。  
  
 たとえば、このアップデートグラムでは、Person.Contact テーブルで、ContactID が 1 となっている連絡先の Phone 列の値が変更されます。 ** \<Before>** block は**Phone**属性を指定して、更新された値を適用する前に、この属性値がデータベース内の対応する列の値と一致するようにします。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" Phone="398-555-0132" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="high-level-of-protection"></a>高レベルの保護  
 高レベルの保護では、アプリケーションで最後に読み取ったレコードが変化していない (他のトランザクションによって変更されていない) ことが確認されます。  
  
 同時実行更新に高レベルの保護を適用するには、次の 2 つの方法があります。  
  
-   テーブルの追加の列を [ ** \<before>** ブロックの前に指定します。  
  
     [ ** \<Before>** ] ブロックで追加の列を指定した場合、アップデートグラムでは、更新プログラムを適用する前に、これらの列に指定されている値と、データベース内の値が比較されます。 トランザクションで読み取ったレコード列のいずれかが変更されている場合、アップデートグラムで更新は実行されません。  
  
     たとえば、次のアップデートグラムでは、シフト名を更新しますが、 ** \<前の>** ブロックで追加の列 (StartTime、EndTime) を指定することで、同時更新に対するより高いレベルの保護を要求します。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1"   
                 Name="Day"   
                 StartTime="1900-01-01 07:00:00.000"   
                 EndTime="1900-01-01 15:00:00.000" />  
    </updg:before>  
    <updg:after>  
       <HumanResources.Shift Name="Morning" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
     この例では、 ** \<[before>** ブロックのレコードのすべての列の値を指定することにより、最も高いレベルの保護を指定します。  
  
-   [ ** \<Before>** block] で timestamp 列 (使用可能な場合) を指定します。  
  
     [ ** \<Before**> block] ですべてのレコード列を指定する代わりに、timestamp 列 (テーブルにテーブルがある場合) と、 ** \<[before>** block] の主キー列を指定するだけで済みます。 データベースでは、レコードが更新されるたびにタイムスタンプ列が一意な値に更新されます。 この場合、アップデートグラムではタイムスタンプの値とデータベースの対応する値を比較します。 データベースに格納されているタイムスタンプ値はバイナリ値です。 したがって、timestamp 列は、スキーマで**dt: type = "bin. hex"**、 **dt: type = "bin. base64"**、または**sql: datatype = "timestamp"** として指定する必要があります。 ( **Xml**データ型または[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型のいずれかを指定できます)。  
  
#### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  **Tempdb**データベースに次のテーブルを作成します。  
  
    ```  
    USE tempdb  
    CREATE TABLE Customer (  
                 CustomerID  varchar(5),  
                 ContactName varchar(20),  
                 LastUpdated timestamp)  
    ```  
  
2.  次のサンプル レコードを追加します。  
  
    ```  
    INSERT INTO Customer (CustomerID, ContactName) VALUES   
                         ('C1', 'Andrew Fuller')  
    ```  
  
3.  次の XSD スキーマをコピーして、メモ帳に貼り付け、 ConcurrencySampleSchema.xml として保存します。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Customer" sql:relation="Customer" >  
       <xsd:complexType>  
            <xsd:attribute name="CustomerID"    
                           sql:field="CustomerID"   
                           type="xsd:string" />   
  
            <xsd:attribute name="ContactName"    
                           sql:field="ContactName"   
                           type="xsd:string" />  
  
            <xsd:attribute name="LastUpdated"   
                           sql:field="LastUpdated"   
                           type="xsd:hexBinary"   
                 sql:datatype="timestamp" />  
  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
4.  次のアップデートグラム コードをメモ帳にコピーして、前の手順で作成したスキーマと同じディレクトリに ConcurrencySampleTemplate.xml として保存します。 次の LastUpdated のタイムスタンプ値は例の Customer テーブルとは異なるため、LastUpdated の実際の値をテーブルからコピーし、アップデートグラムに貼り付けてください。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
    <updg:before>  
       <Customer CustomerID="C1"   
                 LastUpdated = "0x00000000000007D1" />  
    </updg:before>  
    <updg:after>  
       <Customer ContactName="Robert King" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 これは、これと同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="ContactName" />  
    <AttributeType name="LastUpdated"  dt:type="bin.hex"   
                                       sql:datatype="timestamp" />  
    <attribute type="CustomerID" />  
    <attribute type="ContactName" />  
    <attribute type="LastUpdated" />  
</ElementType>  
</Schema>  
```  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0&#41;&#40;アップデートグラムのセキュリティに関する考慮事項](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
