---
title: タスク ホスト コンテナー | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.taskhostcontainer.f1
helpviewer_keywords:
- containers [Integration Services], Task Host
- Task Host container
ms.assetid: 7394a2c2-1b07-427d-b94a-9792e7783d35
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e6286bb35855d0bf775925c93003ae59996ab447
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293894"
---
# <a name="task-host-container"></a>タスク ホスト コンテナー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  タスク ホスト コンテナーは、1 つのタスクをカプセル化します。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、タスク ホストは個別には構成されず、カプセル化するタスクのプロパティを設定する際に構成されます。 タスク ホスト コンテナーがカプセル化するタスクの詳細については、「 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)」を参照してください。  
  
 タスク ホスト コンテナーは、変数とイベント ハンドラーの使用を、タスク レベルに拡張します。 詳細については、「[Integration Services (SSIS) のイベント ハンドラー](../../integration-services/integration-services-ssis-event-handlers.md)」および「[Integration Services (SSIS) の変数](../../integration-services/integration-services-ssis-variables.md)」を参照してください。  
  
## <a name="configuration-of-the-task-host"></a>タスク ホストの構成  
 プロパティは、 **の** [プロパティ] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ウィンドウで設定することも、プログラムで設定することもできます。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でのこれらのプロパティの設定については、「 [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)」を参照してください。  
  
 これらのプロパティのプログラムでの設定については、「 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>参照  
 [Integration Services コンテナー](../../integration-services/control-flow/integration-services-containers.md)  
  
  
