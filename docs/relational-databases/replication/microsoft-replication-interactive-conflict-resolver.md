---
title: インタラクティブ競合回避モジュール (マージ)
describes: Describes the Interactive Conflict Resolver that can be used for merge subscriptions that are synchronized using the Windows Synchronization Manager.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replconflictviewer.interactiveresolver.f1
ms.assetid: d3d4a480-782b-4b1d-b839-565c8cf6cb24
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 5eca59b2277eefc351b63013dbc614eac9ed0b65
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321949"
---
# <a name="microsoft-replication-interactive-conflict-resolver"></a>Microsoft レプリケーション インタラクティブ競合回避モジュール
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  インタラクティブ競合回避モジュールは、Windows 同期マネージャーを使用して同期が行われるマージ サブスクリプションに使用することができます。 これにより、データ競合に対する結果の表示、比較、編集、および選択ができます。 レプリケーションには、コミットされた後で競合結果の表示および修正を行うことができる競合表示モジュールも含まれます。 インタラクティブ競合回避モジュールを使用すると、同期中に結果を選択することができます。  
  
> [!NOTE]  
>  論理レコードに関連する競合は、インタラクティブ競合回避モジュールには表示されません。 これらの競合に関する情報を表示するには、レプリケーション ストアド プロシージャを使用します。 詳細については、「[マージ パブリケーションの競合情報の表示 (レプリケーション Transact-SQL プログラミング)](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **列名**  
 テーブルのすべての列の名前です。 1 つまたは複数の列が競合するデータを持つ場合があります。 どの列が競合するかにかかわらず、競合で優先された行全体が、優先されなかった行全体を上書きします。  
  
 **[提案された解決策]**  
 アーティクルの競合回避モジュールによって提案された解決策です。  
  
 **発行元**  
 パブリッシャーでのデータ値です。  
  
 **サブスクライバー**  
 サブスクライバーでのデータ値です。  
  
 **[推奨設定を優先]** 、 **[パブリッシャーを優先]** 、 **[サブスクライバーを優先]**  
 パブリッシャーまたはサブスクライバーのどちらが競合に優先されなかったかによって、どちらかが適用される行を受け入れます。 パブリッシャーが競合に優先されなかった場合、その他のすべてのサブスクライバーは、次にパブリッシャーと同期される際に、競合に優先される行を受け取ります。  
  
 **[残りの競合を自動的に解決]**  
 アーティクルの競合回避モジュールによって提案された解決策を使用して、残りの競合を解決します。  
  
 **[参照用にこの競合の詳細をログに記録する]**  
 システム テーブルでの競合の詳細をログに記録します。  
  
## <a name="see-also"></a>参照  
 [インタラクティブな競合解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [マージ パブリケーションでのデータの競合の表示および解決 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Windows 同期マネージャーを使用したサブスクリプションの同期 &#40;Windows 同期マネージャー&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)   
 [マージ レプリケーションの競合検出および解決の詳細](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
