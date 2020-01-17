---
title: catalog.worker_agents (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f2678853d13436811b53b40473a04191625535db
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295143"
---
# <a name="catalogworker_agents-ssisdb-database"></a>catalog.worker_agents (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker の情報を表示します。

|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|Scale Out Worker の worker エージェント ID。|
|IsEnabled|**bit**|Scale Out Worker が有効になっているかどうか。|
|DisplayName|**nvarchar (256)**|Scale Out Worker の表示名。|
|[説明]|**nvarchar (256)**|Scale Out Worker の説明。|
|MachineName|**nvarchar (256)**|Scale Out Worker のコンピューター名。|
|Tags|**nvarchar(max)**|Scale Out Worker のタグ。|
|UserAccount|**nvarchar (256)**|Scale Out Worker サービスを実行するユーザー アカウント。|
|LastOnlineTime|**datetimeoffset(7)**|最後に Scale Out Worker がオンラインになった日時。|

## <a name="remarks"></a>Remarks
このビューには、SSISDB カタログと連動している Scale Out Master に接続している各 Scale Out Worker の行が表示されます。

## <a name="permissions"></a>アクセス許可
このビューには、次の権限のいずれかが必要です。

- **ssis_admin** データベース ロールのメンバーシップ

- **ssis_cluster_executor** データベース ロールのメンバーシップ

- **sysadmin** サーバー ロールのメンバーシップ
