---
title: sp_replcmds (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replcmds_TSQL
- sp_replcmds
helpviewer_keywords:
- sp_replcmds
ms.assetid: 7e932f80-cc6e-4109-8db4-2b7c8828df73
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3d60de0f459ec1224f6023e8ee848227fdc17ece
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771007"
---
# <a name="spreplcmds-transact-sql"></a>sp_replcmds (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  レプリケーション用にマークされたトランザクションのコマンドを返します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
> [!IMPORTANT]  
>  **Sp_replcmds**プロシージャは、レプリケーションに関する問題のトラブルシューティングを行う場合にのみ実行してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>引数  
`[ @maxtrans = ] maxtrans`情報を返すトランザクションの数を指定します。 *maxtrans*は**int**,、既定値は**1**,、ディストリビューションを待機している次のトランザクションを指定します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**アーティクル id**|**int**|アーティクルの ID です。|  
|**partial_command**|**bit**|これが部分コマンドであるかどうかを示します。|  
|**command**|**varbinary(1024)**|コマンドの値。|  
|**xactid**|**binary(10)**|トランザクション ID。|  
|**xact_seqno**|**varbinary(16)**|トランザクションのシーケンス番号。|  
|**publication_id**|**int**|パブリケーションの ID です。|  
|**command_id**|**int**|[MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)内のコマンドの ID。|  
|**command_type**|**int**|コマンドの種類。|  
|**originator_srvname**|**sysname**|トランザクションが発生したサーバー。|  
|**originator_db**|**sysname**|トランザクションが発生したデータベース。|  
|**pkHash**|**int**|内部使用のみです。|  
|**originator_publication_id**|**int**|トランザクションが発生したパブリケーションの ID。|  
|**originator_db_version**|**int**|トランザクションが発生したデータベースのバージョン。|  
|**originator_lsn**|**varbinary(16)**|元のパブリケーションのコマンドのログシーケンス番号 (LSN) を識別します。|  
  
## <a name="remarks"></a>コメント  
 **sp_replcmds**は、トランザクションレプリケーションのログリーダープロセスによって使用されます。  
  
 レプリケーションでは、指定されたデータベース内で**sp_replcmds**を実行する最初のクライアントがログリーダーとして扱われます。  
  
 このプロシージャでは、所有者によって修飾されたテーブルのコマンドを生成したり、テーブル名を修飾したりすることはできません (既定)。 修飾されたテーブル名を追加すると、あるデータベースの特定のユーザーが所有するテーブルから、別のデータベースの同じユーザーが所有するテーブルにデータをレプリケートできます。  
  
> [!NOTE]  
>  レプリケーション元データベースのテーブル名は、所有者名により限定されるので、レプリケーション先データベースのテーブルの所有者も同じ所有者名である必要があります。  
  
 同じデータベース内で**sp_replcmds**を実行しようとしたクライアントは、最初のクライアントが切断されるまでエラー18752を受信します。 最初のクライアントが切断されると、別のクライアントが**sp_replcmds**を実行し、新しいログリーダーになります。  
  
 テキストポインターが同じで取得されなかった[!INCLUDE[msCoName](../../includes/msconame-md.md)]ために**sp_replcmds**が[!INCLUDE[msCoName](../../includes/msconame-md.md)]テキストコマンドをレプリケートできない場合、エラーログと Windows アプリケーションログの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]両方に警告メッセージ番号18759が追加されます。取引.  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replcmds**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [エラーメッセージ](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_repldone &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
