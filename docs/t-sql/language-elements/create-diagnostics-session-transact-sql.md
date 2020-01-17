---
title: CREATE DIAGNOSTICS SESSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 662d019e-f217-49df-9e2f-b5662fa0342d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0d4148e002ba84677e13e101a4830f0b6da10915
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088972"
---
# <a name="create-diagnostics-session-transact-sql"></a>CREATE DIAGNOSTICS SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  診断セッションを使用すると、システムまたはクエリのパフォーマンスについての詳細なユーザー定義の診断情報を保存することができます。  
  
 診断セッションは通常、特定のクエリのパフォーマンスをデバッグする、またはアプライアンス操作中に特定のアプライアンス コンポーネントの動作を監視する場合に使用します。  
  
> [!NOTE]  
>  診断セッションを使用するために XML を熟知してください。  
  
## <a name="syntax"></a>構文  
  
```  
Creating a new diagnostics session:  
CREATE DIAGNOSTICS SESSION diagnostics_name AS N'{<session_xml>}';  
  
<session_xml>::  
<Session>  
   [ <MaxItemCount>max_item_count_num</MaxItemCount> ]  
   <Filter>  
      { \<Event Name="event_name"/>  
         [ <Where>\<filter_property_name Name="value" ComparisonType="comp_type"/></Where> ] [ ,...n ]  
      } [ ,...n ]  
   </Filter> ]   
   <Capture>  
      \<Property Name="property_name"/> [ ,...n ]  
   </Capture>  
<Session>  
  
Retrieving results for a diagnostics session:  
SELECT * FROM master.sysdiag.diagnostics_name ;  
  
Removing results for a diagnostics session:  
DROP DIAGNOSTICS SESSION diagnostics_name ;  
```  
  
## <a name="arguments"></a>引数  
 *diagnostics_name*  
 診断セッションの名前。 診断セッションの名前には、文字 a - z、A - Z、0 - 9 のみを含めることができます。 また、診断セッションの名前は、文字で開始する必要があります。 *diagnostics_name* の上限は 127 文字です。  
  
 *max_item_count_num*  
 ビューに保存されるイベントの数。 たとえば、100 を指定した場合は、フィルター条件に一致する最新の 100 イベントが診断セッションに保存されます。 見つかった一致するイベントが 100 より少ない場合は、診断セッションに含まれるイベントは 100 未満になります。 *max_item_count_num* は 100 以上 100,000 以下である必要があります。  
  
 *event_name*  
 診断セッションで収集する実際のイベントを定義します。  *event_name* は、`sys.pdw_diag_events.is_enabled='True'` の場合に [sys.pdw_diag_events](../../relational-databases/system-catalog-views/sys-pdw-diag-events-transact-sql.md) に列挙されるイベントの 1 つです。  
  
 *filter_property_name*  
 結果を制限するプロパティの名前です。 たとえば、セッション ID に基づいて制限する場合は、*filter_property_name* を *SessionId* にする必要があります。 *filter_property_name* に使用できる値の一覧については、以下の *property_name* を参照してください。  
  
 *value*  
 *filter_property_name* に対して評価する値。 値の型は、プロパティの型と一致する必要があります。 たとえば、プロパティの型が decimal の場合、*value* の型も decimal である必要があります。  
  
 *comp_type*  
 比較型。 可能性のある値: Equals、EqualsOrGreaterThan、EqualsOrLessThan、GreaterThan、LessThan、NotEquals、Contains、RegEx  
  
 *property_name*  
 イベントに関連するプロパティです。  プロパティ名は、キャプチャ タグの一部でもかまわず、またはフィルター条件の一部として使用されます。  
  
|プロパティ名|[説明]|  
|-------------------|-----------------|  
|UserName|ユーザー (ログイン) の名前。|  
|SessionId|セッション ID。|  
|QueryId|クエリの ID。|  
|CommandType|コマンドの種類。|  
|CommandText|処理されたコマンド内のテキスト。|  
|[OperationType]|イベントの操作の種類。|  
|Duration|イベントの期間。|  
|SPID|サービス プロセス ID。|  
  
## <a name="remarks"></a>Remarks  
 各ユーザーには、最大 10 個の同時診断セッションが許可されます。 現在のセッションの一覧については、[sys.pdw_diag_sessions](../../relational-databases/system-catalog-views/sys-pdw-diag-sessions-transact-sql.md) を参照してください。不要なセッションがある場合は、`DROP DIAGNOSTICS SESSION` を使用して削除します。  
  
 診断セッションでは、削除されるまでメタデータの収集が続行されます。  
  
## <a name="permissions"></a>アクセス許可  
 **ALTER SERVER STATE** アクセス許可が必要です。  
  
## <a name="locking"></a>ロック  
 診断セッション テーブルで共有ロックを取得します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-diagnostics-session"></a>A. 診断セッションを作成する  
 この例では、データベース エンジンのパフォーマンスのメトリックを記録する診断セッションを作成します。 この例では、エンジン クエリ実行/終了イベントと DMS ブロック   イベントをリッスンする診断セッションを作成します。 返される結果は、コマンド テキスト、コンピューター名、要求 ID (クエリ ID)、イベントが作成されたセッションです。  
  
```  
CREATE DIAGNOSTICS SESSION MYDIAGSESSION AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:EngineQueryRunningEvent" />  
      <Event Name="DmsCoreInstrumentation:DmsBlockingQueueEnqueueBeginEvent" />  
      <Where>  
         <SessionId Value="381" ComparisonType="NotEquals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Query.CommandText" />  
      <Property Name="MachineName" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Alias" />  
      <Property Name="Duration" />  
      <Property Name="Session.SessionId" />  
   </Capture>  
</Session>';  
```  
  
 診断セッションの作成後に、クエリを実行します。  
  
```  
SELECT COUNT(EmployeeKey) FROM AdventureWorksPDW2012..FactSalesQuota;  
```  
  
 その後、sysdiag スキーマから選択して、診断セッションの結果を表示します。  
  
```  
SELECT * FROM master.sysdiag.MYDIAGSESSION;  
```  
  
 sysdiag スキーマには、診断セッション名の名前が付いたビューが含まれることに注意してください。  
  
 接続のアクティビティのみを表示するには、`Session.SPID` プロパティを追加し、`WHERE [Session.SPID] = @@spid;` をクエリに追加します。  
  
 診断セッションが完了したら、**DROP DIAGNOSTICS** コマンドを使用して削除します。  
  
```  
DROP DIAGNOSTICS SESSION MYDIAGSESSION;  
```  
  
### <a name="b-alternative-diagnostic-session"></a>B. 別の診断セッション  
 わずかに異なるプロパティを持つ 2 番目の例です。  
  
```  
-- Determine the session_id of your current session  
SELECT TOP 1 session_id();  
-- Replace \<*session_number*> in the code below with the numbers in your session_id  
CREATE DIAGNOSTICS SESSION PdwOptimizationDiagnostics AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:MemoGenerationBeginEvent" />  
      <Event Name="EngineInstrumentation:MemoGenerationEndEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationBeginEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationEndEvent" />  
      <Event Name="DSQLInstrumentation:BuildRelOpContextTreeBeginEvent" />  
      <Event Name="DSQLInstrumentation:PostPlanGenModifiersEndEvent" />  
      <Where>  
         <SessionId Value="\<*session_number*>" ComparisonType="Equals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Session.SessionId" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Query.CommandText" />  
      <Property Name="Name" />  
      <Property Name="DateTimePublished" />  
      <Property Name="DateTimePublished.Ticks" />  
  </Capture>  
</Session>';  
```  
  
 次のような、クエリを実行します。  
  
```  
USE ssawPDW;  
GO  
SELECT * FROM dbo.FactFinance;  
```  
  
 次のクエリでは、承認のタイミングが返されます。  
  
```  
SELECT *   
FROM master.sysdiag.PdwOptimizationDiagnostics   
ORDER BY DateTimePublished;  
```  
  
 診断セッションが完了したら、**DROP DIAGNOSTICS** コマンドを使用して削除します。  
  
```  
DROP DIAGNOSTICS SESSION PdwOptimizationDiagnostics;  
```  
  
  
