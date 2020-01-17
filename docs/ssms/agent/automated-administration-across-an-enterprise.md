---
title: エンタープライズ全体の管理の自動化 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enterprise automatic administration [SQL Server]
- multiserver administration [SQL Server]
- SQL Server Agent jobs, multiserver administration
- jobs [SQL Server Agent], multiserver administration
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- master servers [SQL Server]
- multiple instances of SQL Server
- target servers [SQL Server]
ms.assetid: 44d8365b-42bd-4955-b5b2-74a8a9f4a75f
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 29884599271e85e1ea1be04391fe387092351d55
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68252062"
---
# <a name="automated-administration-across-an-enterprise"></a>エンタープライズ全体の管理の自動化
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスにわたって管理を自動化することを *マルチサーバー管理*といいます。 次の場合に、マルチサーバー管理を行います。  
  
-   2 台以上のサーバーを管理する場合  
  
-   データ ウェアハウジングのために、企業サーバーの情報フローをスケジュールする場合  
  
マルチサーバー管理機能を活用するには、1 台以上のマスター サーバーと 1 台以上のターゲット サーバーが必要です。 マスター サーバーは、ターゲット サーバーに対してジョブを分散し、ターゲット サーバーからイベントを受け取ります。 また、マスター サーバーは、ターゲット サーバーで実行されるジョブについて、ジョブ定義の中央コピーも保存します。 ターゲット サーバーは、定期的にマスター サーバーに接続して、ジョブのスケジュールを更新します。 マスター サーバー上に新しいジョブがあれば、ターゲット サーバーはそのジョブをダウンロードします。 ターゲット サーバーは、ジョブを完了した後、マスター サーバーに再接続してジョブのステータスをレポートします。 データベース関連アクティビティを実行するときはジョブの定義が同じでなければならないことに注意してください。  
  
次の図は、マスター サーバーとターゲット サーバーの関係を示します。  
  
![マルチ サーバー管理構成](../../ssms/agent/media/multisvr.gif "マルチ サーバー管理構成")  
  
大企業の複数の部門別サーバーを管理する場合は、次のアイテムを定義できます。  
  
-   複数のジョブ ステップから構成される 1 つのバックアップ ジョブ  
  
-   バックアップ エラーが発生した場合に通知するオペレーター  
  
-   バックアップ ジョブの実行スケジュール  
  
マスター サーバーにこのバックアップ ジョブを 1 回書き込んでから、各部門別サーバーをターゲット サーバーとして登録します。 この登録以降は、ジョブを一度しか定義しなくても、すべての部門別サーバーで同じバックアップ ジョブが実行されます。  
  
> [!NOTE]  
> マルチサーバー管理機能は、sysadmin ロールのメンバーを対象としています。 ただし、ターゲット サーバー上の sysadmin ロールのメンバーは、マスター サーバーから、ターゲット サーバーで実行される操作を変更することはできません。 このセキュリティ措置によって、ジョブ ステップが誤って削除されたり、ターゲット サーバー上の操作が中断したりすることを防止できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
[マルチサーバー環境の作成](../../ssms/agent/create-a-multiserver-environment.md)  
マスター サーバーおよびターゲット サーバーを作成および管理する方法について説明します。  
  
[マルチサーバー環境に適した SQL Server エージェント サービス アカウントの選択](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスに管理者以外の Windows アカウントまたはローカル システム アカウントを使用することによる、マルチサーバー環境への影響について説明します。  
  
[ターゲット サーバーでの暗号化オプションの設定](../../ssms/agent/set-encryption-options-on-target-servers.md)  
ターゲット サーバーの MsxEncryptChannelOptions [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのレジストリ サブキーの設定について説明します。  
  
[エンタープライズ全体におけるジョブの管理](../../ssms/agent/manage-jobs-across-an-enterprise.md)  
ジョブ ステータスの確認、ジョブのターゲット サーバーの変更、ターゲット サーバーのクロックの同期、およびマスター サーバーの現在のジョブ ステータスに対するポーリングについて説明します。  
  
[プロキシを使用するマルチサーバー ジョブのトラブルシューティング](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
プロキシを使用しているマルチサーバー ジョブに障害が発生した場合のトラブルシューティングについて説明します。  
  
[サーバーのポーリング](../../ssms/agent/poll-servers.md)  
ターゲット サーバーをマスター サーバーに明示的および暗黙的にポーリングして、ジョブ情報の同期をとる方法について説明します。  
  
[イベントの管理](../../ssms/agent/manage-events.md)  
ターゲット サーバーからマスター サーバーに転送されるイベントについて説明します。  
  
[企業全体の自動管理のチューニング](../../ssms/agent/tune-automated-administration-across-an-enterprise.md)  
マルチサーバー環境で自動化された管理により [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の自己チューニング機能を活用する方法について説明します。  
  
## <a name="see-also"></a>参照  
[SQL Server データベース エンジンのインストールに関する旧バージョンとの互換性のトピック](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
[サーバーの登録](../register-servers/register-servers.md)  
[sp_add_targetservergroup](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)  
[sp_delete_targetserver](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)  
[sp_delete_targetservergroup](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)  
[sp_help_downloadlist](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)  
[sp_help_jobserver](../../relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql.md)  
[sp_help_targetservergroup](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)  
[sp_resync_targetserver](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)  
[sp_update_targetservergroup](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)  
[sysjobservers](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)  
[syslogins](../../relational-databases/system-compatibility-views/sys-syslogins-transact-sql.md)  
[systargetservers](../../relational-databases/system-tables/dbo-systargetservers-transact-sql.md)  
  
