---
title: sys.database_mirroring (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring
- database_mirroring
- sys.database_mirroring_TSQL
- database_mirroring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_mirroring catalog view
ms.assetid: 480de2b0-2c16-497d-a6a3-bf7f52a7c9a0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 515f3dad1f07535a5d0c8e590adadce0923180db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022750"
---
# <a name="sysdatabasemirroring-transact-sql"></a>sys.database_mirroring (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  インスタンス内の各データベースの 1 つの行を含む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 データベースがオンラインでないか、データベース ミラーリングが有効でない場合、database_id を除くすべての列の値は NULL になります。  
  
 Master または tempdb 以外のデータベースの行を表示するには、データベース所有者であるかが少なくとも ALTER ANY DATABASE または VIEW ANY DATABASE のサーバー レベル権限、または master データベースで CREATE DATABASE 権限。 ミラー データベースで NULL 以外の値を表示する、 **sysadmin**固定サーバー ロール。  
  
> [!NOTE]  
>  データベースがミラーリングに参加していない場合、"mirroring ですべて列は NULL を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|データベースの ID です。 インスタンス内で一意では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|**mirroring_guid**|**uniqueidentifier**|ミラーリング パートナーシップの ID。<br /><br /> NULL = データベースにアクセスできないか、ミラー化されていません。<br /><br /> 注:データベースがミラーリングに参加していない場合は場合、"mirroring ですべての列は NULL を使用します。|  
|**mirroring_state**|**tinyint**|ミラー データベースとデータベース ミラーリング セッションの状態します。<br /><br /> 0 = 中断状態<br /><br /> 1 = 他のパートナーから切断<br /><br /> 2 = 同期中<br /><br /> 3 = フェールオーバーを保留しています<br /><br /> 4 = 同期済み<br /><br /> 5 = パートナーが同期されていません。 フェールオーバーは不可能なようになりました。<br /><br /> 6 = パートナーが同期されています。 フェールオーバーは、可能性のある可能性があります。 フェールオーバーでは、「要件について[Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)します。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_state_desc**|**nvarchar(60)**|データベース ミラーリング セッションのミラー データベースの状態の説明には、いずれかを指定できます。<br /><br /> DISCONNECTED<br /><br /> SYNCHRONIZED<br /><br /> SYNCHRONIZING<br /><br /> PENDING_FAILOVER<br /><br /> SUSPENDED<br /><br /> 同期されていません。<br /><br /> SYNCHRONIZED<br /><br /> NULL<br /><br /> 詳細については、「[ミラーリング状態 &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)」を参照してください。|  
|**mirroring_role**|**tinyint**|データベース ミラーリング セッションにおけるローカル データベースの現在のロールです。<br /><br /> 1 = プリンシパル<br /><br /> 2 = ミラー<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_role_desc**|**nvarchar(60)**|ミラー化におけるローカル データベースのロールの説明。次のいずれかになります。<br /><br /> PRINCIPAL<br /><br /> MIRROR|  
|**mirroring_role_sequence**|**int**|ミラーリング パートナーがフェールオーバーによりプリンシパルとミラーの役割を交換またはサービスの強制がある回数。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_safety_level**|**tinyint**|ミラー データベースの更新に関する安全性設定:<br /><br /> 0 = 状態不明<br /><br /> 1 = オフ (非同期)<br /><br /> 2 = 完全 (同期)<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_safety_level_desc**|**nvarchar(60)**|ミラー データベースの更新に関するトランザクションの安全性の設定。次のいずれかになります。<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL<br /><br /> NULL|  
|**mirroring_safety_sequence**|**int**|トランザクションの安全性レベルに変更のシーケンス番号を更新します。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_partner_name**|**nvarchar(128)**|データベース ミラーリング パートナーのサーバー名。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_partner_instance**|**nvarchar(128)**|他のパートナーに対するインスタンス名とコンピューター名。 クライアントでは、プリンシパル サーバーとなる場合に、パートナーに接続するには、この情報が必要です。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_witness_name**|**nvarchar(128)**|データベース ミラーリング監視サーバーのサーバー名。<br /><br /> NULL = ミラーリング監視サーバーはありませんが存在します。|  
|mirroring_witness_state|**tinyint**|データベース ミラーリング セッションは、データベースのミラーリング監視サーバーの状態は、いずれかを指定できます。<br /><br /> 0 = 不明<br /><br /> 1 = 接続済み<br /><br /> 2 = 切断<br /><br /> NULL = No ミラーリング監視サーバーが存在するデータベースがオンラインでないか、データベースがミラー化されていません。|  
|**mirroring_witness_state_desc**|**nvarchar(60)**|状態の説明には、いずれかを指定できます。<br /><br /> UNKNOWN<br /><br /> CONNECTED<br /><br /> DISCONNECTED<br /><br /> NULL|  
|**mirroring_failover_lsn**|**numeric(25,0)**|両方のパートナー上のディスクに書き込まれることが保証される最新のトランザクション ログ レコードのシーケンス番号 (LSN) を記録します。 フェールオーバー後、 **mirroring_failover_lsn**の調整が新しいミラー サーバーが新しいプリンシパル データベースと、新しいミラー データベースを同期する開始点として、パートナーによって使用されます。|  
|**mirroring_connection_timeout**|**int**|接続タイムアウトを秒単位でミラーリングします。 これは、パートナーまたはミラーリング監視サーバーからの返信を待機する秒数です。この時間を過ぎるとパートナーまたはミラーリング監視サーバーは使用できないものと見なされます。 タイムアウトの既定値は 10 秒です。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_redo_queue**|**int**|ミラー化で再実行されるログの最大サイズ。 Mirroring_redo_queue_type が既定の設定はの UNLIMITED に設定されている場合、この列は NULL を使用します。 データベースがオンラインでない場合も、この列は NULL になります。<br /><br /> 上記以外の場合、この列にはログの最大サイズ (MB 単位) が格納されます。 ログが一時停止、最大値に達すると、サーバーが遅れ、ミラーのプリンシパルにします。 この機能は、フェールオーバー時間を制限します。<br /><br /> 詳しくは、「 [役割の交代中に発生するサービスの中断時間の算出 &#40;データベース ミラーリング&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md)という処理により、一般的にプリンシパルとミラーの役割を相互交換できます。|  
|**mirroring_redo_queue_type**|**nvarchar(60)**|無制限では、こと、ミラーリングも再実行キューは抑制しないことを示します。 これが既定の設定です。<br /><br /> メガ バイト単位で再実行キューの最大サイズを MB です。 キューのサイズをキロバイト単位またはギガバイト、として指定された場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]値メガバイト単位に変換します。<br /><br /> データベースがオンラインでない場合、この列は NULL を使用します。|  
|**mirroring_end_of_log_lsn**|**numeric(25,0)**|ローカル エンド ログのフラッシュされたディスクにします。 これは、ミラー サーバーから書き込まれた LSN に相当 (を参照してください、 **mirroring_failover_lsn**列)。|  
|**mirroring_replication_lsn**|**numeric(25,0)**|レプリケーションが送信できる最大 LSN。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [データベースとファイルのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
