---
title: sp_mergemetadataretentioncleanup (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
author: stevestein
ms.author: sstein
ms.openlocfilehash: 41c3a6848d71d7ba8f22667c117686485bb569b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019975"
---
# <a name="spmergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  内のメタデータの手動クリーンアップを実行、 [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)、 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)、 [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)、 [MSmerge_past_partition_マッピング](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)、および[MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md)システム テーブル。 このストアド プロシージャは、トポロジ内の各パブリッシャーおよびサブスクライバーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>引数  
`[ @num_genhistory_rows = ] num_genhistory_rows OUTPUT` 行からクリーンアップの数を返します、 [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)テーブル。 *num_genhistory_rows*は**int**、既定値は**0**します。  
  
`[ @num_contents_rows = ] num_contents_rows OUTPUT` 行からクリーンアップの数を返します、 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)テーブル。 *num_contents_rows*は**int**、既定値は**0**します。  
  
`[ @num_tombstone_rows = ] num_tombstone_rows OUTPUT` 行からクリーンアップの数を返します、 [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)テーブル。 *num_tombstone_rows*は**int**、既定値は**0**します。  
  
`[ @aggressive_cleanup_only = ] aggressive_cleanup_only` 内部でのみ使用します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
  
> [!IMPORTANT]  
>  実行されている場合、データベースに対する複数のパブリケーションが存在し、それらのパブリケーションのいずれかが無期限のパブリケーションの保有期間を使用して、 **sp_mergemetadataretentioncleanup**はマージ レプリケーション変更の追跡のクリーンアップを実行できませんデータベースのメタデータ。 このため、無期限のパブリケーション保有期間は注意して使用してください。 かどうか、パブリケーションが無期限の保有期間を確認するのには、実行[sp_helpmergepublication &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) 、パブリッシャーと注意結果内の任意のパブリケーションの設定の値を持つ**0**の**保有**します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **db_owner** 、パブリッシュされたデータベースで実行できるは、データベース ロールまたはパブリケーション アクセス リスト内のユーザーを固定**sp_mergemetadataretentioncleanup**します。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
