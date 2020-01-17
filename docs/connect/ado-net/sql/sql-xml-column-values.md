---
title: SQL XML 列の値
description: SQL Server から XML データを取得し、使用する方法について説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d8dc9d5100f71fed39c1e4166882230451dd139e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451931"
---
# <a name="sql-xml-column-values"></a>SQL XML 列の値

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server では、`xml` データ型をサポートしています。開発者は、<xref:Microsoft.Data.SqlClient.SqlCommand> クラスの標準動作を使用し、この型を含む結果セットを取得できます。 `xml` 列は、列が取得されたときと同じように取得できますが (たとえば、<xref:Microsoft.Data.SqlClient.SqlDataReader>)、列のコンテンツを XML として操作する場合は、<xref:System.Xml.XmlReader> を使用する必要があります。  
  
## <a name="example"></a>例  
次のコンソール アプリケーションでは、**AdventureWorks** データベースの **Sales.Store** テーブルから 2 行を選択し、この行の `xml` 列を <xref:Microsoft.Data.SqlClient.SqlDataReader> インスタンスに格納します。 行ごとに、<xref:Microsoft.Data.SqlClient.SqlDataReader> の <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> メソッドを使用して `xml` 列の値が読み取られます。 値は <xref:System.Xml.XmlReader> に格納されます。 コンテンツを <xref:System.Data.SqlTypes.SqlXml> 変数に設定する場合は、<xref:System.Data.IDataRecord.GetValue%2A> メソッドではなく <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> を使用する必要があることに注意してください。 <xref:System.Data.IDataRecord.GetValue%2A> は、`xml` 列の値を文字列として返します。  
  
> [!NOTE]
>  **AdventureWorks** サンプル データベースは、既定では SQL Server のインストール時にはインストールされません。 SQL Server セットアップを実行してインストールできます。  
  
[!code-csharp[DataWorks SqlDataReader_GetSqlXml#1](~/../sqlclient/doc/samples/SqlDataReader_GetSqlXml.cs#1)]
  
## <a name="next-steps"></a>次の手順
- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server における XML データ](xml-data-sql-server.md)
