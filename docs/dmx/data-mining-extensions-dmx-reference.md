---
title: データマイニング拡張機能 (DMX) リファレンス |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c47514f551ec07a8c8837533cb38c0e6283645cd
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892883"
---
# <a name="data-mining-extensions-dmx-reference"></a>データ マイニング拡張機能 (DMX) リファレンス
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  データマイニング拡張機能 (DMX) は、で[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]データマイニングモデルを作成および操作するために使用できる言語です。 DMX を使用して、新しいデータ マイニング モデルの構造の作成、これらのモデルの学習、およびモデルの参照、管理、予測を行うことができます。 DMX は、データ定義言語 (DDL) ステートメント、データ操作言語 (DML) ステートメント、および関数と演算子で構成されています。  
  
## <a name="microsoft-ole-db-for-data-mining-specification"></a>Microsoft OLE DB for Data Mining 仕様  
 のデータマイニング機能[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]は、 [!INCLUDE[msCoName](../includes/msconame-md.md)]データマイニング仕様の OLE DB に準拠するように構築されています。  
  
 データ[!INCLUDE[msCoName](../includes/msconame-md.md)]マイニング仕様の OLE DB では、次のものを定義します。  
  
-   データ マイニング モデルを定義する情報を保持するための構造。  
  
-   データ  マイニング モデルの作成および使用のための言語。  
  
 この仕様では、データ マイニングの基礎がデータ マイニング モデル仮想オブジェクトとして定義されます。 データ マイニング モデル オブジェクトは、特定のマイニング モデルに関する既知の事柄をすべてカプセル化します。 データ マイニング モデル オブジェクトは SQL テーブルのような構造になっており、モデルを説明する列、データ型、およびメタ情報から構成されています。 この構造により、SQL の拡張版である DMX 言語を使用して、モデルを作成、使用することができるようになります。  
  
 **詳細情報:** [マイニング構造 (Analysis Services - データ マイニング)](https://docs.microsoft.com/analysis-services/data-mining/mining-structures-analysis-services-data-mining)  
  
##  <a name="BKMK_DMXStatements"></a>DMX ステートメント  
 DMX ステートメントを使用して、データ マイニング モデルの作成、処理、削除、コピー、参照、および予測を行うことができます。 DMX にはデータ定義ステートメントおよびデータ操作ステートメントの 2 種類のステートメントがあります。 いずれかのステートメントを使用して、各種のタスクを実行することができます。  
  
 以下のセクションでは、DMX ステートメントの使用に関する詳細について説明します。  
  
-   [データ定義ステートメント](#BKMK_DDL)  
  
-   [データ操作ステートメント](#BKMK_DML)  
  
-   [クエリの基礎](#BKMK_Queries)  
  
###  <a name="BKMK_DDL"></a>データ定義ステートメント  
 新しいマイニング構造とマイニング モデルの作成および定義、マイニング モデルとマイニング構造のインポートおよびエクスポート、データベースからの既存のモデルの削除を行うには、DMX でデータ定義ステートメントを使用します。 DMX でのデータ定義ステートメントは、データ定義言語 (DDL) の一部です。  
  
 DMX でデータ定義ステートメントを使用して、次のタスクを実行することができます。  
  
-   [CREATE マイニング structure](../dmx/create-mining-structure-dmx.md)ステートメントを使用してマイニング構造を作成し、 [ALTER マイニング structure](../dmx/alter-mining-structure-dmx.md)ステートメントを使用してマイニングモデルをマイニング構造に追加します。  
  
-   [CREATE マイニング model](../dmx/create-mining-model-dmx.md)ステートメントを使用して空のデータマイニングモデルオブジェクトを構築することにより、マイニングモデルと関連するマイニング構造を同時に作成します。  
  
-   [エクスポート](../dmx/export-dmx.md)ステートメントを使用して、マイニングモデルおよび関連するマイニング構造をファイルにエクスポートします。 [Import](../dmx/import-dmx.md)ステートメントを使用して、EXPORT ステートメントによって作成されたファイルから、マイニングモデルおよび関連するマイニング構造をインポートします。  
  
-   [SELECT into](../dmx/select-into-dmx.md)ステートメントを使用して、既存のマイニングモデルの構造を新しいモデルにコピーし、同じデータでトレーニングします。  
  
-   [DROP マイニングモデル](../dmx/drop-mining-model-dmx.md)ステートメントを使用して、データベースからマイニングモデルを完全に削除します。 削除[マイニング構造](../dmx/drop-mining-structure-dmx.md)ステートメントを使用して、マイニング構造とそれに関連付けられているすべてのマイニングモデルをデータベースから完全に削除します。  
  
 DMX ステートメントを使用して実行できるデータマイニングタスクの詳細については、「[データマイニング&#40;拡張&#41;機能 dmx ステートメントリファレンス](../dmx/data-mining-extensions-dmx-statements.md)」を参照してください。  
  
 [DMX ステートメントに戻る](#BKMK_DMXStatements)  
  
###  <a name="BKMK_DML"></a>データ操作ステートメント  
 既存のマイニング モデルの使用、モデルの参照、およびモデルに対する予測の作成を行うには、DMX でデータ操作ステートメントを使用します。 DMX でのデータ操作ステートメントは、データ操作言語 (DML) の一部です。  
  
 DMX でデータ操作ステートメントを使用して、次のタスクを実行することができます。  
  
-   [INSERT INTO](../dmx/insert-into-dmx.md)ステートメントを使用して、マイニングモデルをトレーニングします。 これにより、実際のソース データがデータ マイニング モデル オブジェクトに挿入されることはありませんが、アルゴリズムが作成するマイニング モデルを説明する抽象概念が作成されます。 INSERT INTO ステートメントのソースクエリについては、「 [ \<source data query >](../dmx/source-data-query.md)」を参照してください。  
  
-   モデルのトレーニング中に計算され、ソースデータの統計情報など、データマイニングモデルに格納されている情報を参照するには、SELECT ステートメントを拡張します。 SELECT ステートメントの機能を拡張するために含めることができる句は次のとおりです。  
  
    -   [&#62;モデル&#40;DMX から&#60;DISTINCT を選択&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
    -   [[モデル&#60;&#62;から] を選択します。コンテンツ&#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
    -   [[モデル&#60;&#62;から] を選択します。DMX &#40;のケース&#41;](../dmx/select-from-model-cases-dmx.md)  
  
    -   [[モデル&#60;&#62;から] を選択します。SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
    -   [[モデル&#60;&#62;から] を選択します。DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
-   SELECT ステートメントの[予測結合](../dmx/select-from-model-prediction-join-dmx.md)句を使用して、既存のマイニングモデルに基づく予測を作成します。 予測結合ステートメントのソースクエリについては、「 [ \<source data query >](../dmx/source-data-query.md)」を参照してください。  
  
-   [削除&#40;DMX&#41; ](../dmx/delete-dmx.md)ステートメントを使用して、モデルまたは構造からすべてのトレーニング済みデータを削除します。  
  
 DMX ステートメントを使用して実行できるデータマイニングタスクの詳細については、「[データマイニング&#40;拡張&#41;機能 dmx ステートメントリファレンス](../dmx/data-mining-extensions-dmx-statements.md)」を参照してください。  
  
 [DMX ステートメントに戻る](#BKMK_DMXStatements)  
  
###  <a name="BKMK_Queries"></a>DMX クエリの基礎  
 SELECT ステートメントは、ほとんどの DMX クエリの基礎となります。 これらのステートメントで使用する句によって、マイニング モデルの参照、コピー、および予測を行うことができます。 予測クエリでは、SELECT の形式を使用して、既存のマイニングモデルに基づいて予測を作成します。 関数を使用することで、データ マイニング モデルの固有の機能では行えないマイニング モデルの参照およびクエリを行うことができます。  
  
 DMX 関数を使用すると、モデルの学習中に検出された情報の取得および新しい情報の計算を行うことができます。 これらの関数は、予測の根拠となるデータや正確性を説明する統計を返したり、予測に対するより広範な説明を返すなど、多くの目的で使用することができます。  
  
 **詳細**  **情報:** Dmx の[Select ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)、[一般的&#40;な&#41;予測関数 dmx](../dmx/general-prediction-functions-dmx.md)、[構造と dmx 予測クエリの使用状況](../dmx/structure-and-usage-of-dmx-prediction-queries.md)、[データマイニング拡張機能&#40;の dmx&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
 [DMX ステートメントに戻る](#BKMK_DMXStatements)  
  
## <a name="see-also"></a>参照  
 [データマイニング拡張&#40;機能&#41; DMX 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX オペレーターリファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX ステートメントリファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データマイニング拡張&#40;機能&#41; DMX 構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [データマイニング拡張&#40;機能&#41; DMX 構文要素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [一般的な予測&#40;関数 DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
