---
title: Stretch Database の制限事項
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, limitations
- Stretch Database, blocking issues
- limitations (Stretch Database)
- blocking issues (Stretch Database)
ms.assetid: 2b1fbec1-7859-44fc-8417-724fc57a59c0
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 12b3fae80a7bf2c46c8d1d10ad5c45d74212eef0
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843792"
---
# <a name="limitations-for-stretch-database"></a>Stretch Database の制限事項
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch に対応するテーブルの制限事項について、さらに、テーブルの Stretch の有効化を現在阻止している制限事項について説明します。  
  
##  <a name="Caveats"></a> Stretch に対応するテーブルの制限事項  
  
Stretch に対応するテーブルには次の制限事項があります。  
  
### <a name="constraints"></a>制約  
-   移行データが含まれている Azure テーブルでは、UNIQUE 制約および PRIMARY KEY 制約に一意性は適用されません。  
  
### <a name="dml-operations"></a>DML 操作  
-   Stretch に対応するテーブルまたは Stretch に対応するテーブルを含むビューでは、移行された行または移行対象の行に対して UPDATE 操作または DELETE 操作を実行することはできません。  
  
-   リンク サーバー上の Stretch に対応するテーブルに対して行の INSERT 操作を実行することはできません。  
  
### <a name="indexes"></a>インデックス  
-   Stretch に対応するテーブルを含むビューのインデックスを作成することはできません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インデックスのフィルターは、リモート テーブルには反映されません。  
  
##  <a name="Limitations"></a> テーブルの Stretch の有効化を現在妨げている制限事項  
   
 現在のところ、次のアイテムによって、テーブルの Stretch の有効化は妨げられています。  
  
 ### <a name="table-properties"></a>テーブルのプロパティ  
-   列の数が 1,023 個を上回り、インデックスの数が 998 個を上回っているテーブル  
  
-   FILESTREAM データが含まれる FileTables またはテーブル  
  
-   レプリケートされているテーブル、または変更の追跡または変更データ キャプチャがアクティブに使用されているテーブル  
  
-   メモリ最適化テーブル  
  
### <a name="data-types"></a>データ型  
-   text、ntext、image  
  
-   TIMESTAMP  
  
-   sql_variant  
  
-   XML  
  
-   geometry、geography、hierarchyid、および CLR のユーザー定義型を含む CLR データ型  
  
 ### <a name="column-types"></a>列の型  
 -   COLUMN_SET  
  
-   計算列  
  
### <a name="constraints"></a>制約  
-   既定の制約と CHECK 制約  
  
-   テーブルを参照する外部キー制約。 親子関係 (たとえば、Order と Order_Detail) では、子テーブル (Order_Detail) の Stretch は有効にできますが、親テーブル (Order) の Stretch は有効にできません。  
  
### <a name="indexes"></a>インデックス  
-   フルテキスト インデックス  
  
-   XML インデックス数  
  
-   空間インデックス  
  
-   テーブルを参照するインデックス ビュー  
  
## <a name="see-also"></a>参照  
 [Stretch Database Advisor を実行して Stretch Database のデータベースとテーブルを特定する](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [データベースに対して Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [テーブルに対して Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
