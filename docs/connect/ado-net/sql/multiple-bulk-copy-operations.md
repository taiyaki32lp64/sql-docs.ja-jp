---
title: 複数の一括コピー操作
description: SqlBulkCopy クラスを使用して SQL Server のインスタンスにデータの複数の一括コピー操作を実行する方法について説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5ad12f94-7459-4a93-a421-4160d1a90715
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 6cc373224f4df437665cc48edb78ff81b85b8ac1
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452133"
---
# <a name="multiple-bulk-copy-operations"></a>複数の一括コピー操作

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

<xref:Microsoft.Data.SqlClient.SqlBulkCopy> クラスの単一のインスタンスを使用して、一括コピー操作を複数回実行できます。 コピー元とコピー先で操作パラメーターが変わる場合 (たとえば、コピー先のテーブル名など)、**WriteToServer** メソッドを続けて呼び出す前に、次の例で示すようにパラメーターを更新する必要があります。 明示的に変更した場合を除き、すべてのプロパティ値は、任意のインスタンスに対して前回一括コピー操作を実行したときと同じ状態のままになっています。  
  
> [!NOTE]
>  通常、一括コピー操作を複数回実行する場合は、同じ <xref:Microsoft.Data.SqlClient.SqlBulkCopy> のインスタンスを使用する方が各操作ごとに別のインスタンスを使用するよりも効率的です。  
  
同じ <xref:Microsoft.Data.SqlClient.SqlBulkCopy> オブジェクトを使用して一括コピー操作を複数回実行する場合、コピー元またはコピー先の情報が各操作ごとに一致しているか異なっているかに関する制限はありません。 ただし、サーバーに書き込み処理を行うときは、列の関連付け情報を毎回正しく設定する必要があります。  

## <a name="example"></a>例

> [!IMPORTANT]
>  このサンプルは、「[一括コピーのセットアップ例](bulk-copy-example-setup.md)」で説明しているように作業テーブルを作成して取得してからでないと動作しません。 このコードでは、**SqlBulkCopy** だけを使用した構文について説明します。 コピー元およびコピー先のテーブルが同一の SQL Server インスタンス内に存在する場合、Transact-SQL `INSERT … SELECT` ステートメントを使用すれば簡単かつ高速にデータをコピーすることができます。  
  
[!code-csharp[DataWorks SqlBulkCopy_._ColumnMappingOrdersDetails#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnMappingOrdersDetails.cs#1)]
  
## <a name="next-steps"></a>次の手順
- [SQL Server での一括コピー操作](bulk-copy-operations-sql-server.md)
