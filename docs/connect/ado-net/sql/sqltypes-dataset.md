---
title: SqlTypes とデータセット
description: データセットの SqlTypes の型サポートについて説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 70efb8615a70677c709abd6d9129c63de9420ffc
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451986"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes とデータセット

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ADO.NET 2.0 では、<xref:System.Data.SqlTypes> 名前空間を使用して `DataSet` の拡張型サポートが導入されました。 <xref:System.Data.SqlTypes> の型は、SQL Server データベースのデータ型と同じセマンティクスと有効桁数を持つデータ型を提供するように設計されています。 <xref:System.Data.SqlTypes> の個々のデータ型には、それに相当する SQL Server のデータ型があり、基本となるデータ表現はいずれも同じです。  
  
<xref:System.Data.DataSet> で <xref:System.Data.SqlTypes> を直接使用すると、SQL Server データ型を操作するときにいくつかの利点があります。 <xref:System.Data.SqlTypes> は、ネイティブデータ型 SQL Server と同じセマンティクスをサポートしています。 <xref:System.Data.DataColumn> の定義に含まれるいずれかの <xref:System.Data.SqlTypes> を指定すると、decimal または numeric データ型を共通言語ランタイム (CLR) のデータ型に変換するときに発生する可能性のある精度が失われます。  

次の例では、<xref:System.Data.DataTable> オブジェクトを作成し、CLR データ型の代わりに <xref:System.Data.SqlTypes> を使用して、<xref:System.Data.DataColumn> のデータ型を明示的に定義します。 このコードは、SQL Server の AdventureWorks データベースの Sales.SalesOrderDetail テーブルから取得されたデータを <xref:System.Data.DataTable> に挿入します。 コンソールウィンドウに表示される出力には、各列のデータ型と SQL Server から取得した値が表示されます。  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
