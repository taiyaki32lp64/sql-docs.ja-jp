---
title: PARSENAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PARSENAME_TSQL
- PARSENAME
dev_langs:
- TSQL
helpviewer_keywords:
- PARSENAME function
- parsing [SQL Server], PARSENAME function
- names [SQL Server], objects
- objects [SQL Server], names
- part of object names [SQL Server]
ms.assetid: abf34f99-9ee9-460b-85b2-930ca5c4b5ae
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b36e31e163999a6af70b498fef9d65c2ce0ae55
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843617"
---
# <a name="parsename-transact-sql"></a>PARSENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  オブジェクト名の指定した部分を返します。 取得できるオブジェクトの部分は、オブジェクト名、所有者名、データベース名、およびサーバー名です。  
  
> [!NOTE]  
>  PARSENAME 関数では、指定した名前のオブジェクトが存在するかどうかは示されず、 PARSENAME は、指定したオブジェクト名の指定した部分だけを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
PARSENAME ( 'object_name' , object_piece )   
```  
  
## <a name="arguments"></a>引数  
 '*object_name*'  
 取得対象となるオブジェクトの名前を指定します。 *object_name* は **sysname** です。 このパラメーターは、必要に応じて修飾されたオブジェクト名です。 オブジェクト名のすべての部分が修飾される場合、この名前には、サーバー名、データベース名、所有者名、オブジェクト名の 4 つの部分を指定可能です。  
  
 *object_piece*  
 返すオブジェクトの部分を指定します。 *object_piece* のデータ型は **int**, 、これらの値を持つことができます。  
  
 1 = オブジェクト名  
  
 2 = スキーマ名  
  
 3 = データベース名  
  
 4 = サーバー名  
  
## <a name="return-types"></a>戻り値の型  
 **sysname**  
  
## <a name="remarks"></a>Remarks  
 次のいずれかの条件に該当する場合、PARSENAME は NULL を返します。  
  
-   いずれか *object_name* または *object_piece* は NULL です。  
  
-   構文エラーが発生した。  
  
 要求したオブジェクトの部分の長さが 0 で、有効な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子ではない。 長さ 0 のオブジェクト名は完全修飾名を無効とします。  
  
## <a name="examples"></a>使用例  
 次の例では使用 `PARSENAME` 情報を返す、 `Person` テーブルに、 `AdventureWorks2012` データベース。  
  
```  
-- Uses AdventureWorks  
  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 1) AS 'Object Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 2) AS 'Schema Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 3) AS 'Database Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 4) AS 'Server Name';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
Object Name
------------------------------
DimCustomer

(1 row(s) affected)

Schema Name
------------------------------
dbo

(1 row(s) affected)

Database Name
------------------------------
AdventureWorksPDW2012

(1 row(s) affected)

Server Name
------------------------------
(null)

(1 row(s) affected)
```
  
## <a name="see-also"></a>参照  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  

