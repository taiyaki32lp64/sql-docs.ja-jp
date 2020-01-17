---
title: .NET 環境での SQLXML 機能へのアクセス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], accessing SQLXML functionality
- SQLXML Managed Classes, accessing SQLXML functionality
- DiffGrams [SQLXML], accessing SQLXML functionality
- .NET Framework [SQLXML], accessing SQLXML functionality
ms.assetid: 74744535-2945-414d-9a5b-7e8cc363953a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d4055c52f8d7a9401bf3c9b89754db831d94bb3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012565"
---
# <a name="accessing-sqlxml-functionality-in-the-net-environment"></a>.NET 環境での SQLXML 機能へのアクセス
  この例では、次のことについて説明します。  
  
-   使用する[!INCLUDE[msCoName](../../../includes/msconame-md.md)]SQLXML マネージ クラス (Microsoft.Data.SqlXml) Microsoft へのアクセスに[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]で、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 環境。  
  
-   .NET Framework 環境で生成された DiffGram を使って [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] テーブルにデータ更新を適用する方法  
  
 このアプリケーションでは、XSD スキーマに対して XPath クエリを実行します。 XPath クエリの実行には、連絡先データで構成される XML ドキュメントが返されます (**FirstName**、 **LastName**)。 アプリケーションでは、.NET Framework 環境でこの XML ドキュメントをデータセットに読み込み、 データセットの最初の連絡先の名前を "Susan" に変更します。 このデータセットから DiffGram を生成し、この DiffGram で指定されている更新 (従業員の名前の変更) を、Person.Contact テーブルに適用します。  
  
> [!NOTE]  
>  コードでは、接続文字列に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名を含める必要があります。  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=SqlServerName;database=AdventureWorks;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      DataRow row;  
      SqlXmlAdapter ad;  
      //need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandText = "Con";  
      cmd.CommandType = SqlXmlCommandType.XPath;  
      cmd.SchemaPath = "MySchema.xml";  
      //load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      row = ds.Tables["Con"].Rows[0];  
      row["FName"] = "Susan";  
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
  
 **この例をテストします。**  
  
 この例をテストするには、コンピューターに [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework がインストールされている必要があります。  
  
1.  この XSD スキーマ (MySchema.xml) をフォルダーに保存します。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Con" sql:relation="Person.Contact" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="FName"    
                         sql:field="FirstName"   
                         type="xsd:string" />   
            <xsd:element name="LName"    
                         sql:field="LastName"    
                         type="xsd:string" />  
         </xsd:sequence>  
         <xsd:attribute name="ContactID" type="xsd:integer" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
2.  この例で提供される C# コード (DocSample.cs) を、スキーマと同じフォルダーに保存します。 ファイルを別のフォルダーに保存する場合は、コードを編集して、マッピング スキーマに対する適切なディレクトリ パスを指定する必要があります。  
  
3.  コードをコンパイルします。 コマンド プロンプトでコードをコンパイルするには、次を使用します。  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     これにより、実行可能ファイル (DocSample.exe) が作成されます。  
  
 コマンド プロンプトで、DocSample.exe を実行します。  
  
  
