---
title: 部分バックアップ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- partial backups [SQL Server]
- READ_WRITE_FILEGROUPS option
- database backups [SQL Server], about backing up databases
ms.assetid: fe6b6bb1-38d0-46c4-bab8-31df14e8999c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a2c265d3a373eb53b822142fa2955d07b96b88f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033659"
---
# <a name="partial-backups-sql-server"></a>部分バックアップ (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 復旧モデルで部分バックアップがサポートされるため、このトピックの内容はすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに適用されます。 ただし、部分バックアップは、1 つ以上の読み取り専用のファイル グループを含む非常に大きなデータベースをバックアップする場合の柔軟性を向上するために、単純復旧モデルで使用することを目的としています。  
  
 読み取り専用のファイル グループを除外する場合は、部分バックアップが有効です。 *部分バックアップ* はデータベースの完全バックアップに似ていますが、部分バックアップには一部のファイル グループが含まれません。 部分バックアップに含まれるデータは、読み取り/書き込み可能なデータベースの場合、プライマリ ファイル グループのデータ、読み取りと書き込みが可能なすべてのファイル グループのデータ、および必要に応じて指定された読み取り専用ファイルのデータです。 読み取り専用データベースの部分バックアップには、プライマリ ファイル グループのみが含まれます。  
  
> [!NOTE]  
>  部分バックアップの後に、読み取り専用のデータベースを読み取り/書き込み可能に変更すると、部分バックアップには含まれない、読み取り/書き込みセカンダリ ファイル グループが存在することになります。 この場合、部分的な差分バックアップの実行を試みると、バックアップに失敗します。 データベースの部分的な差分バックアップを実行する前に、別の部分バックアップを実行する必要があります。 新しい部分バックアップには、すべての読み取り/書き込みセカンダリ ファイル グループが含まれるので、このバックアップを部分的な差分バックアップのベースにすることができます。  
  
 読み取り専用ファイル グループのファイル バックアップは、部分バックアップと組み合わせることができます。 ファイルのバックアップの詳細については、「[ファイルの完全バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)」を参照してください。  
  
 部分バックアップは、部分的な差分バックアップの *差分ベース* として使用できます。 詳細については、「 [差分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
> [!NOTE]  
>  部分バックアップは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] またはメンテナンス プラン ウィザードではサポートされません。  
  
 **部分バックアップを作成するには**  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md) (必要に応じて READ_WRITE_FILEGROUPS; FILEGROUP オプションを使用)  
  
 **復元シーケンスで部分バックアップを使用するには**  
  
-   [例: データベースの段階的な部分復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [例: 一部のファイル グループのみを復元する段階的な部分復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="see-also"></a>参照  
 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [ファイルの復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
