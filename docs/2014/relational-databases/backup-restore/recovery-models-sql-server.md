---
title: 復旧モデル (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], recovery models
- bulk-logged recovery model [SQL Server]
- recovery [SQL Server], recovery model
- restoring transaction logs [SQL Server], recovery models
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], about
- transaction log backups [SQL Server]
- simple recovery model [SQL Server]
- backups [SQL Server], recovery models
- recovery models [SQL Server]
- recovery models [SQL Server], transaction log management
- database restores [SQL Server], recovery models
- transaction log restores [SQL Server]
- logs [SQL Server], recovery models
- restoring databases [SQL Server], recovery models
- full recovery model [SQL Server]
- backing up transaction logs [SQL Server], recovery models
ms.assetid: 8cfea566-8f89-4581-b30d-c53f1f2c79eb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6c5b85e316c859e0b6d44fb83e3df6da2edd72ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921767"
---
# <a name="recovery-models-sql-server"></a>復旧モデル (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップ操作および復元操作は、データベースの復旧モデルのコンテキストで発生します。 復旧モデルは、トランザクション ログのメンテナンスを制御するように設計されています。 *復旧モデル* とは、トランザクションをログに記録する方法、トランザクション ログのバックアップを必須 (および可能) にするかどうか、利用できる復元操作の種類などを制御するデータベース プロパティです。 復旧モデルの種類は、単純、完全、および一括ログの 3 種類です。 通常、データベースには完全復旧モデルまたは単純復旧モデルが使用されます。 データベースは、任意の時点で別の復旧モデルに切り替えることができます。  
  
 **このトピックの内容**  
  
-   [復旧モデルの概要](#RMov)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="RMov"></a> 復旧モデルの概要  
 次の表に、3 つの復旧モデルの概要を示します。  
  
|復旧モデル|説明|作業の損失の可能性|指定日時への復旧|  
|--------------------|-----------------|------------------------|-------------------------------|  
|**Simple**|ログ バックアップはありません。<br /><br /> 必要な領域が少なくなるように、ログ領域が自動的に再利用されます。このため、トランザクション ログ領域の管理は基本的に必要ありません。 単純復旧モデルでのデータベース バックアップの詳細については、「[データベースの完全バックアップ &#40;SQL Server&#41;](full-database-backups-sql-server.md)」を参照してください。<br /><br /> トランザクション ログ バックアップを必要とする操作は、単純復旧モデルではサポートされていません。 単純復旧モデルで使用できない機能を次に示します。<br /><br /> ログ配布<br /><br /> AlwaysOn またはデータベース ミラーリング<br /><br /> データ損失のないメディアの復旧<br /><br /> 特定の時点への復元|最新のバックアップ以降の変更は保護されません。 障害が発生した場合、それらの変更は再実行する必要があります。|バックアップの終了時点にのみ復旧できます。 詳細については、「[データベースの全体復元 &#40;単純復旧モデル&#41;](complete-database-restores-simple-recovery-model.md)」を参照してください。|  
|**Full**|ログ バックアップが必要です。<br /><br /> データ ファイルの消失や損傷によって作業が失われることはありません。<br /><br /> アプリケーション エラーやユーザー エラーの発生前など、任意の時点に復旧できます。 完全復旧モデルでのデータベース バックアップの詳細については、「[データベースの完全バックアップ &#40;SQL Server&#41;](full-database-backups-sql-server.md)」および「[データベースの全体復元 &#40;完全復旧モデル&#41;](complete-database-restores-full-recovery-model.md)」を参照してください。|通常はありません。<br /><br /> ログの末尾が損傷している場合は、最新のログ バックアップ以降の変更を再実行する必要があります。|特定の時点に復旧できます (その時点までのバックアップが完全である場合)。 ログ バックアップを使用した障害発生時までの復元の詳細については、「[SQL Server データベースを特定の時点に復元する方法  &#40;完全復旧モデル&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)」を参照してください。<br /><br /> 注:論理的に一貫する必要がある 2 つ以上の完全復旧モデル データベースがあればは、これらのデータベースの回復性を確認する特別な手順を実装する必要があります。 詳細については、「 [マークされたトランザクションを含む関連データベースの復旧](recovery-of-related-databases-that-contain-marked-transaction.md)」を参照してください。|  
|**一括ログ**|ログ バックアップが必要です。<br /><br /> 完全復旧モデルを補完するためのもので、パフォーマンスに優れた一括コピー操作を実行できます。<br /><br /> ほとんどの一括操作で最小ログ記録を使用して、使用されるログ領域を縮小します。 最小ログ記録が可能な操作の詳細については、「[トランザクション ログ &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)」を参照してください。<br /><br /> 一括ログ復旧モデルでのデータベース バックアップの詳細については、「[データベースの完全バックアップ &#40;SQL Server&#41;](full-database-backups-sql-server.md)」および「[データベースの全体復元 &#40;完全復旧モデル&#41;](complete-database-restores-full-recovery-model.md)」を参照してください。|ログが損傷している場合、または最新のログ バックアップ以降に一括ログ操作が行われた場合は、最後のバックアップ以降の変更を再実行する必要があります。<br /><br /> それ以外の場合は、作業が失われることはありません。|バックアップの終了時点に復旧できます。 特定の時点への復旧はサポートされません。|  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベースの復旧モデルの表示または変更 &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [満杯になったトランザクション ログのトラブルシューティング &#40;SQL Server エラー 9002&#41;](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
## <a name="see-also"></a>参照  
 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [SQL Server データベースのバックアップと復元](back-up-and-restore-of-sql-server-databases.md)   
 [トランザクション ログ &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [管理タスクの自動化 &#40;SQL Server エージェント&#41;](../../ssms/agent/sql-server-agent.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
