---
title: ::(スコープ解決) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
author: rothja
ms.author: jroth
ms.openlocfilehash: ff16ec709e8ed3cf7e0d6a4b129641d1e553a11a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072294"
---
# <a name="-scope-resolution-transact-sql"></a>::(スコープ解決) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  スコープ解決演算子 **::** により、複合データ型の静的メンバーにアクセスできます。 複合データ型は、複数の単純なデータ型およびメソッドを含むデータ型です。 複合データ型には、組み込みの CLR 型と、カスタムの SQLCLR ユーザー定義型 (UDT) が含まれます。  
  
## <a name="examples"></a>使用例  
 次の例は、スコープ解決演算子を使用して `GetRoot()` 型の `hierarchyid` メンバーにアクセスする方法を示します。  
  
```  
DECLARE @hid hierarchyid;  
SELECT @hid = hierarchyid::GetRoot();  
PRINT @hid.ToString();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `/`  
  
## <a name="see-also"></a>参照  
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
 