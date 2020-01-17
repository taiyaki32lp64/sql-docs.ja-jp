---
title: sp_replsetoriginator (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replsetoriginator
- sp_replsetoriginator_TSQL
helpviewer_keywords:
- sp_replsetoriginator
ms.assetid: 030e5226-0585-439f-b8cd-36f48367d86d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5ca3487a22989261f0d6039f065ae0c102e534a1
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770872"
---
# <a name="spreplsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  双方向のトランザクション レプリケーションでのループバックの検出および処理を開始するために使用されます。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @server_name = ] 'server_name'`トランザクションが適用されるサーバーの名前を指定します。 *originating_server*は**sysname**,、既定値はありません。  
  
`[ @database_name = ] 'database_name'`トランザクションが適用されるデータベースの名前を指定します。 *originating_db*は**sysname**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replsetoriginator**は、レプリケーションによって適用されたトランザクションのソースを記録するために、ディストリビューションエージェントによって実行されます。 この情報は、ループバック プロパティ セットを持つ双方向のトランザクション サブスクリプションに対するループバックの検出を開始するために使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replsetoriginator**を実行できるのは、パブリッシャー側の**sysadmin**固定サーバーロールのメンバー、パブリケーションデータベースの**db_owner**固定データベースロールのメンバー、またはパブリケーションアクセスリスト (PAL) のユーザーだけです。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
