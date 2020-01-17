---
title: '[スケジュールのプロパティ] ([レポート] ページ) | Microsoft Docs'
ms.date: 06/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.scheduleproperties.reports.f1
ms.assetid: 7db728bd-4b08-43ef-a49a-e8dcdd37cf89
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0e8441dec655398ec530bc95049a339edd9e01ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571405"
---
# <a name="schedule-properties-reports-page"></a>[スケジュールのプロパティ] ([レポート] ページ)
  特定の共有スケジュールを使用するすべてのレポートの一覧を見るには、 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] スケジュール プロパティを使用します。 スケジュールを使用して、レポート スナップショットの更新、レポート履歴の生成、サブスクリプションのトリガー、またはレポートのキャッシュされたコピーの期限の終了を実行できます。 スケジュールがどのように使用されているかを確認するには、レポートのプロパティおよびサブスクリプション情報を参照します。  
  
 このページには共有スケジュールを使用する各レポートが表示されますが、1 つのレポート内で共有スケジュールが何回使用されるかについては示されません。 たとえば、Company Sales レポートの 20 の異なるサブスクライバーがすべて同じ共有スケジュールを使用してサブスクリプション処理を開始するとします。 この場合、Company Sales レポートでは共有スケジュールの参照が 20 回行われますが、この一覧には 1 回しか表示されません。  
  
 スケジュール プロパティ ページを開くには:
 1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を起動します。
 2. レポート サーバーに接続します。
 3. **[共有スケジュール]** フォルダーを開きます。
 4. 共有スケジュールを右クリックし、 **[プロパティ]** を選択します。
 5. **[レポート]** をクリックします。  
  
  **Web ポータルの** [サイトの設定] [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] から共有スケジュールを管理することもできます。
  
> [!NOTE]  
>  この機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、「[SQL Server 2017 の各エディションとサポートされている機能](../../sql-server/editions-and-components-of-sql-server-2017.md)」をご覧ください。  
  
## <a name="options"></a>オプション  
 **フォルダー**  
 レポートのパスを指定します。  
  
 **レポート**  
 スケジュールを使用するレポートの名前を指定します。  
  
## <a name="see-also"></a>参照  
 [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [スケジュール](../../reporting-services/subscriptions/schedules.md)   
 [Management Studio のレポート サーバーの F1 ヘルプ](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Management Studio でレポート サーバーに接続する](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [レポートの全般プロパティを構成する (レポート マネージャー)](https://msdn.microsoft.com/10b941b2-28e6-4408-9ee4-acebc63c8496)  
  
  

