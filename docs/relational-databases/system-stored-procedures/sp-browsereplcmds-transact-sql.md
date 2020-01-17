---
title: sp_browsereplcmds (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsereplcmds_TSQL
- sp_browsereplcmds
helpviewer_keywords:
- sp_browsereplcmds
ms.assetid: 30abcb41-1d18-4f43-a692-4c80914c0450
author: stevestein
ms.author: sstein
ms.openlocfilehash: d049a5e96d9c7212467595aa70cd44db727bdf6e
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768998"
---
# <a name="spbrowsereplcmds-transact-sql"></a>sp_browsereplcmds (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  ディストリビューション データベースに格納されているレプリケートされたコマンドの結果セットを判読可能な形で返します。診断ツールとして使用できます。 このストアド プロシージャは、ディストリビューター側でディストリビューション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_browsereplcmds [ [ @xact_seqno_start = ] 'xact_seqno_start' ]  
    [ , [ @xact_seqno_end = ] 'xact_seqno_end' ]   
    [ , [ @originator_id = ] 'originator_id' ]  
    [ , [ @publisher_database_id = ] 'publisher_database_id' ]  
    [ , [ @article_id = ] 'article_id' ]  
    [ , [ @command_id= ] command_id ]  
    [ , [ @agent_id = ] agent_id ]  
    [ , [ @compatibility_level = ] compatibility_level ]  
```  
  
## <a name="arguments"></a>引数  
`[ @xact_seqno_start = ] 'xact_seqno_start'`返される最小値の正確なシーケンス番号を指定します。 *xact_seqno_start*は**nchar (22)** ,、既定値は0x00000000000000000000 です。  
  
`[ @xact_seqno_end = ] 'xact_seqno_end'`返される正確なシーケンス番号の最大値を指定します。 *xact_seqno_end*は**nchar (22)** ,、既定値は0xffffffffffffffffffff です。  
  
`[ @originator_id = ] 'originator_id'`指定した*originator_id*のコマンドを返すかどうかを指定します。 *originator_id*は**int**,、既定値は NULL です。  
  
`[ @publisher_database_id = ] 'publisher_database_id'`指定した*publisher_database_id*のコマンドを返すかどうかを指定します。 *publisher_database_id*は**int**,、既定値は NULL です。  
  
`[ @article_id = ] 'article_id'`指定した*コ*のコマンドを返すかどうかを指定します。 *コ*は**int**,、既定値は NULL です。  
  
`[ @command_id = ] command_id`デコードする[MSrepl_commands &#40;&#41; ](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)のコマンドの場所を指定します。 *command_id*は**int**,、既定値は NULL です。 指定する場合は、他のすべてのパラメーターも指定する必要があり、 *xact_seqno_start*は*xact_seqno_end*と同じである必要があります。  
  
`[ @agent_id = ] agent_id`特定のレプリケーションエージェントのコマンドのみが返されるように指定します。 *agent_id*は**int**,、既定値は NULL です。  
  
`[ @compatibility_level = ] compatibility_level`*Compatibility_level*が**int**で[!INCLUDE[msCoName](../../includes/msconame-md.md)]あるの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]バージョンを指定します。既定値は900万です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**varbinary(16)**|コマンドのシーケンス番号。|  
|**originator_srvname**|**sysname**|トランザクションが発生したサーバー。|  
|**originator_db**|**sysname**|トランザクションが発生したデータベース。|  
|**article_id**|**int**|アーティクルの ID。|  
|**type**|**int**|コマンドの種類。|  
|**partial_command**|**bit**|部分的なコマンドかどうかを示します。|  
|**hashkey**|**int**|内部使用のみです。|  
|**originator_publication_id**|**int**|トランザクションが発生したパブリケーションの ID。|  
|**originator_db_version**|**int**|トランザクションが発生したデータベースのバージョン。|  
|**originator_lsn**|**varbinary(16)**|元のパブリケーションのコマンドのログシーケンス番号 (LSN) を識別します。 ピアツーピアトランザクションレプリケーションで使用されます。|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)]メニュー.|  
|**command_id**|**int**|[MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)内のコマンドの ID。|  
  
 長いコマンドは、結果セット内の複数の行に分割できます。  
  
## <a name="remarks"></a>コメント  
 **sp_browsereplcmds**は、トランザクションレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_browsereplcmds**を実行できるのは、固定サーバーロール**sysadmin**のメンバー、またはディストリビューションデータベースの固定データベースロール**db_owner**または**replmonitor**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replshowcmds &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
