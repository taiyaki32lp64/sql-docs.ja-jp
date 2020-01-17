---
title: 配信拡張機能の概要 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- subscriptions [Reporting Services], delivery extensions
- delivery extensions [Reporting Services], about extensions
ms.assetid: a30600a9-bbed-4519-9426-3470ff2982e7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5bbc5e58b95ffb4eebc5dfa0400a566868ae5cba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63165213"
---
# <a name="delivery-extensions-overview"></a>配信拡張機能の概要
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] により、ユーザーはレポートを作成し、パブリッシュできます。レポートは、作成しパブリッシュした後、さまざまな場所に配信できます。 さらに、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] には配信拡張機能と配信 API も用意されています。開発者は別の配信拡張機能を作成し、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の配信機能をさらに拡張することもできます。  
  
 次の表は、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] が備えている配信拡張機能を示しています。  
  
|配信拡張機能|説明|  
|------------------------|-----------------|  
|レポート サーバーの電子メール|SMTP サーバーを使用して個々のユーザーまたはグループに電子メールでレポートを送信します。|  
|レポート サーバーのファイル共有|組織内のレポートをネットワーク ファイル共有に配布するときに使用します。 指定したスケジュールでファイル共有にレポートを自動的にコピーできます。|  
  
 ![Reporting Services の配信拡張機能アーキテクチャ](../../media/bk-reportservicedelivery.gif "Reporting Services の配信拡張機能アーキテクチャ")  
Reporting Services の配信拡張機能アーキテクチャ  
  
 配信拡張機能はサブスクリプションと対になっています。 ユーザーはサブスクリプションを作成するとき、レポートの配信方法を決定するために、利用可能な配信拡張機能の 1 つを選択できます。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、サブスクリプションはレポート サーバー データベースに置かれます。 イベントが発生すると、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] はレポート サーバー データベースにあるサブスクリプションとイベントを照合します。 イベントに関連付けられたサブスクリプションごとに、レポート サーバーは通知を作成します。 データ ドリブン サブスクリプションの場合、受信者ごとに通知が作成されます。 通知が作成されると、レポート サーバーでは特定の配信拡張機能を呼び出し、通知に指定された拡張機能設定の値を渡します。 配信拡張機能は、選択された配信拡張機能により指定されたユーザーに通知を送信します。  
  
 配信拡張機能では、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配信拡張機能 API を実装します。 配信拡張機能では、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配信拡張機能 API をサポートすることで、レポート サーバーから通知を受信し、通知のステータスを提供することができます。  
  
 レポート サーバーでは、通知とレポートの配信先を管理しません。 配信先情報の収集は、配信拡張機能に記述するコードで実行されます。  
  
## <a name="subscriptions-and-delivery-extensions"></a>サブスクリプションと配信拡張機能  
 クライアント アプリケーションでは、レポート サーバー Web サービスの 2 つのメソッド <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> および <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A> を使用して、配信拡張機能を使用するサブスクリプションを作成します。 既存のサブスクリプションを変更する場合は、<xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> および <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A> メソッドを使用します。 ユーザーは、サブスクリプションを作成するとき、サブスクリプションの配信拡張機能も選択し、必要な拡張機能設定の値を入力します。 ユーザーがサブスクリプションを保存した場合、サブスクリプションはレポート サーバー データベースに格納されます。 サブスクリプションではスケジュールまたはイベントに基づいて通知が作成されます。 配信が始まると、最初に、選択された配信拡張機能が構成ファイルから構成データを読み込みます。 次に、サブスクリプションの拡張機能設定が取得され、値が設定されます。 最後に、<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> メソッドが呼び出され、通知が送信されます。  
  
## <a name="developer-requirements"></a>開発者要件  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配信拡張機能を開発するための条件は次のとおりです。  
  
-   レポート サーバーがインストールされた配置用コンピューター  
  
-   [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] または [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Software Development Kit (SDK) がインストールされた開発用コンピューター。  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 機能、特にサブスクリプション機能と配信機能についてよく理解していること  
  
-   レポート マネージャーに独自のサブスクリプション ユーザー インターフェイスを実装する場合は、[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] および Web コントロールについてよく理解していること  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# や [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET など、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 言語による開発経験があること。  
  
## <a name="see-also"></a>関連項目  
 [配信拡張機能の実装](../delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../reporting-services-extension-library.md)  
  
  
