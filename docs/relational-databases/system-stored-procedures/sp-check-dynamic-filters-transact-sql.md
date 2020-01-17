---
title: sp_check_dynamic_filters (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- dynamic_filters_TSQL
- sp_check_TSQL
- check
- sp_check_dynamic filter
- check_TSQL
- filters_TSQL
- check_dynamic_filters_TSQL
- dynamic filters
- filters
- check dynamic filters
- sp_check_dynamic filter_TSQL
- sp_check_for_sync_trigger_TSQL
- sp_check
helpviewer_keywords:
- sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
author: stevestein
ms.author: sstein
ms.openlocfilehash: 82b333095adfaf50220e5d2392114e3ab74bf822
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771287"
---
# <a name="spcheckdynamicfilters-transact-sql"></a>sp_check_dynamic_filters (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パブリケーションのパラメーター化された行フィルターのプロパティに関する情報を表示します。特に、パブリケーションに対してフィルター選択されたデータパーティションを生成するために使用される関数と、事前計算済みパーティションを使用するようにパブリケーションが適合するかどうかを示します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|パブリケーションが事前計算済みパーティションを使用するように修飾されているかどうかを示します。**1**は事前計算済みパーティションを使用できることを示し、 **0**は使用できないことを示します。|  
|**has_dynamic_filters**|**bit**|1つ以上のパラメーター化された行フィルターがパブリケーションで定義されているかどうかを示します。**1**は、1つまたは複数のパラメーター化された行フィルターが存在することを示し、 **0**は動的フィルターが存在しないことを示します。|  
|**dynamic_filters_function_list**|**nvarchar(500)**|パブリケーション内のアーティクルをフィルター処理するために使用される関数の一覧です。各関数はセミコロンで区切られます。|  
|**validate_subscriber_info**|**nvarchar(500)**|パブリケーション内のアーティクルをフィルター処理するために使用される関数の一覧です。各関数は、正符号 (+) で区切られます。|  
|**uses_host_name**|**bit**|[HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md)関数がパラメーター化された行フィルターで使用される場合、 **1**は、この関数が動的フィルター処理に使用されることを示します。|  
|**uses_suser_sname**|**bit**|[SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md)関数がパラメーター化された行フィルターで使用されている場合、 **1**はこの関数が動的フィルター処理に使用されることを意味します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_check_dynamic_filters**は、マージレプリケーションで使用します。  
  
 事前計算済みパーティションを使用するようにパブリケーションが定義されている場合、 **sp_check_dynamic_filters**は事前計算済みパーティションの制限に違反していないかどうかを確認します。 見つかった場合は、エラーが返されます。 詳細については、「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)」を参照してください。  
  
 パブリケーションがパラメーター化された行フィルターを持つように定義されているにもかかわらず、パラメーター化された行フィルターが見つからない場合は、エラーが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_check_dynamic_filters**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [パラメーター化されたフィルターを使用してマージパブリケーションのパーティションを管理する](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [sp_check_join_filter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [sp_check_subset_filter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
