---
title: sp_repldone (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3df1b991f160aafdfcfd71818c8bd3e7cbd10ffa
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798388"
---
# <a name="sp_repldone-transact-sql"></a>sp_repldone (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  サーバーで最後にディストリビュートされたトランザクションを識別するレコードを更新します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
> [!CAUTION]  
>  **Sp_repldone**手動で実行する場合は、配信されたトランザクションの順序と一貫性を無効にすることができます。 **sp_repldone**は、経験豊富なレプリケーションサポート担当者が指示するように、レプリケーションのトラブルシューティングにのみ使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```
sp_repldone [ @xactid= ] xactid   
        , [ @xact_seqno= ] xact_seqno   
    [ , [ @numtrans= ] numtrans ]   
    [ , [ @time= ] time   
    [ , [ @reset= ] reset ]  
```  
  
## <a name="arguments"></a>引数  
`[ @xactid = ] xactid` は、サーバーの最後に分散されたトランザクションの最初のレコードのログシーケンス番号 (LSN) です。 *xactid*は**binary (10)** ,、既定値はありません。  
  
`[ @xact_seqno = ] xact_seqno` は、サーバーの最後に分散されたトランザクションの最後のレコードの LSN です。 *xact_seqno*は**binary (10)** ,、既定値はありません。  
  
`[ @numtrans = ] numtrans` は、分散されたトランザクションの数です。 *numtrans*は**int**,、既定値はありません。  
  
トランザクションの最後のバッチを配布するために必要な時間 (ミリ秒単位) を `[ @time = ] time` します。 *time*は**int**,、既定値はありません。  
  
`[ @reset = ] reset` はリセット状態です。 *reset*は**int**,、既定値はありません。 **1**の場合、ログ内のすべてのレプリケートされたトランザクションは、分散としてマークされます。 **0**の場合、トランザクションログは最初のレプリケートされたトランザクションにリセットされ、レプリケートされたトランザクションは配信済みとしてマークされません。 *reset*は、 *xactid*と*xact_seqno*の両方が NULL の場合にのみ有効です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_repldone**は、トランザクションレプリケーションで使用します。  
  
 **sp_repldone**は、配布されたトランザクションを追跡するために、ログリーダープロセスによって使用されます。  
  
 **Sp_repldone**を使用すると、トランザクションがレプリケートされた (ディストリビューターに送信された) ことをサーバーに手動で通知できます。 また、レプリケーションを待機しているトランザクションを次のように変更することもできます。 レプリケートされたトランザクションの一覧で、前方または後方に移動できます。 このトランザクションおよびそれ以前のトランザクションはすべてディストリビュートされたことを示すマークが付きます。  
  
 必要なパラメーター *xactid*と*xact_seqno*は**sp_repltrans**または**sp_replcmds**を使用して取得できます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールまたは**db_owner**固定データベースロールのメンバーは、 **sp_repldone**を実行できます。  
  
## <a name="examples"></a>使用例  
 *Xactid*が null の場合、 *xact_seqno*が null で、 *reset*が**1**の場合、ログ内のすべてのレプリケートされたトランザクションが分散としてマークされます。 これは、トランザクションログに有効ではなく、ログを切り捨てる必要があるトランザクションがレプリケートされている場合に便利です。次に例を示します。  
  
```sql
EXEC sp_repldone @xactid = NULL, @xact_seqno = NULL, @numtrans = 0, @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  このプロシージャは、レプリケーションを保留しているトランザクションが存在するときにトランザクションログが切り捨てられるように、緊急の場合に使用できます。  
  
## <a name="see-also"></a>参照  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [transact-sql &#40;  の&#41; sp_replflush](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_repltrans](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
