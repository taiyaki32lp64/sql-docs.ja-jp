---
title: SQLXML マネージド クラスを使用した、DiffGram の実行
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], Managed Classes
- SQLXML Managed Classes, DiffGrams
- Managed Classes [SQLXML], DiffGrams
- SQLXML, Managed Classes
ms.assetid: 81c687ca-8c9f-4f58-801f-8dabcc508a06
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c92072290b8f0115470bccae46ab0e5fe111a0b3
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257275"
---
# <a name="executing-a-diffgram-by-using-sqlxml-managed-classes"></a>SQLXML マネージド クラスを使用した、DiffGram の実行
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  この例では、.NET Framework 環境で DiffGram ファイルを[!INCLUDE[msCoName](../../../includes/msconame-md.md)]実行して、SQLXML マネージクラス[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (Microsoft. data. SQLXML) を使用してテーブルにデータ更新を適用する方法を示します。  
  
 この例では、DiffGram で顧客 ALFKI の顧客情報 (CompanyName と ContactName) を更新します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 ** \<Before>** ブロックには、 ** \<Customer>** 要素 (**Customer1**) が含まれています。 ** \<Datainstance>** block には、同じ**id**を持つ対応する** \<Customer>** 要素が含まれています。Newdataset>の** \<customer>** 要素では、[変更後のデータ] を指定することもできます。 **haschanges = "modified"** です。 ** \<** これは更新操作であることを示し、Cust テーブルの顧客レコードは指定に従って更新されます。 DiffGram **: hasChanges**属性が指定されていない場合、diffgram 処理ロジックはこの要素を無視し、更新は実行されないことに注意してください。  
  
 次に示すのは、SQLXML マネージクラスを使用して上記の DiffGram を実行し、2つのテーブル (Cust、Ord) を更新して**tempdb**データベースに作成する方法を示す C# チュートリアルアプリケーションのコードです。  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=MyServer;database=tempdb;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      SqlXmlAdapter ad;  
      // Need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandStream = new FileStream("MyDiffgram.xml", FileMode.Open, FileAccess.Read);  
      cmd.CommandType = SqlXmlCommandType.DiffGram;  
      cmd.SchemaPath = "DiffGramSchema.xml";  
      // Load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
### <a name="to-test-the-application"></a>アプリケーションをテストするには  
  
1.  .NET Framework がコンピューターにインストールされていることを確認します。  
  
2.  次の XSD スキーマ (DiffGramSchema.xml) をフォルダーに保存します。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
     </xsd:annotation>  
     <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
     </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  これらのテーブルを**tempdb**データベースに作成します。  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
4.  次のサンプル データを追加します。  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
5.  上の DiffGram をコピーして、テキスト ファイルに貼り付け、 手順 1. と同じフォルダーに MyDiffGram.xml として保存します。  
  
6.  上の C# コード (DiffgramSample.cs) を、上の手順で DiffGramSchema.xml と MyDiffGram.xml を保存したフォルダーに保存します。  
  
    > [!NOTE]  
    >  接続文字列の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前は、'`MyServer`' の部分を、インストールされている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの実際の名前に更新する必要があります。  
  
     ファイルを別のフォルダーに保存する場合は、コードを編集し、マッピングスキーマの適切なディレクトリパスを指定する必要があります。  
  
7.  コードをコンパイルします。 コマンド プロンプトでコードをコンパイルするには、次を使用します。  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DiffgramSample.cs  
    ```  
  
     これにより、実行可能ファイル (DiffgramSample.exe) が作成されます。  
  
8.  コマンド プロンプトで、DiffgramSample.exe を実行します。  
  
## <a name="see-also"></a>参照  
 [&#40;SQLXML 4.0&#41;の DiffGram の例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)  
  
  
