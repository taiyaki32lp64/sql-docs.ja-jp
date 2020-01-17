---
title: マネージ クラス SQLXML を使用して、DiffGram の実行 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 3d8756bb3dc7b030541159c2aa127162907aa4b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013053"
---
# <a name="executing-a-diffgram-by-using-sqlxml-managed-classes"></a>SQLXML マネージド クラスを使用した、DiffGram の実行
  この例で DiffGram ファイルを実行する方法を示しています、[!INCLUDE[msCoName](../../../includes/msconame-md.md)]データを適用する .NET Framework 環境に更新[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]SQLXML マネージ クラス (Microsoft.Data.SqlXml) を使用してテーブルします。  
  
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
  
 **\<する前に >** ブロックが含まれています、 **\<顧客 >** 要素 (**diffgr:id ="Customer1"** )。 **\<DataInstance >** ブロックに含まれる、対応する **\<顧客 >** 要素と同じ **id**します。 **\<顧客 >** 内の要素、 **\<NewDataSet >** も指定 **diffgr:hasChanges ="modified"** します。 これは更新操作であることを示し、Cust テーブルの顧客レコードは指定に従って更新されます。 その場合、 **diffgr:hasChanges**属性が指定されていない、DiffGram の処理ロジックがこの要素は無視されます、および更新は実行されません。  
  
 次にアプリケーションのコードを c# チュートリアル SQLXML マネージ クラスを使用して、上の DiffGram を実行しで作成することも、2 つのテーブル (Cust、Ord) を更新する方法を示す、 **tempdb**データベース。  
  
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
  
3.  これらのテーブルを作成、 **tempdb**データベース。  
  
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
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
5.  上の DiffGram をコピーして、テキスト ファイルに貼り付け、 手順 1. と同じフォルダーに MyDiffGram.xml として保存します。  
  
6.  上の C# コード (DiffgramSample.cs) を、上の手順で DiffGramSchema.xml と MyDiffGram.xml を保存したフォルダーに保存します。  
  
    > [!NOTE]  
    >  接続文字列の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前は、'`MyServer`' の部分を、インストールされている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの実際の名前に更新する必要があります。  
  
     別のフォルダーにファイルを保存する場合は、コードを編集し、マッピング スキーマの適切なディレクトリ パスを指定する必要があります。  
  
7.  コードをコンパイルします。 コマンド プロンプトでコードをコンパイルするには、次を使用します。  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DiffgramSample.cs  
    ```  
  
     これにより、実行可能ファイル (DiffgramSample.exe) が作成されます。  
  
8.  コマンド プロンプトで、DiffgramSample.exe を実行します。  
  
## <a name="see-also"></a>参照  
 [DiffGram の例&#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md)  
  
  
