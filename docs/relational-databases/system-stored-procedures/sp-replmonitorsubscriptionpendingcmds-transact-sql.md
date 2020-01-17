---
title: sp_replmonitorsubscriptionpendingcmds (T-sql)
description: トランザクションパブリケーションに対するサブスクリプションの保留コマンドの数に関する情報を返す sp_replmonitorsubscriptionpendingcmds ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorsubscriptionpendingcmds_TSQL
- sp_replmonitorsubscriptionpendingcmds
helpviewer_keywords:
- sp_replmonitorsubscriptionpendingcmds
ms.assetid: df5b955a-feb0-4863-9b3b-7f71e9653b3d
author: stevestein
ms.author: sstein
ms.openlocfilehash: a493ef87ad2f980f21a99c50da1cb39dfdcda8cf
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75319987"
---
# <a name="sp_replmonitorsubscriptionpendingcmds-transact-sql"></a>sp_replmonitorsubscriptionpendingcmds (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  トランザクションパブリケーションに対するサブスクリプションの保留コマンドの数と、それらの処理にかかる時間の大まかな見積もりに関する情報を返します。 このストアドプロシージャは、返されたサブスクリプションごとに1つの行を返します。 レプリケーションを監視するために使用されるこのストアドプロシージャは、ディストリビューター側のディストリビューションデータベースで実行されます。  
  
 ![トピックリンクアイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-sql 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replmonitorsubscriptionpendingcmds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @subscription_type = ] subscription_type  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`パブリッシャーの名前を指定します。 *publisher*は**sysname**で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'`パブリッシュされたデータベースの名前を指定します。 *publisher_db*は**sysname**であり、既定値はありません。  
  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *publication*は**sysname**,、既定値はありません。  
  
`[ @subscriber = ] 'subscriber'`サブスクライバーの名前を指定します。 *サブスクライバー*は**sysname**,、既定値はありません。  
  
`[ @subscriber_db = ] 'subscriber_db'`サブスクリプションデータベースの名前を指定します。 *subscriber_db*は**sysname**であり、既定値はありません。  
  
`[ @subscription_type = ] subscription_type`サブスクリプションの種類。 *publication_type*は**int**,、既定値はありませんこれらの値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|プッシュ サブスクリプション|  
|**1 で保護されたプロセスとして起動されました**|プルサブスクリプション|  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**pendingcmdcount**|**通り**|サブスクリプションで保留中のコマンドの数。|  
|**estimatedprocesstime**|**通り**|保留中のすべてのコマンドをサブスクライバーに配信するために必要な秒数の見積もり。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replmonitorsubscriptionpendingcmds**は、トランザクションレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replmonitorsubscriptionpendingcmds**を実行できるのは、ディストリビューター側の固定サーバーロール**sysadmin**のメンバー、またはディストリビューションデータベース内の**db_owner**固定データベースロールのメンバーだけです。 ディストリビューションデータベースを使用するパブリケーションのパブリケーションアクセスリストのメンバーは、 **sp_replmonitorsubscriptionpendingcmds**を実行して、そのパブリケーションの保留中のコマンドを返すことができます。  
  
## <a name="see-also"></a>参照  
 [プログラムによるレプリケーションの監視](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
