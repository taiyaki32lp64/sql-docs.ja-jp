---
title: タスク ホスト コンテナー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.taskhostcontainer.f1
helpviewer_keywords:
- containers [Integration Services], Task Host
- Task Host container
ms.assetid: 7394a2c2-1b07-427d-b94a-9792e7783d35
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9d5c965f4012244a3ccc2eb80470205e8d55e887
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62830085"
---
# <a name="task-host-container"></a>タスク ホスト コンテナー
  タスク ホスト コンテナーは、1 つのタスクをカプセル化します。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、タスク ホストは個別には構成されず、カプセル化するタスクのプロパティを設定する際に構成されます。 タスク ホスト コンテナーがカプセル化するタスクの詳細については、「 [Integration Services タスク](integration-services-tasks.md)」を参照してください。  
  
 タスク ホスト コンテナーは、変数とイベント ハンドラーの使用を、タスク レベルに拡張します。 詳細については、「[Integration Services (SSIS) のイベント ハンドラー](../integration-services-ssis-event-handlers.md)」および「[Integration Services (SSIS) の変数](../integration-services-ssis-variables.md)」を参照してください。  
  
## <a name="configuration-of-the-task-host"></a>タスク ホストの構成  
 プロパティは、 **の** [プロパティ] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ウィンドウで設定することも、プログラムで設定することもできます。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でのこれらのプロパティの設定については、「 [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)」を参照してください。  
  
 これらのプロパティのプログラムでの設定については、「 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>参照  
 [Integration Services コンテナー](integration-services-containers.md)  
  
  
