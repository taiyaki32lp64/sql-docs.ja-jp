---
title: エンタープライズ全体の管理の自動化 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b3be16ea856b5d632ba5a0285bad2c4d2d93709c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62473150"
---
# <a name="automated-administration-across-an-enterprise"></a>エンタープライズ全体の管理の自動化
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の複数のインスタンスにわたって管理を自動化することを*マルチサーバー管理*といいます。 次の場合に、マルチサーバー管理を行います。  
  
-   2 台以上のサーバーを管理する場合  
  
-   データ ウェアハウジングのために、企業サーバーの情報フローをスケジュールする場合  
  
> [!NOTE]  
>  一部として[!INCLUDE[msCoName](../../includes/msconame-md.md)]、所有権の総コストを削減する継続的な取り組み[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]2 つの機能が導入されました: ポリシー ベースの管理と構成サーバーとサーバーを使用するマルチ サーバー クエリに呼び出されるサーバーを管理する方法グループ。 この 2 つの機能は、ここで説明する機能の一部と組み合わせたり、それらの代わりとして使用したりすることができます。 詳細については、次を参照してください。[でポリシー ベースの管理サーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)と[複数サーバーを使用して中央管理サーバーの管理](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)します。  
  
 マルチサーバー管理機能を活用するには、1 台以上のマスター サーバーと 1 台以上のターゲット サーバーが必要です。 マスター サーバーは、ターゲット サーバーに対してジョブを分散し、ターゲット サーバーからイベントを受け取ります。 また、マスター サーバーは、ターゲット サーバーで実行されるジョブについて、ジョブ定義の中央コピーも保存します。 ターゲット サーバーは、定期的にマスター サーバーに接続して、ジョブのスケジュールを更新します。 マスター サーバー上に新しいジョブがあれば、ターゲット サーバーはそのジョブをダウンロードします。 ターゲット サーバーは、ジョブを完了した後、マスター サーバーに再接続してジョブのステータスをレポートします。  
  
 次の図は、マスター サーバーとターゲット サーバーの関係を示します。  
  
 ![マルチ サーバー管理構成](../../database-engine/media/multisvr.gif "マルチ サーバー管理構成")  
  
 大企業の複数の部門別サーバーを管理する場合は、次のアイテムを定義できます。  
  
-   複数のジョブ ステップから構成される 1 つのバックアップ ジョブ  
  
-   バックアップ エラーが発生した場合に通知するオペレーター  
  
-   バックアップ ジョブの実行スケジュール  
  
 マスター サーバーにこのバックアップ ジョブを 1 回書き込んでから、各部門別サーバーをターゲット サーバーとして登録します。 この登録以降は、ジョブを一度しか定義しなくても、すべての部門別サーバーで同じバックアップ ジョブが実行されます。  
  
> [!NOTE]  
>  マルチサーバー管理機能は、sysadmin ロールのメンバーを対象としています。 ただし、ターゲット サーバー上の sysadmin ロールのメンバーは、マスター サーバーから、ターゲット サーバーで実行される操作を変更することはできません。 このセキュリティ措置によって、ジョブ ステップが誤って削除されたり、ターゲット サーバー上の操作が中断したりすることを防止できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [マルチサーバー環境の作成](create-a-multiserver-environment.md)  
 マスター サーバーおよびターゲット サーバーを作成および管理する方法について説明します。  
  
 [マルチサーバー環境に適した SQL Server エージェント サービス アカウントの選択](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント サービスに管理者以外の Windows アカウントまたはローカル システム アカウントを使用することによる、マルチサーバー環境への影響について説明します。  
  
 [対象サーバーでの暗号化オプションの設定](set-encryption-options-on-target-servers.md)  
 ターゲット サーバーの MsxEncryptChannelOptions [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントのレジストリ サブキーの設定について説明します。  
  
 [エンタープライズ全体におけるジョブの管理](manage-jobs-across-an-enterprise.md)  
 ジョブ ステータスの確認、ジョブのターゲット サーバーの変更、ターゲット サーバーのクロックの同期、およびマスター サーバーの現在のジョブ ステータスに対するポーリングについて説明します。  
  
 [プロキシを使用するマルチサーバー ジョブのトラブルシューティング](troubleshoot-multiserver-jobs-that-use-proxies.md)  
 プロキシを使用しているマルチサーバー ジョブに障害が発生した場合のトラブルシューティングについて説明します。  
  
 [サーバーのポーリング](poll-servers.md)  
 ターゲット サーバーをマスター サーバーに明示的および暗黙的にポーリングして、ジョブ情報の同期をとる方法について説明します。  
  
 [イベントの管理](manage-events.md)  
 ターゲット サーバーからマスター サーバーに転送されるイベントについて説明します。  
  
 [企業全体の自動管理のチューニング](tune-automated-administration-across-an-enterprise.md)  
 マルチサーバー環境で自動化された管理により [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の自己チューニング機能を活用する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [SQL Server データベース エンジンの旧バージョンとの互換性](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [サーバーの登録](../register-servers/register-servers.md)   
 [sp_add_targetservergroup &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql)   
 [sp_delete_targetserver &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql)   
 [sp_delete_targetservergroup &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql)   
 [sp_help_downloadlist &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql)   
 [sp_help_jobserver &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql)   
 [sp_help_targetservergroup &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql)   
 [sp_resync_targetserver &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)   
 [sp_update_targetservergroup &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql)   
 [dbo.sysjobservers &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobservers-transact-sql)   
 [sys.syslogins &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslogins-transact-sql)   
 [dbo.systargetservers &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-tables/dbo-systargetservers-transact-sql)  
  
  
