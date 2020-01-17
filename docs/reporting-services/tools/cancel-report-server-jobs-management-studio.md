---
title: '[レポート サーバー ジョブのキャンセル] (Management Studio) | Microsoft Docs'
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.cancelreportserverjobs.f1
ms.assetid: 1c5b4975-49e9-4d0b-b298-2638e81edbfd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8c433b8fcc0d768b3db48edf8bc56bed6440839a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574218"
---
# <a name="cancel-report-server-jobs-management-studio"></a>[レポート サーバー ジョブのキャンセル] (Management Studio)
  実行中のレポートの表示や実行のキャンセルを行うには、 **[レポート サーバー ジョブのキャンセル]** ダイアログ ボックスを使用します。 このダイアログ ボックスには、レポート サーバーで現在実行中のすべてのジョブが表示されます。 現在処理中のジョブを一時停止または再開することはできませんが、すべてのジョブ、または時間がかかりすぎて完了できない場合は個々のジョブをキャンセルできます。  
  
 ユーザー ジョブとシステム ジョブをキャンセルできます。  
  
-   ユーザー ジョブは、各ユーザーによって開始される任意のジョブです。 このジョブには、要求時のレポートの実行、レポート履歴スナップショットの手動作成、またはレポート実行スナップショットの手動作成が含まれます。 実行中の標準サブスクリプションも、ユーザー ジョブです。  
  
-   システム ジョブは、レポート サーバーで開始されるジョブです。 システム ジョブには、スケジュールされたレポート処理が含まれます。  
  
 このページを開くには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を起動してレポート サーバーに接続し、 **[ジョブ]** を右クリックして **[すべてのジョブのキャンセル]** をクリックします。 または、 **[ジョブ]** を開き、レポート サーバーで実行中のジョブを右クリックして、 **[ジョブのキャンセル]** をクリックします。  
  
 ジョブを取り消す前に、そのプロパティを表示し、ジョブがいつ開始されたかを確認します。 詳細については、「[ジョブのプロパティ &#40;Management Studio&#41;](../../reporting-services/tools/job-properties-management-studio.md)」を参照してください。  
  
> [!NOTE]  
>  この機能は、 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services ではサポートされません。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]を実行している場合、このページは表示されません。  
  
## <a name="options"></a>オプション  
 **[名前]**  
 レポートの名前が表示されます。 サブスクリプションは、説明で識別されます。  
  
 **型**  
 有効な値は、 **[ユーザー]** または **[システム]** です。  
  
 **Start Time**  
 ジョブの開始時刻が表示されます。  
  
 **[ユーザー名]**  
 ユーザーによって開始されたジョブの場合、この列には処理を開始したユーザーの名前が表示されます。  
  
 **ステータス**  
 ジョブの状態が表示されます。 有効な値は、 **[新規]** および **[実行中]** です。 ジョブの開始時の状態は常に **[新規]** です。 60 秒後に、状態は **[実行中]** に変わります。 変更を確認するには、ページを更新する必要があります。  
  
 **[OK]**  
 1 つのジョブまたは複数のジョブを取り消します。 ジョブはすぐに取り消され、再開することはできません。 誤ってジョブを取り消した場合は、レポートまたはサブスクリプションを再度要求して新しいジョブを開始する必要があります。  
  
## <a name="see-also"></a>参照  
 [Management Studio のレポート サーバーの F1 ヘルプ](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Management Studio でレポート サーバーに接続する](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [実行中の処理を管理する](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
