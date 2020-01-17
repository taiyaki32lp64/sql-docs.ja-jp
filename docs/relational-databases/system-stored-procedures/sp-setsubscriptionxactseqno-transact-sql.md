---
title: sp_setsubscriptionxactseqno (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setsubscriptionxactseqno
- sp_setsubscriptionxactseqno_TSQL
helpviewer_keywords:
- sp_setsubscriptionxactseqno
ms.assetid: cdb4e0ba-5370-4905-b03f-0b0c6f080ca6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 27a7f35a915e2bff62932124aef64984a63cbd0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021084"
---
# <a name="sp_setsubscriptionxactseqno-transact-sql"></a>sp_setsubscriptionxactseqno (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  トラブルシューティングの際に使用すると、次のトランザクションで提供を開始するディストリビューション エージェントを許可するログ シーケンス番号 (LSN) を使用して、最後に配信されたトランザクションを指定します。 、再起動時に、ディストリビューション エージェントを返すトランザクションこの透かし (LSN) より大きい、ディストリビューション データベースのキャッシュ (msrepl_commands) から。 このストアド プロシージャは、サブスクライバーのサブスクリプション データベースで実行されます。 SQL Server 以外のサブスクライバーをサポートされていません。  
  
> [!CAUTION]  
>  このストアド プロシージャの使用または不正な LSN 値を指定する、サブスクライバーに既に適用された変更を元に戻すか、残りのすべての変更をスキップするには、ディストリビューション エージェントが発生することができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_setsubscriptionxactseqno [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @xact_seqno = ] xact_seqno   
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` パブリッシャーの名前です。 *パブリッシャー* は **sysname** 、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` パブリケーション データベースの名前です。 *publisher_db* は **sysname** 、既定値はありません。 SQL Server 以外のパブリッシャー、 *publisher_db*ディストリビューション データベースの名前を指定します。  
  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。 ディストリビューション エージェントは、1 つ以上のパブリケーションが共有しているときにのすべての値を指定する必要があります*パブリケーション*します。  
  
`[ @xact_seqno = ] xact_seqno` サブスクライバーで適用されるディストリビューター側では、次のトランザクションの LSN です。 *xact_seqno*は**varbinary (16)** 、既定値はありません。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**ORIGINAL XACT_SEQNO**|**varbinary(16)**|サブスクライバーで適用される次のトランザクションの元の LSN。|  
|**UPDATED XACT_SEQNO**|**varbinary(16)**|サブスクライバー側で適用される次のトランザクションの、更新された LSN。|  
|**SUBSCRIPTION STREAM COUNT**|**int**|最後の同期中に使用されたサブスクリプション ストリームの数。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_setsubscriptionxactseqno**はトランザクション レプリケーションで使用します。  
  
 **sp_setsubscriptionxactseqno**ピア ツー ピア トランザクション レプリケーション トポロジでは使用できません。  
  
 **sp_setsubscriptionxactseqno**エラーの原因となっている特定のトランザクションをスキップするために使用するときに、サブスクライバーで適用されます。 障害が発生したときにディストリビューション エージェントが停止し、呼び出す[sp_helpsubscriptionerrors &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql.md)して失敗したトランザクションの xact_seqno 値を取得し、を呼び出してディストリビューター**sp_setsubscriptionxactseqno**のこの値を渡す*xact_seqno*します。 こうすると、この LSN より後のコマンドだけが処理されます。  
  
 値を指定**0**の*xact_seqno*ディストリビューション データベースで保留中のすべてのコマンドをサブスクライバーに配信します。  
  
 **sp_setsubscriptionxactseqno**ディストリビューション エージェントでマルチ サブスクリプション ストリームを使用する場合に失敗する可能性があります。  
  
 このエラーが発生したときに、単一サブスクリプション ストリームでディストリビューション エージェントを実行する必要があります。 詳細については、「 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_setsubscriptionxactseqno**します。  
  
## <a name="see-more"></a>詳細情報

[ブログ:トランザクションをスキップする方法](https://repltalk.com/2019/05/28/how-to-skip-a-transaction/)  
