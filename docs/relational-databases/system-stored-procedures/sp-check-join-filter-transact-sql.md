---
title: sp_check_join_filter (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- filter_TSQL
- sp_check_TSQL
- sp_check_join_filter
- sp_check_join_filter_TSQL
- join
- join_TSQL
- filter
- sp_check
helpviewer_keywords:
- sp_check_join_filter
ms.assetid: e9699d59-c8c9-45f6-a561-f7f95084a540
author: stevestein
ms.author: sstein
ms.openlocfilehash: 28589be83c62f705457e990b328be98e88905568
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771271"
---
# <a name="spcheckjoinfilter-transact-sql"></a>sp_check_join_filter (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  2 つのテーブル間の結合フィルターを検証し、結合フィルター句が有効かどうかを判別する場合に使用します。 このストアド プロシージャは、指定したテーブルの事前計算されたパーティションで、指定した結合フィルターを使用できるかどうかなど、指定した結合フィルターに関する情報を返します。 このストアド プロシージャは、パブリケーション上のパブリッシャー側で実行されます。 詳細については、「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>引数  
`[ @filtered_table = ] 'filtered_table'`フィルター選択されたテーブルの名前を指定します。 *filtered_table*は**nvarchar (400)** ,、既定値はありません。  
  
`[ @join_table = ] 'join_table'`*Filtered_table*に結合されているテーブルの名前を指定します。 *join_table*は**nvarchar (400)** ,、既定値はありません。  
  
`[ @join_filterclause = ] 'join_filterclause'`テストする結合フィルター句を選択します。 *join_filterclause*は**nvarchar (1000)** ,、既定値はありません。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|パブリケーションが事前計算済みパーティションに対して限定される場合はです。**1**はたパーティションを使用できることを示し、 **0**は使用できないことを示します。|  
|**has_dynamic_filters**|**bit**|指定したフィルター句にパラメーター化されたフィルター関数が少なくとも1つ含まれているかどうかを示します。**1**は、パラメーター化されたフィルター関数が使用されることを示します。 **0**は、このような関数が使用されないことを示します。|  
|**dynamic_filters_function_list**|**nvarchar(500)**|アーティクルのパラメーター化されたフィルターを定義するフィルター句内の関数の一覧。各関数はセミコロンで区切られます。|  
|**uses_host_name**|**bit**|[HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md)関数がフィルター句で使用されている場合は、 **1**はこの関数が存在することを意味します。|  
|**uses_suser_sname**|**bit**|[SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md)関数がフィルター句で使用されている場合は、 **1**はこの関数が存在することを意味します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_check_join_filter**は、マージレプリケーションで使用します。  
  
 **sp_check_join_filter**は、パブリッシュされていない場合でも、関連するテーブルに対して実行できます。 このストアド プロシージャは、2 つのアーティクル間の結合フィルターを定義する前に、結合フィルター句を検証するときに使用できます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_check_join_filter**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
