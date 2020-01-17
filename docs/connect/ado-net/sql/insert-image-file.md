---
title: ファイルからのイメージの挿入
description: ファイルからイメージを操作する方法について説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 35900aa2-5615-4174-8212-ba184c6b82fb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d8f7b561a6aba4539964d73dacfd9e45db2dd6aa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452176"
---
# <a name="inserting-an-image-from-a-file"></a>ファイルからのイメージの挿入

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

バイナリラージオブジェクト (BLOB) は、データソースのフィールドの種類に応じて、バイナリデータまたは文字データとしてデータベースに書き込むことができます。 BLOB は、`text`、`ntext`、および `image` データ型を参照する一般的な用語であり、通常はドキュメントと画像が含まれます。  
  
BLOB 値をデータベースに書き込むには、適切な INSERT または UPDATE ステートメントを実行し、入力パラメーターとして BLOB 値を渡します。 BLOB が SQL Server `text` フィールドなどのテキストとして格納されている場合は、BLOB を文字列パラメーターとして渡すことができます。 BLOB がバイナリ形式 (SQL Server `image` フィールドなど) で格納されている場合は、`byte` 型の配列をバイナリパラメーターとして渡すことができます。
  
## <a name="example"></a>例  
次のコード例では、Northwind データベースの Employees テーブルに従業員情報を追加します。 従業員の写真がファイルから読み取られ、テーブルの Photo フィールド (画像フィールド) に追加されます。  
  
```csharp  
public static void AddEmployee(  
  string lastName,   
  string firstName,   
  string title,   
  DateTime hireDate,   
  int reportsTo,   
  string photoFilePath,   
  string connectionString)  
{  
  byte[] photo = GetPhoto(photoFilePath);  
  
  using (SqlConnection connection = new SqlConnection(  
    connectionString))  
  
  SqlCommand command = new SqlCommand(  
    "INSERT INTO Employees (LastName, FirstName, " +  
    "Title, HireDate, ReportsTo, Photo) " +  
    "Values(@LastName, @FirstName, @Title, " +  
    "@HireDate, @ReportsTo, @Photo)", connection);   
  
  command.Parameters.Add("@LastName",    
     SqlDbType.NVarChar, 20).Value = lastName;  
  command.Parameters.Add("@FirstName",   
      SqlDbType.NVarChar, 10).Value = firstName;  
  command.Parameters.Add("@Title",       
      SqlDbType.NVarChar, 30).Value = title;  
  command.Parameters.Add("@HireDate",   
       SqlDbType.DateTime).Value = hireDate;  
  command.Parameters.Add("@ReportsTo",   
      SqlDbType.Int).Value = reportsTo;  
  
  command.Parameters.Add("@Photo",  
      SqlDbType.Image, photo.Length).Value = photo;  
  
  connection.Open();  
  command.ExecuteNonQuery();  
  }  
}  
  
public static byte[] GetPhoto(string filePath)  
{  
  FileStream stream = new FileStream(  
      filePath, FileMode.Open, FileAccess.Read);  
  BinaryReader reader = new BinaryReader(stream);  
  
  byte[] photo = reader.ReadBytes((int)stream.Length);  
  
  reader.Close();  
  stream.Close();  
  
  return photo;  
}  
```  
  
## <a name="next-steps"></a>次の手順
- [SQL Server のバイナリ データと大きな値のデータ](sql-server-binary-large-value-data.md)
