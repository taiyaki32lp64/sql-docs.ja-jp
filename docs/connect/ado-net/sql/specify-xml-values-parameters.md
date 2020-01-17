---
title: パラメーターとしての XML 値の指定
description: XML データをパラメーターとしてコマンドに渡す方法について説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 2c4d08b8-fc29-4614-97fa-29c8ff7ca5b3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 5ef73529119245397932a3a2414ce65f381b55bd
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452113"
---
# <a name="specifying-xml-values-as-parameters"></a>パラメーターとしての XML 値の指定

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

値が XML 文字列であるパラメーターがクエリに必要な場合、開発者はその値を **SqlXml** のインスタンスを使用して提供することができます。 特別な処理は必要ありません。SQL Server の XML 列は、他のデータ型と同じ方法でパラメーター値を受け入れます。  
  
## <a name="example"></a>例  
次のコンソール アプリケーションでは、**AdventureWorks** データベースに新しいテーブルを作成します。 新しいテーブルには、**SalesID** という名前の列と、**SalesInfo** という名前の XML 列があります。  
  
> [!NOTE]
>  **AdventureWorks** サンプル データベースは、既定では SQL Server のインストール時にはインストールされません。 SQL Server セットアップを実行してインストールできます。  
  
この例では、<xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトを準備して、新しいテーブルに行を挿入します。 保存されたファイルは、**SalesInfo** 列に必要な XML データを提供します。  
  
例を実行するために必要なファイルを作成するには、プロジェクトと同じフォルダーに新しいテキストファイルを作成します。 ファイルに MyTestStoreData という名前を指定します。 メモ帳でファイルを開き、次のテキストをコピーして貼り付けます。  
  
```xml  
<StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>International Bank</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1970</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>7000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>T1</Internet>  
  <NumberEmployees>2</NumberEmployees>  
</StoreSurvey>  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
using System.Xml;  
using System.Data.SqlTypes;  
  
class Class1  
{  
    static void Main()  
    {  
        using (SqlConnection connection = new SqlConnection(GetConnectionString()))  
       {  
        connection.Open();  
        //  Create a sample table (dropping first if it already  
        //  exists.)  
  
        string commandNewTable =   
            "IF EXISTS (SELECT * FROM dbo.sysobjects " +   
            "WHERE id = " +  
                  "object_id(N'[dbo].[XmlDataTypeSample]') " +   
            "AND OBJECTPROPERTY(id, N'IsUserTable') = 1) " +   
            "DROP TABLE [dbo].[XmlDataTypeSample];" +   
            "CREATE TABLE [dbo].[XmlDataTypeSample](" +   
            "[SalesID] [int] IDENTITY(1,1) NOT NULL, " +   
            "[SalesInfo] [xml])";  
        SqlCommand commandAdd =   
                   new SqlCommand(commandNewTable, connection);  
        commandAdd.ExecuteNonQuery();  
        string commandText =   
            "INSERT INTO [dbo].[XmlDataTypeSample] " +   
            "([SalesInfo] ) " +   
            "VALUES(@xmlParameter )";  
        SqlCommand command =   
                  new SqlCommand(commandText, connection);  
  
        //  Read the saved XML document as a   
        //  SqlXml-data typed variable.  
        SqlXml newXml =   
            new SqlXml(new XmlTextReader("MyTestStoreData.xml"));  
  
        //  Supply the SqlXml value for the value of the parameter.  
        command.Parameters.AddWithValue("@xmlParameter", newXml);  
  
        int result = command.ExecuteNonQuery();  
        Console.WriteLine(result + " row was added.");  
        Console.WriteLine("Press Enter to continue.");  
        Console.ReadLine();  
    }  
  }  
  
    private static string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,              
        // you can retrieve it from a configuration file.   
        return "Data Source=(local);Integrated Security=true;" +  
        "Initial Catalog=AdventureWorks; ";  
    }  
}  
```  
  
## <a name="next-steps"></a>次の手順
- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server における XML データ](xml-data-sql-server.md)
