---
title: FileTable DDL、関数、ストアド プロシージャ、およびビュー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 85e0c761f5dc784698b3aed361ce50488a93e366
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010100"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>FileTable DDL、関数、ストアド プロシージャ、およびビュー
  [!INCLUDE[tsql](../../includes/tsql-md.md)] の FileTable 機能をサポートするために追加または変更された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース オブジェクトの一覧を示します。  
  
 次の表の「状態」列は、その項目が [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]で新しく導入された項目であるか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンからあり、セマンティック検索をサポートするために [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] で変更された項目であるかを示します。  
  
 FILESTREAM をサポートするステートメントおよびデータベース オブジェクトの一覧については、「 [FILESTREAM DDL, Functions, Stored Procedures, and Views](../views/views.md)」を参照してください。  
  
##  <a name="ddl"></a> Transact-SQL データ定義言語 (DDL) ステートメント  
  
|オブジェクト|状態|詳細情報|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)<br /><br /> [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)|変更|[FileTable の前提条件の有効化](enable-the-prerequisites-for-filetable.md)<br /><br /> [FileTable の管理](manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)|変更|[FileTable の作成、変更、および削除](create-alter-and-drop-filetables.md)<br /><br /> [FileTable の管理](manage-filetables.md)|  
|[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)|変更|[FileTable の前提条件の有効化](enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)|変更|[FileTable の作成、変更、および削除](create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)<br /><br /> [RESTORE の引数 &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)|変更||  
  
##  <a name="func"></a> 関数  
  
|オブジェクト|状態|詳細情報|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filetablerootpath-transact-sql)|**追加**|[FileTable 内のディレクトリとパスの操作](work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql)|**追加**|[FileTable 内のディレクトリとパスの操作](work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql)|**追加**|[FileTable 内のディレクトリとパスの操作](work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="sproc"></a> ストアド プロシージャ  
  
|オブジェクト|状態|詳細情報|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles)|**追加**|[FileTable の管理](manage-filetables.md)|  
  
##  <a name="cv"></a> カタログ ビュー  
  
|オブジェクト|状態|詳細情報|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql)|**追加**|[FileTable の前提条件の有効化](enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql)|**追加**|[FileTable の作成、変更、および削除](create-alter-and-drop-filetables.md)<br /><br /> [FileTable の管理](manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetables-transact-sql)|**追加**|[FileTable の管理](manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|変更|[FileTable の管理](manage-filetables.md)|  
  
##  <a name="dmv"></a> 動的管理ビュー  
  
|オブジェクト|状態|詳細情報|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql)|**追加**|[FileTable の管理](manage-filetables.md)|  
  
## <a name="see-also"></a>参照  
 [FileTable の管理](manage-filetables.md)  
  
  
