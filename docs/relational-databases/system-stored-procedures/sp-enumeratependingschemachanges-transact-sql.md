---
title: sp_enumeratependingschemachanges (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumeratependingschemachanges
- sp_enumeratependingschemachanges_TSQL
helpviewer_keywords:
- sp_enumeratependingschemachanges
ms.assetid: df169b21-d10a-41df-b3a1-654cfb58bc21
author: stevestein
ms.author: sstein
ms.openlocfilehash: da5579c52d1ffe1400e3b4c8c01210ca5856597b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124575"
---
# <a name="sp_enumeratependingschemachanges-transact-sql"></a>sp_enumeratependingschemachanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  保留中のすべてのスキーマ変更に関する一覧を返します。 このストアド プロシージャを使用できる[sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)、これにより、管理者がレプリケートされないように選択した保留中のスキーマの変更をスキップします。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_enumeratependingschemachanges [ @publication = ] 'publication'   
    [ , [ @starting_schemaversion = ] starting_schemaversion ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @starting_schemaversion = ] starting_schemaversion` 結果セットに含めるスキーマ変更の最小数です。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**article_name**|**sysname**|スキーマの変更を適用するアーティクルの名前または**パブリケーション全体**のパブリケーション全体に適用されるスキーマ変更します。|  
|**schemaversion**|**int**|保留中のスキーマ変更の数。|  
|**schematype**|**sysname**|スキーマの種類を表すテキスト値を変更します。|  
|**schematext**|**nvarchar(max)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] スキーマの変更について説明します。|  
|**schemastatus**|**nvarchar(10)**|スキーマ変更がアーティクルに対して保留になっているかどうかを示します。次のいずれかの値をとります。<br /><br /> **active**= スキーマ変更が保留中<br /><br /> **inactive**= スキーマ変更がアクティブでないです。<br /><br /> **skip**= スキーマ変更はレプリケートされません|  
|**schemaguid**|**uniqueidentifier**|スキーマの変更を識別します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_enumeratependingschemachanges**はマージ レプリケーションで使用します。  
  
 **sp_enumeratependingschemachanges**, で使用[sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)、マージ レプリケーションのサポートのためのものでは、および使用する場合にのみ、他の修正操作など再初期化、状況を解決できませんでした。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_enumeratependingschemachanges**します。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sysmergeschemachange &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
