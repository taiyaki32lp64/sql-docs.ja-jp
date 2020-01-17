---
title: PERMISSIONS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PERMISSIONS_TSQL
- PERMISSIONS
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- current permission status
- users [SQL Server], permissions status
- checking permission status
- security [SQL Server], permissions
- verifying permission status
- testing permissions
- PERMISSIONS function
ms.assetid: 81625a56-b160-4424-91c5-1ce8b259a8e6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fc38de8bffc09461dc69a24acf15ce143276422b
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843628"
---
# <a name="permissions-transact-sql"></a>PERMISSIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在のユーザーのステートメント権限、オブジェクト権限、または列権限を示すビットマップを含む値を返します。  
  
 **重要** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]代わりに、[fn_my_permissions](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md) および [Has_Perms_By_Name](../../t-sql/functions/has-perms-by-name-transact-sql.md) を使用してください。 PERMISSIONS 関数を継続して使用すると、パフォーマンスが低下する場合があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
PERMISSIONS ( [ objectid [ , 'column' ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *objectid*  
 セキュリティ保護可能なリソースの ID を指定します。 *objectid* を指定しない場合、ビットマップ値には現在のユーザーのステートメント権限が含まれます。それ以外の場合、ビットマップ値には現在のユーザーのセキュリティ保護可能なリソースについての権限が含まれます。 指定したセキュリティ保護可能なリソースは、現在のデータベースに存在する必要があります。 *objectid* 値を確認するには、[OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) 関数を使用します。  
  
 **'** *column* **'**  
 権限情報を返す列の名前を指定します (省略可能)。 *objectid* で指定したテーブル内の有効な列名を指定する必要があります。  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 PERMISSIONS は、現在のユーザーがステートメントを実行するのに必要な権限を所有しているか、または別のユーザーに対して権限を許可 (GRANT) できるかを調べるときに使用できます。  
  
 返される権限情報は 32 ビットのビットマップです。  
  
 下位 16 ビットは、ユーザーに許可されている権限と、現在のユーザーがメンバーである Windows グループまたは固定サーバー ロールに適用されている権限を表します。 たとえば、*objectid* を指定せず、戻り値 66 (16 進値の 0x42) が返された場合は、ユーザーが CREATE TABLE ステートメント (10 進値の 2) と BACKUP DATABASE ステートメント (10 進値の 64) を実行する権限を所有していることがわかります。  
  
 上位 16 ビットは、ユーザーが他のユーザーに許可 (GRANT) できる権限を表します。 上位 16 ビットの解釈は、次の表の下位 16 ビットを左側に 16 ビット移す (65,536 を乗算する) だけです。 たとえば、*objectid* を指定した場合、0x8 (10 進値の 8) は INSERT 権限を表すビットです。 これに対して、0x80000 (10 進値の 524288) は、524288 = 8 × 65536 であり、INSERT 権限を許可 (GRANT) できることを表します。  
  
 ロールのメンバーシップにより、ステートメントの実行権限のないユーザーでも、他のユーザーに権限を許可できる場合があります。  
  
 次の表は、*objectid* を指定しない場合の、ステートメント権限に使用されるビットです。  
  
|ビット (10 進)|ビット (16 進)|ステートメント権限|  
|-----------------|-----------------|--------------------------|  
|1|0x1|CREATE DATABASE (master データベースのみ)|  
|2|0x2|CREATE TABLE|  
|4|0x4|CREATE PROCEDURE|  
|8|0x8|CREATE VIEW|  
|16|0x10|CREATE RULE|  
|32|0x20|CREATE DEFAULT|  
|64|0x40|BACKUP DATABASE|  
|128|0x80|BACKUP LOG|  
|256|0x100|予約済み。|  
  
 次の表は、*objectid* だけを指定したときに返される、オブジェクト権限に使用されるビットです。  
  
|ビット (10 進)|ビット (16 進)|ステートメント権限|  
|-----------------|-----------------|--------------------------|  
|1|0x1|SELECT ALL|  
|2|0x2|UPDATE ALL|  
|4|0x4|REFERENCES ALL|  
|8|0x8|INSERT|  
|16|0x10|DELETE|  
|32|0x20|EXECUTE (プロシージャのみ)|  
|4096|0x1000|SELECT ANY (少なくとも 1 列)|  
|8192|0x2000|UPDATE ANY|  
|16384|0x4000|REFERENCES ANY|  
  
 次の表は、*objectid* と column の両方を指定したときに返される、列レベルのオブジェクト権限に使用されるビットです。  
  
|ビット (10 進)|ビット (16 進)|ステートメント権限|  
|-----------------|-----------------|--------------------------|  
|1|0x1|SELECT|  
|2|0x2|UPDATE|  
|4|0x4|REFERENCES|  
  
 指定したパラメーターが NULL の場合や無効な場合 (存在しない *objectid* や column が指定されている場合など) は、NULL が返されます。 適用されない権限 (テーブルに対するビット 0x20 の EXECUTE 権限など) のビット値は定義されていません。  
  
 PERMISSIONS 関数で返すビットマップ内の各ビットを指定するには、ビットごとの AND 演算子 (&) を使用します。  
  
 現在のデータベース内のユーザーに与えられている権限の一覧を返すには、sp_helprotect システム ストアド プロシージャを使用することもできます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-the-permissions-function-with-statement-permissions"></a>A. PERMISSIONS 関数をステートメント権限に対して使用する  
 次の例では、現在のユーザーが `CREATE TABLE` ステートメントを実行できるかどうかを判定します。  
  
```  
IF PERMISSIONS()&2=2  
   CREATE TABLE test_table (col1 INT)  
ELSE  
   PRINT 'ERROR: The current user cannot create a table.';  
```  
  
### <a name="b-using-the-permissions-function-with-object-permissions"></a>B. PERMISSIONS 関数をオブジェクト権限に対して使用する  
 次の例では、現在のユーザーが `Address` データベース内の `AdventureWorks2012` テーブルにデータ行を挿入できるかどうかを判定します。  
  
```  
IF PERMISSIONS(OBJECT_ID('AdventureWorks2012.Person.Address','U'))&8=8   
   PRINT 'The current user can insert data into Person.Address.'  
ELSE  
   PRINT 'ERROR: The current user cannot insert data into Person.Address.';  
```  
  
### <a name="c-using-the-permissions-function-with-grantable-permissions"></a>C. PERMISSIONS 関数を、付与できる権限に対して使用する  
 次の例では、現在のユーザーが別のユーザーに `Address` データベース内の `AdventureWorks2012` テーブルに対する INSERT 権限を許可できるかどうかを判定します。  
  
```  
IF PERMISSIONS(OBJECT_ID('AdventureWorks2012.Person.Address','U'))&0x80000=0x80000  
   PRINT 'INSERT on Person.Address is grantable.'  
ELSE  
   PRINT 'You may not GRANT INSERT permissions on Person.Address.';  
```  
  
## <a name="see-also"></a>参照  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
