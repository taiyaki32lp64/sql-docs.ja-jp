---
title: ^ (ビットごとの排他的 OR) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ^_TSQL
- Bitwise Exclusive OR
- Exclusive
- ^
- bitwise
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- OR operator
- exclusive OR mathematical operations
- bitwise exclusive OR (^)
ms.assetid: f38f0ad4-46d0-40ea-9851-0f928fda5293
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 664e3cd0fc687509c630258a681c155d94863d39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943067"
---
# <a name="-bitwise-exclusive-or-transact-sql"></a>^ (ビットごとの排他的 OR) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  2 つの整数の間でビットごとの排他的 OR 演算を実行します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
expression ^ expression  
```  
  
## <a name="arguments"></a>引数  
 *式 (expression)*  
 整数データ型に分類されるデータ型のいずれか、または **bit**、または **binary** または **varbinary** データ型の有効な[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。 *式*は、ビットごとの演算に対して 2 進数として扱われます。  
  
> [!NOTE]  
>  ビットごとの演算では、1 つの*式*のみが **binary** または **varbinary** データ型のいずれかになります。  
  
## <a name="result-types"></a>戻り値の型  
 入力値が **int** の場合は **int** です。  
  
 入力値が **smallint** の場合は **smallint** です。  
  
 入力値が **tinyint** の場合は **tinyint** です。  
  
## <a name="remarks"></a>Remarks  
 ビットごとの **^** 演算子では、2 つの式の対応するビットを対象に、ビットごとの排他的論理 OR 演算が実行されます。 入力式で現在処理対象となっているビットについて、両方ではなくいずれか一方のビットだけが 1 の場合、結果セットのビットは 1 に設定されます。 両方のビットが 0 または 1 の場合、結果セットのビットはクリアされて 0 になります。  
  
 左側の式と右側の式が異なる整数型の場合 (たとえば、左側の*式*が **smallint** 型で、右側の*式*が **int** 型の場合)、小さいデータ型の引数が大きいデータ型の引数に変換されます。 この場合、**smallint**_expression_ は **int** に変換されます。  
  
## <a name="examples"></a>使用例  
 次の例では、**int** データ型を使用して元の値を格納するテーブルを作成し、1 行に 2 つの値を挿入します。  
  
```  
CREATE TABLE bitwise  
(   
a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 次のクエリでは、`a_int_value` 列と `b_int_value` 列との間でビットごとの排他的論理 OR を実行します。  
  
```  
SELECT a_int_value ^ b_int_value  
FROM bitwise;  
GO  
```  
  
 結果セットは次のようになります。  
  
```  
-----------   
225           
  
(1 row(s) affected)  
```  
  
 170 (`a_int_value` または `A`) をバイナリで表すと、`0000 0000 1010 1010` になります。 75 (`b_int_value` または `B`) をバイナリで表すと、`0000 0000 0100 1011` になります。 2 つの値に対してビットごとの排他的論理 OR 演算を実行すると、バイナリで `0000 0000 1110 0001` が生成されます。これは 10 進数では 225 です。  
  
```  
(A ^ B)     
         0000 0000 1010 1010  
         0000 0000 0100 1011  
         -------------------  
         0000 0000 1110 0001  
```  
  

  
## <a name="see-also"></a>参照  
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [ビットごとの演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [^= &#40;ビットごとの排他的 OR 代入&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)   
 [複合演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


