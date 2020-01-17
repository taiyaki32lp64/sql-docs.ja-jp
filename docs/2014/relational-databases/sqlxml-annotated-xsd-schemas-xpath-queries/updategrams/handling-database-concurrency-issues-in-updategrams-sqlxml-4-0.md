---
title: アップデート グラム (SQLXML 4.0) でデータベースの同時実行の問題の処理 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: b561de7d655001e2c62f7c85e57cc7eb098af12d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014749"
---
# <a name="handling-database-concurrency-issues-in-updategrams-sqlxml-40"></a>アップデートグラムでのデータベース コンカレンシーに関する問題への対応 (SQLXML 4.0)
  アップデートグラムは、他のデータベースの更新メカニズムと同様に、マルチサーバー環境での同時実行更新に対応しています。 アップデートグラムではオプティミスティック コンカレンシーが使用されます。この機能では、更新するデータがデータベースからの読み取り後に他のユーザー アプリケーションによって変更され邸内事を確認するために、選択フィールド データの比較がスナップショットとして使用されます。 アップデート グラムでこれらのスナップショット値を含める、 **\<する前に >** アップデート グラムのブロック。 指定されている値をチェックするアップデート グラムでデータベースを更新する前に、 **\<する前に >** 更新が有効であることを確認するデータベースの現在の値に対してブロック。  
  
 アップデートグラムでは、オプティミスティック コンカレンシーによる保護を低 (なし)、中、高の 3 レベルで使用できます。 必要な保護レベルを適用するには、アップデートグラムで適切に指定する必要があります。  
  
## <a name="lowest-level-of-protection"></a>最低レベルの保護  
 このレベルでは、最後のデータベースの読み取り後に行われたその他の更新を無視して更新操作を実行します。 このような場合は、主キー列でのみを指定する、 **\<する前に >** 、レコードを識別するためにブロックし、で更新された情報を指定する、 **\<後 >** ブロックです。  
  
 たとえば次のアップデートグラムでは、以前の電話番号に関係なく、新しい連絡先の電話番号として正しい番号を設定できます。 通知方法、 **\<する前に >** ブロックが主キー列 (ContactID) だけを指定します。  
  
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
  
 で更新している列の主キー列を指定することで、この保護レベルを取得できます、 **\<する前に >** ブロックします。  
  
 たとえば、このアップデートグラムでは、Person.Contact テーブルで、ContactID が 1 となっている連絡先の Phone 列の値が変更されます。 **\<する前に >** ブロックを指定します、 **Phone**この属性値が更新された値を適用する前に、データベース内の対応する列の値を一致させる属性.  
  
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
  
-   内のテーブルの追加の列の指定、 **\<する前に >** ブロックします。  
  
     追加の列を指定する場合、 **\<する前に >** ブロック、アップデート グラムでは、更新プログラムを適用する前に、データベースに含まれていた値を持つこれらの列に対して指定されている値を比較します。 トランザクションで読み取ったレコード列のいずれかが変更されている場合、アップデートグラムで更新は実行されません。  
  
     たとえば、次のアップデート グラムの勤務時間名をソフトウェア更新プログラムがで追加の列 (StartTime、EndTime) を指定します、 **\<する前に >** ブロック、高いレベルの同時実行に対する保護が要求されています更新します。  
  
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
  
     この例では、最高レベルの保護を指定のレコードのすべての列の値を指定することによって、 **\<する前に >** ブロックします。  
  
-   Timestamp 列を指定 (該当する場合)、 **\<する前に >** ブロックします。  
  
     すべてのレコード列を指定する代わりに、 `<before`> ブロックを指定するだけのタイムスタンプ列 (テーブルには 1 つ) の場合に主キー列と共に、 **\<する前に >** ブロックします。 データベースでは、レコードが更新されるたびにタイムスタンプ列が一意な値に更新されます。 この場合、アップデートグラムではタイムスタンプの値とデータベースの対応する値を比較します。 データベースに格納されているタイムスタンプ値はバイナリ値です。 したがって、スキーマ内にタイムスタンプ列を `dt:type="bin.hex"`、`dt:type="bin.base64"`、または `sql:datatype="timestamp"` のように指定する必要があります。 (どちらかを指定することができます、`xml`データ型、または[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型です)。  
  
#### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  このテーブルを作成、 **tempdb**データベース。  
  
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
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 これは、同等の XDR スキーマです。  
  
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
 [アップデート グラムのセキュリティに関する考慮事項&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
