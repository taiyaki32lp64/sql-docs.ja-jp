---
title: MDX 関数リファレンス (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ff14718e09fa3732a40ea245430f33c599325eea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003511"
---
# <a name="mdx-function-reference-mdx"></a>MDX 関数リファレンス (MDX)


  Analysis Services は、多次元式 (MDX) 構文で関数の使用を提供します。 関数は有効な MDX ステートメントで使用でき、クエリ、カスタム ロールアップ定義、およびその他の計算で頻繁に使用します。 このセクションでは、MDX 関数についての情報を提供します。  
  
 以下の表では、戻り値の種類ごとに関数がまとめられています。また、目次には、関数名がアルファベット順に一覧表示されます。  
  
## <a name="array-functions"></a>配列関数  
  
|関数|説明|  
|--------------|-----------------|  
|[SetToArray &#40;MDX&#41;](../mdx/settoarray-mdx.md)|1 つまたは複数のセットをユーザー定義関数で使用する配列に変換します。|  
  
## <a name="hierarchy-functions"></a>階層関数  
  
|関数|説明|  
|--------------|-----------------|  
|[Hierarchy &#40;MDX&#41;](../mdx/hierarchy-mdx.md)|指定されたメンバーまたはレベルを含む階層を返します。|  
|[Dimensions &#40;MDX&#41;](../mdx/dimension-mdx.md)|指定されたメンバー、レベル、または階層を含むディメンションを返します。|  
|[Dimensions &#40;MDX&#41;](../mdx/dimensions-mdx.md)|数値または文字列式で指定された階層を返します。|  
  
## <a name="level-functions"></a>レベル関数  
  
|関数|説明|  
|--------------|-----------------|  
|[Level &#40;MDX&#41;](../mdx/level-mdx.md)|メンバーのレベルを返します。|  
|[Level &#40;MDX&#41;](../mdx/levels-mdx.md)|ディメンションまたは階層内の位置が数値式で指定された、または文字列式で名前が指定されたレベルを返します。|  
  
## <a name="logical-functions"></a>論理関数  
  
|関数|説明|  
|--------------|-----------------|  
|[IsAncestor &#40;MDX&#41;](../mdx/isancestor-mdx.md)|指定したメンバーが別の指定したメンバーの先祖であるかどうかを返します。|  
|[IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)|評価した式が空のセル値かどうかを返します。|  
|[IsGeneration &#40;MDX&#41;](../mdx/isgeneration-mdx.md)|指定したメンバーが指定された世代内かどうかを返します。|  
|[IsLeaf &#40;MDX&#41;](../mdx/isleaf-mdx.md)|指定されたメンバーがリーフ メンバーであるかどうかを返します。|  
|[IsSibling &#40;MDX&#41;](../mdx/issibling-mdx.md)|指定されたメンバーが別の指定したメンバーの兄弟であるかどうかを返します。|  
  
## <a name="member-functions"></a>メンバー関数  
  
|関数|説明|  
|--------------|-----------------|  
|[Ancestor &#40;MDX&#41;](../mdx/ancestor-mdx.md)|メンバーの先祖のうち、指定されたレベルまたは距離にある先祖を返します。|  
|[ClosingPeriod &#40;MDX&#41;](../mdx/closingperiod-mdx.md)|指定したレベルのメンバーの子孫のうち、最後の兄弟を返します。|  
|[Cousin &#40;MDX&#41;](../mdx/cousin-mdx.md)|同じ相対位置として、指定した子メンバーの親メンバーの子メンバーを返します。|  
|[CurrentMember &#40;MDX&#41;](../mdx/currentmember-mdx.md)|イテレーション中に、指定したディメンションまたは階層から現在のメンバーを返します。|  
|[DataMember &#40;MDX&#41;](../mdx/datamember-mdx.md)|ディメンションの非リーフ メンバーに関連付けられているシステムで生成されたデータ メンバーを返します。|  
|[DefaultMember &#40;MDX&#41;](../mdx/defaultmember-mdx.md)|ディメンションまたは階層の既定のメンバーを返します。|  
|[FirstChild &#40;MDX&#41;](../mdx/firstchild-mdx.md)|メンバーの先頭の子メンバーを返します。|  
|[FirstSibling &#40;MDX&#41;](../mdx/firstsibling-mdx.md)|メンバーの親の最初の子を返します。|  
|[Item &#40;Members &#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)|指定された組からメンバーを返します。|  
|[Lag &#40;MDX&#41;](../mdx/lag-mdx.md)|指定したメンバーのディメンション メンバーの前に位置の指定した数であるメンバーを返します。|  
|[LastChild &#40;MDX&#41;](../mdx/lastchild-mdx.md)|指定したメンバーの最後の子を返します。|  
|[LastSibling &#40;MDX&#41;](../mdx/lastsibling-mdx.md)|指定したメンバーの親の最後の子を返します。|  
|[Lead &#40;MDX&#41;](../mdx/lead-mdx.md)|ディメンション内の指定されたメンバーから指定された数だけ後にあるメンバーを返します。|  
|[LinkMember &#40;MDX&#41;](../mdx/linkmember-mdx.md)|指定された階層の指定されたメンバーと等価のメンバーを返します。|  
|[Members &#40;文字列&#41; &#40;MDX&#41;](../mdx/members-string-mdx.md)|文字列式で指定されたメンバーを返します。|  
|[NextMember &#40;MDX&#41;](../mdx/nextmember-mdx.md)|指定したメンバーを含むレベルで、次のメンバーを返します。|  
|[OpeningPeriod &#40;MDX&#41;](../mdx/openingperiod-mdx.md)|指定したレベル、オプションで指定されたメンバーの子孫のうち、最初の兄弟を返します。|  
|[ParallelPeriod &#40;MDX&#41;](../mdx/parallelperiod-mdx.md)|指定されたメンバーと同じ相対位置で、前の期間からメンバーを返します。|  
|[Parent &#40;MDX&#41;](../mdx/parent-mdx.md)|メンバーの親メンバーを返します。|  
|[PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)|指定したメンバーを含むレベルで、前のメンバーを返します。|  
|[StrToMember &#40;MDX&#41;](../mdx/strtomember-mdx.md)|MDX 形式の文字列によって指定されたメンバーを返します。|  
|[UnknownMember &#40;MDX&#41;](../mdx/unknownmember-mdx.md)|レベルまたはメンバーに関連付けられた不明なメンバーを返します。|  
|[ValidMeasure &#40;MDX&#41;](../mdx/validmeasure-mdx.md)|適用できないディメンションをトップ レベルにすることにより、仮想キューブ内の有効なメジャーを返します。|  
  
## <a name="numeric-functions"></a>数値関数  
  
|関数|説明|  
|--------------|-----------------|  
|[Aggregate &#40;MDX&#41;](../mdx/aggregate-mdx.md)|指定されたセットの組に対し、メジャーを集計するか、またはオプションとして指定された数値式を集計することによって、スカラー値を返します。|  
|[Avg &#40;MDX&#41;](../mdx/avg-mdx.md)|メジャーの平均値または指定されたセットに対して評価される省略可能な数値式の平均値を返します。|  
|[CalculationCurrentPass (MDX)](../mdx/calculationcurrentpass-mdx.md)|指定したクエリ コンテキストのキューブの現在の計算パスを返します。|  
|[CalculationPassValue (MDX)](../mdx/calculationpassvalue-mdx.md)|キューブの指定された計算パスで評価される MDX 式の値を返します。|  
|[CoalesceEmpty &#40;MDX&#41;](../mdx/coalesceempty-mdx.md)|空のセル値を数値または文字列に連結し、結合された値を返します。|  
|[Correlation &#40;MDX&#41;](../mdx/correlation-mdx.md)|セットに対して評価される 2 つの系列の相関係数を返します。|  
|[Count &#40;Dimension &#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)|キューブ内のディメンション数を返します。|  
|[Count &#40;階層レベル&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)|ディメンションまたは階層レベル数を返します。|  
|[Count &#40;設定&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)|セット内のセルの数を返します。|  
|[Count &#40;組&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)|組の次元数を返します。|  
|[Covariance &#40;MDX&#41;](../mdx/covariance-mdx.md)|バイアスをかけた母集団の公式を使用し、セットに対して評価される 2 つの系列の母共分散を返します。|  
|[CovarianceN &#40;MDX&#41;](../mdx/covariancen-mdx.md)|バイアスをかけない母集団の公式を使用し、セットに対して評価される 2 つの系列のサンプル共分散を返します。|  
|[DistinctCount &#40;MDX&#41;](../mdx/distinctcount-mdx.md)|セット内の個別の空でないタプルの数を返します。|  
|[IIf &#40;MDX&#41;](../mdx/iif-mdx.md)|論理テストによって判別される 2 つの値の 1 つを返します。|  
|[LinRegIntercept &#40;MDX&#41;](../mdx/linregintercept-mdx.md)|セットの線形回帰を計算し、回帰直線の切片の値を返します y ax+b の a を = です。|  
|[LinRegPoint &#40;MDX&#41;](../mdx/linregpoint-mdx.md)|セットの線形回帰を計算しの値を返します*y*回帰直線 y = ax+b の a。|  
|[LinRegR2 &#40;MDX&#41;](../mdx/linregr2-mdx.md)|セットの線型回帰を計算し、決定、R2 の係数を返します。|  
|[LinRegSlope &#40;MDX&#41;](../mdx/linregslope-mdx.md)|セットの線形回帰を計算し、回帰直線の傾きの値を返します y ax+b の a を = です。|  
|[LinRegVariance &#40;MDX&#41;](../mdx/linregvariance-mdx.md)|セットの線型回帰を計算し、回帰直線に関連付けられた変位を返します y ax+b の a を = です。|  
|[LookupCube &#40;MDX&#41;](../mdx/lookupcube-mdx.md)|同じデータベース内で別に指定されたキューブに対して評価される MDX 式の値を返します。|  
|[Max &#40;MDX&#41;](../mdx/max-mdx.md)|セットに対して評価される数値式の最大値を返します。|  
|[Median &#40;MDX&#41;](../mdx/median-mdx.md)|セットに対して評価される数値式の中央値を返します。|  
|[Min &#40;MDX&#41;](../mdx/min-mdx.md)|セットに対して評価される数値式の最小値を返します。|  
|[Ordinal &#40;MDX&#41;](../mdx/ordinal-mdx.md)|レベルに関連付けられた 0 から始まる序数値を返します。|  
|[Predict &#40;MDX&#41;](../mdx/predict-mdx.md)|データ マイニング モデルに対して評価される数値式の値を返します。|  
|[Rank &#40;MDX&#41;](../mdx/rank-mdx.md)|指定されたセット内の指定された組のランクを返します。|  
|[RollupChildren &#40;MDX&#41;](../mdx/rollupchildren-mdx.md)|指定された単項演算子を使用して、指定したメンバーの子の値をロール アップによって生成された値を返します。|  
|[Stddev &#40;MDX&#41;](../mdx/stddev-mdx.md)|別名[Stdev &#40;MDX&#41;](../mdx/stdev-mdx.md)します。|  
|[StddevP &#40;MDX&#41;](../mdx/stddevp-mdx.md)|別名[StdevP &#40;MDX&#41;](../mdx/stdevp-mdx.md)します。|  
|[Stdev &#40;MDX&#41;](../mdx/stdev-mdx.md)|バイアスをかけない母集団の公式を使用し、セットに対して評価される数値式のサンプル標準偏差を返します。|  
|[StdevP &#40;MDX&#41;](../mdx/stdevp-mdx.md)|バイアスをかけた母集団の公式を使用して、セットに対して評価される数値式の母標準偏差を返します。|  
|[StrToValue &#40;MDX&#41;](../mdx/strtovalue-mdx.md)|MDX 形式の文字列によって指定された値を返します。|  
|[Sum &#40;MDX&#41;](../mdx/sum-mdx.md)|セットに対して評価される数値式の合計を返します。|  
|[Value &#40;MDX&#41;](../mdx/value-mdx.md)|メジャーの値を返します。|  
|[Var &#40;MDX&#41;](../mdx/var-mdx.md)|バイアスをかけない母集団の公式を使用して、セットに対して評価される数値式のサンプル分散を返します。|  
|[Variance &#40;MDX&#41;](../mdx/variance-mdx.md)|別名[Var &#40;MDX&#41;](../mdx/var-mdx.md)します。|  
|[VarianceP &#40;MDX&#41;](../mdx/variancep-mdx.md)|別名[VarP &#40;MDX&#41;](../mdx/varp-mdx.md)します。|  
|[VarP &#40;MDX&#41;](../mdx/varp-mdx.md)|バイアスをかけた母集団の公式を使用して、セットに対して評価される数値式の母分散を返します。|  
  
## <a name="set-functions"></a>集合関数  
  
|関数|説明|  
|--------------|-----------------|  
|[AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)|指定されたセットに計算されるメンバーを追加することによって生成されるセットを返します。|  
|[AllMembers &#40;MDX&#41;](../mdx/allmembers-mdx.md)|指定されたディメンション、階層、またはレベルの計算されるメンバーを含むすべてのメンバーを含むセットを返します。|  
|[Ancestor &#40;MDX&#41;](../mdx/ancestors-mdx.md)|メンバーの先祖のうち、指定されたレベルまたは距離にあるすべての先祖のセットを返します。|  
|[Ancestor &#40;MDX&#41;](../mdx/ascendants-mdx.md)|指定されたメンバー自体も含めたメンバーの先祖のセットを返します。|  
|[Axis &#40;MDX&#41;](../mdx/axis-mdx.md)|軸で定義されているセットを返します。|  
|[BottomCount &#40;MDX&#41;](../mdx/bottomcount-mdx.md)|セットを昇順に並べ替え、値の小さい方から指定された数の組を返します。|  
|[BottomPercent &#40;MDX&#41;](../mdx/bottompercent-mdx.md)|セットを昇順で並べ替え、累積合計が同じか、または指定されたパーセンテージより小さい最小値を持つタプルのセットを返します。|  
|[BottomSum &#40;MDX&#41;](../mdx/bottomsum-mdx.md)|セットを昇順で並べ替え、合計が指定された値以下になるように、値の小さい方から組のセットを作成して返します。|  
|[Children &#40;MDX&#41;](../mdx/children-mdx.md)|指定されたメンバーの子メンバーを返します。|  
|[Crossjoin &#40;MDX&#41;](../mdx/crossjoin-mdx.md)|1 つ以上のセットのクロス積を返します。|  
|[CurrentOrdinal &#40;MDX&#41;](../mdx/currentordinal-mdx.md)|イテレーション中に、セット内の現在のイテレーション数を返します。|  
|[Descendants &#40;MDX&#41;](../mdx/descendants-mdx.md)|他のレベルの子孫を除外したり、指定されたレベルまたは距離にあるメンバーの子孫のセットを返します。|  
|[Distinct &#40;MDX&#41;](../mdx/distinct-mdx.md)|指定されたセットから重複した組を削除して、セットを返します。|  
|[DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)|1 つのレベル、セットの最下位レベル下に、または 1 つのレベルを必要に応じて指定したレベル、セットで表されるメンバーの下に一連のメンバーをドリル ダウンします。|  
|[DrilldownLevelBottom &#40;MDX&#41;](../mdx/drilldownlevelbottom-mdx.md)|1 レベル下に、指定したレベル、セットの最下位メンバーをドリル ダウンします。|  
|[DrilldownLevelTop &#40;MDX&#41;](../mdx/drilldownleveltop-mdx.md)|1 レベル下に、指定したレベル、セットの最上位メンバーをドリル ダウンします。|  
|[DrilldownMember &#40;MDX&#41;](../mdx/drilldownmember-mdx.md)|2 番目に指定されたセット内に存在する、指定されたセットのメンバーをドリル ダウンします。 または、関数をドリル ダウン組のセット。|  
|[DrilldownMemberBottom &#40;MDX&#41;](../mdx/drilldownmemberbottom-mdx.md)|2 番目の指定されたセットに存在する、指定されたセット メンバーをドリルダウンするは、結果を制限することを指定したメンバーの設定。 また、この関数をドリル ダウン組のセット。|  
|[DrilldownMemberTop &#40;MDX&#41;](../mdx/drilldownmembertop-mdx.md)|2 番目の指定されたセットに存在する、指定されたセット メンバーをドリルダウンするは、結果を制限することを指定したメンバーの設定。 また、この関数をドリル ダウン組のセット。|  
|[DrillupLevel &#40;MDX&#41;](../mdx/drilluplevel-mdx.md)|セットのメンバーのうち、指定されたレベルの下位に属するメンバーをドリル アップします。|  
|[DrillupMember &#40;MDX&#41;](../mdx/drillupmember-mdx.md)|2 番目に指定したセットに存在するメンバーを指定したセットにドリル アップします。|  
|[Except &#40;MDX&#41;](../mdx/except-mdx-function.md)|2 つのセットの差異を検出します。重複部分を保持することも可能です。|  
|[Exists &#40;MDX&#41;](../mdx/exists-mdx.md)|その他の 1 つまたは複数のセットの 1 つまたは複数の組、セットのいずれかのメンバーのセットを返しますが存在します。|  
|[Extract &#40;MDX&#41;](../mdx/extract-mdx.md)|抽出したディメンション要素から組のセットを返します。|  
|[Filter &#40;MDX&#41;](../mdx/filter-mdx.md)|検索条件に基づいて、指定されたセットをフィルター処理の結果セットを返します。|  
|[Generate &#40;MDX&#41;](../mdx/generate-mdx.md)|あるセットを別のセットの各メンバーに適用し、その結果セットを和集合で結合します。 また、この関数は、セットに対して文字列式を評価することによって作成される連結文字列を返します。|  
|[Head &#40;MDX&#41;](../mdx/head-mdx.md)|重複部分を保持しながら、セット内の最初の指定数の要素を返します。|  
|[Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)|階層内の一連のメンバーを並べ替えます。|  
|[交差&#40;MDX&#41;](../mdx/intersect-mdx.md)|必要に応じて重複部分を保持、2 つの入力セットの積集合を返します。|  
|[LastPeriods &#40;MDX&#41;](../mdx/lastperiods-mdx.md)|指定したメンバーを含むメンバーのセットを返します。|  
|[Members &#40;設定&#41; &#40;MDX&#41;](../mdx/members-set-mdx.md)|ディメンション、レベル、または階層でメンバーのセットを返します。|  
|[Mtd &#40;MDX&#41;](../mdx/mtd-mdx.md)|時間ディメンションの年 (Year) レベルという制約の中で、指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。先頭は最初の兄弟、末尾は指定されたメンバーになります。|  
|[NameToSet &#40;MDX&#41;](../mdx/nametoset-mdx.md)|MDX 形式の文字列によって指定されたメンバーを含むセットを返します。|  
|[NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)|1 つ以上のセットのクロス積を 1 つのセットとして返します。ただし、空の組と、ファクト テーブル データに関連付けられていない組は含まれません。|  
|[Order &#40;MDX&#41;](../mdx/order-mdx.md)|保持したり、階層を変更するオプションで指定したセットのメンバーを並べ替えます。|  
|[PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)|時間ディメンションで指定されているレベル内で、指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。先頭は最初の兄弟、末尾は指定されたメンバーになります。|  
|[Qtd &#40;MDX&#41;](../mdx/qtd-mdx.md)|以降で最初の兄弟、という制約の指定したメンバーで終わる、指定されたメンバーと同じレベルのメンバーの兄弟のセットを返します、*四半期*時間ディメンション内のレベル。|  
|[Siblings &#40;MDX&#41;](../mdx/siblings-mdx.md)|指定されたメンバー自体を含めて、メンバーの兄弟を返します。|  
|[StripCalculatedMembers &#40;MDX&#41;](../mdx/stripcalculatedmembers-mdx.md)|指定したセットから計算されるメンバーを削除することによって生成されるセットを返します。|  
|[StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)|MDX 形式の文字列によって指定されたセットを返します。|  
|[Subset &#40;MDX&#41;](../mdx/subset-mdx.md)|指定したセットから組のサブセットを返します。|  
|[Tail &#40;MDX&#41;](../mdx/tail-mdx.md)|セットの末尾からサブセットを返します。|  
|[ToggleDrillState &#40;MDX&#41;](../mdx/toggledrillstate-mdx.md)|メンバーのドリル状態を切り替えます。|  
|[TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)|セットを降順で並べ替えおよび指定した数の最大値を持つ要素を返します。|  
|[TopPercent &#40;MDX&#41;](../mdx/toppercent-mdx.md)|セットを降順で並べ替え、累積合計が指定された割合以下になるように、値の大きい方から組のセットを作成して返します。|  
|[TopSum &#40;MDX&#41;](../mdx/topsum-mdx.md)|セットを並べ替え、累積合計が指定された値以上に最上位の要素を返します。|  
|[Union &#40;MDX&#41;](../mdx/union-mdx.md)|必要に応じて重複部分を保持、2 つのセットの和集合を返します。|  
|[Unorder &#40;MDX&#41;](../mdx/unorder-mdx.md)|適用済みの順序指定されたセットから削除します。|  
|[VisualTotals &#40;MDX&#41;](../mdx/visualtotals-mdx.md)|必要に応じて結果のセル セット内の親メンバーの名前のパターンを使用して、指定されたセット内の子メンバーの合計を動的に生成されるセットを返します。|  
|[Wtd &#40;MDX&#41;](../mdx/wtd-mdx.md)|時間ディメンションの週 (Week) レベルという制約の中で、指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。先頭は最初の兄弟、末尾は指定されたメンバーになります。|  
|[Ytd &#40;MDX&#41;](../mdx/ytd-mdx.md)|以降で最初の兄弟、という制約の指定したメンバーで終わる、指定されたメンバーと同じレベルのメンバーの兄弟のセットを返します、*年*時間ディメンション内のレベル。|  
  
## <a name="string-functions"></a>文字列関数  
  
|関数|説明|  
|--------------|-----------------|  
|[CalculationPassValue (MDX)](../mdx/calculationpassvalue-mdx.md)|キューブの指定された計算パスを評価し、MDX 式の値を返します。|  
|[CoalesceEmpty &#40;MDX&#41;](../mdx/coalesceempty-mdx.md)|空のセル値を数値または文字列に連結し、結合された値を返します。|  
|[Generate &#40;MDX&#41;](../mdx/generate-mdx.md)|あるセットを別のセットの各メンバーに適用し、その結果セットを和集合で結合します。 また、この関数は、セットに対して文字列式を評価することによって作成される連結文字列を返します。|  
|[IIf &#40;MDX&#41;](../mdx/iif-mdx.md)|論理テストによって判別される 2 つの値の 1 つを返します。|  
|[LookupCube &#40;MDX&#41;](../mdx/lookupcube-mdx.md)|同じデータベース内で別に指定されたキューブに対して評価される MDX 式の値を返します。|  
|[MemberToStr &#40;MDX&#41;](../mdx/membertostr-mdx.md)|指定されたメンバーに対応する MDX 形式の文字列を返します。|  
|[Name &#40;MDX&#41;](../mdx/name-mdx.md)|ディメンション、階層、レベル、またはメンバーの名前を返します。|  
|[Properties &#40;MDX&#41;](../mdx/properties-mdx.md)|メンバー プロパティ値を含む文字列または厳密に型指定された値を返します。|  
|[SetToStr &#40;MDX&#41;](../mdx/settostr-mdx.md)|指定されたセットに対応してその MDX 形式の文字列を返します。|  
|[TupleToStr &#40;MDX&#41;](../mdx/tupletostr-mdx.md)|指定された組に対応する MDX 形式の文字列を返します。|  
|[UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)|指定されたディメンション、階層、レベル、メンバーの一意の名前を返します。|  
|[Username &#40;MDX&#41;](../mdx/username-mdx.md)|現在の接続のユーザー名とドメインの名前を返します。|  
  
## <a name="subcube-functions"></a>サブキューブ関数  
  
|関数|説明|  
|--------------|-----------------|  
|[This &#40;MDX&#41;](../mdx/this-mdx.md)|現在のサブキューブを返します。|  
|[Leaves &#40;MDX&#41;](../mdx/leaves-mdx.md)|指定されたディメンション、メンバー、または組には、リーフ メンバーのセットを返します。|  
  
## <a name="tuple-functions"></a>組関数  
  
|関数|説明|  
|--------------|-----------------|  
|[Current &#40;MDX&#41;](../mdx/current-mdx.md)|イテレーション中に、セットから現在の組を返します。|  
|[Item &#40;組&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)|セットから組を返します。|  
|[Root &#40;MDX&#41;](../mdx/root-mdx.md)|構成される組を返します、**すべて**キューブ、ディメンション、または組には、各属性階層のメンバー。|  
|[StrToTuple &#40;MDX&#41;](../mdx/strtotuple-mdx.md)|MDX 形式の文字列によって指定された組を返します。|  
  
## <a name="other-functions"></a>その他の関数  
  
|関数|説明|  
|--------------|-----------------|  
|[Error &#40;MDX&#41;](../mdx/error-mdx.md)|必要に応じて指定したエラー メッセージを提供するエラーが発生します。|  
  
## <a name="see-also"></a>関連項目  
 [MDX 言語リファレンス &#40;MDX&#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
