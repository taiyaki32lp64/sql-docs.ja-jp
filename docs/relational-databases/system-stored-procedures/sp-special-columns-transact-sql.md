---
title: sp_special_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_special_columns_TSQL
- sp_special_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sp_special_columns
ms.assetid: 0b0993f8-73e0-402b-8c6c-1b0963956f5d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c82970caa25089320a1dc5daf68076f27478081f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032843"
---
# <a name="spspecialcolumns-transact-sql"></a>sp_special_columns (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  テーブルの行を一意に識別する列の最適なセットを返します。 トランザクションによって行の任意の値が更新されたときに自動的に更新列も返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_special_columns [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @qualifier = ] 'qualifier' ]   
     [ , [ @col_type = ] 'col_type' ]   
     [ , [ @scope = ] 'scope' ]  
     [ , [ @nullable = ] 'nullable' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]   
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 [ @table_name=] '*table_name*'  
 カタログ情報を返すために使用するテーブルの名前です。 *名前*は**sysname**、既定値はありません。 ワイルドカードによるパターン照合はサポートされていません。  
  
 [ @table_owner=] '*table_owner*'  
 カタログ情報を返すために使用するテーブルのテーブル所有者です。 *所有者*は**sysname**、既定値は NULL です。 ワイルドカードによるパターン照合はサポートされていません。 場合*所有者*が指定されていない、基になる DBMS の既定のテーブル可視性規則が適用されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、現在のユーザーが指定した名前のテーブルを所有している場合、そのテーブルの列が返されます。 場合*所有者*が指定されていない、現在のユーザーが、指定のテーブルを所有していない*名前*、この手順は、指定のテーブルを探します*名前*データベースによって所有されています。所有者。 テーブルが存在する場合は、その列が返されます。  
  
 [ @qualifier=] '*修飾子*'  
 テーブル修飾子の名前です。 *修飾子*は**sysname**、既定値は NULL です。 さまざまな DBMS 製品は、3 つの部分がテーブルの名前付けをサポート (*qualifier.owner.name*)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列は、データベース名を表します。 一部の製品で、テーブルのデータベース環境のサーバー名を表します。  
  
 [ @col_type=] '*col_type*'  
 列の型です。 *col_type*は**char (** 1 **)** 、既定値は r です種類 R 最適な列または列のセットを返します、または複数の列から値を取得することによって、指定した任意の行では、。一意に識別するテーブル。 列には、この目的では、または、列またはテーブルの一意のインデックスの列用にデザインされた疑似をすることができます。 V の型を返します、列、指定したテーブルであれば、任意のトランザクションによって行の任意の値が更新されたときに、データ ソースによって自動的に更新されます。  
  
 [ @scope=] '*スコープ*'  
 ROWID の最低限必要な範囲です。 *スコープ*は**char (** 1 **)** 、既定値は t です。 範囲 C には、、ROWID がその行に配置されている場合にのみ有効であることを指定します。 範囲 T は、ROWID がトランザクションに対して有効であることを指定します。  
  
 [ @nullable=] '*null 許容*'  
 特別列に NULL 値を認めるかどうかを示します。 *null 許容*は**char (** 1 **)** 、既定値は u です。 O には、null 値を許容しない特別列を指定します。 U は部分的に null を許容する列を指定します。  
  
 [ @ODBCVer=] '*ODBCVer*'  
 使用する ODBC のバージョンを指定します。 *ODBCVer*は**int (** 4 **)** 、既定値は 2 です。 既定値は ODBC Version 2.0 を示します。 ODBC version 2.0 と ODBC version 3.0 の違いの詳細については、ODBC version 3.0 の ODBC SQLSpecialColumns 仕様を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|SCOPE|**smallint**|行 ID の実際の範囲 0、1、または 2 を指定できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 常に 0 を返します。 このフィールドは、常に値を返します。<br /><br /> 0 = SQL_SCOPE_CURROW。 行 ID をその行に位置している間のみ有効にすることが保証されます。 その行が別のトランザクションによって更新または削除された場合は、後でその行 ID を使って再度選択しても行は返されません。<br /><br /> 1 = SQL_SCOPE_TRANSACTION します。 行 ID を現在のトランザクションの期間を有効にすることが保証されます。<br /><br /> 2 = SQL_SCOPE_SESSION します。 行 ID は、セッションの期間は (複数のトランザクション境界)、有効であることが保証されます。|  
|COLUMN_NAME|**sysname**|各列の列名、*テーブル*が返されます。 このフィールドは、常に値を返します。|  
|DATA_TYPE|**smallint**|ODBC SQL データ型します。|  
|TYPE_NAME|**sysname**|データ ソースに依存するデータ型名です。たとえば、 **char**、 **varchar**、 **money**、または**テキスト**します。|  
|PRECISION|**Int**|データ ソースの列の有効桁数。 このフィールドは、常に値を返します。|  
|LENGTH|**Int**|データ ソース内のバイナリ形式でのデータ型の長さ (バイト単位) の必須の 10 **char (** 10 **)** 、4 の**整数**、および 2 の**smallint**.|  
|SCALE|**smallint**|データ ソースの列の小数点以下桁数。 データ型に対して NULL が返されますの小数点以下桁数は適用されません。|  
|PSEUDO_COLUMN|**smallint**|その列が疑似列であるかどうかを示します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 常に 1 を返します。<br /><br /> 0 = SQL_PC_UNKNOWN<br /><br /> 1 = SQL_PC_NOT_PSEUDO<br /><br /> 2 = SQL_PC_PSEUDO|  
  
## <a name="remarks"></a>コメント  
 sp_special_columns は、odbc SQLSpecialColumns と同じです。 返される結果は、スコープによって並べ替えられます。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例は、内の行を一意に識別する列についての情報を返します、`HumanResources.Department`テーブル。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_special_columns @table_name = 'Department'   
    ,@table_owner = 'HumanResources';  
```  
  
## <a name="see-also"></a>関連項目  
 [ストアド プロシージャ カタログ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
