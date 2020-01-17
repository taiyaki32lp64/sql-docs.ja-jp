---
title: sp_scriptpublicationcustomprocs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptpublicationcustomprocs
- sp_scriptpublicationcustomprocs_TSQL
helpviewer_keywords:
- sp_scriptpublicationcustomprocs
ms.assetid: b06102d5-4284-4834-b126-bc0baea49be5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8436616ced84892dc7e484a5d83f3f0c3779f244
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771579"
---
# <a name="spscriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  自動生成カスタムプロシージャスキーマオプションが有効になっているパブリケーション内のすべてのテーブルアーティクルに対して、カスタムの INSERT、UPDATE、および DELETE プロシージャをスクリプト化します。 **sp_scriptpublicationcustomprocs**は、スナップショットが手動で適用されるサブスクリプションを設定する場合に特に便利です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication_name'`パブリケーションの名前を指定します。 *publication_name*は**sysname**既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 1つの**nvarchar (4000)** 列で構成される結果セットを返します。 この結果セットは、カスタム ストアド プロシージャの作成に必要な、完全な CREATE PROCEDURE ステートメントを構成します。  
  
## <a name="remarks"></a>コメント  
 カスタムプロシージャは、自動生成カスタムプロシージャ (0x2) スキーマオプションを指定しないと、アーティクルに対してスクリプト化されません。  
  
 次の手順は、 **sp_scriptpublicationcustomprocs**がサブスクライバーのプロシージャを作成するために使用されます。このプロシージャを直接実行することはできません。  
  
 **sp_script_reconciliation_delproc**  
  
 **sp_script_reconciliation_insproc**  
  
 **sp_script_reconciliation_vdelproc**  
  
 **sp_script_reconciliation_xdelproc**  
  
 **sp_scriptdelproc**  
  
 **sp_scriptinsproc**  
  
 **sp_scriptmappedupdproc**  
  
 **sp_scriptupdproc**  
  
 **sp_scriptvdelproc**  
  
 **sp_scriptvupdproc**  
  
 **sp_scriptxdelproc**  
  
 **sp_scriptxupdproc**  
  
## <a name="permissions"></a>アクセス許可  
 実行権限が**public**に付与されます。このストアドプロシージャ内では、現在のデータベースの**sysadmin**固定サーバーロールおよび**db_owner**固定データベースロールのメンバーへのアクセスを制限するために、手続き型のセキュリティチェックが実行されます。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
