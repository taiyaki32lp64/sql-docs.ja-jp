---
title: '&lt;ソースデータクエリ&gt; |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e523d33da502a971b950e33ec0bd935149ed26f7
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892341"
---
# <a name="ltsource-data-querygt"></a>&lt;ソースデータクエリ&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  データマイニングモデルをトレーニングし、マイニングモデルから予測を作成するには、データベースの[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]外部にあるデータにアクセスする必要があります。 この外部データ\<を定義するには、データマイニング拡張機能 (DMX) でソースデータクエリ > 句を使用します。 [ &#40;Dmx&#41;への挿入](../dmx/insert-into-dmx.md)、[モデル&#60;&#62;予測からの選択&#40;、&#41;dmx](../dmx/select-from-model-prediction-join-dmx.md)の選択、および[[自然予測 join ステートメントからの選択]](../dmx/select-from-model-prediction-join-dmx.md)では、すべて **\<ソースデータクエリが使用され >** .  
  
## <a name="query-types"></a>クエリの種類  
 ソース データの指定には、最も一般的な次の 3 つの方法があります。  
  
 [OPENQUERY &#40;DMX&#41;](../dmx/source-data-query-openquery.md)  
 このステートメントは、既存のデータソースを使用し[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]て、のインスタンスの外部にあるデータを照会します。  
  
 **Openquery**は関数の**OPENROWSET**に似ていますが、 **openquery**には次のような利点があります。  
  
-   DMX クエリは、 **OPENQUERY**を使用した方がはるかに簡単に記述できます。 クエリを記述するたびに新しい接続文字列を作成するのではなく、データソース内の既存の接続文字列を利用できます。 データ ソース オブジェクトは、各ユーザーのデータ アクセスを制御することもできます。  
  
-   管理者は、サーバー上のデータへのアクセス方法をより細かく制御できます。 たとえば、管理者は、サーバーに読み込まれるプロバイダーや、アクセスできる外部データを管理できます。  
  
 [OPENROWSET &#40;DMX&#41;](../dmx/source-data-query-openrowset.md)  
 このステートメントは、既存のデータソースを使用し[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]て、のインスタンスの外部にあるデータを照会します。  
  
 [図形&#40;DMX&#41;](../dmx/source-data-query-shape.md)  
 このステートメントは複数のデータ ソースをクエリして、入れ子になったテーブルを作成します。 **SHAPE**を使用すると、複数のソースのデータを1つの階層テーブルに結合できます。 これは、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] の機能を利用して、テーブル内にテーブルを埋め込むことによってテーブルを入れ子にします。  
  
 ソースデータを指定するには、次のオプションを使用することもできます。  
  
-   任意の有効な DMX ステートメント  
  
-   すべての有効な多次元式 (MDX) ステートメント  
  
-   ストアド プロシージャを返すテーブル  
  
-   XML for Analysis (XMLA) 行セット  
  
-   行セットパラメーター  
  
## <a name="see-also"></a>関連項目  
 [データマイニング拡張&#40;機能&#41; DMX データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データマイニング拡張&#40;機能&#41; DMX ステートメントリファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [入れ子に&#40;なったテーブル Analysis Services-データマイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/nested-tables-analysis-services-data-mining)  
  
  
