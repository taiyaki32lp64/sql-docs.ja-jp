---
title: レポート サーバー Windows サービス (MSSQLServer) 107 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- MSSQLServer 107 error
ms.assetid: 52b5704b-27f9-400a-a821-d8fa0786afe4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0133ef77db176910c33ae8e78174cb5c3e507c3c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65575545"
---
# <a name="report-server-windows-service-mssqlserver-107"></a>レポート サーバー Windows サービス (MSSQLServer) 107
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|107|  
|イベント ソース|レポート サーバー Windows サービス|  
|コンポーネント|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|メッセージ テキスト|レポート サーバー Windows サービス (MSSQLSERVER) はレポート サーバー データベースに接続できません。|  
  
## <a name="explanation"></a>説明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レポート サーバー サービスは、レポート サーバー データベースに接続できません。 このエラーは、サービスの再起動中、レポート サーバー データベースへの接続を確立できない場合に発生します。 このエラーは、次のような状況で発生します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスが実行されていない場合。  
  
-   リモート接続または TCP/IP プロトコルが無効になっているため、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスへの接続に失敗する場合。  
  
-   レポート サーバー データベースが正しく構成されていない場合。  
  
-   サービス アカウントが正しく構成されていないか、レポート サーバー データベースに対する権限がアカウントにない場合。 この状況は、アカウントやレポート サーバー データベースの設定に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用しない場合に発生することがあります。  
  
## <a name="user-action"></a>ユーザーの操作  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスが実行されていない場合はこのサービスを開始し、TCP/IP プロトコルでのリモート接続が有効になっていることを確認します。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用して、レポート サーバー データベースとサービス アカウントを構成します。  
  
## <a name="internal-only"></a>内部使用のみ  
  
## <a name="see-also"></a>参照  
 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Start and Stop the Report Server Service](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
