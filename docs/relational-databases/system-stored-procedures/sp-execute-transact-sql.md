---
title: sp_execute (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_execute
- sp_cursor_execute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute
ms.assetid: 2009acd3-0d92-435a-a8fb-057e50dc7146
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1957103cf2c817f0ef77816446be5fb2d352c9d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124459"
---
# <a name="spexecute-transact-sql"></a>sp_execute (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  実行、準備された[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントが指定されたハンドルと省略可能なパラメーター値を使用します。 sp_execute は、ID を指定して呼び出される、表形式データ ストリーム (TDS) パケットで 12 を = です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_execute handle OUTPUT  
    [,bound_param  ]  [,...n ]  ]  
```  
  
## <a name="arguments"></a>引数  
 *handle*  
 *処理*sp_prepare から返される値。 *処理*を呼び出して取得する必須パラメーター **int**値を入力します。  
  
 *bound_param*  
 追加のパラメーターの使用を示します。 *bound_param*プロシージャの追加のパラメーターを示すために任意のデータ型の入力値を必要なパラメーターです。  
  
> [!NOTE]  
>  *bound_param* 、sp_prepare から行われた宣言に一致する必要があります*params*値し、形式にすることができます *@name値 =* または*値*します。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)  
  
  
