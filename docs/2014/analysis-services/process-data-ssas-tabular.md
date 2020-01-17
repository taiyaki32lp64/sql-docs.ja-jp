---
title: データ (SSAS テーブル) の処理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a0ca45681866e0ba96edaa81c21445a89f94275
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070698"
---
# <a name="process-data-ssas-tabular"></a>データの処理 (SSAS テーブル)
  キャッシュ モードでデータをテーブル モデルにインポートするときは、そのデータのインポート時点でのスナップショットを取得することになります。 場合によっては、そのデータは変更されることはないため、モデルで更新される必要はありません。 ただし、インポートするデータが定期的に変更され、かつデータ ソースから取得した最新データをモデルで反映できるようにするため、そのデータを処理 (更新) し計算済みデータを再計算しなければならなくなる可能性が高くなります。 モデルのデータを更新するため、すべてのテーブルと個別のテーブルでパーティションまたはデータ ソース接続ごとに処理を実行します。  
  
 モデル プロジェクト作成時には、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で処理アクションを手動で開始する必要があります。 モデルを配置した後は、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を使用して処理操作を実行するか、スクリプトを使用してスケジュールできます。 ここで説明するタスクはすべて、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] でのモデル作成時に実行できる処理アクションに関係します。 配置済みモデルの処理アクションの詳細については、次を参照してください。[データベースの処理、テーブル、またはパーティション](tabular-models/process-database-table-or-partition-analysis-services.md)します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|トピック|説明|  
|-----------|-----------------|  
|[データの手動処理 &#40;SSAS テーブル&#41;](manually-process-data-ssas-tabular.md)|モデル ワークスペース データを手動で処理する方法について説明します。|  
|[データの処理のトラブルシューティング &#40;SSAS テーブル&#41;](troubleshoot-process-data-ssas-tabular.md)|処理操作のトラブルシューティング方法について説明します。|  
  
  
