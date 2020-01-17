---
title: ネイティブモードのレポートサーバーへの接続 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.connectiondialog.F1
helpviewer_keywords:
- report servers [Reporting Services], configuring
ms.assetid: 8b9ea8d3-827c-4011-9e02-be2eac3bb364
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5bf32c8427679b342bee89d6541b051beed2e8ce
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952290"
---
# <a name="connect-to-a-native-mode-report-server"></a>ネイティブ モードのレポート サーバーへの接続
  このダイアログ ボックスを使用すると、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のローカルまたはリモートの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバー インスタンスに接続できます。 このツールを使用して、以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーに接続することはできません。 一度に接続できるインスタンスは 1 つだけです。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードを構成および管理するために、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーは使用しません。 SharePoint モードでレポート サーバーを構成するには、SharePoint サーバーの全体管理と PowerShell スクリプトを使用します。 詳細については、「 [SharePoint 2010 用 Reporting Services の SharePoint モードのインストール](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)」を参照してください。  
  
> [!TIP]  
>  @ No__t-0 Configuration Manager (RSConfigTool .exe) は、"highestAvailable" の特権レベルでインストールされます。 この動作は仕様による結果です。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI API と通信する必要があります。 一部の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 通信には、高いレベルまたは管理者の特権が必要です。  
  
-   ローカル レポート サーバー インスタンスに接続するには、既定値を使用して **[接続]** をクリックします。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーにより、ローカル サーバー名が提供され、既定のインスタンスが検出されます。 ほとんどの場合、値を変更せずに **[接続]** をクリックできます。 複数のインスタンスがインストールされている場合は、使用するインスタンスを選択する必要があります。  
  
-   リモート レポート サーバー インスタンスに接続するには、サーバー名を入力して **[検索]** をクリックします。次に、インスタンスを選択して **[接続]** をクリックします。  
  
 このダイアログ ボックスを開くには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを起動します。 このダイアログ ボックスは、ツールを起動すると直ちに表示されます。 詳細については、「 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[サーバー名]**  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] がインストールされているコンピューターのネットワーク名を入力します。 プレフィックスやスラッシュを含めずに、コンピューター名だけを入力してください。  
  
 **探す**  
 **[サーバー名]** で指定したコンピューターを検索します。  
  
 **レポートサーバーインスタンス**  
 複数のレポート サーバー インスタンスをインストールしている場合は、接続先のインスタンスを選択します。 選択できるのは有効なインスタンスだけです。 以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスをサイド バイ サイドで実行している場合は、一覧にインスタンスが表示されません。  
  
 **Connect**  
 指定したサーバーおよびインスタンスに接続します。  
  
## <a name="see-also"></a>関連項目  
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
