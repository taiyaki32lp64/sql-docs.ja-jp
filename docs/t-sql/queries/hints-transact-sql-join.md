---
title: 結合ヒント (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Join Hint
- Join_Hint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- HASH join hint
- REMOTE join hint
- LOOP join hint
- join hints
- MERGE join hint
- hints [SQL Server], join
ms.assetid: 09069f4a-f2e3-4717-80e1-c0110058efc4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f6f89e973d5f021dbd48a1bc7fc8234f9c9b6a89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902013"
---
# <a name="hints-transact-sql---join"></a>ヒント (Transact-SQL) - Join
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  結合ヒントにより、クエリ オプティマイザーで、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の 2 つのテーブル間の結合方法を設定します。 結合および結合の構文に関する一般的な情報については、「[FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)」を参照してください。  
  
> [!CAUTION]  
>  通常、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーでは、クエリにとって最適な実行プランが選択されるため、ヒントは、経験を積んだ開発者やデータベース管理者が最後の手段としてのみ使用することをお勧めします。
  
 **適用対象:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
<join_hint> ::=   
     { LOOP | HASH | MERGE | REMOTE }  
```  
  
## <a name="arguments"></a>引数  
 LOOP | HASH | MERGE  
 クエリ内の結合は、ループ、ハッシュ、またはマージを使用します。 LOOP | HASH | MERGE JOIN を使用すると、2 つのテーブル間に特定の結合が設定されます。 LOOP は、RIGHT または FULL と共に結合の種類として指定することはできません。  
  
 REMOTE  
 右側のテーブルのサイトで結合操作を実行します。 これは、左側のテーブルがローカル テーブルで、右側のテーブルがリモート テーブルの場合に効果的です。 REMOTE は、左側のテーブルの行数が右側のテーブルの行数よりも少ないときだけ使用します。  
  
 右側のテーブルがローカルの場合、結合はローカルで実行されます。 両方のテーブルがリモート テーブルでデータ ソースは異なる場合、REMOTE の指定によって結合は右側のテーブルのサイトで実行されます。 両方のテーブルが同じデータ ソースのリモート テーブルの場合、REMOTE は必要ありません。  
  
 結合述語で比較されている値のいずれかを COLLATE 句を使用して別の照合順序にキャストする場合は、REMOTE を使用できません。  
  
 REMOTE は、INNER JOIN 操作に対してのみ使用できます。  
  
## <a name="remarks"></a>Remarks  
 結合ヒントは、クエリの FROM 句で指定します。 結合ヒントにより、2 つのテーブル間の結合方法を設定できます。 2 つのテーブルに対して結合ヒントが指定されると、クエリ オプティマイザーは、ON キーワードの位置に基づいて、クエリ内のすべての結合テーブルに対して結合の順番を自動的に設定します。 ON 句を指定せずに CROSS JOIN を使用する場合は、かっこを使用して結合の順番を指定できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-hash"></a>A. HASH を使用する  
 次の例では、クエリの `JOIN` 操作を `HASH` 結合によって実行することを指定します。 この例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースを使用します。  
  
```  
SELECT p.Name, pr.ProductReviewID  
FROM Production.Product AS p  
LEFT OUTER HASH JOIN Production.ProductReview AS pr  
ON p.ProductID = pr.ProductID  
ORDER BY ProductReviewID DESC;  
```  
  
### <a name="b-using-loop"></a>B. LOOP を使用する  
 次の例では、クエリの `JOIN` 操作を `LOOP` 結合によって実行することを指定します。 この例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースを使用します。  
  
```  
DELETE FROM Sales.SalesPersonQuotaHistory   
FROM Sales.SalesPersonQuotaHistory AS spqh  
    INNER LOOP JOIN Sales.SalesPerson AS sp  
    ON spqh.SalesPersonID = sp.SalesPersonID  
WHERE sp.SalesYTD > 2500000.00;  
GO  
```  
  
### <a name="c-using-merge"></a>C. MERGE を使用する  
 次の例では、クエリの `JOIN` 操作を `MERGE` 結合によって実行することを指定します。 この例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースを使用します。  
  
```  
SELECT poh.PurchaseOrderID, poh.OrderDate, pod.ProductID, pod.DueDate, poh.VendorID   
FROM Purchasing.PurchaseOrderHeader AS poh  
INNER MERGE JOIN Purchasing.PurchaseOrderDetail AS pod   
    ON poh.PurchaseOrderID = pod.PurchaseOrderID;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)  
  
  
