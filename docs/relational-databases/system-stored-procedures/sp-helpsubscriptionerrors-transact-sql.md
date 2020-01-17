---
title: sp_helpsubscriptionerrors (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscriptionerrors_TSQL
- sp_helpsubscriptionerrors
helpviewer_keywords:
- sp_helpsubscriptionerrors
ms.assetid: 01c8bc21-939e-490d-8cc8-219c068be31e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2fe01c857d8a9e27de56538d0e595f3ad89f4d96
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771521"
---
# <a name="sphelpsubscriptionerrors-transact-sql"></a>sp_helpsubscriptionerrors (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  指定されたサブスクリプションのすべてのトランザクションレプリケーションエラーを返します。 このストアド プロシージャは、ディストリビューター側でディストリビューション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpsubscriptionerrors [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`パブリッシャーの名前を指定します。 *パブリッシャー* は **sysname** 、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'`パブリケーションデータベースの名前を指定します。 *publisher_db* は **sysname** 、既定値はありません。  
  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @subscriber = ] 'subscriber'`サブスクライバーの名前を指定します。 *サブスクライバー*は**sysname**,、既定値はありません。  
  
`[ @subscriber_db = ] 'subscriber_db'`サブスクリプションデータベースの名前を指定します。 *subscriber_db*は**sysname**、既定値はありません。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|エラーの ID。|  
|**time**|**datetime**|エラーが発生した時刻。|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|エラーソースの種類 ID。|  
|**source_name**|**nvarchar(100)**|エラーソースの名前。|  
|**error_code**|**sysname**|エラー コードです。|  
|**error_text**|**ntext**|エラーメッセージ。|  
|**xact_seqno**|**varbinary(16)**|失敗した実行バッチの先頭のトランザクション ログ シーケンス番号。 ディストリビューションエージェントでのみ使用されます。これは、失敗した実行バッチ内の最初のトランザクションのトランザクションログシーケンス番号です。|  
|**command_id**|**int**|失敗した実行バッチのコマンド ID。 ディストリビューションエージェントでのみ使用されます。これは、失敗した実行バッチ内の最初のコマンドのコマンド ID です。|  
|**session_id**|**int**|エラーが発生したエージェントセッションの ID。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpsubscriptionerrors**は、スナップショットレプリケーションとトランザクションレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpsubscriptionerrors**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [sp_helpsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
