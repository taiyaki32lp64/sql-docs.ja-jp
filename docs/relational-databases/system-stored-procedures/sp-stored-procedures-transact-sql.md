---
title: sp_stored_procedures (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_stored_procedures_TSQL
- sp_stored_procedures
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stored_procedures
ms.assetid: fe52dd83-000a-4665-83fb-7a0024193dec
author: stevestein
ms.author: sstein
ms.openlocfilehash: 554b9317d6b474b23e9dbbc10dea03156ccc6287
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702782"
---
# <a name="spstoredprocedures-transact-sql"></a>sp_stored_procedures (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在の環境内にあるストアド プロシージャの一覧を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_stored_procedures [ [ @sp_name = ] 'name' ]   
    [ , [ @sp_owner = ] 'schema']   
    [ , [ @sp_qualifier = ] 'qualifier' ]  
    [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @sp_name = ] 'name'`カタログ情報を返すために使用するプロシージャの名前を指定します。 *名前*は**nvarchar (390)** ,、既定値は NULL です。 ワイルドカードパターンマッチングがサポートされています。  
  
`[ @sp_owner = ] 'schema'`プロシージャが属しているスキーマの名前を指定します。 *スキーマ*は**nvarchar (384)** ,、既定値は NULL です。 ワイルドカードパターンマッチングがサポートされています。 *Owner*が指定されていない場合、基になる DBMS の既定のプロシージャ可視性ルールが適用されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、指定した名前のプロシージャが現在のスキーマに含まれている場合、そのプロシージャが返されます。 修飾名なしでストアド プロシージャを指定した場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では次の順序でプロシージャが検索されます。  
  
-   現在のデータベースの **sys** スキーマ。  
  
-   バッチまたは動的 SQL で実行された場合は、呼び出し元の既定のスキーマ。または、修飾されていないプロシージャ名が別のプロシージャ定義の本文内にある場合は、その他のプロシージャを含むスキーマが次に検索されます。  
  
-   現在のデータベースの **dbo** スキーマ。  
  
`[ @qualifier = ] 'qualifier'`プロシージャ修飾子の名前を指定します。 *修飾子*は**sysname**,、既定値は NULL です。 さまざまな DBMS 製品で、3つの要素で構成されるテーブル名 (_修飾子_) がサポートさ**れています。** _スキーマ_ **.** _名前_。 で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は、*修飾子*はデータベース名を表します。 一部の製品では、テーブルのデータベース環境のサーバー名を表します。  
  
`[ @fUsePattern = ] 'fUsePattern'`アンダースコア (_)、パーセント (%)、または角かっこ []) をワイルドカード文字として解釈するかどうかを決定します。 *Fusepattern*は**ビット**,、既定値は1です。  
  
 **0** = パターンマッチングは無効です。  
  
 **1** = パターンマッチングはオンです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|プロシージャ修飾子の名前。 この列は NULL にすることができます。|  
|**PROCEDURE_OWNER**|**sysname**|プロシージャ所有者の名前。 この列は常に値が返されます。|  
|**PROCEDURE_NAME**|**nvarchar(134)**|プロシージャの名前。 この列は常に値が返されます。|  
|**NUM_INPUT_PARAMS**|**int**|将来使用するために予約されています。|  
|**NUM_OUTPUT_PARAMS**|**int**|将来使用するために予約されています。|  
|**NUM_RESULT_SETS**|**int**|将来使用するために予約されています。|  
|**」**|**varchar(254)**|プロシージャの説明。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]はこの列の値を返しません。|  
|**PROCEDURE_TYPE**|**smallint**|プロシージャの種類。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は常に 2.0 を返します。 この値には、次のいずれかを指定できます。<br /><br /> 0 = SQL_PT_UNKNOWN<br /><br /> 1 = SQL_PT_PROCEDURE<br /><br /> 2 = SQL_PT_FUNCTION|  
  
## <a name="remarks"></a>コメント  
 相互運用性を最大限に高めるために、ゲートウェイのクライアントでは、SQL 標準のパターン照合 (パーセント (%) とアンダースコア (_) ワイルドカード文字) のみを前提としています。  
  
 現在のユーザーに対する特定のストアドプロシージャへの実行アクセスに関する権限情報は必ずしもチェックされません。そのため、アクセスは保証されません。 3部構成の名前付けのみが使用されていることに注意してください。 これは、リモートストアドプロシージャ (4 つの部分で構成される名前を必要とする) ではなく、ローカルストアドプロシージャ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]だけが返されることを意味します。 **Sp_server_info**の結果セットで SERVER 属性 ACCESSIBLE_SPROC が Y の場合、現在のユーザーが実行できるストアドプロシージャのみが返されます。  
  
 **sp_stored_procedures**は、ODBC の**sqlprocedures**と同じです。 返される結果は、 **PROCEDURE_QUALIFIER**、 **PROCEDURE_OWNER**、および**PROCEDURE_NAME**の順序で並べ替えられます。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-all-stored-procedures-in-the-current-database"></a>A. 現在のデータベース内のすべてのストアドプロシージャを返す  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内のすべてのストアド プロシージャを返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_stored_procedures;  
```  
  
### <a name="b-returning-a-single-stored-procedure"></a>B. 1 つのストアド プロシージャを返す  
 次の例では、 `uspLogError`ストアドプロシージャの結果セットが返されます。  
  
```  
USE AdventureWorks2012;  
GO  
sp_stored_procedures N'uspLogError', N'dbo', N'AdventureWorks2012', 1;  
```  
  
## <a name="see-also"></a>関連項目  
 [カタログストアドプロシージャ&#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
