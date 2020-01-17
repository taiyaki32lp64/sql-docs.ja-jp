---
title: SCHEMA_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SCHEMA_ID
- SCHEMA_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], schemas
- schemas [SQL Server], IDs
- SCHEMA_ID function
- IDs [SQL Server], schemas
- default schema IDs
ms.assetid: c8e34df5-3eea-459f-ae40-050909ce9fda
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5882a98a856916ebeaa0ad30d545d29cdf21071c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68089876"
---
# <a name="schemaid-transact-sql"></a>SCHEMA_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  スキーマ名に関連付けられているスキーマ ID を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SCHEMA_ID ( [ schema_name ] )   
```  
  
## <a name="arguments"></a>引数  
  
|項目|定義|  
|----------|----------------|  
|*schema_name*|スキーマの名前です。 *schema_name* は、 **sysname**です。 場合 *schema_name* が指定されていない、SCHEMA_ID は、呼び出し元の既定のスキーマの ID を返します。|  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
 場合に、NULL が返される *schema_name* 有効なスキーマではありません。  
  
## <a name="remarks"></a>Remarks  
 SCHEMA_ID は、システム スキーマ ID とユーザー定義スキーマ ID を返します。 SCHEMA_ID は、選択リストの中、WHERE 句の中、また、式を使える所であればどこでも呼び出すことができます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>A. 呼び出し元の既定のスキーマ ID を返す  
  
```  
SELECT SCHEMA_ID();  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>B. 名前付きスキーマのスキーマ ID を返す  
  
```  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>参照  
 [メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  

