---
title: FileTable 関数、ストアド プロシージャ、およびビュー | Microsoft Docs
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6f429d40b3bc93a4897cf23c5f9985fbf71c9016
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252714"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>FileTable DDL、関数、ストアド プロシージャ、およびビュー

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] の FileTable 機能をサポートするために追加または変更された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース オブジェクトの一覧を示します。  
  
 次の表の「状態」列は、その項目が [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]で新しく導入された項目であるか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンからあり、セマンティック検索をサポートするために [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] で変更された項目であるかを示します。  
  
 FILESTREAM をサポートするステートメントおよびデータベース オブジェクトの一覧については、「 [FILESTREAM DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filestream-ddl-functions-stored-procedures-and-views.md)」を参照してください。  
  
##  <a name="ddl"></a> Transact-SQL データ定義言語 (DDL) ステートメント  
  
|Object|Status|詳細情報|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)<br /><br /> [ALTER DATABASE SET のオプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)|変更|[FileTable の前提条件の有効化](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)<br /><br /> [FileTable の管理](../../relational-databases/blob/manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|変更|[FileTable の作成、変更、および削除](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [FileTable の管理](../../relational-databases/blob/manage-filetables.md)|  
|[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)|変更|[FileTable の前提条件の有効化](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|変更|[FileTable の作成、変更、および削除](../../relational-databases/blob/create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)<br /><br /> [RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)|変更||  
  
##  <a name="func"></a> 関数  
  
|Object|Status|詳細情報|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|**追加**|[FileTable 内のディレクトリとパスの操作](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|**追加**|[FileTable 内のディレクトリとパスの操作](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|**追加**|[FileTable 内のディレクトリとパスの操作](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="sproc"></a> ストアド プロシージャ  
  
|Object|Status|詳細情報|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)|**追加**|[FileTable の管理](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="cv"></a> カタログ ビュー  
  
|Object|Status|詳細情報|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)|**追加**|[FileTable の前提条件の有効化](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)|**追加**|[FileTable の作成、変更、および削除](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [FileTable の管理](../../relational-databases/blob/manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)|**追加**|[FileTable の管理](../../relational-databases/blob/manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)|変更|[FileTable の管理](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="dmv"></a> 動的管理ビュー  
  
|Object|Status|詳細情報|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)|**追加**|[FileTable の管理](../../relational-databases/blob/manage-filetables.md)|  
  
## <a name="see-also"></a>参照  
 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)  
  
  
