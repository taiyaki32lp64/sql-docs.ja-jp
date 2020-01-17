---
title: MSMQ 接続マネージャー エディター |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msmqconnectionmanager.f1
helpviewer_keywords:
- MSMQ Connection Manager Editor
ms.assetid: ef842cb4-82da-4550-85fe-9bedbc1e77c7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 91b448a87408a830464b50f641e6eefa8cf3f12c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057639"
---
# <a name="msmq-connection-manager-editor"></a>MSMQ 接続マネージャー エディター
  **[MSMQ 接続マネージャー]** ダイアログ ボックスでは、Message Queuing (MSMQ) メッセージ キューへのパスを指定できます。  
  
 MSMQ 接続マネージャーの詳細については、「 [MSMQ Connection Manager](connection-manager/msmq-connection-manager.md)」を参照してください。  
  
> [!NOTE]  
>  MSMQ 接続マネージャーでは、ローカルのパブリック キューと専用キュー、およびリモートのパブリック キューがサポートされています。 リモートの専用キューはサポートされていません。 スクリプト タスクを使用する回避策については、「 [スクリプト タスクによるリモート プライベート メッセージ キューへの送信](control-flow/script-task.md)」を参照してください。  
  
## <a name="options"></a>および  
 **名前**  
 ワークフローにおける MSMQ 接続マネージャーの一意な名前を指定します。 指定された名前は、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーに表示されます。  
  
 **[説明]**  
 接続マネージャーの説明を記述します。 パッケージを自己文書化して目的を明確にし、保守が容易になるように、接続マネージャーの目的について記述することをお勧めします。  
  
 **[パス]**  
 メッセージ キューの完全なパスを入力します。 パスの形式はキューの種類によって異なります。  
  
|[キューの種類]|パスのサンプル|  
|----------------|-----------------|  
|パブリック|\<コンピューター名>\\<キュー名\>|  
|プライベート|\<コンピューター名>\Private$\\<キュー名\>|  
  
 "." を使用してローカル コンピューターを表すことができます。  
  
 **テスト**  
 MSMQ 接続マネージャーを構成した後に、 **[テスト]** をクリックして、接続が利用可能であることを確認します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
