---
title: (レプリケーション TRANSACT-SQL プログラミング) のバックアップからトランザクション サブスクリプションの初期化 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7e7fb32de254729c4173fab260e5797db5f2cc2f
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793299"
---
# <a name="initialize-a-transactional-subscription-from-a-backup-replication-transact-sql-programming"></a>トランザクション サブスクリプションのバックアップからの初期化 (レプリケーション Transact-SQL プログラミング)
  トランザクション パブリケーションのサブスクリプションは通常、スナップショットを使用して初期化されますが、レプリケーション ストアド プロシージャを使用して、バックアップからサブスクリプションを初期化することもできます。 詳細については、「 [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md)を使用して、サブスクリプションを手動で初期化する方法について説明します。  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>トランザクション サブスクライバーをバックアップから初期化するには  
  
1.  既存のパブリケーションの場合は、パブリッシャーのパブリケーション データベースで [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) を実行して、バックアップから初期化する機能をパブリケーションがサポートしているかどうかを確認します。 結果セットの **allow_initialize_from_backup** の値を確認します。  
  
    -   この値が **1**の場合、パブリケーションはこの機能をサポートしています。  
  
    -   この値が **0** の場合、パブリッシャー側のパブリケーション データベースに対して [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) を実行します。 値を指定**allow_initialize_from_backup**の **\@プロパティ**の値と`true`の **\@値**します。  
  
2.  新しいパブリケーションの場合、パブリッシャー側のパブリケーション データベースに対して [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) を実行します。 値を指定`true`の**allow_initialize_from_backup**します。 詳細については、「 [Create a Publication](publish/create-a-publication.md)」を参照してください。  
  
    > [!WARNING]  
    >  サブスクライバー データの欠落を回避するために、 **sp_addpublication** で `@allow_initialize_from_backup = N'true'`を使用する場合は、常に `@immediate_sync = N'true'`を使用します。  
  
3.  [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql) ステートメントを使用して、パブリケーション データベースのバックアップを作成します。  
  
4.  [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql) ステートメントを使用し、サブスクライバー上でバックアップを復元します。  
  
5.  パブリッシャー側のパブリケーション データベースに対して、ストアド プロシージャ [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) を実行します。 次のパラメーターを指定します。  
  
    -   **\@sync_type** -の値**バックアップを使用して初期化**します。  
  
    -   **\@backupdevicetype** -バックアップ デバイスの種類:**論理**(既定)、**ディスク**、または**テープ**します。  
  
    -   **\@backupdevicename** -復元に使用する論理または物理バックアップ デバイス。  
  
         論理デバイスの場合は、 **sp_addumpdevice** を使ってデバイスを作成する際に指定したバックアップ デバイスの名前を指定します。  
  
         物理デバイスの場合は、「 `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\BACKUP\Mybackup.dat'` 」または「 `TAPE = '\\.\TAPE0'`」のように、完全なパスとファイル名を指定します。  
  
    -   (省略可能) **\@パスワード**-バックアップ セットの作成時に提供されたパスワード。  
  
    -   (省略可能) **\@mediapassword** -メディア セットのフォーマット時に指定されたパスワード。  
  
    -   (省略可能) **\@fileidhint** -復元するバックアップ セットの識別子。 たとえば、 **1** はバックアップ メディアの 1 番目のバックアップ セットを示し、 **2** は 2 番目のバックアップ セットを示します。  
  
    -   (テープ デバイスは省略可能) **\@アンロード**-の値を指定**1** (既定) 場合は、復元が完了した後にテープがドライブから読み込まれたにするか、 **0**アンロードする場合.  
  
6.  (省略可能) プル サブスクリプションの場合は、サブスクライバーのサブスクリプション データベースで [sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql) と [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) を実行します。 詳細については、「 [Create a Pull Subscription](create-a-pull-subscription.md)」を参照してください。  
  
7.  (省略可) ディストリビューション エージェントを起動します。 詳細については、「 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 」または「 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [バックアップと復元によるデータベースのコピー](../databases/copy-databases-with-backup-and-restore.md)   
 [SQL Server データベースのバックアップと復元](../backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
