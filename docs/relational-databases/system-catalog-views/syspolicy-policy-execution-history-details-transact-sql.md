---
title: syspolicy_policy_execution_history_details (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_execution_history_details
- syspolicy_policy_execution_history_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_execution_history_details view
ms.assetid: 97ef6573-5e8b-4ba5-8ae0-7901e79a9683
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c2d0daf21a479bff171f31beb30e9dc188a9c97b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094829"
---
# <a name="syspolicypolicyexecutionhistorydetails-transact-sql"></a>syspolicy_policy_execution_history_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  実行された条件式が表示されます、式のターゲット、実行するたび、および存在する場合のエラーの詳細の結果が発生しました。 次の表では、syspolicy_execution_history_details ビューの列について説明します。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|detail_id|**bigint**|このレコードの識別子。 各レコードでは、評価したり、ポリシー内の 1 つの条件式を強制する試行を表します。 複数の対象に適用された場合、条件ごと、対象ごとに明細レコードが作成されます。|  
|history_id|**bigint**|履歴イベントの識別子。 各履歴イベントは、ポリシーを実行する試行が 1 回を表します。 条件には複数の条件式や複数の対象が含まれる場合があるため、1 つの history_id に対して複数の詳細レコードが作成されることもあります。 このビューに参加するには history_id 列を使用して、 [syspolicy_policy_execution_history](../../relational-databases/system-catalog-views/syspolicy-policy-execution-history-transact-sql.md)ビュー。|  
|target_query_expression|**nvarchar(max)**|ポリシーおよび syspolicy_policy_execution_history ビューの対象。|  
|execution_date|**datetime**|この詳細レコードが作成された日時。|  
|結果|**bit**|この対象と条件式の評価が成功したか失敗したかを表します。<br /><br /> 0 (成功) または 1 (失敗)。|  
|result_detail|**nvarchar(max)**|結果メッセージ。 ファセットによって提供される場合にのみ使用できます。|  
|exception_message|**nvarchar(max)**|1 つの場合、例外によって生成されたメッセージが発生しました。|  
|exception|**nvarchar(max)**|いずれかが発生した場合、例外の説明です。|  
  
## <a name="remarks"></a>コメント  
 ポリシー ベースの管理のトラブルシューティングを行う場合に、失敗した対象と条件式の組み合わせ、失敗した日時、および関連するエラーを調べるには、syspolicy_policy_execution_history_details ビューに対してクエリを実行します。  
  
 次のクエリの結合、`syspolicy_policy_execution_history_details`を見る、`syspolicy_policy_execution_history_details`と`syspolicy_policies`条件の名前は、ポリシーの名前を表示するビューし、エラーの詳細。  
  
```  
SELECT Pol.name AS Policy,   
Cond.name AS Condition,   
PolHistDet.target_query_expression,   
PolHistDet.execution_date,   
PolHistDet.result,   
PolHistDet.result_detail,   
PolHistDet.exception_message,   
PolHistDet.exception   
FROM msdb.dbo.syspolicy_policies AS Pol  
JOIN msdb.dbo.syspolicy_conditions AS Cond  
    ON Pol.condition_id = Cond.condition_id  
JOIN msdb.dbo.syspolicy_policy_execution_history AS PolHist  
    ON Pol.policy_id = PolHist.policy_id  
JOIN msdb.dbo.syspolicy_policy_execution_history_details AS PolHistDet  
    ON PolHist.history_id = PolHistDet.history_id  
WHERE PolHistDet.result = 0 ;  
```  
  
## <a name="permissions"></a>アクセス許可  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>関連項目  
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [ポリシーベースの管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
