---
title: sp_column_privileges (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_TSQL
- sp_column_privileges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges
ms.assetid: a3784301-2517-4b1d-bbd9-47404483fad0
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fc0ad8fcdf8c72e1b91df651a75227975d18294e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061811"
---
# <a name="spcolumnprivileges-transact-sql"></a>sp_column_privileges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在の環境では、1 つのテーブルに対する列権限情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_column_privileges [ @table_name = ] 'table_name'   
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @column_name = ] 'column' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @table_name= ] '*table_name*'  
 カタログ情報を返すために使用するテーブルを指定します。 *table_name*は**sysname**、既定値はありません。 ワイルドカードによるパターン照合はサポートされていません。  
  
 [ @table_owner= ] '*table_owner*'  
 カタログ情報を返すために使用するテーブルの所有者です。 *table_owner*は**sysname**、既定値は NULL です。 ワイルドカードによるパターン照合はサポートされていません。 場合*table_owner*が指定されていない、基になるデータベース管理システム (DBMS) の既定のテーブル可視性規則が適用されます。  
  
 指定した名前のテーブルを現在のユーザーが所有している場合は、そのテーブルの列が返されます。 場合*table_owner*が指定されていない、現在のユーザーが、指定したテーブルを所有していない*table_name*、sp_column privileges、指定したテーブル*table_name*データベース所有者が所有します。 1 つが存在する場合は、そのテーブルの列が返されます。  
  
 [ @table_qualifier= ] '*table_qualifier*'  
 テーブル修飾子の名前です。 *table_qualifier*は*sysname*、既定値は NULL です。 さまざまな DBMS 製品は、3 つの部分がテーブルの名前付けをサポート (_修飾子_ **.** _所有者_ **.** _名前_)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列は、データベース名を表します。 一部の製品で、テーブルのデータベース環境のサーバー名を表します。  
  
 [ @column_name=] '*列*'  
 カタログ情報の 1 つだけの列が取得されるときに 1 つの列が使用されます。 *列*は**nvarchar (** 384 **)** 、既定値は NULL です。 場合*列*が指定されていないすべての列が返されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、*列*sys.columns テーブルに表示される、列名を表します。 *列*基になる DBMS のワイルドカード パターンを使用して、ワイルドカード文字を含めることができます。 相互運用性を最大に、ゲートウェイのクライアントが、ISO 標準のパターン照合 (% と _ ワイルドカード文字) のみを想定してください。  
  
## <a name="result-sets"></a>結果セット  
 sp_column_privileges は odbc SQLColumnPrivileges と同じです。 返される結果は、TABLE_QUALIFIER、TABLE_OWNER、TABLE_NAME、COLUMN_NAME、PRIVILEGE の順序に従って並べ替えられます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|テーブル修飾子の名前。 このフィールドは NULL を指定できます。|  
|TABLE_OWNER|**sysname**|テーブルの所有者名です。 このフィールドは、常に値を返します。|  
|TABLE_NAME|**sysname**|テーブル名です。 このフィールドは、常に値を返します。|  
|COLUMN_NAME|**sysname**|返される TABLE_NAME の各列の名前。 このフィールドは、常に値を返します。|  
|GRANTOR|**sysname**|COLUMN_NAME に対する権限を、表示される GRANTEE に与えたデータベース ユーザーの名前。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この列は常に TABLE_OWNER と同じです。 このフィールドは、常に値を返します。<br /><br /> GRANTOR 列の値は、データベース所有者 (TABLE_OWNER) か、GRANT ステートメントで WITH GRANT OPTION 句を使用して、データベース所有者が権限を許可したユーザーになります。|  
|GRANTEE|**sysname**|COLUMN_NAME に対する権限を、表示される GRANTOR によって与えられたデータベース ユーザーの名前。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この列には常に、sysusers テーブルに記録されているデータベース ユーザーが格納されます。 このフィールドは、常に値を返します。|  
|PRIVILEGE|**varchar(** 32 **)**|使用可能な列のアクセス許可の 1 つ。 列権限には、次の値 (または実装が定義されているときに、データ ソースでサポートされるその他の値) のいずれかを指定できます。<br /><br /> SELECT。GRANTEE は、列からデータを取得できます。<br /><br /> INSERT。GRANTEE は、テーブルに新しい行を挿入したときにこの列のデータを設定できます。<br /><br /> UPDATE。GRANTEE は、列内の既存のデータを修正できます。<br /><br /> REFERENCES。GRANTEE は、主キー/外部キーのリレーションシップで外部テーブル内の列を参照できます。 主キー/外部キーのリレーションシップはテーブル制約を使用して定義されます。|  
|IS_GRANTABLE|**varchar(** 3 **)**|(「許可の許可」とも呼ばれます) の他のユーザーに権限を与える、権限付与対象ユーザーが許可されているかどうかを示します。 いいえ、はい、できますまたは NULL。 不明な値または NULL の場合は、"許可の許可" が適用されないデータ ソースであることを示します。|  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、権限は GRANT ステートメントで与え、REVOKE ステートメントで取り消します。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、特定の列に対する列権限情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_column_privileges @table_name = 'Employee'   
    ,@table_owner = 'HumanResources'  
    ,@table_qualifier = 'AdventureWorks2012'  
    ,@column_name = 'SalariedFlag';  
```  
  
## <a name="see-also"></a>関連項目  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
