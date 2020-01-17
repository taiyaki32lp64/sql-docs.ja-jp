---
title: モデリング フラグ (データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- data types [data mining]
- REGRESSOR flag
- MODEL_EXISTENCE_ONLY flag
- REGRESSOR column
- columns [data mining], modeling flags
- NOT NULL modeling flag
- modeling flags [data mining]
- null values [Analysis Services]
- MODEL_EXISTENCE_ONLY column
- coding [Data Mining]
ms.assetid: 8826d5ce-9ba8-4490-981b-39690ace40a4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 37263c42e4e9f37b1b782dc07b8df03f77092b14
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083309"
---
# <a name="modeling-flags-data-mining"></a>モデリング フラグ (データ マイニング)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のモデリング フラグを使用すると、ケース テーブルで定義されているデータに関する追加情報をデータ マイニング アルゴリズムに提供できます。 アルゴリズムは、この情報を使用して、より正確なデータ マイニング モデルを作成することができます。  
  
 マイニング構造のレベルで定義されるモデリング フラグもあれば、マイニング モデル列のレベルで定義されるモデリング フラグもあります。 たとえば、`NOT NULL` モデリング フラグはマイニング構造列で使用されます。 モデルの作成に使用するアルゴリズムに応じて、追加的なモデリング フラグをマイニング モデル列に定義することができます。  
  
> [!NOTE]  
>  サードパーティ プラグインには、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]であらかじめ定義されているフラグに加えて他のモデリング フラグがある場合もあります。  
  
## <a name="list-of-modeling-flags"></a>モデリング フラグの一覧  
 次の一覧に、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]でサポートされているモデリング フラグを示します。 特定のアルゴリズムでサポートされているモデリング フラグについては、モデルの作成に使用したアルゴリズムのテクニカル リファレンス トピックを参照してください。  
  
 `NOT NULL`  
 この属性列の値が NULL 値を含むことはないことを示します。 モデルの学習プロセス中に、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] がこの属性列に NULL 値を検出した場合、エラーが発生します。  
  
 **MODEL_EXISTENCE_ONLY**  
 列が、`Missing` および `Existing` の 2 つの状態を持つ列として扱われることを示します。 値が `NULL` の場合は Missing として扱われます。 MODEL_EXISTENCE_ONLY フラグは、予測可能な属性に適用され、ほとんどのアルゴリズムでサポートされます。  
  
 実際、MODEL_EXISTENCE_ONLY フラグを `True` に設定すると、`Missing` と `Existing` の 2 つの状態だけが存在するように値の形式が変わります。 Missing に該当しない状態はすべて単一の `Existing` 値に統合されます。  
  
 このモデリング フラグは、`NULL` 状態が暗黙的な意味を持ち、`NOT NULL` 状態の明示的な値はその列に値があるという事実ほど重要ではないような属性に使用されるのが一般的です。 たとえば [DateContractSigned] 列は、契約書が署名されなかった場合には `NULL` に、署名された場合には `NOT NULL` になります。 したがって、契約書が署名されるかどうかの予測を目的とするモデルでは、MODEL_EXISTENCE_ONLY フラグを使用して、`NOT NULL` のケースの正確な日付の値は無視して、契約書が `Missing` のケースと `Existing` のケースの区別のみを行うことができます。  
  
> [!NOTE]  
>  Missing はアルゴリズムによって使用される特殊な状態であり、列のテキスト値の "Missing" とは異なります。 詳細については、「 [不足値 &#40;Analysis Services - データ マイニング&#41;](missing-values-analysis-services-data-mining.md)であらかじめ定義されているフラグに加えて他のモデリング フラグがある場合もあります。  
  
 `REGRESSOR`  
 列が処理中にリグレッサーとして使用される候補であることを示します。 このフラグは、マイニング モデル列で定義され、連続する数値データ型の列にのみ適用できます。 このフラグの使用の詳細については、このトピックの「 [REGRESSOR モデリング フラグの使用](#bkmk_UseRegressors)」を参照してください。  
  
## <a name="viewing-and-changing-modeling-flags"></a>モデリング フラグの表示と変更  
 マイニング構造列やマイニング モデル列に関連付けられているモデリング フラグは、その構造またはモデルのプロパティをデータ マイニング デザイナーで表示することによって確認できます。  
  
 現在のマイニング構造に適用されているモデリング フラグを確認するには、データ マイニングのスキーマ行セットに対するクエリを作成し、その構造列のみのモデリング フラグを取得します。たとえば、次のクエリを使用します。  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_STRUCTURE_COLUMNS  
WHERE STRUCTURE_NAME = '<structure name>'  
```  
  
 モデルに使用されるモデリング フラグは、データ マイニング デザイナーを使用し、関連する列のプロパティを編集することによって追加または変更できます。 このような変更を行った場合、該当する構造またはモデルを再処理する必要があります。  
  
 新しいマイニング構造またはマイニング モデルでモデリング フラグを指定するには、DMX を使用するか、AMO スクリプトまたは XMLA スクリプトを使用します。 ただし、DMX を使用して、既存のマイニング モデルやマイニング構造で使用されているモデリング フラグを変更することはできません。 `ALTER MINING STRUCTURE....ADD MINING MODEL`構文を使用して新しいマイニング モデルを作成する必要があります。  
  
##  <a name="bkmk_UseRegressors"></a> REGRESSOR モデリング フラグの使用  
 列に REGRESSOR モデリング フラグを設定すると、その列にリグレッサー候補が含まれていることがアルゴリズムに対して示されます。 モデルで使用される実際のリグレッサーはアルゴリズムによって決定されます。 予測可能な属性をモデル化しないリグレッサー候補は破棄できます。  
  
 データ マイニング ウィザードを使用してモデルを作成すると、連続列である入力列のすべてにリグレッサー候補のフラグが付けられます。 したがって、REGRESSOR フラグを明示的に設定していない列がモデルでリグレッサーとして使用される場合もあります。  
  
 処理されたモデルで実際に使用されたリグレッサーを特定するには、マイニング モデルのスキーマ行セットに対してクエリを実行します。以下に例を示します。  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_COLUMNS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 **注** マイニング モデルを変更して、列のコンテンツの種類を連続から不連続に変更した場合は、マイニング列のフラグを手動で変更してからモデルを再処理する必要があります。  
  
### <a name="regressors-in-linear-regression-models"></a>線形回帰モデルのリグレッサー  
 線形回帰モデルは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムに基づいています。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムを使用していない場合でも、連続属性の回帰を表すツリーやノードがデシジョン ツリー モデルに含まれることはあります。  
  
 したがって、これらのモデルについては、連続列がリグレッサーを表すことを指定する必要はありません。 列に REGRESSOR フラグを設定しなくても、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムにより、データセットが意味のあるパターンを持つ領域に分割されます。 違いは、このモデリング フラグを設定すると、ツリーのノードのパターンに合う以下の形式の回帰式をアルゴリズムが見つけようとするということです。  
  
 a*C1 + b\*C2 + ...  
  
 その後、残差の合計が計算され、偏差が大きすぎる場合には、ツリーが強制的に分割されます。  
  
 たとえば、 **Income** を属性として使用して顧客の購入行動を予測する場合に、その列に REGRESSOR モデリング フラグを設定すると、アルゴリズムはまず、標準の回帰式を使用して **Income** の値を試します。 偏差が大きすぎる場合はその回帰式が放棄され、ツリーが他の属性で分割されます。 その後デシジョン ツリー アルゴリズムは、分割後の各分岐で、Income をリグレッサーとして使用できるかどうかを試します。  
  
 FORCE_REGRESSOR パラメーターを使用すると、アルゴリズムで特定のリグレッサーが使用されるようにすることができます。 このパラメーターは、デシジョン ツリー アルゴリズムと線形回帰アルゴリズムで使用できます。  
  
## <a name="related-tasks"></a>Related Tasks  
 モデリング フラグの使用の詳細については、次のリンクを参照してください。  
  
|タスク|トピック|  
|----------|-----------|  
|データ マイニング デザイナーを使用してモデリング フラグを編集する|[モデリング フラグの表示または変更 &#40;データ マイニング&#41;](modeling-flags-data-mining.md)|  
|適切なリグレッサーを推奨するためのヒントをアルゴリズムに対して指定する|[モデルでリグレッサーとして使用する列の指定](specify-a-column-to-use-as-regressor-in-a-model.md)|  
|特定のアルゴリズムでサポートされているモデリング フラグを確認する (各アルゴリズムのリファレンス トピックの「モデリング フラグ」セクション)|[データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining-algorithms-analysis-services-data-mining.md)|  
|マイニング構造列とそこに設定できるプロパティについて詳しく知る|[マイニング構造列](mining-structure-columns.md)|  
|モデル レベルで適用できるマイニング モデル列とモデリング フラグについて知る|[マイニング モデル列](mining-model-columns.md)|  
|モデリング フラグを DMX ステートメントで扱うための構文を確認する|[モデリング フラグ &#40;DMX&#41;](/sql/dmx/modeling-flags-dmx)|  
|不足値とその取り扱いの方法について知る|[不足値 &#40;Analysis Services - データ マイニング&#41;](missing-values-analysis-services-data-mining.md)|  
|モデルと構造の管理および使用法のプロパティの設定について知る|[データ マイニング オブジェクトの移動](moving-data-mining-objects.md)|  
  
  
