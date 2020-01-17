---
title: COL_LENGTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COL_LENGTH
- COL_LENGTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lengths [SQL Server], columns
- COL_LENGTH function
- column properties [SQL Server]
- column length [SQL Server]
ms.assetid: cf891206-c49f-40eb-858e-eefd2b638a33
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bf23672374db7d8348154e95ca6228723934aa5a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064732"
---
# <a name="col_length-transact-sql"></a>COL_LENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は、定義されている列の長さをバイト単位で返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
COL_LENGTH ( 'table' , 'column' )   
```  
  
## <a name="arguments"></a>引数  
**'** *table* **'**  
列の長さ情報を定義するテーブルの名前。 *テーブル* 型の式は、 **nvarchar**です。
  
**'** *column* **'**  
長さを定義する列名。 *列* 型の式は、 **nvarchar**です。
  
## <a name="return-type"></a>の戻り値の型 :
**smallint**
  
## <a name="exceptions"></a>例外  
エラーが発生した場合、または呼び出し元にオブジェクトを表示するための適切な権限がない場合は、NULL が返されます。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、そのユーザーが所有している、または権限を与えられている、セキュリティ保護可能なアイテムのメタデータのみを表示できます。 つまり、オブジェクトに対する適切な権限がユーザーに与えられていない場合、メタデータを生成する組み込み関数 (COL_LENGTH など) が NULL を返す可能性があります。 詳細については、「[メタデータ表示の構成](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。
  
## <a name="remarks"></a>Remarks  
**max** 指定子 (**varchar (max)** ) で宣言された **varchar** 列の場合、COL_LENGTH では値 -1 が返されます。
  
## <a name="examples"></a>使用例  
この例では、`varchar(40)` 型と `nvarchar(40)` 型の列の値を返します。
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE t1(c1 varchar(40), c2 nvarchar(40) );  
GO  
SELECT COL_LENGTH('t1','c1')AS 'VarChar',  
      COL_LENGTH('t1','c2')AS 'NVarChar';  
GO  
DROP TABLE t1;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
VarChar     NVarChar  
40          80  
```  
  
## <a name="see-also"></a>参照
[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COL_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/col-name-transact-sql.md)  
[COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)
  
  
