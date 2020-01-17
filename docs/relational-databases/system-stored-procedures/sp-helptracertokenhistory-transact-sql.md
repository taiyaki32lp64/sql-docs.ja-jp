---
title: sp_helptracertokenhistory (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokenhistory_TSQL
- sp_helptracertokenhistory
helpviewer_keywords:
- sp_helptracertokenhistory
ms.assetid: 96910d1c-be76-43eb-9c93-4477e6761749
author: stevestein
ms.author: sstein
ms.openlocfilehash: b8755bea5e318d1ded2631a2253134fd8721a421
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771154"
---
# <a name="sp_helptracertokenhistory-transact-sql"></a>sp_helptracertokenhistory (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  指定されたトレーサー トークンの詳細な待機時間情報を、各サブスクライバーに対して 1 行ずつ返します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して、またはディストリビューター側でディストリビューションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helptracertokenhistory [ @publication = ] 'publication'   
        , [ @tracer_id = ] tracer_id  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`トレーサートークンが挿入されたパブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @tracer_id = ] tracer_id`履歴情報が返される[MStracer_tokens &#40;transact-sql&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)テーブル内のトレーサートークンの ID を指定します。 *tracer_id*は**int**,、既定値はありません。  
  
`[ @publisher = ] 'publisher'`パブリッシャーの名前です。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]
>  このパラメーターは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリッシャーに対してのみ指定する必要があります。  
  
`[ @publisher_db = ] 'publisher_db'`パブリケーションデータベースの名前です。 *publisher_db*は**sysname**,、既定値は NULL です。 ストアドプロシージャがパブリッシャーで実行される場合、このパラメーターは無視されます。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**distributor_latency**|**bigint**|トレーサートークンレコードがパブリッシャーでコミットされてからディストリビューター側でコミットされるまでの秒数。|  
|**subscriber**|**sysname**|トレーサートークンを受け取ったサブスクライバーの名前。|  
|**subscriber_db**|**sysname**|トレーサートークンレコードが挿入されたサブスクリプションデータベースの名前。|  
|**subscriber_latency**|**bigint**|トレーサートークンレコードがディストリビューター側でコミットされてからサブスクライバー側でコミットされるまでの秒数。|  
|**overall_latency**|**bigint**|トレーサートークンレコードがパブリッシャーでコミットされてから、サブスクライバーでトークンレコードがコミットされるまでの秒数。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helptracertokenhistory**は、トランザクションレプリケーションで使用します。  
  
 [Sp_helptracertokens &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md)を実行して、パブリケーションのトレーサートークンの一覧を取得します。  
  
 結果セットの値が NULL の場合は、待機時間の統計を計算できないことを意味します。 これは、トレーサートークンがディストリビューターまたはいずれかのサブスクライバーで受信されていないためです。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokenhistor_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 固定サーバーロール**sysadmin**のメンバー、パブリケーションデータベースの**db_owner**固定データベースロールのメンバー、またはディストリビューションデータベース内の**db_owner**固定データベースロールまたは**replmonitor**ロールのメンバーだけが、sp_ を実行できます。 **helptracertokenhistory**。  
  
## <a name="see-also"></a>関連項目  
 [トランザクション レプリケーションの待機時間の計測および接続の検証](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
