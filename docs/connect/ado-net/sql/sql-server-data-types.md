---
title: SQL Server のデータ型と ADO.NET
description: SQL Server データ型を操作する方法と、.NET データ型を操作する方法について説明します。
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 12ad13d6788ae2b8995289100883b06c5ab6d7c6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452037"
---
# <a name="sql-server-data-types-and-adonet"></a>SQL Server のデータ型と ADO.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server と .NET は異なる型システムに基づいているため、データが失われる可能性があります。 データの整合性を維持するために、Microsoft SqlClient Data Provider for SQL Server (<xref:Microsoft.Data.SqlClient>) は、SQL Server データを操作するための型指定されたアクセサーメソッドを提供します。 <xref:System.Data.SqlDbType> クラスの列挙体を使用して、<xref:Microsoft.Data.SqlClient.SqlParameter> データ型を指定できます。  
  
SQL Server 2008 では、日付と時刻、構造化データ、半構造化データ、および非構造化データを操作するビジネスニーズを満たすように設計された新しいデータ型が導入されています。 これらは SQL Server 2008 オンライン ブックで説明されています。  
  
アプリケーションで使用できる SQL Server のデータ型は、使用している SQL Server のバージョンによって異なります。 詳細については、SQL Server オンラインブックの「[データ型 (データベースエンジン)](https://go.microsoft.com/fwlink/?LinkID=107468) 」を参照してください。
  
## <a name="in-this-section"></a>このセクションの内容  
[SqlTypes とデータセット](sqltypes-dataset.md)  
`DataSet` 内の `SqlTypes` に対する新しい型のサポートについて説明します。  
  
[null 値の処理](handle-null-values.md)  
Null 値と3つの値を持つロジックを操作する方法を示します。  
  
[GUID と uniqueidentifier 値の比較](compare-guid-uniqueidentifier-values.md)  
SQL Server と .NET で GUID と uniqueidentifier の値を操作する方法について説明します。  
  
[日付型と時刻型のデータ](date-time-data.md)  
SQL Server 2008 で導入された新しい日付と時刻のデータ型の使用方法について説明します。  
  
[大きな UDT](large-udts.md)  
SQL Server 2008 で導入された大きな値の Udt からデータを取得する方法を示します。  
  
[SQL Server における XML データ](xml-data-sql-server.md)  
SQL Server から取得した XML データを操作する方法について説明します。  
  
## <a name="reference"></a>リファレンス  
<xref:System.Data.DataSet>  
`DataSet` クラスとそのすべてのメンバーについて説明します。  
  
<xref:System.Data.SqlTypes>  
`SqlTypes` 名前空間とそのすべてのメンバーについて説明します。  
  
<xref:System.Data.SqlDbType>  
`SqlDbType` 列挙型とそのすべてのメンバーについて説明します。  
  
<xref:System.Data.DbType>  
`DbType` 列挙型とそのすべてのメンバーについて説明します。  
  
## <a name="next-steps"></a>次の手順
- [テーブル値パラメーター](table-valued-parameters.md)
- [SQL Server のバイナリ データと大きな値のデータ](sql-server-binary-large-value-data.md)
