---
title: SELECT DISTINCT FROM &lt;model &gt; (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 67ed5236aad0549fa6850114280ee15d8cebcaeb
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892528"
---
# <a name="select-distinct-from-ltmodel-gt-dmx"></a>SELECT DISTINCT FROM &lt;model &gt; (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  モデル内の選択された列に対して可能なすべての状態を返します。 返される値は、指定された列に含まれているのが不連続値か、分離された数値か、連続する数値かによって異なります。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [FLATTENED] DISTINCT [TOP <n>] <expression list> FROM <model>   
[WHERE <condition list>][ORDER BY <expression>]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 任意。 返す行数を指定する整数。  
  
 *式の一覧*  
 関連する列識別子 (モデルより抽出) または式のコンマ区切りリストです。  
  
 *model*  
 モデル識別子です。  
  
 *条件一覧*  
 列のリストから返される値を制限する条件です。  
  
 *式 (expression)*  
 任意。 スカラー値を返す式。  
  
## <a name="remarks"></a>コメント  
 **SELECT DISTINCT FROM**ステートメントは、1つの列、または関連する列のセットでのみ機能します。 この句は、関連しない列のセットでは動作しません。  
  
 **SELECT DISTINCT FROM**ステートメントを使用すると、入れ子になったテーブル内の列を直接参照できます。 以下に例を示します。  
  
```  
<model>.<table column reference>.<column reference>  
```  
  
 **Select DISTINCT FROM \<model >** ステートメントの結果は、列の型によって異なります。 次の表は、サポートされている列の型およびステートメントからの出力について示しています。  
  
|列の型|[出力]|  
|-----------------|------------|  
|Discrete|列内の一意な値です。|  
|Discretized|列内の各離散化バケットの中点です。|  
|Continuous|列内の値の中間点です。|  
  
## <a name="discrete-column-example"></a>不連続列の例  
 次のコードサンプルは、「 `[TM Decision Tree]` [基本的なデータマイニングチュートリアル](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」で作成したモデルに基づいています。 クエリは、不連続列 `Gender` 内に存在する一意の値を返します。  
  
```  
SELECT DISTINCT [Gender]  
FROM [TM Decision Tree]  
```  
  
 例の結果を次に示します。  
  
|Gender|  
|------------|  
||  
|F|  
|M|  
  
 不連続値を含む列の場合、結果には、NULL 値として示される、存在しない状態が常に含まれます。  
  
## <a name="continuous-column-example"></a>連続列の例  
 次のコード サンプルは、列内のすべての値の中間点、最小年齢、最大年齢を返します。  
  
```  
SELECT DISTINCT [Age] AS [Midpoint Age],   
    RangeMin([Age]) AS [Minimum Age],   
    RangeMax([Age]) AS [Maximum Age]  
FROM [TM Decision Tree]  
```  
  
 例の結果を次に示します。  
  
|Midpoint Age|Minimum Age|Maximum Age|  
|------------------|-----------------|-----------------|  
||||  
|62|26|97|  
  
 クエリは、不足値を表すために、NULL 値の 1 行を返します。  
  
## <a name="discretized-column-example"></a>離散化列の例  
 次のコード サンプルは、列 `Yearly Income]` のアルゴリズムで作成された各バケットの中間点、最大値、および最小値を返します。 この例の結果を再現するには、`[Targeted Mailing]` と同じマイニング構造を新しく作成する必要があります。 ウィザードで、 `Yearly Income`列のコンテンツの種類を **[連続]** から **[分離]** に変更します。  
  
> [!NOTE]  
>  また、「基本的なデータ マイニング チュートリアル」で作成したマイニング モデルを変更して、マイニング構造列 `Yearly Income]` を分離できます。 この方法の詳細については、「[マイニングモデルの列の分離を変更](https://docs.microsoft.com/analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model)する」を参照してください。 ただし、列の分離を変更した場合は、マイニング構造が強制的に再処理され、その構造を使用して作成した他のモデルの結果が変更されます。  
  
```  
SELECT DISTINCT [Yearly Income] AS [Bucket Average],   
    RangeMin([Yearly Income]) AS [Bucket Minimum],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
 例の結果を次に示します。  
  
|Bucket Average|Bucket Minimum|Bucket Maximum|  
|--------------------|--------------------|--------------------|  
||||  
|24610.7|10000|39221.41|  
|55115.73|39221.41|71010.05|  
|84821.54|71010.05|98633.04|  
|111633.9|98633.04|124634.7|  
|147317.4|124634.7|170000|  
  
 [Yearly Income] 列の値が 5 つのバケットに分離されていることに加え、不足値を表すために NULL 値の行が追加されていることがわかります。  
  
 結果の小数点以下表示桁数は、クエリに使用するクライアントによって異なります。 ここでは、説明を簡単にするためおよび [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で表示される値を反映するために、小数点以下 2 桁に丸められています。  
  
 たとえば、デシジョン ツリー ビューアーを使用してモデルを参照し、収入ごとにグループ化された顧客を含むノードをクリックすると、次のノードのプロパティがツールヒントに表示されます。  
  
 Age >=69 AND Yearly Income < 39221.41  
  
> [!NOTE]  
>  最小バケットの最小値および最大バケットの最大値は、計測された値のうちの最大値と最小値になります。 この計測された範囲に該当しないすべての値は、最小バケットおよび最大バケットに属していると見なされます。  
  
## <a name="see-also"></a>参照  
 [SELECT&#40;DMX&#41;](../dmx/select-dmx.md)   
 [データマイニング拡張&#40;機能&#41; DMX データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
