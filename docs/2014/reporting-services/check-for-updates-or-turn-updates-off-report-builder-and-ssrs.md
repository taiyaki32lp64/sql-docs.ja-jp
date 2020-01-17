---
title: チェックの更新または更新をオフ (レポート ビルダーおよび SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9c69792d-d7c4-453b-ae2f-6d2d071d8606
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 27942be9c32d4537f729adbd69df1c64a9c9ff6f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109871"
---
# <a name="check-for-updates-or-turn-updates-off-report-builder-and-ssrs"></a>更新を確認するまたは更新をオフにする (レポート ビルダーおよび SSRS)
  レポートを開くたびに、レポート ビルダーによって、そのレポートにあるレポート パーツのパブリッシュ済みインスタンスがレポート サーバー、またはレポート サーバーと統合されている SharePoint サイト上で更新されたかどうかが確認されます。 また、データセットやパラメーターなどのレポート パーツの依存アイテムに変更が加えられたかどうかも確認されます。 レポート パーツまたはレポート パーツの依存アイテムがサイトまたはサーバー上で更新されている場合は、レポート内の情報バーに、更新されたパーツの数が表示されます。 更新は、表示して受け入れることも、拒否することもできます。また、情報バーを消去することもできます。  
  
 情報バーを無効にして、レポート パーツのパブリッシュ済みインスタンスの変更に関する情報が表示されないようにすることもできます。 これは、そのユーザーが開くすべてのレポートでこの機能を無効にするためのユーザー設定です。 情報バーを無効にした場合でも、更新を確認できます。  
  
### <a name="to-turn-on-and-off-report-part-updates"></a>レポート パーツ更新のオン/オフを切り替えるには  
  
1.  レポート ビルダーのボタンをクリックして**オプション**します。  
  
2.  **オプション**] ダイアログ ボックスの [、**リソース**タブ、オンまたはオフ、**個人用レポートのレポート パーツへの更新プログラムの表示**チェック ボックスをオンします。  
  
> [!NOTE]  
>  これは、ユーザー設定です。 そのユーザーが開くすべてのレポートで無効になります。  
  
### <a name="to-check-for-updates"></a>更新を確認するには  
  
-   デザイン画面またはレポート本文内のレポートの外側を右クリックし、をクリックして**更新プログラムの確認**します。  
  
## <a name="see-also"></a>参照  
 [レポート パーツ &#40;レポート ビルダーおよび SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [およびレポート パーツを再パブリッシュ&#40;レポート ビルダーおよび SSRS&#41;](report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)   
 [レポート パーツの参照し、既定のフォルダーの設定&#40;レポート ビルダーおよび SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)   
 [レポート パーツのトラブルシューティング&#40;レポート ビルダーおよび SSRS&#41;](../../2014/reporting-services/troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [レポート ビルダーのレポート パーツおよびデータセット](report-data/report-parts-and-datasets-in-report-builder.md)  
  
  
