---
title: sp_helptracertokens (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokens
- sp_helptracertokens_TSQL
helpviewer_keywords:
- sp_helptracertokens
ms.assetid: 61f27234-531d-4b37-8fa3-fe4c32e6f521
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9b4df50d1cf43ba1b0f4eb8b8f313634b4d11d18
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771538"
---
# <a name="sphelptracertokens-transact-sql"></a>sp_helptracertokens (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  待機時間を決定するためにパブリケーションに挿入されたトレーサートークンごとに1行の値を返します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して、またはディストリビューター側でディストリビューションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helptracertokens [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`トレーサートークンが挿入されたパブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @publisher = ] 'publisher'`パブリッシャーの名前です。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]
>  このパラメーターは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリッシャーに対してのみ指定する必要があります。  
  
`[ @publisher_db = ] 'publisher_db'`パブリケーションデータベースの名前です。 *publisher_db*は**sysname**,、既定値は NULL です。 ストアドプロシージャがパブリッシャーで実行される場合、このパラメーターは無視されます。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|トレーサートークンレコードを識別します。|  
|**publisher_commit**|**datetime**|パブリッシャーでパブリケーション データベースにトークン レコードがコミットされた日付と時刻です。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helptracertokens**は、トランザクションレプリケーションで使用します。  
  
 **sp_helptracertokens**は、 [sp_helptracertokenhistory &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)の実行時にトレーサートークン id を取得するために使用されます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokens-tran_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 固定サーバーロール**sysadmin**のメンバー、パブリケーションデータベースの**db_owner**固定データベースロールのメンバー、またはディストリビューションデータベース内の**db_owner**固定データベースロールまたは**replmonitor**ロールのメンバーだけが、sp_ を実行できます。 **helptracertokenhistory**。  
  
## <a name="see-also"></a>関連項目  
 [トランザクション レプリケーションの待機時間の計測および接続の検証](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
