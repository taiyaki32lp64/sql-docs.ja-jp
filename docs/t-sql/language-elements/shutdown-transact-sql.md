---
title: SHUTDOWN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SHUTDOWN_TSQL
- SHUTDOWN
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server, stopping
- shutting down SQL Server
- SHUTDOWN statement
- stopping SQL Server
- immediately stopping SQL Server
ms.assetid: c8b03ff9-688c-4fe8-86e8-bd6bd401c9a4
author: rothja
ms.author: jroth
ms.openlocfilehash: 01cf9fcf7795e8f353565b767bbf79b1da43f4de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121702"
---
# <a name="shutdown-transact-sql"></a>SHUTDOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  SQL Server を直ちに停止します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SHUTDOWN [ WITH NOWAIT ]   
```  
  
## <a name="arguments"></a>引数  
 WITH NOWAIT  
 省略可。 各データベースでチェックポイントを実行せずに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をシャットダウンします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はすべてのユーザー プロセスの停止を試行した後に終了します。 サーバーが再起動すると、完了しなかったトランザクションのロールバック操作が行われます。  
  
## <a name="remarks"></a>Remarks  
 WITHNOWAIT オプションを使用しない場合、SHUTDOWN では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が次のようにシャットダウンされます。  
  
1.  ログインを無効にする (固定サーバー ロール **sysadmin** および **serveradmin** のメンバーを除く)。  
  
    > [!NOTE]  
    >  現在のすべてのユーザーの一覧を表示するには、**sp_who** を実行します。  
  
2.  現在実行中の Transact-SQL ステートメントまたはストアド プロシージャが終了するまで待機する。 すべてのアクティブなプロセスとロックの一覧を表示するには、それぞれ **sp_who** および **sp_lock** を実行します。  
  
3.  各データベースにチェックポイントを挿入する。  
  
 SHUTDOWN ステートメントを使用すると、固定サーバー ロール **sysadmin** のメンバーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動したときに必要となる自動復旧作業が最小限に抑えられます。  
  
 後に示すツールや方法を使用しても [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を停止できます。 いずれの停止方法でも、すべてのデータベースでチェックポイントが発行されます。 コミットされたデータをデータ キャッシュからフラッシュして、サーバーを停止できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用する。  
  
-   既定のインスタンスのコマンド プロンプトから **net stop mssqlserver** を実行する。または、名前付きインスタンスのコマンド プロンプトから **net stop mssql$** _instancename_ を実行する。  
  
-   [コントロール パネル] の [サービス] を使用する。  
  
 **sqlservr.exe** をコマンド プロンプトから起動した場合は、Ctrl キーを押しながら C キーを押すと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がシャットダウンされます。 Ctrl+C キーを押してもチェックポイントは挿入されません。  
  
> [!NOTE]  
>  どの方法で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を停止しても、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には `SERVICE_CONTROL_STOP` メッセージが送信されます。  
  
## <a name="permissions"></a>アクセス許可  
 SHUTDOWN アクセス許可は、既定では固定サーバー ロール **sysadmin** および **serveradmin** のメンバーに与えられています。このアクセス許可を譲渡することはできません。  
  
## <a name="see-also"></a>参照  
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sqlservr アプリケーション](../../tools/sqlservr-application.md)   
 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
