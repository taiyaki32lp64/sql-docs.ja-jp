---
title: catalog.execution_component_phases | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 07a9a163-4787-40f7-b371-ac5c6cb4b095
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9c4580c6b6b4dc6ea0d7ab9bb93f9614b90feb1d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295176"
---
# <a name="catalogexecution_component_phases"></a>catalog.execution_component_phases 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  各実行フェーズでデータ フロー コンポーネントが費やした時間を表示します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|phase_stats_id|**bigint**|フェーズの一意識別子 (ID)。|  
|execution_id|**bigint**|実行のインスタンスの一意の ID。|  
|package_name|**nvarchar(260)**|実行中に開始された最初のパッケージの名前。|  
|task_name|**nvarchar (4000)**|データ フロー タスクの名前。|  
|subcomponent_name|**nvarchar (4000)**|データ フロー コンポーネントの名前。|  
|phase|**nvarchar(128)**|実行フェーズの名前。|  
|start_time|**datetimeoffset(7)**|フェーズの開始時刻。|  
|end_time|**datetimeoffset(7)**|フェーズの終了時刻。|  
|execution_path|**nvarchar(max)**|データ フロー タスクの実行パス。|  
  
## <a name="remarks"></a>Remarks  
 このビューには、Validate、Pre-Execute、Post-Execute、PrimeOutput、ProcessInput など、データ フロー コンポーネントの実行フェーズごとに 1 行表示されます。 各行には、特定の実行フェーズの開始時刻と終了時刻が表示されます。  
  
## <a name="example"></a>例  
 次の例では、catalog.execution_component_phases ビューを使用して、特定のパッケージがすべてのフェーズで実行に費やした時間の合計 (**Verbose**)、およびパッケージの経過時間の合計 (**total_time**) を確認します。  
  
> [!WARNING]  
>  catalog.execution_component_phases ビューでは、パッケージ実行のログ記録レベルが [パフォーマンス] または [詳細] に設定されている場合のみ、この情報が表示されます。 詳細については、「 [SSIS サーバーでのパッケージ実行のログ記録を有効にする](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)」を参照してください。  
  
```sql
use SSISDB  
select package_name, task_name, subcomponent_name, execution_path,  
    SUM(DATEDIFF(ms,start_time,end_time)) as active_time,  
    DATEDIFF(ms,min(start_time), max(end_time)) as total_time  
from catalog.execution_component_phases  
where execution_id = 1841  
group by package_name, task_name, subcomponent_name, execution_path  
order by package_name, task_name, subcomponent_name, execution_path  
```  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  サーバー上で操作を実行する権限がある場合は、操作に関する情報を表示する権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
