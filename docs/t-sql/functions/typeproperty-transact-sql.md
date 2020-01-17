---
title: TYPEPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TYPEPROPERTY
- TYPEPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], data types
- data types [SQL Server], status information
- TYPEPROPERTY function
ms.assetid: bc311c80-bac5-46ab-a5c8-68b1c6bbf24a
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6fc6da38a122f2397c41232cb1a0ec5ad0831cd5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098633"
---
# <a name="typeproperty-transact-sql"></a>TYPEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  データ型に関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
TYPEPROPERTY (type , property)  
```  
  
## <a name="arguments"></a>引数  
 *type*  
 データ型の名前です。  
  
 *property*  
 データ型について返される情報の種類です。 *プロパティ* 値は次のいずれかを指定することができます。  
  
|プロパティ|[説明]|返される値|  
|--------------|-----------------|--------------------|  
|**AllowsNull**|データ型で NULL 値が許容されるかどうか。|1 = True<br /><br /> 0 = False<br /><br /> NULL = データ型が見つからない|  
|**OwnerId**|型の所有者。<br /><br /> 注:スキーマの所有者は型の所有者である必要はありません。|NULL 以外 = 型所有者のデータベース ユーザー ID。<br /><br /> NULL = サポートされない型、または型の ID が無効。|  
|**[精度]**|データ型の有効桁数。|桁数または文字数。<br /><br /> -1 = **xml** または大きな値のデータ型<br /><br /> NULL = データ型が見つからない|  
|**[スケール]**|データ型の小数点以下桁数。|データ型の小数点以下桁数<br /><br /> NULL = データ型が **numeric** でないか、見つからない|  
|**UsesAnsiTrim**|データ型の作成時に ANSI による埋め込みがオンであるかどうか。|1 = True<br /><br /> 0 = False<br /><br /> NULL = データ型が見つからないか、データ型が binary と文字列型のどちらでもない。|  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="exceptions"></a>例外  
 エラーが発生した場合、または呼び出し元にオブジェクトの表示権限がない場合は、NULL が返されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、そのユーザーが所有している、または権限を与えられている、セキュリティ保護可能なアイテムのメタデータのみを表示できます。 つまり、オブジェクトに対する権限がユーザーに与えられていない場合、メタデータを生成する組み込み関数 (TYPEPROPERTY など) が NULL を返す可能性があります。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-identifying-the-owner-of-a-data-type"></a>A. データ型の所有者を特定する  
 次の例では、データ型の所有者を返します。  
  
```  
SELECT TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId') AS owner_id, name, system_type_id, user_type_id, schema_id  
FROM sys.types;  
```  
  
### <a name="b-returning-the-precision-of-the-tinyint-data-type"></a>B. tinyint データ型の有効桁数を返す  
 次の例では、`tinyint` データ型の有効桁数を返します。  
  
```  
SELECT TYPEPROPERTY( 'tinyint', 'PRECISION');  
```  
  
## <a name="see-also"></a>参照  
 [TYPE_ID &#40;Transact-SQL&#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPE_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/type-name-transact-sql.md)   
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  

