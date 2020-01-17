---
title: CREATE WORKLOAD CLASSIFIER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- CREATE WORKLOAD CLASSIFIER
- CREATE_WORKLOAD_CLASSIFIER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD CLASSIFIER statement
ms.assetid: ''
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: adf8b1e04e7dcd75bcad0c4b184ae60f2b59d248
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056495"
---
# <a name="create-workload-classifier-transact-sql"></a>CREATE WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

ワークロード管理で使用する分類子オブジェクトを作成します。  分類子では、受信要求が分類子ステートメントの定義に指定されたパラメーターに基づいて、ワークロード グループに割り当てられます。  分類子は要求が送信されるごとに評価されます。  要求が分類子と一致しない場合、要求は既定のワークロード グループに割り当てられます。  既定のワークロード グループは、smallrc リソース クラスです。

> [!NOTE]
> ワークロード分類子は、sp_addrolemember リソース クラスの割り当ての代わりになります。  ワークロード分類子を作成した後、sp_droprolemember を実行して、冗長なリソース クラスのマッピングを削除します。

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>構文

```
CREATE WORKLOAD CLASSIFIER classifier_name  
WITH  
    (   WORKLOAD_GROUP = ‘name’  
    ,   MEMBERNAME = ‘security_account’ 
[ [ , ] WLM_LABEL = ‘label’ ]  
[ [ , ] WLM_CONTEXT = ‘context’ ]  
[ [ , ] START_TIME = ‘HH:MM’ ]  
[ [ , ] END_TIME = ‘HH:MM’ ]  
  
[ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]) 
[;]
```

## <a name="arguments"></a>引数

 *classifier_name*  
 ワークロード分類子を識別する名前を指定します。  classifier_name は sysname です。  これは長さを最大で 128 文字とすることができ、インスタンス内では一意である必要があります。

 *WORKLOAD_GROUP* =  *'name'*    
 分類子の規則によって条件が満たされると、name によって要求がワークロード グループにマップされます。  name は sysname です。  これは長さを最大で 128 文字とすることができ、分類子作成時には有効なワークロード グループ名とする必要があります。

 使用可能なワークロード グループは、[sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md) カタログ ビューで見つけることができます。

 *MEMBERNAME* ='security_account'*    
 これはロールに追加されるセキュリティ アカウントです。  security_account は sysname です。既定値はありません。 security_account は、データベース ユーザー、データベース ロール、Azure Active Directory ログイン、または Azure Active Directory グループとすることができます。
 
 *WLM_LABEL*   
 要求を分類できるラベル値を指定します。  ラベルは、nvarchar(255) 型の省略可能なパラメーターです。  要求の [OPTION (LABEL)](/azure/sql-data-warehouse/sql-data-warehouse-develop-label) を使用して、分類子の構成を一致させます。

例:

```sql
CREATE WORKLOAD CLASSIFIER wcELTLoads WITH  
( WORKLOAD_GROUP = 'wgDataLoad'
 ,MEMBERNAME     = 'ELTRole'  
 ,WLM_LABEL      = 'dimension_loads' )

SELECT COUNT(*) 
  FROM DimCustomer
  OPTION (LABEL = 'dimension_loads')
```

*WLM_CONTEXT*  
要求を分類できるセッション コンテキスト値を指定します。  コンテキストは、nvarchar(255) 型の省略可能なパラメーターです。  セッション コンテキストを設定する要求を送信する前に、`wlm_context` と同じ変数名と共に [sys. sp_set_session_context](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md?view=azure-sqldw-latest) を使用します。

例:

```sql
CREATE WORKLOAD CLASSIFIER wcDataLoad WITH  
( WORKLOAD_GROUP = 'wgDataLoad'
 ,MEMBERNAME     = 'ELTRole'
 ,WLM_CONTEXT    = 'dim_load' )
 
--set session context
EXEC sys.sp_set_session_context @key = 'wlm_context', @value = 'dim_load'

--run multiple statements using the wlm_context setting
SELECT COUNT(*) FROM stg.daily_customer_load
SELECT COUNT(*) FROM stg.daily_sales_load

--turn off the wlm_context session setting
EXEC sys.sp_set_session_context @key = 'wlm_context', @value = null
```

*START_TIME* と *END_TIME*  
要求を分類できる start_time と end_time を指定します。  start_time と end_time はどちらも UTC タイムゾーンの HH:MM 形式です。  start_time と end_time は、一緒に指定する必要があります。

例:

```sql
CREATE WORKLOAD CLASSIFIER wcELTLoads WITH  
( WORKLOAD_GROUP = 'wgDataLoads'
 ,MEMBERNAME     = 'ELTRole'  
 ,START_TIME     = '22:00'
 ,END_TIME       = '02:00' )
```

*IMPORTANCE* = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }  
要求の相対的な重要度を指定します。  重要度は次のいずれかです。

- LOW
- BELOW_NORMAL
- NORMAL (既定値)
- ABOVE_NORMAL
- HIGH  

重要度が指定されていない場合は、ワークロード グループの重要度の設定が使用されます。  既定のワークロード グループの重要度は NORMAL です。  重要度は要求がスケジュールされる順番に影響します。それによって、リソースおよびロックへの最初のアクセスが指定されます。

## <a name="classification-parameter-precedence"></a>分類パラメーターの優先順位

要求は、複数の分類子と照合できます。  分類子パラメーターには優先順位があります。  優先順位の高い一致した分類子が、ワークロード グループと重要度の割り当てに、最初に使用されます。  優先順位は次のとおりです。
1. User
2. ROLE
3. WLM_LABEL
4. WLM_SESSION
5. START_TIME/END_TIME

次の分類子構成について考えてみます。

```sql
CREATE WORKLOAD CLASSIFIER classiferA WITH  
( WORKLOAD_GROUP = 'wgDashboards'  
 ,MEMBERNAME     = 'userloginA'
 ,IMPORTANCE     = HIGH
 ,WLM_LABEL      = 'salereport' )

CREATE WORKLOAD CLASSIFIER classiferB WITH  
( WORKLOAD_GROUP = 'wgUserQueries'  
 ,MEMBERNAME     = 'userloginA'
 ,IMPORTANCE     = LOW
 ,START_TIME     = '18:00')
 ,END_TIME       = '07:00' )
```

ユーザー `userloginA` は両方の分類子で構成されています。  userloginA が UTC の午後 6 時から午前 7 時までの間に `salesreport` と等しいラベルを持つクエリを実行すると、要求は wgDashboards ワークロード グループに分類され、重要度が HIGH になります。  時間外のレポートの重要度が LOW の wgUserQueries に要求が分類されることが予想されますが、WLM_LABEL の優先順位は START_TIME/END_TIME よりも高くなります。  この場合、START_TIME/END_TIME を classiferA に追加できます。

 詳細については、[ワークロードの分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification#classification-precedence)に関するページを参照してください。

## <a name="permissions"></a>アクセス許可

 CONTROL DATABASE アクセス許可が必須です。  
  
## <a name="examples"></a>使用例

 次の例は、`wgcELTRole` という名前のワークロード分類子を作成する方法を示します。 この例では、ワークロード グループ staticrc20 およびユーザー `ELTRole` が使用され、重要度が `above_normal` に設定されています。

```sql
CREATE WORKLOAD CLASSIFIER wgcELTRole
  WITH (WORKLOAD_GROUP = 'staticrc20'
       ,MEMBERNAME = 'ELTRole'
      ,IMPORTANCE = above_normal);
```

## <a name="see-also"></a>参照

[SQL Data Warehouse の分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)</br>
[DROP WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-classifier-transact-sql.md)</br>
[sys.workload_management_workload_classifiers](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)</br>
[sys.workload_management_workload_classifier_details](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)

