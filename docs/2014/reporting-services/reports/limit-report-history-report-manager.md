---
title: レポート履歴を制限する (レポート マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fd493fae67e3aa47c5c53cd3ad12d018b0b72f70
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102639"
---
# <a name="limit-report-history-report-manager"></a>レポート履歴を制限する (レポート マネージャー)
  レポート履歴とは、時間の経過と共に作成されるレポート スナップショットの集まりです。 レポート履歴は必要時に作成できるほか、どの程度の頻度でスナップショットを作成し、レポート履歴に追加するかをスケジュールで設定することもできます。  
  
 レポート履歴は、レポート サーバー データベースに格納されます。 レポート スナップショットに大量のデータが含まれている場合は、スナップショットを保持することによるデータベース サイズへの影響を最小限に抑えるために、レポート履歴を制限することを検討する必要があります。  
  
### <a name="to-configure-report-history-for-a-report-server"></a>レポート サーバーのレポート履歴を構成するには  
  
1.  レポート マネージャーのグローバル ツール バーで、 **[サイトの設定]** をクリックします。  
  
2.  すべてのレポート履歴を制限なく保持する場合は、 **[レポート履歴に無制限の数のスナップショットを保持する]** を選択します。 それ以外の場合は、 **[レポート履歴のコピーの数を制限する]** を選択し、特定のレポートに対して保持できるスナップショットの最大数を指定します。  
  
3.  **[適用]** をクリックします。  
  
### <a name="to-configure-report-history-for-a-specific-report"></a>特定のレポートのレポート履歴を構成するには  
  
1.  レポート マネージャーで、履歴を構成するレポートに移動し、そのレポートをクリックして開きます。  
  
2.  **[プロパティ]** タブをクリックします。  
  
3.  **[履歴]** タブをクリックします。  
  
4.  レポートのオプションを選択し、 **[適用]** をクリックします。 各オプションに関する詳細については、「[[スナップショット オプション] プロパティ ページ &#40;レポート マネージャー&#41;](../snapshot-options-properties-page-report-manager.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [レポート履歴へのスナップショットの追加 &#40;レポート マネージャー&#41;](../report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../report-manager-ssrs-native-mode.md)  
  
  
