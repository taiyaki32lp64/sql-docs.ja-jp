---
title: RunningValue 関数 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6bee2f15-0e69-49c8-9689-b04544063b1d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a72673641fc0f67e22d88d5ea104089b273dedce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105159"
---
# <a name="runningvalue-function-report-builder-and-ssrs"></a>RunningValue 関数 (レポート ビルダーおよび SSRS)
  式で指定された NULL 以外のすべての数値の実行中の集計を、指定されたスコープに対して評価して返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>構文  
  
```  
  
RunningValue(expression, function, scope)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *式 (expression)*  
 この集計関数の実行対象の式です ( `[Quantity]`など)。  
  
 *function*  
 (`Enum`) 式に適用する集計関数の名前です (`Sum` など)。 この関数は、`RunningValue`、`RowNumber`、または `Aggregate` にすることはできません。  
  
 *スコープ (scope)*  
 (`String`) 集計を評価するコンテキストを示すデータセット、データ領域、またはグループの名前である文字列定数か、NULL ([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] では `Nothing`) です。 `Nothing` は、最も外側のコンテキスト (通常はレポート データセット) を示します。  
  
## <a name="return-type"></a>戻り値の型  
 *function* パラメーターに指定された集計関数によって決まります。  
  
## <a name="remarks"></a>コメント  
 `RunningValue` の値は、スコープの新しいインスタンスごとに 0 にリセットされます。 グループが指定された場合は、累計値はグループ式の変更時にリセットされます。 データ領域が指定された場合は、累計値はデータ領域の新しいインスタンスごとにリセットされます。 データセットが指定された場合は、累計値はデータセット全体にわたってリセットされません。  
  
 `RunningValue` は、フィルター式または並べ替え式では使用できません。  
  
 実行中の値が計算される一連のデータは、同じデータ型である必要があります。 複数の数値データ型のデータを同じデータ型に変換するには、`CInt`、`CDbl`、`CDec` などの変換関数を使用します。 詳細については、「 [データ型変換関数](https://go.microsoft.com/fwlink/?LinkId=96142)」を参照してください。  
  
 *Scope* には、式を指定することはできません。  
  
 *Expression* には、入れ子になった集計関数への呼び出しを含めることができます。ただし、次に示すように、これには例外および条件があります。  
  
-   入れ子集計のスコープは、外部集計のスコープと同じであるか、そのスコープに含まれている必要があります。 式内のすべてのスコープについては、1 つのスコープがそれ以外のすべてのスコープに対する子であるようなリレーションシップが必要です。  
  
-   入れ子集計のスコープには、データセット名は使用できません。  
  
-   *式*する必要がありますが含まれていない`First`、 `Last`、 `Previous`、または`RunningValue`関数。  
  
-   *Expression* には、 *recursive*を指定する入れ子集計を含めることができません。  
  
 行数の累計値を計算するには、`RowNumber` を使用します。 詳細については、「[RowNumber 関数 &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-rownumber-function.md)」を参照してください。  
  
 詳細については、「[集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)」および「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
 再帰的集計については、「[複数の再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次のコード例では、最も外側のスコープ (データセット) の `Cost` フィールドの累計が返されます。  
  
```  
=RunningValue(Fields!Cost.Value, Sum, Nothing)  
```  
  
 次のコード例では、 `Score` データセットの `DataSet1`フィールドの累計が返されます。  
  
```  
=RunningValue(Fields!Score.Value,sum,"DataSet1")  
```  
  
 次のコード例では、最も外側のスコープの `Traffic Charges` フィールドの累計が返されます。  
  
```  
=RunningValue(Fields!Traffic Charges.Value, Sum, Nothing)  
```  
  
## <a name="see-also"></a>関連項目  
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
