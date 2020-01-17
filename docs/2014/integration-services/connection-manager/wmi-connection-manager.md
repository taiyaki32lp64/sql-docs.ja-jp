---
title: WMI 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5d57a0783c8af0121169f09622b8e5bd8547d1ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833090"
---
# <a name="wmi-connection-manager"></a>WMI 接続マネージャー
  WMI 接続マネージャーを使用すると、パッケージは Windows Management Instrumentation (WMI) を使用して、企業環境の情報を管理できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれる Web サービス タスクでは、WMI 接続マネージャーを使用します。  
  
 WMI 接続マネージャーをパッケージに追加すると[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]接続マネージャーを実行時に WMI 接続を解決するを接続マネージャーのプロパティを設定し、接続マネージャーを追加作成、`Connections`パッケージのコレクション. 接続マネージャーの `ConnectionManagerType` プロパティは、`WMI` に設定されます。  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>WMI 接続マネージャーの構成  
 WMI 接続マネージャーは、次の方法で構成できます。  
  
-   サーバーの名前を指定します。  
  
-   サーバー上の名前空間を指定します。  
  
-   サーバーに接続する認証モードを選択します。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティについては、「 [[WMI 接続マネージャー エディター]](../wmi-connection-manager-editor.md)」を参照してください。  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」および「 [プログラムによる接続の追加](../building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="see-also"></a>参照  
 [Web サービス タスク](../control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS&#41; の接続](integration-services-ssis-connections.md)  
  
  
