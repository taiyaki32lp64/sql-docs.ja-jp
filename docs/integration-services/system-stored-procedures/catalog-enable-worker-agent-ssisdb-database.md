---
title: catalog.enable_worker_agent (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c6e5266b-c32d-49ff-aa69-f09664009fb4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8fd9d387d84836ca35c1b0bfb9fd564e2efd4a48
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281024"
---
# <a name="catalogenable_worker_agent-ssisdb-database"></a>catalog.enable_worker_agent (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Scale Out Master でこの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログを操作する場合に Scale Out Worker を有効にします。

## <a name="syntax"></a>構文

```sql
catalog.enable_worker_agent [@WorkerAgentId =] WorkerAgentId
```
## <a name="arguments"></a>引数
[@WorkerAgentId =] *WorkerAgentId* Scale Out Worker のワーカー エージェント ID。 *WorkerAgentId* は **uniqueidentifier** です。

## <a name="example"></a>例
この例では、MachineA で Scale Out Worker を有効にします。

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  

## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ 

## <a name="errors-and-warnings"></a>エラーおよび警告
ワーカー エージェント ID が無効の場合、ストアド プロシージャによってエラーが返されます。
