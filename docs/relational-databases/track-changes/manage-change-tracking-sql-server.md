---
title: 変更の追跡の管理
ms.custom: seo-dt-2019
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- tracking data changes [SQL Server]
- change tracking [SQL Server], overhead
- change tracking [SQL Server]
- change tracking [SQL Server], managing
ms.assetid: 94a8d361-e897-4d6d-9a8f-1bb652e7a850
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e129ce11414f27c5502279b392f88204b502bd32
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095415"
---
# <a name="manage-change-tracking-sql-server"></a>変更の追跡の管理 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  このトピックでは、変更の追跡を管理する方法について説明します。 また、セキュリティを構成する方法、および変更の追跡を使用する場合のストレージとパフォーマンスへの影響を判断する方法について説明します。  
  
## <a name="managing-change-tracking"></a>変更の追跡の管理  
 ここでは、変更の追跡の管理に関連するカタログ ビュー、権限、および設定の一覧を示します。  
  
### <a name="catalog-views"></a>カタログ ビュー  
 変更の追跡が有効になっているテーブルおよびデータベースを確認するには、次のカタログ ビューを使用します。  
  
-   [sys.change_tracking_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)  
  
-   [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)  
  
 また、 [sys.internal_tables](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md) カタログ ビューには、ユーザー テーブルの変更の追跡を有効にしたときに作成された内部テーブルが表示されます。  
  
### <a name="security"></a>Security  
 [変更追跡関数](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)を使用して変更追跡情報にアクセスするには、プリンシパルに次の権限が必要です。  
  
-   少なくともクエリ対象テーブルへの変更の追跡対象テーブルの主キー列に対する SELECT 権限。  
  
-   変更が取得されるテーブルに対する VIEW CHANGE TRACKING 権限。 VIEW CHANGE TRACKING 権限は、次の理由のため必要です。  
  
    -   変更追跡レコードには、削除された行に関する情報 (特に削除された行の主キー値) が含まれます。 機密データが削除された後の変更の追跡対象テーブルに対する SELECT 権限がプリンシパルに付与されている可能性があります。 この場合、そのプリンシパルが変更の追跡を使用して、削除済みの情報にアクセスできることは望ましくありません。  
  
    -   変更追跡情報には、更新操作によってどの列が変更されたかという情報が格納される場合があります。 プリンシパルは、機密情報を含む列に対する権限を拒否されている場合があります。 ただし、変更追跡情報は参照できるので、列の値が更新されたことは確認できますが、列の値を確認することはできません。  
  
## <a name="understanding-change-tracking-overhead"></a>変更の追跡のオーバーヘッドについて  
 テーブルの変更の追跡を有効にすると、一部の管理操作が影響を受けます。 次の表に、考慮する必要がある操作と影響を示します。  
  
|演算|変更の追跡が有効になっている場合|  
|---------------|-------------------------------------|  
|DROP TABLE|削除するテーブルのすべての変更追跡情報が削除されます。|  
|ALTER TABLE DROP CONSTRAINT|PRIMARY KEY 制約を削除しようとすると失敗します。 PRIMARY KEY 制約を削除する前に、変更の追跡を無効にする必要があります。|  
|ALTER TABLE DROP COLUMN|削除する列が主キーの一部である場合、変更の追跡に関係なく列は削除できません。<br /><br /> 削除する列が主キーの一部ではない場合、列の削除は成功します。 ただし、このデータの同期を実行しているアプリケーションへの影響についてまず理解しておく必要があります。 テーブルで列の変更の追跡が有効になっている場合、削除した列がまだ変更追跡情報の一部として返される場合があります。 削除した列の処理は、アプリケーションで行う必要があります。|  
|ALTER TABLE ADD COLUMN|変更の追跡対象のテーブルに新しい列を追加する場合、その列の追加は追跡されません。 新しい列に加えられた更新および変更のみが追跡されます。|  
|ALTER TABLE ALTER COLUMN|主キー列以外の列のデータ型の変更は追跡されません。|  
|ALTER TABLE SWITCH|いずれかまたは両方のテーブルで変更の追跡が有効になっている場合、パーティションの切り替えは失敗します。|  
|DROP INDEX または ALTER INDEX DISABLE|主キーを設定するインデックスは削除または無効化できません。|  
|TRUNCATE TABLE|テーブルの切り捨ては、変更の追跡が有効になっているテーブルに対して実行できます。 ただし、この操作によって削除される行は追跡されず、有効な最小バージョンが更新されます。 アプリケーションがそのバージョンをチェックすると、バージョンが古すぎるため再初期化が必要であることが示されます。 これは、テーブルの変更の追跡を無効にして再度有効にした場合と同じです。|  
  
 変更の追跡を使用すると、DML 操作の一部として格納される変更追跡情報が原因で、DML 操作のオーバーヘッドが多少増加します。  
  
### <a name="effects-on-dml"></a>DML への影響  
 変更の追跡は、DML 操作のパフォーマンスのオーバーヘッドを最小限に抑えるように最適化されています。 テーブルに対する変更の追跡の使用に関連するパフォーマンスのオーバーヘッドの増加は、テーブルにインデックスを作成して維持する必要がある場合に発生するオーバーヘッドに似ています。  
  
 DML 操作で変更された行ごとに、行が内部変更追跡テーブルに追加されます。 DML 操作に関連するこの影響は、次のようなさまざまな要因によって異なります。  
  
-   主キー列の数  
  
-   ユーザー テーブル行で変更されるデータの量  
  
-   トランザクションで実行される操作の数  
  
 スナップショット分離を使用している場合も、変更の追跡が有効になっているかどうかに関係なく、すべての DML 操作のパフォーマンスに影響します。  
  
### <a name="effects-on-storage"></a>ストレージへの影響  
 変更追跡データは、次の種類の内部テーブルに格納されます。  
  
-   内部変更テーブル  
  
     変更の追跡が有効になっているユーザー テーブルごとに 1 つずつ内部変更テーブルがあります。  
  
-   内部トランザクション テーブル  
  
     データベースごとに 1 つずつ内部トランザクション テーブルがあります。  
  
 これらの内部テーブルは、ストレージ要件に次のような影響を与えます。  
  
-   ユーザー テーブル内の各行が変更されるごとに、行が内部変更テーブルに追加されます。 この行によって、一定のわずかなオーバーヘッドおよび主キー列のサイズと同じ可変のオーバーヘッドが生じます。 この行には、アプリケーションによって設定されるオプションのコンテキスト情報が含まれる場合があります。 また、列の追跡が有効になっている場合、列が変更されるごとに追跡テーブルで 4 バイトが必要になります。  
  
-   トランザクションがコミットされるごとに、行が内部トランザクション テーブルに追加されます。  
  
 その他の内部テーブルと同様に、変更追跡テーブルに使用される領域は、 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) ストアド プロシージャを使用して確認できます。 内部テーブルの名前は、次の例に示すように、 [sys.internal_tables](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md) カタログ ビューを使用して取得できます。  
  
```sql  
sp_spaceused 'sys.change_tracking_309576141'  
sp_spaceused 'sys.syscommittab'  
```  
  
## <a name="see-also"></a>参照  
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [[データベースのプロパティ] &#40;[変更の追跡] ページ&#41;](../../relational-databases/databases/database-properties-changetracking-page.md)   
 [ALTER DATABASE SET のオプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.change_tracking_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)   
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [変更の追跡について &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [変更データの処理 &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
  
