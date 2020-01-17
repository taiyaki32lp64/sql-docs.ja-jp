---
title: sp_settriggerorder (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_settriggerorder
- sp_settriggerorder_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_settriggerorder
ms.assetid: 8b75c906-7315-486c-bc59-293ef12078e8
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e258badbcf304fddbaf7575269194bd409ec8645
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982231"
---
# <a name="sp_settriggerorder-transact-sql"></a>sp_settriggerorder (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  最初または最後に起動される AFTER トリガーを指定します。 最初と最後のトリガーの間で起動される AFTER トリガーは、任意の順序で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_settriggerorder [ @triggername = ] '[ triggerschema. ] triggername'   
    , [ @order = ] 'value'   
    , [ @stmttype = ] 'statement_type'   
    [ , [ @namespace = ] { 'DATABASE' | 'SERVER' | NULL } ]  
```  
  
## <a name="arguments"></a>引数  
`[ @triggername = ] '[ _triggerschema.] _triggername'` は、トリガーの名前と、そのトリガーが属するスキーマ (該当する場合) の順序を設定または変更するものです。 [_triggerschema_ **.** ]*トリガー*は**sysname**です。 名前がトリガーに対応していない場合、または名前が INSTEAD OF トリガーに対応している場合、プロシージャはエラーを返します。 *triggerschema*を DDL トリガーまたはログオントリガーに対して指定することはできません。  
  
`[ @order = ] 'value'` は、トリガーの新しい順序の設定です。 *値*は**varchar (10)** で、次のいずれかの値を指定できます。  
  
> [!IMPORTANT]  
>  **First**と**Last**トリガーは 2 つの異なるトリガーである必要があります。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**First**|トリガーは最初に起動されます。|  
|**Last**|最後にトリガーが起動されます。|  
|**なし**|トリガーは、定義されていない順序で発生します。|  
  
`[ @stmttype = ] 'statement_type'`、トリガーを起動する SQL ステートメントを指定します。 *statement_type*は**varchar (50)** で、INSERT、UPDATE、DELETE、LOGON、または[DDL イベント](../../relational-databases/triggers/ddl-events.md)に記載されている [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントイベントを指定できます。 イベントグループを指定することはできません。  
  
 トリガーとして指定できる、**First**または**Last**ステートメントの種類のトリガーとしてそのトリガーが定義した後にのみステートメントの種類のトリガー。 たとえば、トリガー **TR1**指定できるは**First**テーブルに挿入**T1**場合**TR1** INSERT トリガーとして定義されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]エラーが返されます**TR1**、として設定されますが、INSERT トリガーとしてのみ定義されている、**First**、または**Last**、UPDATE ステートメントをトリガーします。 詳細については、「解説」を参照してください。  
  
 **\@名前空間 =** { **' データベース '**  |  **' SERVER '** |空白  
 *トリガー*が DDL トリガーである場合、 **\@名前空間**は、データベーススコープまたはサーバースコープで*トリガー*が作成されたかどうかを指定します。 *トリガー*が logon トリガーの場合は、SERVER を指定する必要があります。 DDL トリガーのスコープの詳細については、「 [Ddl Triggers](../../relational-databases/triggers/ddl-triggers.md)」を参照してください。 指定されていない場合、または NULL が指定されている場合、*トリガー*は DML トリガーです。  
  
||  
|-|  
|サーバーの適用対象: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) と 1 (失敗)  
  
## <a name="remarks"></a>Remarks  
  
## <a name="dml-triggers"></a>DML トリガー  
 1 つのみ**First**と 1 つ**Last**1 つのテーブルの各ステートメントに対してトリガーします。  
  
 場合、**First**トリガーがテーブル、データベース、またはサーバーで既に定義されている、として新しいトリガーを指定することはできません**First**の同じテーブル、データベース、またはサーバーで、同じ*statement_type*. この制限は適用も**Last**トリガーします。  
  
 レプリケーションは、テーブルが即時更新サブスクリプションまたはキュー更新サブスクリプションに含まれる場合、自動的に最初のトリガーを生成します。 レプリケーションのトリガーは最初のトリガーであることが必要です。 レプリケーションでは、最初のトリガーを持つテーブルを即時更新サブスクリプションまたはキュー更新サブスクリプションに含めるよう設定すると、エラーが発生します。 テーブルをサブスクリプションに含めた後、トリガーを最初のトリガーに設定すると、 **sp_settriggerorder** はエラーを返します。 レプリケーション トリガーに ALTER TRIGGER を使用して、または使用するかどうかは**sp_settriggerorder**レプリケーション トリガーを変更する、**Last**または**None**トリガーでは、サブスクリプションは正しく機能しません。  
  
## <a name="ddl-triggers"></a>DDL トリガー  
 両方のトリガーがあることを指定するにはデータベース スコープの DDL トリガーとサーバー スコープの DDL トリガーが、同じイベントで存在する場合、**First**トリガーまたは**Last**トリガーします。 ただし、常にサーバー スコープのトリガーが最初に起動します。 一般に、同じイベント上に存在する DDL トリガーの実行の順序のとおりです。  
  
1.  サーバー レベル トリガー**First**します。  
  
2.  その他のサーバー レベル トリガー。  
  
3.  サーバー レベル トリガー**Last**します。  
  
4.  データベース レベル トリガー**First**します。  
  
5.  その他のデータベース レベル トリガー。  
  
6.  データベース レベル トリガー**Last**します。  
  
## <a name="general-trigger-considerations"></a>トリガーについての留意事項  
 ALTER TRIGGER ステートメントが最初と最後のトリガーの場合は、変更された場合、**First**または**Last**トリガーに設定されていた属性が削除され、値が置き換え**None**します。 使用して、順序の値をリセットする必要があります**sp_settriggerorder**します。  
  
 1 つ以上のステートメントの種類の最初と最後の順序と同じトリガーを指定する必要がある場合**sp_settriggerorder**ステートメントの種類ごとに実行する必要があります。 また、トリガーする必要があります最初ステートメントの種類の前に定義することを指定できます、**First**または**Last**にステートメントの種類に対して起動されるトリガー。  
  
## <a name="permissions"></a>アクセス許可  
 サーバースコープ (すべてのサーバーで作成) またはログオントリガーの DDL トリガーの順序を設定するには、CONTROL SERVER 権限が必要です。  
  
 (データベースで作成された) データベーススコープを持つ DDL トリガーの順序を設定するには、ALTER ANY DATABASE DDL TRIGGER 権限が必要です。  
  
 DML トリガーの順序を設定するには、トリガーが定義されているテーブルまたはビューに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-setting-the-firing-order-for-a-dml-trigger"></a>A. DML トリガーの起動順序を設定する  
 次の例では、`uSalesOrderHeader`テーブルで`UPDATE`操作が発生した後に、`Sales.SalesOrderHeader`が最初にトリガーされるように指定しています。  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'Sales.uSalesOrderHeader', @order='First', @stmttype = 'UPDATE';  
```  
  
### <a name="b-setting-the-firing-order-for-a-ddl-trigger"></a>b. DDL トリガーの起動順序を設定する  
 次の例では、トリガー `ddlDatabaseTriggerLog` が、`ALTER_TABLE` データベースで [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] イベントの発生後、最初に起動されるトリガーとなるよう指定します。  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'ddlDatabaseTriggerLog', @order='First', @stmttype = 'ALTER_TABLE', @namespace = 'DATABASE';  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データベース エンジン ストアド プロシージャ&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
  
