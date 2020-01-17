---
title: WMI 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmiconnection.f1
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7b3f33d0c37ba9c856d9cc0b66674c8ca4221e0d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294355"
---
# <a name="wmi-connection-manager"></a>WMI 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  WMI 接続マネージャーを使用すると、パッケージは Windows Management Instrumentation (WMI) を使用して、企業環境の情報を管理できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれる Web サービス タスクでは、WMI 接続マネージャーを使用します。  
  
 WMI 接続マネージャーをパッケージに追加すると、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、実行時に WMI 接続を解決する接続マネージャーを作成し、接続マネージャーのプロパティを設定して、接続マネージャーをパッケージの **Connections** コレクションに追加します。 接続マネージャーの **ConnectionManagerType** プロパティは、 **WMI**に設定されます。  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>WMI 接続マネージャーの構成  
 WMI 接続マネージャーは、次の方法で構成できます。  
  
-   サーバーの名前を指定します。  
  
-   サーバー上の名前空間を指定します。  
  
-   サーバーに接続する認証モードを選択します。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティについては、「 [[WMI 接続マネージャー エディター]](../../integration-services/connection-manager/wmi-connection-manager-editor.md)」を参照してください。  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="wmi-connection-manager-editor"></a>WMI 接続マネージャー エディター
  **[WMI 接続マネージャー]** ダイアログ ボックスを使用すると、サーバーに対する Microsoft Windows Management Instrumentation (WMI) 接続を指定できます。  
  
 WMI 接続マネージャーの詳細については、「 [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 接続マネージャーの一意な名前を指定します。  
  
 **[説明]**  
 接続マネージャーの説明を記述します。 パッケージを自己文書化して目的を明確にし、保守が容易になるように、接続マネージャーの目的について記述することをお勧めします。  
  
 **サーバー名**  
 WMI 接続の対象となるサーバーの名前を指定します。  
  
 **Namespace**  
 WMI 名前空間を指定します。  
  
 **[Windows 認証を使用する]**  
 Windows 認証を使用する場合に選択します。 Windows 認証を使用すると、接続の際にユーザー名とパスワードを入力する必要がなくなります。  
  
 **User name**  
 Windows 認証を使用しない場合、接続に使用するユーザー名を入力する必要があります。  
  
 **パスワード**  
 Windows 認証を使用しない場合、接続に使用するパスワードを入力する必要があります。  
  
 **テスト**  
 接続マネージャーの設定をテストします。  
  
## <a name="see-also"></a>参照  
 [Web サービス タスク](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS&#41; の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
