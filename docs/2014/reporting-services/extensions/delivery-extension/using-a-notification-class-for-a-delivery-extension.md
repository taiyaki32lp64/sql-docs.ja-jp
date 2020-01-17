---
title: 配信拡張機能での Notification クラスの使用 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], notifications
- notifications [Reporting Services]
- retry queues
- Nofication class
ms.assetid: 549c40c4-d33d-46c2-9d6a-7bbb671ac67a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: db6467b21f84a80bb14a5e6ccad30e16d7cfb584
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63180388"
---
# <a name="using-a-notification-class-for-a-delivery-extension"></a>配信拡張機能での Notification クラスの使用
  <xref:Microsoft.ReportingServices.Interfaces.Notification> クラスは <xref:Microsoft.ReportingServices.Interfaces> 名前空間にあり、配信拡張機能がレポートの配信に使用するサブスクリプション情報を表します。 <xref:Microsoft.ReportingServices.Interfaces.Notification> クラスには、配信するレポートの表示、通知の状態の決定、およびユーザー データの設定に使用できる多数のプロパティが用意されています。  
  
 ![レポート通知のプロセス](../../media/bk-ext-03.gif "レポート通知のプロセス")  
notification は、配信の中心的なオブジェクトです。  
  
 カスタム配信拡張機能を使用するサブスクリプションに関連付けられたイベントが起動すると、<xref:Microsoft.ReportingServices.Interfaces.Report> オブジェクトを含む通知が作成されます。 <xref:Microsoft.ReportingServices.Interfaces.Report> オブジェクトは、特定のレポートをサポートされている表示形式で表示するための機能をカプセル化します。また、このオブジェクトには、サーバー上のレポートの URL やレポート名など、レポート関連のプロパティが含まれます。 <xref:Microsoft.ReportingServices.Interfaces.Report> クラスの詳細については、「[配信拡張機能での Report クラスの使用](../delivery-extension/using-the-report-class-for-a-delivery-extension.md)」を参照してください。  
  
 <xref:Microsoft.ReportingServices.Interfaces.Notification> オブジェクトは、表示拡張機能の <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> メソッドに渡します。 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> メソッドに、通知を処理してレポートを配信するためのコードが含まれている必要があります。  
  
 <xref:Microsoft.ReportingServices.Interfaces.Notification> クラスの使用例については、「[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)」 (SQL Server Reporting Services 製品サンプル) を参照してください。  
  
## <a name="retry-functionality"></a>再試行機能  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、すぐに配信できない通知に対する再試行キューを作成できます。 レポート サーバーが配信拡張機能の <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> メソッドを呼び出した後、配信拡張機能はレポート サーバーが後で配信を再試行するように要求できます。 この場合、レポート サーバーは通知を内部キューに配置し、特定の時間が経過した後に配信を再試行します。 管理者は、**MaxNumberOfRetries** XML 要素と **PeriodBetweenRetries** XML 要素を使用して、RSReportServer.config ファイルの配信拡張機能セクションに、レポート サーバーが実行する再試行回数の最大数と再試行の間隔を構成できます。 後の配信が成功するか、再試行の最大回数に達すると、通知が再試行キューから削除されます。 再試行の最大回数後に配信が失敗すると、通知が破棄されます。  
  
## <a name="see-also"></a>関連項目  
 [配信拡張機能の実装](../delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../reporting-services-extension-library.md)  
  
  
