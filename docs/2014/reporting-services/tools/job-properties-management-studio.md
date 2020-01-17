---
title: '[ジョブのプロパティ] (Management Studio) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.jobproperties.f1
ms.assetid: 807ffd0e-9363-4f8f-9c36-c5d746ad19fd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f00250011f3c325ca39c3c040e5252b804182d86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100222"
---
# <a name="job-properties-management-studio"></a>[ジョブのプロパティ]\(Management Studio)
  **[ジョブのプロパティ]** ページを使用して、進行中のレポートまたはサブスクリプションを取り消す前にそれらの情報を表示できます。  
  
 このページを開くには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を起動して、レポート サーバーに接続し、 **[ジョブ]** フォルダーを開きます。 実行中のジョブを右クリックし、 **[プロパティ]** をクリックします。  
  
> [!NOTE]  
>  この機能は、 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services ではサポートされません。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]を実行している場合、このページは表示されません。  
  
## <a name="tasks"></a>処理手順  
 ジョブに関する情報を表示する前に、ページを更新してレポート サーバーで現在実行されているジョブに関する情報を取得します。  
  
1.  レポート サーバーのフォルダーを開きます。  
  
2.  **[ジョブ]** を右クリックし、 **[更新]** をクリックします。  
  
3.  ジョブが表示されたら、ジョブを右クリックして、 **[プロパティ]** をクリックします。  
  
## <a name="options"></a>および  
 **[ジョブ ID]**  
 処理中にジョブに割り当てられる GUID。 この値は、レポートまたはサブスクリプションが実行されるたびにランダムに生成されます。  
  
 **[ジョブの状態]**  
 有効な値は、 **[新規]** および **[実行中]** です。 ジョブの開始時の状態は常に **[新規]** です。 60 秒後に、状態は **[実行中]** に変わります。 変更を確認するには、ページを更新する必要があります。  
  
 **ジョブの種類**  
 有効な値は、 **[ユーザー]** および **[システム]** です。 ユーザー ジョブは、各ユーザーによって開始される任意のジョブです。 このジョブには、要求時のレポートの実行、レポート履歴スナップショットの手動生成、またはレポート実行スナップショットの手動作成が含まれます。 実行中の標準サブスクリプションも、ユーザー ジョブです。 システム ジョブは、レポート サーバーで開始されるジョブです。 システム ジョブには、スケジュールでトリガーされるレポートの処理が含まれます。  
  
 **ジョブの操作**  
 レポートの場合、この列には実行中のレポート実行処理が表示されます。 この値は常に **[表示]** です。  
  
 **[ジョブの説明]**  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、既定ではジョブの説明は表示されません。  
  
 **[サーバー名]**  
 ジョブを処理しているレポート サーバーの名前が表示されます。 スケールアウト配置を構成している場合、この値にはジョブを処理しているサーバーが表示されます。  
  
 **[レポート名]**  
 レポートの名前が表示されます。 サブスクリプションは、説明で識別されます。  
  
 **[レポートのパス]**  
 レポート サーバー フォルダー階層のレポートのパスが表示されます。  
  
 **Start Time**  
 処理の開始時刻が表示されます。  
  
 **[ユーザー名]**  
 ユーザーによって開始された処理の場合、この列には処理を開始したユーザーの名前が表示されます。 システム ジョブの場合は、レポート サーバーの名前になります。  
  
## <a name="see-also"></a>参照  
 [Management Studio のレポート サーバーの F1 ヘルプ](report-server-in-management-studio-f1-help.md)   
 [Management Studio でレポート サーバーに接続する](connect-to-a-report-server-in-management-studio.md)   
 [実行中の処理を管理する](../subscriptions/manage-a-running-process.md)  
  
  
