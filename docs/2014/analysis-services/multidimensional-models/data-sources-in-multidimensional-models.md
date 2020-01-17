---
title: 多次元モデルのデータ ソース |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- metadata [Analysis Services]
- Analysis Services objects, data sources
- storing data [Analysis Services], data sources
- data sources [Analysis Services], about data sources
- security [Analysis Services], data sources
- data sources [Analysis Services]
- storage [Analysis Services], data sources
ms.assetid: a16469d9-9d53-4e35-9982-fc06327a9d33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bf51e9e73d1748d2be0a514d17ea727941391829
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076042"
---
# <a name="data-sources-in-multidimensional-models"></a>多次元モデルのデータ ソース
  多次元モデルにインポートするデータまたは読み込むデータは、すべて外部データ ソースから取得されます。 通常、ソース データはレポート生成用に設計されたデータ ウェアハウスから取得されますが、直接的または [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージなどを介して間接的にアクセスされるリレーショナル データベースから取得される場合もあります。  
  
 **の** データ ソース [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトでは、外部データ ソースへの直接接続を指定します。 物理的な場所だけでなく、接続文字列、データ プロバイダー、資格情報、および接続動作を制御する他のプロパティも指定します。  
  
 データ ソース オブジェクトによって提供される情報は、次の操作で使用されます。  
  
-   データ ソース ビューの生成に使用されるスキーマ情報とその他のメタデータのモデルへの取り込み  
  
-   処理中のクエリの実行またはモデルへのデータの読み込み  
  
-   ROLAP ストレージ モードを使用する多次元モデルまたはデータ マイニング モデルに対するクエリの実行  
  
-   リモート パーティションに対する読み取りまたは書き込み  
  
-   リンク オブジェクトへの接続と、ターゲットからソースへの同期  
  
-   リレーショナル データベースに格納されているファクト テーブル データを更新する書き戻し操作の実行  
  
 多次元モデルを最初から作成するときは、まずデータ ソース オブジェクトを作成します。次に、このオブジェクトを使用して、次のオブジェクト ( **データ ソース ビュー**) を生成します。 データ ソース ビューは、モデルのデータ抽象化レイヤーです。 通常は、ソース データベースのスキーマを基盤として使用して、データ ソース オブジェクトの後に作成されます。 ただし、他の方法でモデルを作成することもできます。たとえば、キューブとディメンションから作成する方法や、デザインを最適にサポートするスキーマを生成する方法などがあります。  
  
 モデルの作成方法に関係なく、各モデルにはソース データへの接続を指定する 1 つ以上のデータ ソース オブジェクトが必要です。 1 つのモデルに複数のデータ ソース オブジェクトを作成して、さまざまなソースのデータを使用したり、特定のオブジェクトの接続プロパティを変更したりできます。  
  
 データ ソース オブジェクトは、モデルの他のオブジェクトとは別に管理できます。 データ ソースを作成した後にプロパティを変更し、データが正しく取得されるようにモデルを前処理できます。  
  
## <a name="related-topics-and-tasks"></a>関連項目およびタスク  
  
|トピック|説明|  
|-----------|-----------------|  
|[サポートされるデータ ソース&#40;SSAS 多次元&#41;](supported-data-sources-ssas-multidimensional.md)|多次元モデルで使用できるデータ ソースの種類について説明します。|  
|[データ ソースの作成 &#40;SSAS 多次元&#41;](create-a-data-source-ssas-multidimensional.md)|多次元モデルにデータ ソース オブジェクトを追加する方法について説明します。|  
|[ソリューション エクスプローラーでのデータ ソースの削除 &#40;SSAS 多次元&#41;](delete-a-data-source-in-solution-explorer-ssas-multidimensional.md)|この手順で、多次元モデルからデータ ソース オブジェクトを削除します。|  
|[データ ソースのプロパティの設定 &#40;SSAS 多次元&#41;](set-data-source-properties-ssas-multidimensional.md)|各プロパティとその設定方法について説明します。|  
|[権限借用オプションの設定 &#40;SSAS - 多次元&#41;](set-impersonation-options-ssas-multidimensional.md)|[権限借用情報] ダイアログ ボックスのオプションを構成する方法について説明します。|  
  
## <a name="see-also"></a>関連項目  
 [データベース オブジェクト &#40;Analysis Services - 多次元データ&#41;](olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [論理アーキテクチャ &#40;Analysis Services - 多次元データ&#41;](olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [多次元モデルのデータ ソース ビュー](data-source-views-in-multidimensional-models.md)   
 [データ ソースとバインド &#40;SSAS 多次元&#41;](data-sources-and-bindings-ssas-multidimensional.md)  
  
  
