---
title: 比較演算子 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], testing
- operators [Transact-SQL], comparison
- testing expressions
- Boolean data type
- Boolean expressions
- comparing expressions
- comparison operators [SQL Server]
ms.assetid: b0cc68ef-3029-484c-a917-0c15dcbc230d
author: rothja
ms.author: jroth
ms.openlocfilehash: a1cc6427e01055a3aa97f8f79f9270dc22579255
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140258"
---
# <a name="comparison-operators-transact-sql"></a>比較演算子 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  比較演算子は、2 つの式が同じかどうかをテストします。 比較演算子は **text**、**ntext**、または **image** データ型の式を除くすべての式で使用できます。 次の表は、[!INCLUDE[tsql](../../includes/tsql-md.md)] の比較演算子の一覧です。  
  
|演算子|意味|  
|--------------|-------------|  
|[= (等しい)](../../t-sql/language-elements/equals-transact-sql.md)|等しい|  
|[> (より大きい)](../../t-sql/language-elements/greater-than-transact-sql.md)|より大きい|  
|[< (より小さい)](../../t-sql/language-elements/less-than-transact-sql.md)|より小さい|  
|[>= (以上)](../../t-sql/language-elements/greater-than-or-equal-to-transact-sql.md)|以上|  
|[<= (以下)](../../t-sql/language-elements/less-than-or-equal-to-transact-sql.md)|以下|  
|[<> (等しくない)](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)|等しくない|  
|[\!= (等しくない)](../../t-sql/language-elements/not-equal-to-transact-sql-exclamation.md)|等しくない (ISO 標準外)|  
|[\!< (以上)](../../t-sql/language-elements/not-less-than-transact-sql.md)|より小さくない (ISO 標準外)|  
|[\!> (以下)](../../t-sql/language-elements/not-greater-than-transact-sql.md)|より大きくない (ISO 標準外)|  
  
## <a name="boolean-data-type"></a>ブール値型  
 比較演算子の結果は**ブール** データ型になります。 これには 3 つの値があります。TRUE、FALSE、UNKNOWN です。 **ブール** データ型を返す式は、ブール式とも呼ばれます。  
  
 **ブール** データ型は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のデータ型と異なり、テーブルの列や変数のデータ型として指定することはできず、結果セットで返すこともできません。  
  
 SET ANSI_NULLS が ON の場合、1 つまたは 2 つの NULL 式が含まれる演算子では UNKNOWN が返されます。 SET ANSI_NULLS が OFF の場合、等号 (=) 演算子と不等号 (<>) 演算子を除き、同じ規則が適用されます。 SET ANSI_NULLS が OFF の場合、これらの演算子では、他の NULL と同等の、既知の値として NULL を処理し、TRUE または FALSE のみを返します (UNKNOWN を返すことはありません)。  
  
 **ブール** データ型の式は、検索条件を満たす行をフィルター選択するための WHERE 句、または IF や WHILE などのフロー制御言語ステートメントで使用します。たとえば次のようになります。  
  
```  
-- Uses AdventureWorks  
  
DECLARE @MyProduct int;  
SET @MyProduct = 750;  
IF (@MyProduct <> 0)  
   SELECT ProductID, Name, ProductNumber  
   FROM Production.Product  
   WHERE ProductID = @MyProduct;  
```  
  
## <a name="see-also"></a>参照  
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
