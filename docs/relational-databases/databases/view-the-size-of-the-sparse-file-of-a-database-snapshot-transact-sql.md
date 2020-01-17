---
title: データベース スナップショット (T-SQL) のスパース ファイルのサイズを表示する方法
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server database snapshots], sparse files
- space [SQL Server], sparse files
- sparse files [SQL Server]
- size [SQL Server], sparse files
- maximum sparse file size
- database snapshots [SQL Server], sparse files
- space [SQL Server], database snapshots
ms.assetid: 1867c5f8-d57c-46d3-933d-3642ab0a8e24
author: stevestein
ms.author: sstein
ms.openlocfilehash: 71881edf1c98b0588a731964cf6f23dcffe6aa82
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74055208"
---
# <a name="view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql"></a>データベース スナップショットのスパース ファイルのサイズを表示する方法 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、[!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ファイルがスパース ファイルであることを確認する方法と、その実サイズおよび最大サイズを調べる方法について説明します。 NTFS ファイル システムの機能であるスパース ファイルは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース スナップショットによって使用されます。  
  
> [!NOTE]  
>  スパース ファイルは、データベース スナップショットの作成時に CREATE DATABASE ステートメント内のファイル名を使用して作成されます。 これらのファイル名は、 **sys.master_files** の **physical_name** 列に格納されます。 ソース データベース内とスナップショット内のいずれであっても、 **sys.database_files** の **physical_name** 列には、ソース データベース ファイルの名前が必ず格納されます。  
  
## <a name="verify-that-a-database-file-is-a-sparse-file"></a>データベース ファイルがスパース ファイルであることを確認する  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで次の操作を実行する:  

     データベース スナップショットの **sys.database_files** または **sys.master_files** から **is_sparse**列を選択します。 次に示すように、この値からファイルがスパース ファイルであるかどうかがわかります。  
  
     1 = ファイルはスパース ファイルです。  
  
     0 = ファイルはスパース ファイルではありません。  
  
## <a name="find-out-the-actual-size-of-a-sparse-file"></a>スパース ファイルの実際のサイズを調べる  
  
> [!NOTE]  
>  スパース ファイルは 64 KB 単位で大きくなるので、ディスク上のスパース ファイルのサイズは常に 64 KB の倍数になります。  
  
 スナップショットの各スパース ファイルが現在ディスク上で使用しているバイト数を表示するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) 動的管理ビューの **size_on_disk_bytes** 列に対してクエリを実行します。  
  
 スパース ファイルが使用するディスク領域を表示するには、Microsoft Windows でファイルを右クリックして **[プロパティ]** をクリックし、 **[ディスク上のサイズ]** の値を確認します。  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>スパース ファイルの最大サイズを調べる  
 スパース ファイルの最大サイズは、スナップショット作成時点での対応するソース データベース ファイルのサイズです。 このサイズを調べるには、次のいずれかを実行します。  
  
-   Windows コマンド プロンプトを使用する:  
  
    1.  Windows の **dir** コマンドを使用します。  
  
    2.  スパース ファイルを選択し、ファイルの **[プロパティ]** ダイアログ ボックスを開き、 **[サイズ]** の値を確認します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで次の操作を実行する:  
  
     データベース スナップショットの **sys.database_files** または **sys.master_files** から **size**列を選択します。 **size** 列の値には、スナップショットが使用できる最大領域 (SQL ページ数) が反映されます。この値は、Windows の **[サイズ]** フィールドに相当しますが、ファイル内の SQL ページ数で表されている点が異なります。バイト単位のサイズは次のように表されます。  
  
     ( *number_of_pages* * 8192)  

## <a name="example"></a>例
次のスクリプトは、各スパース ファイルのディスク上のサイズを KB 単位で表示します。  また、スパース ファイルが増えた場合の最大サイズも MB 単位で表示します。  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で Transact-SQL スクリプトを実行します。

```sql
SELECT  DB_NAME(sd.source_database_id) AS [SourceDatabase], 
        sd.name AS [Snapshot],
        mf.name AS [Filename], 
        size_on_disk_bytes/1024 AS [size_on_disk (KB)],
        mf2.size/128 AS [MaximumSize (MB)]
FROM sys.master_files mf
JOIN sys.databases sd
    ON mf.database_id = sd.database_id
JOIN sys.master_files mf2
    ON sd.source_database_id = mf2.database_id
    AND mf.file_id = mf2.file_id
CROSS APPLY sys.dm_io_virtual_file_stats(sd.database_id, mf.file_id)
WHERE mf.is_sparse = 1
AND mf2.is_sparse = 0
ORDER BY 1;
```
  
## <a name="see-also"></a>参照  
 [Database Snapshots &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [sys.fn_virtualfilestats &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
