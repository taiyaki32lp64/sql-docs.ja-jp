---
title: sys.sql_modules (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_modules_TSQL
- sql_modules
- sql_modules_TSQL
- sys.sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_modules catalog view
ms.assetid: 23d3ccd2-f356-4d89-a2cd-bee381243f99
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f3e007a0676afd507af54e3b3406297cf40042e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108988"
---
# <a name="syssqlmodules-transact-sql"></a>sys.sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  SQL 言語定義モジュールであるオブジェクトごとに 1 行を返します [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 、ネイティブを含むユーザー定義のスカラー関数をコンパイルします。 種類が P、RF、V、TR、FN、IF、TF、および R のオブジェクトには、SQL モジュールが関連付けられています。 スタンドアロンの既定値である種類 D のオブジェクトにも、このビューで SQL モジュール定義が関連付けられています。 これらの型の説明は、次を参照してください。、**型**内の列、 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)カタログ ビューです。  
  
 詳しくは、「[インメモリ OLTP でのユーザー定義のスカラー関数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)」をご覧ください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|このオブジェクトが属するオブジェクトの ID です。 データベース内で一意です。|  
|**definition**|**nvarchar(max)**|このモジュールを定義する SQL テキスト。 使用してこの値を取得することも、 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)組み込み関数。<br /><br /> NULL は、暗号化されていることを示します。|  
|**uses_ansi_nulls**|**bit**|モジュールは、SET ANSI_NULLS ON で作成されました。<br /><br /> ルールとデフォルトに対しては、常に 0 になります。|  
|**uses_quoted_identifier**|**bit**|モジュールは、SET QUOTED_IDENTIFIER ON で作成されました。|  
|**is_schema_bound**|**bit**|モジュールは SCHEMABINDING オプションを使用して作成されました。<br /><br /> ネイティブ コンパイル ストアド プロシージャでは、常に値 1 が含まれます。|  
|**uses_database_collation**|**bit**|スキーマ バインドのモジュール定義が適切な評価のためにデータベースの既定の照合順序に依存する場合は 1 になります。それ以外の場合は 0 になります。 このような依存関係により、データベースの既定の照合順序は変更されないようになっています。|  
|**is_recompiled**|**bit**|プロシージャは WITH RECOMPILE オプションを使用して作成されました。|  
|**null_on_null_input**|**bit**|モジュールは、任意の NULL 入力上で NULL 出力を生成するように宣言されました。|  
|**execute_as_principal_id**|**Int**|EXECUTE AS データベース プリンシパルの ID です。<br /><br /> 既定値または EXECUTE AS CALLER の場合は、NULL になります。<br /><br /> 場合は、指定したプリンシパルの ID または EXECUTE AS SELF の実行\<プリンシパル >。<br /><br /> -2 = EXECUTE AS OWNER。|  
|**uses_native_compilation**|**bit**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] から [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]<br /><br /> 0 = ネイティブでコンパイルされていない<br /><br /> 1 = ネイティブでコンパイルされている<br /><br /> 既定値は 0 です。|  
|**is_inlineable**|**bit**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssqlv15-md.md)] 以降。<br/><br />かどうかには、モジュールが lineable いないかどうかを示します。 変換が指定された条件に基づいて[ここ](../user-defined-functions/scalar-udf-inlining.md#inlineable-scalar-udfs-requirements)します。<br /><br /> 0 = inlineable しません<br /><br /> 1 = lineable ではありません。 <br /><br /> スカラー udf の場合、値は、UDF inlineable、および 0 それ以外の場合 1 になります。 インライン Tvf、およびその他のすべてのモジュール型の場合は 0 1 の値を常に含まれています。<br />|  
|**inline_type**|**bit**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssqlv15-md.md)] 以降。<br /><br />示すインライン化するかどうか、モジュールの現在オンします。 <br /><br />0 = インライン化はオフになります<br /><br /> 1 = インライン展開がオンにします。<br /><br /> スカラー Udf は、値は 1 にインライン化 (明示的または暗黙的に) がオンします。 値は、インライン Tvf、1 およびその他のモジュール型の場合は 0 に常になります。<br />|  

  
## <a name="remarks"></a>コメント  
 既定の制約では、種類 D のオブジェクトの SQL 式がある、 [sys.default_constraints](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md)カタログ ビューです。 CHECK 制約、C の型のオブジェクトの SQL 式がある、 [sys.check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)カタログ ビューです。  
  
 この情報が記載されても[sys.dm_db_uncontained_entities &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、現在のデータベース内の各モジュールの名前、型、および定義を返します。  
  
```  
SELECT sm.object_id, OBJECT_NAME(sm.object_id) AS object_name, o.type, o.type_desc, sm.definition  
FROM sys.sql_modules AS sm  
JOIN sys.objects AS o ON sm.object_id = o.object_id  
ORDER BY o.type;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [SQL Server のシステム カタログよく寄せられる質問のクエリを実行します。](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
