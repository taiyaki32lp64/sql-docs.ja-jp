---
title: sp_ivindexhasnullcols (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
author: stevestein
ms.author: sstein
ms.openlocfilehash: 27ebcdf656effb97529bea42972be96f9a993cfc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139911"
---
# <a name="spivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  インデックス付きビューを使ってトランザクション パブリケーションを作成する場合に、インデックス付きビューのクラスター化インデックスが一意であることと、NULL 値が許容される列を含まないことを検証します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>引数  
`[ @viewname = ] 'view_name'` 検証するビューの名前です。 *view_name*は**sysname**、既定値はありません。  
  
`[ @fhasnullcols = ] field_has_null_columns OUTPUT` NULL が許容される列がビュー インデックスにあるかどうかを示すフラグです。 *view_name*は**sysname**、既定値はありません。 値を返します**1**場合は NULL が許容される列がビュー インデックスにします。 値を返します**0**ビューに NULL を許容する列が含まれていない場合。  
  
> [!NOTE]  
>  ストアド プロシージャ自体でのリターン コードを返すかどうか**1**、障害がストアド プロシージャの実行の意味、この値は**0**無視する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_ivindexhasnullcols**トランザクション レプリケーションで使用されます。  
  
 既定では、サブスクライバー側でパブリケーション内のインデックス付きビュー アーティクルはテーブルとして作成されます。 ただし、インデックス付き列には、NULL 値が許可されている場合、インデックス付きビューは、テーブルではなく、サブスクライバーでインデックス付きビューとして作成されます。 このストアド プロシージャを実行するには、現在のインデックス付きビューでこの問題が存在するかどうかをユーザーに知らせることができます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_ivindexhasnullcols**します。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
