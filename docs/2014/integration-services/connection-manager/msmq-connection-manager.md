---
title: MSMQ 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 78377fe5eaf5b9f0639533f17fa7a45cca69a537
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833661"
---
# <a name="msmq-connection-manager"></a>MSMQ 接続マネージャー
  MSMQ 接続マネージャーを使用すると、Message Queuing (MSMQ) を使用するメッセージ キューにパッケージが接続できるようになります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれるメッセージ キュー タスクでは、MSMQ 接続マネージャーを使用します。  
  
 MSMQ 接続マネージャーをパッケージに追加すると、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、実行時に MSMQ 接続を解決する接続マネージャーを作成し、接続マネージャーのプロパティを設定し、接続マネージャーをパッケージの `Connections` コレクションに追加します。 接続マネージャーの `ConnectionManagerType` プロパティは、`MSMQ` に設定されます。  
  
 MSMQ 接続マネージャーは、次の方法で構成できます。  
  
-   接続文字列を指定します。  
  
-   接続するメッセージ キューのパスを指定します。  
  
 次の表に示すように、パスの形式はキューの種類によって異なります。  
  
|[キューの種類]|パスのサンプル|  
|----------------|-----------------|  
|パブリック|\<コンピューター名>\\<キュー名\>|  
|プライベート|\<コンピューター名>\Private$\\<キュー名\>|  
  
 ピリオド (.) を使用してローカル コンピューターを表すことができます。  
  
## <a name="configuration-of-the-msmq-connection-manager"></a>MSMQ 接続マネージャーの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、「 [MSMQ 接続マネージャー エディター](../msmq-connection-manager-editor.md)」を参照してください。  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="see-also"></a>参照  
 [メッセージ キュー タスク](../control-flow/message-queue-task.md)   
 [Integration Services &#40;SSIS&#41; の接続](integration-services-ssis-connections.md)  
  
  
