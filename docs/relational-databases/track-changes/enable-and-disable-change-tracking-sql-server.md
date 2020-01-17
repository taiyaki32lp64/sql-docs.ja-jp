---
title: 変更の追跡の有効化と無効化
ms.custom: seo-dt-2019
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server], disabling
- data changes [SQL Server]
- change tracking [SQL Server], enabling
- tracking data changes [SQL Server]
- change tracking [SQL Server], configuring
- data [SQL Server], changing
ms.assetid: 1c92ec7e-ae53-4498-8bfd-c66a42a24d54
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 075d192e2fba3849ae1293cce6f9125f4190ab4b
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095271"
---
# <a name="enable-and-disable-change-tracking-sql-server"></a>変更の追跡の有効化と無効化 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  このトピックでは、データベースとテーブルに対する変更の追跡を有効または無効にする方法について説明します。  
  
## <a name="enable-change-tracking-for-a-database"></a>データベースの変更の追跡を有効にする  
 変更の追跡を使用するには、あらかじめデータベース レベルで変更の追跡を有効にしておく必要があります。 次の例では、 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md)を使用して変更の追跡を有効にする方法を示します。  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
```  
  
 変更の追跡は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で [[データベースのプロパティ] &#40;[変更の追跡] ページ&#41;](../../relational-databases/databases/database-properties-changetracking-page.md) ダイアログ ボックスを使用して有効にすることもできます。  
  
 変更の追跡を有効にするときに、CHANGE_RETENTION および AUTO_CLEANUP オプションを指定できます。これらの値は、変更の追跡を有効にした後いつでも変更できます。  
  
 change retention 値は、変更追跡情報を保持する期間を指定します。 この期間を過ぎると、変更追跡情報は定期的に削除されます。 この値を設定する場合は、アプリケーションとデータベース内のテーブルを同期する間隔を考慮する必要があります。 保有期間は、同期間隔と同じかそれ以上の長さに指定する必要があります。 アプリケーションが変更を取得する間隔の方が長い場合、変更情報の一部が削除済みである可能性があるので、正しくない結果が返されることがあります。 正しくない結果を取得しないようにするために、アプリケーションでは、CHANGE_TRACKING_MIN_VALID_VERSION システム関数を使用して、同期間隔が長すぎないかどうかを判断できます。  
  
 AUTO_CLEANUP オプションは、古い変更追跡情報を削除するクリーンアップ タスクを有効または無効にするために使用できます。 これは、アプリケーションを同期できない一時的な問題が発生しており、保有期間を過ぎた変更追跡情報を削除するプロセスを問題が解決されるまで一時停止する必要がある場合に役立ちます。  
  
 変更の追跡を使用するデータベースについて、以下の点に注意してください。  
  
-   変更の追跡を使用するには、データベースの互換性レベルを 90 以上に設定する必要があります。 データベースの互換性レベルが 90 未満の場合でも、変更の追跡は構成できます。 ただし、変更追跡情報の取得に使用される CHANGETABLE 関数からエラーが返されます。  
  
-   スナップショット分離を使用すると、すべての変更追跡情報の一貫性を最も簡単に確保できます。 このため、データベースのスナップショット分離を ON に設定することを強くお勧めします。 詳細については、「[変更の追跡のしくみ &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)」を参照してください。  
  
## <a name="enable-change-tracking-for-a-table"></a>テーブルの変更の追跡を有効にする  
 変更の追跡は、追跡するテーブルごとに有効にする必要があります。 変更の追跡を有効にすると、DML 操作の影響を受けるテーブル内のすべての行に関する変更追跡情報が保持されます。  
  
 次の例では、 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)を使用してテーブルの変更の追跡を有効にする方法を示します。  
  
```sql  
ALTER TABLE Person.Contact  
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)  
```  
  
 テーブルの変更の追跡は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で [[データベースのプロパティ] &#40;[変更の追跡] ページ&#41;](../../relational-databases/databases/database-properties-changetracking-page.md) ダイアログ ボックスを使用して有効にすることもできます。  
  
 TRACK_COLUMNS_UPDATED オプションが ON に設定されている場合、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] によって、どの列が更新されたかという追加情報が内部変更追跡テーブルに格納されます。 列追跡を行うと、アプリケーションは更新された列のみを同期できます。 これにより、効率とパフォーマンスが向上します。 ただし、列追跡情報を保持すると追加のストレージ オーバーヘッドがかかるので、このオプションは既定では OFF に設定されています。  
  
## <a name="disable-change-tracking-for-a-database-or-table"></a>データベースまたはテーブルに対する変更の追跡を無効にする  
 まず変更の追跡の対象になっているすべてのテーブルの変更の追跡を無効にして、次にデータベースの変更の追跡を OFF に設定する必要があります。 データベース内で変更の追跡が有効になっているテーブルを確認するには、 [sys.change_tracking_tables](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md) カタログ ビューを使用します。  
  
 データベース内のテーブルで変更が追跡されていなければ、データベースの変更の追跡を無効にすることができます。 次の例では、 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md)を使用してデータベースの変更の追跡を無効にする方法を示します。  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF  
```  
  
 次の例では、 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)を使用してテーブルの変更の追跡を無効にする方法を示します。  
  
```sql  
ALTER TABLE Person.Contact  
DISABLE CHANGE_TRACKING;  
```  
  
## <a name="see-also"></a>参照  
 [[データベースのプロパティ] &#40;[変更の追跡] ページ&#41;](../../relational-databases/databases/database-properties-changetracking-page.md)   
 [ALTER DATABASE SET のオプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.change_tracking_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)   
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [変更の追跡について &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [変更データの処理 &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)   
 [変更の追跡の管理 &#40;SQL Server&#41;](../../relational-databases/track-changes/manage-change-tracking-sql-server.md)  
  
  
