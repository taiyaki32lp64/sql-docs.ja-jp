---
title: SMO 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.smoconnection.f1
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 87400e2216b51bfab0132f369e452f27447b0572
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294400"
---
# <a name="smo-connection-manager"></a>SMO 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  SMO 接続マネージャーを使用すると、パッケージは、SQL 管理オブジェクト (SMO) サーバーに接続できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれる転送タスクでは、SMO 接続マネージャーを使用します。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを転送するログイン転送タスクでは、SMO 接続マネージャーを使用します。  
  
 SMO 接続マネージャーをパッケージに追加すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、実行時に SMO 接続を解決する接続マネージャーを作成し、接続マネージャーのプロパティを設定し、接続マネージャーをパッケージの **Connections** コレクションに追加します。 接続マネージャーの **ConnectionManagerType** プロパティは、 **SMOServer**に設定されます。  
  
 SMO 接続マネージャーは、次の方法で構成できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているサーバーの名前を指定します。  
  
-   サーバーに接続する認証モードを選択します。  
  
## <a name="configuration-of-the-smo-connection-manager"></a>SMO 接続マネージャーの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、「 [SMO 接続マネージャー エディター](../../integration-services/connection-manager/smo-connection-manager-editor.md)」を参照してください。  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="smo-connection-manager-editor"></a>SMO 接続マネージャー エディター
  **[SMO 接続マネージャー エディター]** を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトを転送するさまざまなタスクで使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続を構成します。  
  
 SMO 接続マネージャーの詳細については、「 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **サーバー名**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前を入力するか、サーバーを一覧から選択します。  
  
 **[更新]**  
 ネットワークで検出できる利用可能な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの一覧を更新します。  
  
 **[Windows 認証を使用する]**  
 Windows 認証を使用して、選択されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。  
  
 **[SQL Server 認証を使用する]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して、選択されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。  
  
 **User name**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を選択している場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー名を入力します。  
  
 **パスワード**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を選択している場合は、パスワードを入力します。  
  
 **[接続テスト]**  
 構成されたとおりに接続をテストします。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
