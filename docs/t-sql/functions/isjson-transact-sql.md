---
title: ISJSON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ISJSON
- ISJSON_TSQL
helpviewer_keywords:
- ISJSON function
- JSON, validating
ms.assetid: c836f3d3-3e17-44ae-92bf-f341918896c3
author: jovanpop-msft
ms.author: jovanpop
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 0d3060af2114f62c1c21b25e79abf4714acfbe4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109441"
---
# <a name="isjson-transact-sql"></a>ISJSON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  文字列に有効な JSON が含まれているかどうかをテストします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
ISJSON ( expression )  
```  
  
## <a name="arguments"></a>引数  
 *式 (expression)*  
 テストする文字列です。  
  
## <a name="return-value"></a>戻り値  
 文字列に有効な JSON が含まれている場合は 1 を、それ以外の場合は 0 を返します。 *式* が null の場合は null を返します。  
  
 エラーは返されません。  
  
## <a name="remarks"></a>Remarks  
 **ISJSON** は、同じレベルのキーの一意性をチェックしません。  
  
## <a name="examples"></a>使用例  
  
### <a name="example-1"></a>例 1  
次の例では、パラメーター値 `@param` に有効な JSON が含まれている場合は、ステートメント ブロックを条件付きで実行します。  
  
```sql  
DECLARE @param <data type>
SET @param = <value>

IF (ISJSON(@param) > 0)  
BEGIN  
     -- Do something with the valid JSON value of @param.  
END
 
```  
  
### <a name="example-2"></a>例 2  
次の例は、列 `json_col` に有効な JSON が含まれている行を返します。  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  
  
## <a name="see-also"></a>参照  
 [JSON データ &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
