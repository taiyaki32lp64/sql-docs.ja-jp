---
title: OBJECT_DEFINITION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OBJECT_DEFINITION_TSQL
- OBJECT_DEFINITION
dev_langs:
- TSQL
helpviewer_keywords:
- viewing source text
- source text [SQL Server]
- displaying source text
- OBJECT_DEFINITION function
ms.assetid: 2ac837c7-eca9-4d29-b06e-72e30450c68d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0ec1dc88832c4a44b3f019bb0e63369ab2d3587a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914893"
---
# <a name="objectdefinition-transact-sql"></a>OBJECT_DEFINITION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定したオブジェクトの定義の [!INCLUDE[tsql](../../includes/tsql-md.md)] ソース テキストを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
OBJECT_DEFINITION ( object_id )  
```  
  
## <a name="arguments"></a>引数  
 *object_id*  
 使用するオブジェクトの ID です。 *object_id* は **int**, 、現在のデータベース コンテキスト内のオブジェクトが想定されます。  
  
## <a name="return-types"></a>戻り値の型  
 **nvarchar(max)**  
  
## <a name="exceptions"></a>例外  
 エラーが発生した場合、または呼び出し元にオブジェクトの表示権限がない場合は、NULL が返されます。  
  
 ユーザーが所有しているか、または権限を与えられている、セキュリティ保護可能なリソースのメタデータのみを表示できます。 つまり、オブジェクトに対する権限がユーザーに与えられていない場合、メタデータを生成する組み込み関数 (OBJECT_DEFINITION など) が NULL を返す可能性があります。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  を前提としています *object_id* が現在のデータベース コンテキストでします。 オブジェクト定義の照合順序は、呼び出し元のデータベース コンテキストのそれと常に一致します。  
  
 OBJECT_DEFINITION は、次の種類のオブジェクトに適用されます。  
  
-   C = CHECK 制約  
  
-   D = 既定値 (制約またはスタンドアロン)  
  
-   P = SQL ストアド プロシージャ  
  
-   FN = SQL スカラー関数  
  
-   R = ルール  
  
-   RF = レプリケーション フィルター プロシージャ  
  
-   TR = SQL トリガー (スキーマ スコープ DML トリガー、またはデータベースまたはサーバー スコープの DDL トリガー)  
  
-   IF = SQL インライン テーブル値関数  
  
-   TF = SQL テーブル値関数  
  
-   V = ビュー  
  
## <a name="permissions"></a>アクセス許可  
 システム オブジェクトの定義は、公開されます。 ユーザー オブジェクトの定義は、オブジェクトの所有者、または次のいずれかの権限を許可された人が表示できます。ALTER、CONTROL、TAKE OWNERSHIP、VIEW DEFINITION。 これらの権限は **db_owner**、 **db_ddladmin**、および **db_securityadmin** 固定データベース ロールのメンバーが暗黙的に保有します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-the-source-text-of-a-user-defined-object"></a>A. ユーザー定義オブジェクトのソース テキストを返す  
 次の例では、ユーザー定義トリガー `uAddress` の定義を `Person` スキーマで返します。 組み込み関数 `OBJECT_ID` を使用して、トリガーのオブジェクト ID を `OBJECT_DEFINITION` ステートメントに返します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'Person.uAddress')) AS [Trigger Definition];   
GO  
```  
  
### <a name="b-returning-the-source-text-of-a-system-object"></a>B. システム オブジェクトのソース テキストを返す  
 次の例では、システム ストアド プロシージャ `sys.sp_columns` の定義を返します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'sys.sp_columns')) AS [Object Definition];  
GO  
```  
  
## <a name="see-also"></a>参照  
 [メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)  
  
  
