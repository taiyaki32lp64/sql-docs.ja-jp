---
title: master_files (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.master_files
- master_files_TSQL
- sys.master_files_TSQL
- master_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_files catalog view
ms.assetid: 803b22f2-0016-436b-a561-ce6f023d6b6a
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2aa7c30f132f0c0e8774dcb39f31e1a254e8689c
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313723"
---
# <a name="sysmaster_files-transact-sql"></a>master_files (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  master データベースに格納されているデータベースのファイルごとに 1 行のデータを保持します。 これは、単一のシステム全体のビューです。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|database_id|**int**|このファイルが適用されるデータベースの ID。 Masterdatabase_id は常に1です。|  
|file_id|**int**|データベース内のファイルの ID。 プライマリ ファイルの file_id は常に 1 です。|  
|file_guid|**uniqueidentifier**|ファイルの一意識別子。<br /><br /> NULL = データベースは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からアップグレードされました (SQL Server 2005 以前で有効)。|  
|型|**tinyint**|ファイルの種類です。<br /><br /> 0 = 行。<br /><br /> 1 = ログ<br /><br /> 2 = FILESTREAM<br /><br /> 3 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 4 = フルテキスト ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] より前のフルテキスト カタログです。[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降用にアップグレードまたは作成されたフルテキスト カタログの場合、ファイルの種類は 0 で報告されます。)|  
|type_desc|**nvarchar(60)**|ファイルの種類の説明。<br /><br /> ROWS<br /><br /> LOG<br /><br /> FILESTREAM<br /><br /> FULLTEXT ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] より前のフルテキスト カタログです。)|  
|data_space_id|**int**|このファイルが属しているデータ領域の ID。 データ領域はファイルグループです。<br /><br /> 0 = ログ ファイル|  
|name|**sysname**|データベース内のファイルの論理名。|  
|physical_name|**nvarchar(260)**|オペレーティングシステムのファイル名。|  
|state|**tinyint**|ファイルの状態です。<br /><br /> 0 = ONLINE<br /><br /> 1 = 復元中<br /><br /> 2 = 回復中<br /><br /> 3 = RECOVERY_PENDING<br /><br /> 4 = 問題あり<br /><br /> 5 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT|  
|state_desc|**nvarchar(60)**|ファイルの状態の説明です。<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> OFFLINE<br /><br /> DEFUNCT<br /><br /> 詳しくは、「[ファイルの状態](../../relational-databases/databases/file-states.md)」をご覧ください。|  
|幅|**int**|現在のファイルサイズ (8 KB ページ単位)。 データベース スナップショットの場合、size は、スナップショットがファイルに対して使用する中で最大の領域を表します。<br /><br /> メモ: このフィールドは、FILESTREAM コンテナーの場合は0として設定されます。 FILESTREAM コンテナーの実際のサイズについては、 *database_files*カタログビューに対してクエリを実行します。|  
|max_size|**int**|最大ファイルサイズ (8 KB ページ単位):<br /><br /> 0 = 拡張は許可されません。<br /><br /> -1 = ディスクがいっぱいになるまでファイル サイズが拡張します。<br /><br /> 268435456 = ログファイルは、最大サイズの 2 TB まで拡張されます。<br /><br /> 注: ログファイルのサイズを無制限にアップグレードしたデータベースは、ログファイルの最大サイズに対して-1 を報告します。|  
|成長|**int**|0 = ファイルは固定サイズであり、拡張されません。<br /><br /> > 0 = ファイルは自動的に拡張されます。<br /><br /> is_percent_growth が 0 の場合、拡張増分は 8 KB ページ単位で表され、最も近い 64 KB 単位の値に切り上げられます。<br /><br /> is_percent_growth が 1 の場合、拡張増分は、整数のパーセンテージで表されます。|  
|is_media_read_onlyF|**bit**|1 = ファイルは読み取り専用メディア上にあります。<br /><br /> 0 = ファイルは読み取り/書き込みメディア上にあります。|  
|is_read_only|**bit**|1 = ファイルは読み取り専用に設定されています。<br /><br /> 0 = ファイルは読み取り/書き込み用にマークされています。|  
|is_sparse|**bit**|1 = ファイルはスパース ファイルです。<br /><br /> 0 = ファイルはスパース ファイルではありません。<br /><br /> 詳細については、「[データベース スナップショットのスパース ファイルのサイズを表示する方法 &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)」を参照してください。|  
|is_percent_growth|**bit**|1 = ファイルの拡張はパーセンテージで表されます。<br /><br /> 0 = ページ単位の絶対拡張サイズ。|  
|is_name_reserved|**bit**|1 = 削除されたファイル名は再利用可能です。 新しいファイル名に対して名前 (name または physical_name) を再使用するには、ログのバックアップを実行する必要があります。<br /><br /> 0 = ファイル名を再利用することはできません。|  
|create_lsn|**numeric(25,0)**|ファイルが作成されたログ シーケンス番号 (LSN) です。|  
|drop_lsn|**numeric(25,0)**|ファイルが削除された LSN。|  
|read_only_lsn|**numeric(25,0)**|ファイルを含むファイルグループが読み取り/書き込みから読み取り専用 (最新の変更) に変更された LSN。|  
|read_write_lsn|**numeric(25,0)**|ファイルを含むファイルグループが読み取り専用から読み取り/書き込み (最新の変更) に変更された LSN。|  
|differential_base_lsn|**numeric(25,0)**|差分バックアップのベースです。 この LSN の後に変更されたデータエクステントは、差分バックアップに含まれます。|  
|differential_base_guid|**uniqueidentifier**|差分バックアップの基になるベースバックアップの一意識別子。|  
|differential_base_time|**datetime**|differential_base_lsn に対応する時間です。|  
|redo_start_lsn|**numeric(25,0)**|次のロールフォワードを開始する必要がある LSN です。<br /><br /> state = RESTORING または state = RECOVERY_PENDING でない場合は NULL です。|  
|redo_start_fork_guid|**uniqueidentifier**|復旧分岐の一意識別子です。 復元される次のログ バックアップの first_fork_guid は、この値と一致する必要があります。 これは、コンテナーの現在の状態を表します。|  
|redo_target_lsn|**numeric(25,0)**|このファイルのオンラインロールフォワードが停止できる LSN です。<br /><br /> state = RESTORING または state = RECOVERY_PENDING でない場合は NULL です。|  
|redo_target_fork_guid|**uniqueidentifier**|コンテナーを回復できる復旧分岐。 redo_target_lsn と組み合わせて使用します。|  
|backup_lsn|**numeric(25,0)**|ファイルの最新のデータまたは差分バックアップの LSN。|  
|credential_id|**int**|ファイルの格納に使用される `sys.credentials` の `credential_id`。 たとえば、Azure 仮想マシンで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されていて、データベースファイルが Azure blob storage に格納されている場合、資格情報はストレージの場所のアクセス資格情報を使用して構成されます。|  
  
> [!NOTE]  
>  大きなインデックスを削除または再構築したり、大きなテーブルを削除したり切り捨てたりすると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] は、トランザクションがコミットされるまで、実際のページ割り当て解除とそれに関連付けられているロックを延期します。 遅延削除操作では、割り当てられた領域はすぐに解放されません。 そのため、ラージ オブジェクトを削除または切り捨てた後すぐに sys.master_files から返される値は、実際の使用可能ディスク領域を表していない場合があります。  
  
## <a name="permissions"></a>アクセス許可  
 対応する行を表示するために必要な最小限の権限は、CREATE DATABASE、ALTER ANY DATABASE、または VIEW ANY DEFINITION です。  
  
## <a name="see-also"></a>参照  
 [データベースとファイルのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [ファイルの状態](../../relational-databases/databases/file-states.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [データベース ファイルとファイル グループ](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
