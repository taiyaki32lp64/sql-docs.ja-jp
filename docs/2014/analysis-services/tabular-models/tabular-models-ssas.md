---
title: テーブル モデリング (SSAS テーブル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 38ebc261b8d1c5a2a134de7085c2e6f34a704b34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066288"
---
# <a name="tabular-modeling-ssas-tabular"></a>テーブル モデリング (SSAS テーブル)
  表形式のモデルは、Analysis Services のメモリ内データベースです。 xVelocity メモリ内分析エンジン (VertiPaq) は、最新の圧縮アルゴリズムとマルチスレッド クエリ プロセッサを使用して、Microsoft Excel や Microsoft [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] などのレポート クライアント アプリケーションによる、表形式のモデルのオブジェクトとデータへの高速アクセスを実現します。  
  
 テーブル モデルでは、2 つのモードでのデータ アクセスをサポートします。キャッシュ モードと DirectQuery モード。 キャッシュ モードでは、リレーショナル データベース、データ フィード、フラット テキスト ファイルなどの複数のソースからのデータを統合できます。 DirectQuery モードでは、メモリ内モデルをバイパスでき、クライアント アプリケーションはデータを (SQL Server リレーショナル) ソースで直接クエリできます。  
  
 表形式のモデルは、新しい表形式モデル プロジェクトのテンプレートを使用して [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] で作成されます。 複数のソースからデータをインポートしてから、リレーションシップ、計算列、メジャー、KPI、および階層を追加すると、階層モデルを拡充できます。 モデルは、クライアント レポート アプリケーションの接続先の Analysis Services のインスタンスに配置できます。 配置済みのモデルは、SQL Server Management Studio で多次元モデルのように管理できます。 また、最適処理のためにパーティション分割したり、ロール ベースのセキュリティを使用して行レベルに保護したりすることもできます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [テーブル モデル ソリューション &#40;SSAS テーブル&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
 [表形式モデルのデータベース (SSAS 表形式)](tabular-model-databases-ssas-tabular.md)  
  
 [テーブル モデル データ アクセス](tabular-model-data-access.md)  
  
  
