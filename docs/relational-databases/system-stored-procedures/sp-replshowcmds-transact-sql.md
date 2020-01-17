---
title: sp_replshowcmds (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
author: stevestein
ms.author: sstein
ms.openlocfilehash: 96a32ea04fc53f1a0bf3a842a5e68cde5586ac29
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770881"
---
# <a name="spreplshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  レプリケーション対象のマークが付けられたトランザクションのコマンドを判読可能な形式で返します。 **sp_replshowcmds**を実行できるのは、クライアント接続 (現在の接続を含む) が、レプリケートされたトランザクションをログから読み取っていない場合のみです。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>引数  
`[ @maxtrans = ] maxtrans`情報を返すトランザクションの数を指定します。 *maxtrans*のデータ**型は int**で、既定値は**1**です。これは、 **sp_replshowcmds**が情報を返す、レプリケーション保留中のトランザクションの最大数を指定します。  
  
## <a name="result-sets"></a>結果セット  
 **sp_replshowcmds**は、実行元のパブリケーションデータベースに関する情報を返す診断プロシージャです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|コマンドのシーケンス番号。|  
|**originator_id**|**int**|コマンドの発信元の ID。常に**0**です。|  
|**publisher_database_id**|**int**|パブリッシャーデータベースの ID、常に**0**です。|  
|**article_id**|**int**|アーティクルの ID。|  
|**type**|**int**|コマンドの種類。|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)]メニュー.|  
  
## <a name="remarks"></a>コメント  
 **sp_replshowcmds**は、トランザクションレプリケーションで使用します。  
  
 **Sp_replshowcmds**を使用すると、現在ディストリビュートされていないトランザクション (つまり、ディストリビューターにまだ送信されていないトランザクションログに残っているトランザクション) を表示できます。  
  
 **Sp_replshowcmds**と**sp_replcmds**を同じデータベース内で実行するクライアントは、エラー18752を受信します。  
  
 このエラーを回避するには、最初のクライアントを切断するか、 **sp_replflush**を実行してログリーダーとしてクライアントの役割を解放する必要があります。 すべてのクライアントがログリーダーから切断された後、 **sp_replshowcmds**を正常に実行できます。  
  
> [!NOTE]  
>  **sp_replshowcmds**は、レプリケーションに関する問題のトラブルシューティングを行う場合にのみ実行してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replshowcmds**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [エラーメッセージ](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
