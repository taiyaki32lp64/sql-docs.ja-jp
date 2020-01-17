---
title: sp_check_subset_filter (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_check_TSQL
- sp_check_subset_filter
- filter
- subset
- subset_TSQL
- sp_check
- sp_check_subset_filter_TSQL
helpviewer_keywords:
- sp_check_subset_filter
ms.assetid: 525cfcfc-f317-478d-ba84-72e62285f160
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3c1510260a5b381b91a399984121834ca4ce30b5
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771314"
---
# <a name="spchecksubsetfilter-transact-sql"></a>sp_check_subset_filter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  テーブルに対してフィルター句を確認して、フィルター句がテーブルに対して有効であるかどうかを判定するのに使用します。 このストアド プロシージャは、フィルターが事前計算済みパーティションでの使用条件を満たすかどうかも含め、指定されたフィルターに関する情報を返します。 このストアドプロシージャは、パブリッシャー側でパブリケーションを含むデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_check_subset_filter [ @filtered_table = ] 'filtered_table'  
        , [ @subset_filterclause = ] 'subset_filterclause'  
    [ , [ @has_dynamic_filters = ] has_dynamic_filters OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @filtered_table = ] 'filtered_table'`フィルター選択されたテーブルの名前を指定します。 *filtered_table*は**nvarchar (400)** ,、既定値はありません。  
  
`[ @subset_filterclause = ] 'subset_filterclause'`テストするフィルター句を選択します。 *subset_filterclause*は**nvarchar (1000)** ,、既定値はありません。  
  
`[ @has_dynamic_filters = ] has_dynamic_filters`フィルター句がパラメーター化された行フィルターであるかどうかを示します。 *has_dynamic_filters*は**ビット**,、既定値は NULL の場合は、出力パラメーターです。 フィルター句がパラメーター化された行フィルターの場合、値**1**を返します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|パブリケーションが事前計算済みパーティションを使用するように修飾されているかどうかを示します。**1**は事前計算済みパーティションを使用できることを示し、 **0**は使用できないことを示します。|  
|**has_dynamic_filters**|**bit**|指定したフィルター句にパラメーター化された行フィルターが少なくとも1つ含まれているかどうかを示します。**1**は、パラメーター化された行フィルターが使用されることを示します。 **0**は、このような関数が使用されないことを示します。|  
|**dynamic_filters_function_list**|**nvarchar(500)**|アーティクルを動的にフィルター選択するフィルター句内の関数の一覧です。各関数は、セミコロンで区切られます。|  
|**uses_host_name**|**bit**|[HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md)関数がフィルター句で使用されている場合は、 **1**はこの関数が存在することを意味します。|  
|**uses_suser_sname**|**bit**|[SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md)関数がフィルター句で使用されている場合は、 **1**はこの関数が存在することを意味します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_check_subset_filter**は、マージレプリケーションで使用します。  
  
 **sp_check_subset_filter**は、テーブルがパブリッシュされていない場合でも、任意のテーブルに対して実行できます。 フィルター選択されたアーティクルを定義する前に、このストアドプロシージャを使用してフィルター句を検証することができます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_check_subset_filter**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
  
