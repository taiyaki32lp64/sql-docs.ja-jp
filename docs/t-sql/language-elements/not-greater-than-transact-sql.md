---
title: '!&gt;(より大きくない) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Not Greater
- Greater
- '!>_TSQL'
- '!>'
- Not Greater Than
dev_langs:
- TSQL
helpviewer_keywords:
- '!> (not greater than)'
- not greater than operator (!>)
ms.assetid: 71a413ed-64f1-4ab9-9c52-c5959a77d00f
author: rothja
ms.author: jroth
ms.openlocfilehash: ddc661b856767c140091e662118f3d5198318266
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072455"
---
# <a name="gt-not-greater-than-transact-sql"></a>!&gt;(より大きくない) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  2 つの式を比較します (比較演算子)。 NULL でない式を比較したときに、左側のオペランドの値が右側のオペランドの値よりも大きくない場合、結果は TRUE です。 それ以外の場合、結果は FALSE です。 = (等価) 比較演算子と異なり、2 つの NULL 値の !> 比較の結果は ANSI_NULLS の設定に依存しません。  
  
 ![記事のリンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事のリンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
expression !> expression  
```  
  
## <a name="arguments"></a>引数  
 *式 (expression)*  
 任意の有効な[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。 両方の式とも、暗黙的に変換可能なデータ型でなければなりません。 変換は、[データ型の優先順位](../../t-sql/data-types/data-type-precedence-transact-sql.md)のルールに依存します。  
  
## <a name="result-types"></a>戻り値の型  
 **Boolean**  
  
## <a name="see-also"></a>参照  
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  