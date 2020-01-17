---
title: VERSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ed3eab701a8edbbf118e228bd90080a61a214b32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927439"
---
# <a name="version---transact-sql-metadata-functions"></a>Version - Transact SQL メタデータ関数
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 アプライアンスで実行されている [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] または [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] のバージョンを返します。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>引数  
  
## <a name="general-remarks"></a>全般的な解説  
結果を返すには、テーブル名をこの関数の [FROM](../../t-sql/queries/from-transact-sql.md) 句で指定する必要があります。 クエリの結果セットの各行の結果の行が返されます。[TOP (Transact-SQL)](../../t-sql/queries/top-transact-sql.md) を使用して、返された行の数を制限します。  
  
## <a name="examples"></a>使用例  
次の例では、バージョン番号を返します。  
  
```  
SELECT VERSION();  
```  
  
## <a name="see-also"></a>参照 
[SESSION_ID &amp;#40;Transact-SQL&amp;#41;](../../t-sql/functions/session-id-transact-sql.md)  
[DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
  
  
