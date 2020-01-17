---
title: データベース スナップショットのスパース ファイルのサイズを表示する方法 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: c2a7e507e45d8429312834911b7bef5ae1e784c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62870881"
---
# <a name="view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql"></a>データベース スナップショットのスパース ファイルのサイズを表示する方法 (Transact-SQL)
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
  
 スナップショットの各スパース ファイルが現在ディスク上で使用しているバイト数を表示するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [sys.dm_io_virtual_file_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql) 動的管理ビューの **size_on_disk_bytes** 列に対してクエリを実行します。  
  
 スパース ファイルが使用するディスク領域を表示するには、Microsoft Windows でファイルを右クリックして **[プロパティ]** をクリックし、 **[ディスク上のサイズ]** の値を確認します。  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>スパース ファイルの最大サイズを調べる  
 スパース ファイルの最大サイズは、スナップショット作成時点での対応するソース データベース ファイルのサイズです。 このサイズを調べるには、次のいずれかを実行します。  
  
-   Windows コマンド プロンプトを使用する:  
  
    1.  Windows の **dir** コマンドを使用します。  
  
    2.  スパース ファイルを選択し、ファイルの **[プロパティ]** ダイアログ ボックスを開き、 **[サイズ]** の値を確認します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで次の操作を実行する:  
  
     データベース スナップショットの **sys.database_files** または **sys.master_files** から **size**列を選択します。 **size** 列の値には、スナップショットが使用できる最大領域 (SQL ページ数) が反映されます。この値は、Windows の **[サイズ]** フィールドに相当しますが、ファイル内の SQL ページ数で表されている点が異なります。バイト単位のサイズは次のように表されます。  
  
     ( *number_of_pages* * 8192)  
  
## <a name="see-also"></a>関連項目  
 [Database Snapshots &#40;SQL Server&#41;](database-snapshots-sql-server.md)   
 [sys.fn_virtualfilestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql)   
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
  
