---
title: SQL クエリの実行 (SQLXML マネージ クラス) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXML Managed Classes
- SQLXML Managed Classes, executing SQL queries
- Managed Classes [SQLXML], executing SQL queries
- ExecuteToStream method
- SQL queries [SQLXML]
ms.assetid: a561ae83-a8b6-4b9b-a819-9b86839546b4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f8e16ff3651b9ce23fafe99137b4905eb3961ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014939"
---
# <a name="executing-sql-queries-sqlxml-managed-classes"></a>SQL クエリの実行 (SQLXML マネージド クラス)
  この例では、次のことを行います。  
  
-   パラメーター (SqlXmlParameter オブジェクト) を作成します。  
  
-   SqlXmlParameter オブジェクトのプロパティ (名前と値) に値を割り当てます。  
  
 この例では、単純な SQL クエリを実行して、従業員の姓、名、および誕生日を取得します。従業員の姓の値はパラメーターとして渡されます。 パラメーターを指定するときに (*LastName*)、Value プロパティのみを設定します。 Name プロパティは設定されていませんので、このクエリでは、パラメーターは位置指定し、名前は必要ありません。  
  
 既定で SqlXmlCommand オブジェクトの CommandType プロパティが**Sql**します。 したがって、このプロパティは明示的に設定しません。  
  
> [!NOTE]  
>  コードでは、接続文字列に Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名を含める必要があります。  
  
 この C# コードは次のとおりです。  
  
```  
using System;  
  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         Stream strm;  
         SqlXmlParameter p;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);        
         cmd.CommandText = "SELECT FirstName, LastName FROM Person.Contact WHERE LastName=? For XML Auto";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         string strResult;  
         try   
         {  
            strm = cmd.ExecuteStream();  
            strm.Position = 0;  
            using(StreamReader sr = new StreamReader(strm))  
            {  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         catch (SqlXmlException e)  
         {  
            //in case of an error, this prints error returned.  
            e.ErrorStream.Position=0;  
            strResult=new StreamReader(e.ErrorStream).ReadToEnd();  
            System.Console.WriteLine(strResult);  
         }  
  
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
  
1.  このトピックで提供される C# コード (DocSample.cs) をフォルダーに保存します。  
  
2.  コードをコンパイルします。 コマンド プロンプトでコードをコンパイルするには、次を使用します。  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     これにより、実行可能ファイル (DocSample.exe) が作成されます。  
  
3.  コマンド プロンプトで、DocSample.exe を実行します。  
  
 この例をテストするには、コンピューターに [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework がインストールされている必要があります。  
  
 コマンド テキストとして SQL クエリを指定する代わりに、次のコード フラグメントのようなテンプレートを指定して、(同様にテンプレートとして提供されている) アップデートグラムを実行し、顧客レコードを挿入することもできます。 テンプレートとアップデートグラムはファイル内に指定し、ファイルとして実行できます。 詳細については、次を参照してください。 [CommandText プロパティを使用してテンプレート ファイルを実行する](executing-template-files-by-using-the-commandtext-property.md)します。  
  
```  
SqlXmlCommand cmd = new SqlXmlCommand("Provider=SQLOLEDB;Data Source=SqlServerName;Initial Catalog=Database; Integrated Security=SSPI;");  
Stream stm;  
cmd.CommandType = SqlXmlCommandType.UpdateGram;  
cmd.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql' xmlns:updg='urn:schemas-microsoft-com:xml-updategram'>" +  
      "<updg:sync>" +  
       "<updg:before/>" +  
       "<updg:after>" +  
         "<Customer CustomerID='aaaaa' CustomerName='Some Name' CustomerTitle='SomeTitle' />" +  
       "</updg:after>" +  
       "</updg:sync>" +  
       "</ROOT>";  
  
stm = cmd.ExecuteStream();  
stm = null;  
cmd = null;  
```  
  
## <a name="using-executetostream"></a>ExecuteToStream の使用  
 既存のストリームがある場合は、Stream オブジェクトを作成して、Execute メソッドを使用してではなく ExecuteToStream メソッドを使用できます。 前の例のコードを改訂され、ここで ExecuteToStream メソッドを使用します。  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=SqlServerName;database=AdventureWorks;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      SqlXmlParameter p;  
      MemoryStream ms = new MemoryStream();  
      StreamReader sr = new StreamReader(ms);  
      ms.Position = 0;  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.CommandText = "select FirstName, LastName from Person.Contact where LastName = ? For XML Auto";  
      p = cmd.CreateParameter();  
      p.Value = "Achong";  
      cmd.ExecuteToStream(ms);  
      ms.Position = 0;  
      Console.WriteLine(sr.ReadToEnd());  
      return 0;        
   }  
   public static int Main(String[] args)  
   {  
      testParams();     
      return 0;  
   }  
}  
```  
  
> [!NOTE]  
>  XmlReader オブジェクトを返す ExecuteXMLReadermethod を使用することもできます。 詳細については、次を参照してください。 [ExecuteXMLReader メソッドを使用して SQL クエリを実行する](executing-sql-queries-by-using-the-executexmlreader-method.md)します。  
  
  
