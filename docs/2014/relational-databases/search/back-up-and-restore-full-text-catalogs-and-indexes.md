---
title: フルテキスト カタログとフルテキスト インデックスのバックアップおよび復元 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], backing up
- full-text search [SQL Server], back up and restore
- recovery [full-text search]
- backups [SQL Server], full-text indexes
- full-text indexes [SQL Server], restoring
- restore operations [full-text search]
ms.assetid: 6a4080d9-e43f-4b7b-a1da-bebf654c1194
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 28ab36c2f9f500df89b1d936ec60871c0904bc1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012818"
---
# <a name="back-up-and-restore-full-text-catalogs-and-indexes"></a>フルテキスト カタログとフルテキスト インデックスのバックアップおよび復元
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で作成されたフルテキスト インデックスのバックアップと復元を行う方法について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、フルテキスト カタログは論理的概念であり、ファイル グループ内には存在しません。 そのため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でフルテキスト カタログをバックアップするには、カタログに属しているフルテキスト インデックスが含まれるファイル グループをすべて特定する必要があります。 そのうえで、これらのファイルのグループを 1 つずつバックアップする必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースをアップグレードする場合は、フルテキスト カタログをインポートすることができます。 インポートした各フルテキスト カタログは、自身のファイル グループのデータベース ファイルです。 インポートされたカタログをバックアップするには、単にそのファイル グループをバックアップします。 詳細については、 [オンライン ブックの「](https://go.microsoft.com/fwlink/?LinkID=121052)フルテキスト カタログのバックアップと復元 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 」を参照してください。  
  
##  <a name="backingup"></a> フルテキスト カタログのフルテキスト インデックスのバックアップ  
  
###  <a name="Find_FTIs_of_a_Catalog"></a> フルテキスト カタログのフルテキスト インデックスの検索  
 次の [SELECT](/sql/t-sql/queries/select-transact-sql) ステートメントを使用して、フルテキスト インデックスのプロパティを取得できます。このステートメントでは、 [sys.fulltext_indexes](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql) カタログ ビューおよび [sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql) カタログ ビューから列を選択します。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @TableID int;  
SET @TableID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product'));  
SELECT object_name(@TableID), i.is_enabled, i.change_tracking_state,   
   i.has_crawl_completed, i.crawl_type, c.name as fulltext_catalog_name   
   FROM sys.fulltext_indexes i, sys.fulltext_catalogs c   
   WHERE i.fulltext_catalog_id = c.fulltext_catalog_id;  
GO  
```  
  

  
###  <a name="Find_FG_of_FTI"></a> フルテキスト インデックスが含まれるファイル グループまたはファイルの検索  
 フルテキスト インデックスが作成されたら、次の場所のいずれかに配置されます。  
  
-   ユーザー指定のファイル グループ。  
  
-   非パーティション テーブルの場合、ベース テーブルまたはベース ビューと同じファイル グループ。  
  
-   パーティション テーブルの場合、プライマリ ファイル グループ。  
  
> [!NOTE]  
>  フルテキスト インデックスの作成の詳細については。「[フルテキスト インデックスの作成と管理](create-and-manage-full-text-indexes.md)」および「[CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)」を参照してください。  
  
 テーブルまたはビューでフルテキスト インデックスのファイル グループを検索するには、次のクエリを使用します。ここで、 *object_name* はテーブルまたはビューの名前です。  
  
```  
SELECT name FROM sys.filegroups f, sys.fulltext_indexes i   
   WHERE f.data_space_id = i.data_space_id   
      and i.object_id = object_id('object_name');  
GO  
  
```  
  

  
###  <a name="Back_up_FTIs_of_FTC"></a> フルテキスト インデックスを含んだファイル グループのバックアップ  
 フルテキスト カタログのインデックスが含まれるファイル グループを検索したら、各ファイル グループをバックアップする必要があります。 バックアップの処理中に、フルテキスト カタログを削除したり、追加したりすることはできません。  
  
 ファイル グループの最初のバックアップは、ファイルの完全バックアップである必要があります。 ファイル グループの完全バックアップを作成した後は、その完全バックアップに基づいたファイルの差分バックアップを 1 つ以上作成して、ファイル グループの変更内容のみをバックアップできます。  
  
 **ファイルおよびファイル グループをバックアップするには**  
  
-   [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](../backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)  
  

  
##  <a name="Restore_FTI"></a> フルテキスト インデックスの復元  
 バックアップされたファイル グループを復元すると、フルテキスト インデックス ファイルがファイル グループのその他のファイルと共に復元されます。 既定では、ファイル グループはファイル グループがバックアップされたディスク位置に復元されます。  
  
 バックアップが作成されたときに、フルテキスト インデックスが設定されたテーブルがオンラインで、インデックスを作成中だった場合は、復元後に作成が再開されます。  
  
 **ファイル グループを復元するには**  
  
-   [ファイルおよびファイル グループの復元 &#40;SQL Server&#41;](../backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [既存のファイルにファイルとファイル グループを復元する &#40;SQL Server&#41;](../backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [新しい場所へのファイルの復元 &#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  

  
## <a name="see-also"></a>関連項目  
 [サーバー インスタンスでのフルテキスト検索の管理と監視](manage-and-monitor-full-text-search-for-a-server-instance.md)   
 [フルテキスト検索のアップグレード](upgrade-full-text-search.md)  
  
  
