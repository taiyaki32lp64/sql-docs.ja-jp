---
title: Microsoft レプリケーション インタラクティブ競合回避モジュール | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replconflictviewer.interactiveresolver.f1
ms.assetid: d3d4a480-782b-4b1d-b839-565c8cf6cb24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68ddc4f6b42dcc53445b8afaae0bc15e666a5711
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667284"
---
# <a name="microsoft-replication-interactive-conflict-resolver"></a>Microsoft レプリケーション インタラクティブ競合回避モジュール
  インタラクティブ競合回避モジュールは、Windows 同期マネージャーを使用して同期が行われるマージ サブスクリプションに使用することができます。 これにより、データ競合に対する結果の表示、比較、編集、および選択ができます。 レプリケーションには、コミットされた後で競合結果の表示および修正を行うことができる競合表示モジュールも含まれます。 インタラクティブ競合回避モジュールを使用すると、同期中に結果を選択することができます。  
  
> [!NOTE]  
>  論理レコードに関連する競合は、インタラクティブ競合回避モジュールには表示されません。 これらの競合に関する情報を表示するには、レプリケーション ストアド プロシージャを使用します。 詳細については、「[マージ パブリケーションの競合情報の表示 (レプリケーション Transact-SQL プログラミング)](view-conflict-information-for-merge-publications.md)」を参照してください。  
  
## <a name="options"></a>および  
 **列名**  
 テーブルのすべての列の名前です。 1 つまたは複数の列が競合するデータを持つ場合があります。 どの列が競合するかにかかわらず、競合で優先された行全体が、優先されなかった行全体を上書きします。  
  
 **[提案された解決策]**  
 アーティクルの競合回避モジュールによって提案された解決策です。  
  
 **パブリッシャー**  
 パブリッシャーでのデータ値です。  
  
 **サブスクライバー (Subscriber)**  
 サブスクライバーでのデータ値です。  
  
 **[推奨設定を優先]** 、 **[パブリッシャーを優先]** 、 **[サブスクライバーを優先]**  
 パブリッシャーまたはサブスクライバーのどちらが競合に優先されなかったかによって、どちらかが適用される行を受け入れます。 パブリッシャーが競合に優先されなかった場合、その他のすべてのサブスクライバーは、次にパブリッシャーと同期される際に、競合に優先される行を受け取ります。  
  
 **[残りの競合を自動的に解決]**  
 アーティクルの競合回避モジュールによって提案された解決策を使用して、残りの競合を解決します。  
  
 **[参照用にこの競合の詳細をログに記録する]**  
 システム テーブルでの競合の詳細をログに記録します。  
  
## <a name="see-also"></a>関連項目  
 [インタラクティブな競合解決](merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [マージ パブリケーションでのデータの競合の表示および解決 &#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Windows 同期マネージャーを使用したサブスクリプションの同期 &#40;Windows 同期マネージャー&#41;](synchronize-a-subscription-using-windows-synchronization-manager.md)   
 [マージ レプリケーションの競合検出および解決の詳細](merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
