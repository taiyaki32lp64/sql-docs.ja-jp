---
title: sp_who (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_who_TSQL
- sp_who
dev_langs:
- TSQL
helpviewer_keywords:
- sp_who
ms.assetid: 132dfb08-fa79-422e-97d4-b2c4579c6ac5
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5d758c7ca2d21183b9486030704c31b9d5f621d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950512"
---
# <a name="sp_who-transact-sql"></a>sp_who (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のユーザー、セッション、およびプロセスのインスタンスに関する情報を提供、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]します。 情報は、アイドル状態ではない、特定のユーザーに属している、または特定のセッションに属するプロセスだけを返すフィルター処理できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_who [ [ @loginame = ] 'login' | session ID | 'ACTIVE' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @loginame = ] 'login' | session ID | 'ACTIVE'` 結果セットをフィルター処理に使用されます。  
  
 *ログイン*は**sysname**特定のログインに属するプロセスを識別します。  
  
 *セッション ID*に属するセッション識別番号、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス。 *セッション ID*は**smallint**します。  
  
 **アクティブな**ユーザーからの次のコマンドを待機しているセッションを除外します。  
  
 値を指定しない場合は、インスタンスに属するすべてのセッションがレポートされます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 **sp_who**次の情報を含む結果セットを返します。  
  
|[列]|データ型|説明|  
|------------|---------------|-----------------|  
|**spid**|**smallint**|セッション ID。|  
|**ecid**|**smallint**|特定のセッション ID に関連付けられている、指定されたスレッドの実行コンテキスト ID。<br /><br /> ECID = {0、1、2、3、...*n*} 0 常を表しますメインまたは親スレッド、および {1、2、3、...、*n*}、サブスレッドを表します。|  
|**status**|**nchar(30)**|プロセスの状態。 設定できる値は次のとおりです。<br /><br /> **dormant** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でセッションがリセットされています。<br /><br /> **running** セッションには、1 つまたは複数のバッチが実行中です。 複数のアクティブな結果セット (MARS) が有効にすると、セッションは、複数のバッチを実行できます。 詳細については、「[複数のアクティブな結果セット &#40;MARS&#41; の使用](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)」を参照してください。<br /><br /> **background** セッションがデッドロック検出などのバック グラウンド タスクを実行中です。<br /><br /> **rollback** セッションでトランザクション ロールバックが実行中です。<br /><br /> **pending** セッションは、ワーカー スレッドが使用可能になるのを待機しています。<br /><br /> **runnable** セッションのタスクはクォンタムの取得を待機中にスケジューラの実行可能キューでです。<br /><br /> **spinloop**します。 セッションのタスクはスピンロックの空きを待機しています。<br /><br /> **suspended** セッションが完了する I/O などのイベントを待機しています。|  
|**loginame**|**nchar(128)**|特定のプロセスに関連付けられているログイン名です。|  
|**hostname**|**nchar(128)**|各プロセスのホストまたはコンピューターの名前。|  
|**blk**|**char (5)**|ブロック中のプロセスが存在する場合は、そのプロセスのセッション ID。 存在しない場合は、この列は 0 になります。<br /><br /> 指定したセッション ID に関連付けられたトランザクションが、孤立した分散トランザクションによってブロックされると、この列は、ブロックの孤立したトランザクションに対して '-2' を返します。|  
|**dbname**|**nchar(128)**|プロセスによって使用されるデータベース。|  
|**cmd**|**nchar(16)**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] コマンド ([!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントでは、内部[!INCLUDE[ssDE](../../includes/ssde-md.md)]プロセスが、)、プロセスを実行します。|  
|**request_id**|**int**|特定のセッションで実行されている要求の ID。|  
  
 特定のセッション ID に対してサブスレッドが生成並列処理の場合 メイン スレッドは `spid = <xxx>` および `ecid =0` のように示されます。 その他のサブスレッドが同じである`spid = <xxx>`、ですが、 **ecid** > 0。  
  
## <a name="remarks"></a>コメント  
 排他ロックがあります、ブロックしているプロセスは、別のプロセスが必要なリソースを保持している 1 つ。  
  
 孤立したすべての分散トランザクションにセッション ID 値 '-2' が割り当てられます。 孤立した分散トランザクションとは、どのセッション ID にも関連付けられていない分散トランザクションです。 詳細については、「 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)」を参照してください。  
  
 クエリ、 **is_user_process**ユーザー プロセスからシステム プロセスを分離する sys.dm_exec_sessions の列。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで実行されているすべてのセッションを確認するには、サーバーに対する VIEW SERVER STATE 権限が必要です。 権限がない場合、ユーザーは現在のセッションだけを確認できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-all-current-processes"></a>A. 現在のすべてのプロセスを一覧表示する  
 次の例では`sp_who`すべて現在のユーザーをレポートにパラメーターを指定せずします。  
  
```  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
### <a name="b-listing-a-specific-users-process"></a>B. 特定のユーザーのプロセスを一覧表示する  
 次の例では、ログイン名を使用して、現在のユーザーに関する情報を表示します。  
  
```  
USE master;  
GO  
EXEC sp_who 'janetl';  
GO  
```  
  
### <a name="c-displaying-all-active-processes"></a>C. すべてのアクティブ プロセスを表示します。  
  
```  
USE master;  
GO  
EXEC sp_who 'active';  
GO  
```  
  
### <a name="d-displaying-a-specific-process-identified-by-a-session-id"></a>D. セッション ID で識別される特定のプロセスを表示します。  
  
```  
USE master;  
GO  
EXEC sp_who '10' --specifies the process_id;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
