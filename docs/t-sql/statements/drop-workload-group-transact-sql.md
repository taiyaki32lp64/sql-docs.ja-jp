---
title: DROP WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_WORKLOAD_GROUP_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD GROUP statement
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 90622710b19ef3c2692cdcff62089cb7539fcf97
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632802"
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>製品をクリックしてください

次の行から興味がある製品名をクリックしてみてください。 この Web ページでは、クリックした製品に合わせて、異なるコンテンツが表示されます。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**\* _SQL Server \*_** &nbsp;|[SQL Database<br />マネージド インスタンス](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server と SQL Database Managed Instance


  既存のユーザー定義の Resource Governor ワークロード グループを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>構文  
  
```  
  
DROP WORKLOAD GROUP group_name  
[;]  
```  
  
## <a name="arguments"></a>引数  
 *group_name*  
 既存のユーザー定義のワークロード グループの名前を指定します。  
  
## <a name="remarks"></a>Remarks  
 Resource Governor の内部グループや既定のグループに対して、DROP WORKLOAD GROUP ステートメントを使用することはできません。  
  
 DDL ステートメントを実行する場合、Resource Governor の状態について詳しく理解しておくことをお勧めします。 詳細については、「[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)」を参照してください。  
  
 アクティブなセッションが含まれているワークロード グループを削除したり別のリソース プールに移動したりした場合、その変更を適用するために ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを呼び出すと失敗します。 この問題を回避するには、次のいずれかの操作を実行します。  
  
-   そのグループからすべてのセッションが切断されるまで待ってから、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを再実行します。  
  
-   そのグループ内のセッションを KILL コマンドで明示的に停止してから、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを再実行します。  
  
-   サーバーを再起動します。 再起動プロセスの完了後、削除したグループは作成されず、移動したグループは新しいリソース プール割り当てを使用します。  
  
-   DROP WORKLOAD GROUP ステートメントを実行してから、変更適用のためにセッションを明示的に停止するのは不適切であると判断した場合、DROP ステートメントの実行前と同じ名前でグループを再作成し、このグループを元のリソース プールに移動することができます。 変更を適用するには、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを実行します。  
  
## <a name="permissions"></a>アクセス許可

 CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例

 次の例では、`adhoc` という名前のワークロード グループを削除します。  
  
```  
DROP WORKLOAD GROUP adhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)||[SQL Database<br />マネージド インスタンス](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* SQL Data<br />Warehouse \*_** &nbsp;||||

&nbsp;

## <a name="sql-data-warehouse-preview"></a>SQL Data Warehouse (プレビュー)

ワークロード グループを削除します。  ステートメントが完了すると、設定が有効になります。

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

## <a name="syntax"></a>構文

```
DROP WORKLOAD GROUP group_name  
```

## <a name="arguments"></a>引数

 *group_name*  
 既存のユーザー定義のワークロード グループの名前を指定します。

## <a name="remarks"></a>Remarks

ワークロード グループに分類子が存在する場合、ワークロード グループを削除することはできません。  ワークロード グループが削除される前に、分類子を削除します。  ワークロード グループのリソースを使用しているアクティブな要求が削除されると、それらの背後で DROP WORKLOAD ステートメントがブロックされます。

## <a name="examples"></a>使用例

ワークロード グループを削除するには、その前に次のコード例を使用して、削除する必要がある分類子を決定する必要があります。

```sql
SELECT c.name as classifier_name
      ,'DROP WORKLOAD CLASSIFIER '+c.name as drop_command
  FROM sys.workload_management_workload_classifiers c
  JOIN sys.workload_management_workload_groups g
    ON c.group_name = g.name
  WHERE g.name = 'wgXYZ' --change the filter to the workload being dropped
```

## <a name="permissions"></a>アクセス許可

CONTROL DATABASE アクセス許可が必須です

## <a name="see-also"></a>参照
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 
::: moniker-end
