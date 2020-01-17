---
title: ジョブ転送タスク エディター ([全般] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferjobstask.general.f1
helpviewer_keywords:
- Transfer Jobs Task Editor
ms.assetid: 96531920-92d4-4a3b-a38a-6f0c8bc78ada
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f8f8c9fd4f0a7f377640b99ac0bc7831c3f43de3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055009"
---
# <a name="transfer-jobs-task-editor-general-page"></a>[ジョブ転送タスク エディター] ([全般] ページ)
  **[ジョブ転送タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、ジョブ転送タスクの名前と説明を入力できます。 ジョブ転送タスクの詳細については、「 [Transfer Jobs Task](control-flow/transfer-jobs-task.md)」を参照してください。  
  
> [!NOTE]  
>  転送先サーバー上の **sysadmin** 固定サーバー ロールのメンバー、または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント固定データベース ロールのうち 1 つのロールのメンバーだけが、転送先にジョブを正常に作成できます。 転送元サーバー上のジョブにアクセスするには、ユーザーは少なくとも転送元サーバー上で **SQLAgentUserRole** 固定データベース ロールのメンバーである必要があります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント固定データベース ロールおよびその権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
## <a name="options"></a>および  
 **名前**  
 ジョブ転送タスクの一意な名前を入力します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 ジョブ転送タスクの説明を入力します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services タスク](control-flow/integration-services-tasks.md)   
 [[ジョブ転送タスク エディター] &#40;[ジョブ] ページ&#41;](../../2014/integration-services/transfer-jobs-task-editor-jobs-page.md)   
 [[式] ページ](expressions/expressions-page.md)  
  
  
