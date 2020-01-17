---
title: sp_sproc_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_sproc_columns
- sp_sproc_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_sproc_columns
ms.assetid: 62c18c21-35c5-4772-be0d-ffdcc19c97ab
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6739d9bcff2639b4b4f3562624beaf2cb3a76507
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032824"
---
# <a name="spsproccolumns-transact-sql"></a>sp_sproc_columns (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  現在の環境では、単一のストアド プロシージャまたはユーザー定義関数の列情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_sproc_columns [[@procedure_name = ] 'name']   
    [ , [@procedure_owner = ] 'owner']   
    [ , [@procedure_qualifier = ] 'qualifier']   
    [ , [@column_name = ] 'column_name']  
    [ , [@ODBCVer = ] 'ODBCVer']  
    [ , [@fUsePattern = ] 'fUsePattern']  
```  
  
## <a name="arguments"></a>引数  
`[ @procedure_name = ] 'name'` カタログ情報を返すために使用するプロシージャの名前です。 *名前*は**nvarchar (** 390 **)** % の既定値は、現在のデータベース内のすべてのテーブルを意味します。 ワイルドカードによるパターン照合はサポートされています。  
  
`[ @procedure_owner = ] 'owner'` プロシージャの所有者の名前です。 *所有者*は**nvarchar (** 384 **)** 、既定値は NULL です。 ワイルドカードによるパターン照合はサポートされています。 場合*所有者*が指定されていない、基になる DBMS の既定のプロシージャの可視性規則が適用されます。  
  
 現在のユーザーに指定した名前のプロシージャが所有している場合は、そのプロシージャに関する情報が返されます。 場合*所有者*が指定されていない、現在のユーザーが、指定した名前を持つプロシージャを所有していない**sp_sproc_columns**データベースの所有者によって所有されている指定の名前を持つプロシージャを探します。 プロシージャが存在する場合は、その列の情報が返されます。  
  
`[ @procedure_qualifier = ] 'qualifier'` プロシージャ修飾子の名前です。 *修飾子*は**sysname**、既定値は NULL です。 さまざまな DBMS 製品は、3 つの部分がテーブルの名前付けをサポート (*qualifier.owner.name*)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、このパラメーターは、データベース名を表します。 一部の製品で、テーブルのデータベース環境のサーバー名を表します。  
  
`[ @column_name = ] 'column_name'` 1 つの列は、カタログ情報の 1 つだけの列が必要なときに使用されます。 *column_name*は**nvarchar (** 384 **)** 、既定値は NULL です。 場合*column_name*は省略すると、すべての列が返されます。 ワイルドカードによるパターン照合はサポートされています。 相互運用性を最大に、ゲートウェイのクライアントが、ISO 標準のパターン照合 (% と _ ワイルドカード文字) のみを想定してください。  
  
`[ @ODBCVer = ] 'ODBCVer'` ODBC のバージョンは使用されています。 *ODBCVer*は**int**を既定値は 2 には、ODBC version 2.0 を示します。 ODBC version 2.0 と ODBC version 3.0 の違いの詳細については、ODBC を参照してください**SQLProcedureColumns** ODBC version 3.0 の仕様  
  
`[ @fUsePattern = ] 'fUsePattern'` アンダー スコア (_)、パーセント (%)、および角かっこ ([) 文字がワイルドカードとして解釈されるかどうかを判断します。 有効な値は 0 (パターン一致がオフ) および 1 (パターン一致では)。 *fUsePattern*は**ビット**、既定値は 1 です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|プロシージャ修飾子の名前。 この列は NULL を指定できます。|  
|**PROCEDURE_OWNER**|**sysname**|プロシージャ所有者の名前。 この列は常に値が返されます。|  
|**PROCEDURE_NAME**|**nvarchar(** 134 **)**|プロシージャの名前。 この列は常に値が返されます。|  
|**COLUMN_NAME**|**sysname**|各列の列名、 **TABLE_NAME**が返されます。 この列は常に値が返されます。|  
|**COLUMN_TYPE**|**smallint**|このフィールドは、常に値を返します。<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE|  
|**DATA_TYPE**|**smallint**|ODBC データ型用の整数コードです。 このデータ型が ISO 型にマッピングできない場合、値は NULL です。 ネイティブ データ型の名前が返されます、 **TYPE_NAME**列。|  
|**TYPE_NAME**|**sysname**|データ型の文字列表現。 これは、基になる DBMS によって表されるデータ型の名前です。|  
|**PRECISION**|**int**|有効桁数の値。 戻り値、**精度**列は 10 進数。|  
|**LENGTH**|**int**|データの転送サイズです。|  
|**スケール**|**smallint**|小数点の右側にある数字の数。|  
|**RADIX**|**smallint**|数値型の基数です。|  
|**NULLABLE**|**smallint**|Null 値許容属性を指定します。<br /><br /> 1 = データ型を作成できる null 値を許容します。<br /><br /> 0 = null 値は許可されません。|  
|**「解説」**|**varchar(** 254 **)**|プロシージャの列の説明です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] この列の値は返されません。|  
|**COLUMN_DEF**|**nvarchar(** 4000 **)**|列の既定値です。|  
|**SQL_DATA_TYPE**|**smallint**|表示されるように SQL データ型の値、**型**の記述子フィールド。 この列は、**datetime** データ型と ISO **interval** データ型以外は、**DATA_TYPE** 列と同じです。 この列は常に値が返されます。|  
|**SQL_DATETIME_SUB**|**smallint**|**SQL_DATA_TYPE** の値が **SQL_DATETIME** または **SQL_INTERVAL** の場合は、**datetime** ISO **interval** サブコードになります。 型のデータ型以外**datetime**と ISO**間隔**、このフィールドは NULL です。|  
|**CHAR_OCTET_LENGTH**|**int**|最大長のバイト単位、**文字**または**バイナリ**データ型の列。 他のすべてのデータ型の場合、この列は NULL を返します。|  
|**ORDINAL_POSITION**|**int**|テーブル内の列の序数です。 テーブルの最初の列には 1 です。 この列は常に値が返されます。|  
|**IS_NULLABLE**|**varchar(254)**|テーブル内の列の null 値許容属性。 NULL 値の許容属性の検査は ISO の規則に従います。 ISO 準拠の DBMS では、空の文字列を返すことはできません。<br /><br /> 列が NULL を含むことができる場合は YES、含むことができない場合は NO を表示します。<br /><br /> NULL が許可されているかどうかがわからない列は、長さ 0 の文字列を返します。<br /><br /> この列に返される値は、NULLABLE 列に返される値とは異なります。|  
|**SS_DATA_TYPE**|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用されるデータ型は拡張ストアド プロシージャです。 詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。|  
  
## <a name="remarks"></a>コメント  
 **sp_sproc_columns**と等価**SQLProcedureColumns** ODBC にします。 返される結果は並べ**PROCEDURE_QUALIFIER**、 **PROCEDURE_OWNER**、 **PROCEDURE_NAME**、およびプロシージャで使用されるパラメーターの順序定義。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [ストアド プロシージャ カタログ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
