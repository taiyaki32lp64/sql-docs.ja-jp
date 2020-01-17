---
title: パーティションと DirectQuery モード (SSAS テーブル) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5f179ba9-6efb-46ae-90e5-945bbfddb719
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1fe22de3cc0718647de84345260017a4dd4e477e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067307"
---
# <a name="partitions-and-directquery-mode-ssas-tabular"></a>パーティションと DirectQuery モード (SSAS テーブル)
  ここでは、DirectQuery モデルでのパーティションの使用方法について説明します。 テーブル モデルでのパーティションに関する一般的な情報については、「[パーティション (SSAS テーブル)](partitions-ssas-tabular.md)」を参照してください。  
  
 パーティションに関する情報を表示または、使用されるパーティションを変更する方法については、次を参照してください。 [DirectQuery パーティションを変更する&#40;SSAS 表形式&#41;](../change-the-directquery-partition-ssas-tabular.md)します。  
  
## <a name="using-partitions-in-directquery-mode"></a>DirectQuery モードでのパーティションの使用  
 テーブルごとに、DirectQuery データ ソースとして使用する 1 つのパーティションを指定する必要があります。  複数のパーティションがある場合は、モデルを切り替えて DirectQuery モードを有効にすると、テーブル内に作成された最初のパーティションに DirectQuery パーティションのフラグが既定で設定されます。 この設定は、後で [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のパーティション マネージャーを使用して変更できます。  
  
 DirectQuery モードで 1 つのパーティションのみ許可するのはなぜでしょうか。  
  
 テーブル モデルでは、OLAP モデルの場合と同様に、テーブルのパーティションが SQL クエリによって定義されます。 パーティションの定義を作成する開発者は、パーティションが重ならないようにする必要があります。 Analysis Services では、レコードが 1 つのパーティションに属しているか、複数のパーティションに属しているかはチェックされません。  
  
 キャッシュされたテーブル モデル内のパーティションは同じように動作します。 インメモリ モデルを使用する場合は、キャッシュがアクセスされるときに、DAX 数式がパーティションごとに評価され、結果が結合されます。 一方、テーブル モデルが DirectQuery モードを使用する場合は、複数のパーティションを評価して結果を結合し、リレーショナル データ ストアに送信する SQL ステートメントに変換することは不可能です。 この操作を行うと、パフォーマンスが許容できないほど低下し、集計される結果が不正確になる可能性があります。  
  
 したがって、DirectQuery モードで応答されたクエリに対して、サーバーは DirectQuery アクセスのプライマリ パーティションとしてマークされた単一のパーティション ( *DirectQuery パーティション*) を使用します。  このパーティションの定義で指定された SQL クエリは、DirectQuery モードでのクエリの応答に使用できるデータの完全なセットを定義します。  
  
 パーティションを明示的に定義していない場合、エンジンは単純にリレーショナル データ ソース全体に SQL クエリを発行し、DAX 数式で指定されたセットベース操作を実行してクエリ結果を返します。  
  
 テーブルに複数のパーティションがあり、1 つのパーティションを DirectQuery パーティションとして選択した場合、既定では他のすべてのパーティションはメモリ内でのみ使用されるように自動的にマークされます。  
  
## <a name="partitions-in-cached-models-and-in-directquery-models"></a>キャッシュ モデルと DirectQuery モデルのパーティション  
 DirectQuery パーティションを構成するときは、パーティションの処理オプションを指定する必要があります。  
  
 DirectQuery パーティションには 2 つの処理オプションがあります。 このプロパティを設定するには、 **の** [パーティション マネージャー] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、 **[処理オプション]** プロパティを選択します。 次の表にこのプロパティの値を示し、接続文字列の [DirectQueryUsage] プロパティと組み合わせた場合の各値の影響について説明します。  
  
|**DirectQueryUsage**プロパティ|**[処理オプション]** プロパティ|メモ|  
|-----------------------------------|------------------------------------|-----------|  
|DirectQuery|[このパーティションを処理しない]|モデルが DirectQuery のみを使用している場合、処理は必要ありません。<br /><br /> ハイブリッド モデルでは、DirectQuery パーティションが処理されないように構成できます。 たとえば、非常に大きなデータ セットを操作する場合に、キャッシュに結果のすべてを追加する必要がなければ、DirectQuery パーティションにテーブル内の他のパーティションに対する結果の和集合を含めて、和集合を処理しないことを指定できます。 リレーショナル ソースに対するクエリは影響を受けず、キャッシュ データに対するクエリは他のパーティションからのデータを結合します。|  
|InMemory (DirectQuery あり)|[パーティションを処理できる]|モデルがハイブリッド モードを使用している場合は、メモリ内に対するクエリと DirectQuery データ ソースに対するクエリで同じパーティションを使用する必要があります。|  
  
## <a name="see-also"></a>参照  
 [パーティション (SSAS テーブル)](partitions-ssas-tabular.md)  
  
  
