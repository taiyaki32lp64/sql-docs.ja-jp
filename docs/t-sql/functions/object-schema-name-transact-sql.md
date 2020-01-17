---
title: OBJECT_SCHEMA_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OBJECT_SCHEMA_NAME
- OBJECT_SCHEMA_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], names
- schemas [SQL Server], names
- displaying schema names
- database objects [SQL Server], names
- OBJECT_SCHEMA_NAME function
ms.assetid: 5ba90bb9-d045-4164-963e-e9e96c0b1e8b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 70556dd6365c6c3b204456db2877fdbc61e53d44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914751"
---
# <a name="objectschemaname-transact-sql"></a>OBJECT_SCHEMA_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  スキーマ スコープ オブジェクトのデータベース スキーマ名を返します。 スキーマ スコープ オブジェクトの一覧については、「[sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」をご覧ください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
OBJECT_SCHEMA_NAME ( object_id [, database_id ] )  
```  
  
## <a name="arguments"></a>引数  
 *object_id*  
 使用するオブジェクトの ID です。 *object_id* のデータ型は **int** です。指定したデータベース コンテキスト、または現在のデータベース コンテキストのスキーマ スコープ オブジェクトと見なされます。  
  
 *database_id*  
 オブジェクトを検索するデータベースの ID を指定します。 *database_id* は **int** です。  
  
## <a name="return-types"></a>戻り値の型  
 **sysname**  
  
## <a name="exceptions"></a>例外  
 エラーが発生した場合、または呼び出し元にオブジェクトの表示権限がない場合は、NULL が返されます。 呼び出し先データベースの AUTO_CLOSE オプションが ON に設定されている場合、データベースが開きます。  
  
 ユーザーが所有しているか、または権限を与えられている、セキュリティ保護可能なリソースのメタデータのみを表示できます。 つまり、オブジェクトに対する権限がユーザーに与えられていない場合、メタデータを生成する組み込み関数 (OBJECT_SCHEMA_NAME など) が NULL を返す可能性があります。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 オブジェクトに対する ANY 権限が必要です。 データベース ID を指定するには、そのデータベースの CONNECT 権限を持っているか、ゲスト アカウントが有効である必要があります。  
  
## <a name="remarks"></a>Remarks  
 システム関数は、選択リストの中、WHERE 句の中、また、式を使える所ならどこにでも使用できます。 詳しくは、「[式](../../t-sql/language-elements/expressions-transact-sql.md)」および「[WHERE](../../t-sql/queries/where-transact-sql.md)」をご覧ください。  
  
 このシステム関数が返す結果セットには、現在のデータベースの照合順序が使用されます。  
  
 *database_id* が指定されていない場合、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] は *object_id* が現在のデータベースのコンテキストであると見なします。 別のデータベースの *object_id* を参照するクエリは、NULL または正しくない値を返します。 たとえば、次のクエリでは、現在のデータベースのコンテキストは [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] です。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]は、クエリの FROM 句に指定されたデータベースではなく、このデータベースの指定されたオブジェクト ID のオブジェクト スキーマ名を返します。 したがって、正しくない情報が返されます。  
  
```sql
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id)  
FROM master.sys.objects;  
  
```  
  
 次の例では、`master` 関数で `OBJECT_SCHEMA_NAME` データベースのデータベース ID を指定し、正確な結果を返します。  
  
```sql
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id, 1) AS schema_name  
FROM master.sys.objects;  
  
```  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-the-object-schema-name-and-object-name"></a>A. オブジェクト スキーマ名とオブジェクト名を取得する  
 この例では、アドホック ステートメントでも準備されたステートメントでもない、キャッシュされたすべてのクエリ プランについて、オブジェクト スキーマ名、オブジェクト名、SQL テキストを返します。  
  
```sql
SELECT DB_NAME(st.dbid) AS database_name,   
    OBJECT_SCHEMA_NAME(st.objectid, st.dbid) AS schema_name,  
    OBJECT_NAME(st.objectid, st.dbid) AS object_name,   
    st.text AS query_statement  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
WHERE st.objectid IS NOT NULL;  
GO  
```  
  
### <a name="b-returning-three-part-object-names"></a>B. 3 つの要素で構成されたオブジェクト名を取得する  
 この例では、データベース名、スキーマ名、およびオブジェクト名と共に、すべてのデータベースのすべてのオブジェクトの統計を示す `sys.dm_db_index_operational_stats` 動的管理ビューの残りのすべての列を返します。  
  
```sql
SELECT QUOTENAME(DB_NAME(database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_SCHEMA_NAME(object_id, database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_NAME(object_id, database_id))  
    , *   
FROM sys.dm_db_index_operational_stats(null, null, null, null);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [セキュリティ保護可能](../../relational-databases/security/securables.md)
