---
title: RowNumber 関数 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d4a06a24525b3d9d0c4e4a5f3f0b749a7db70261
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105166"
---
# <a name="rownumber-function-report-builder-and-ssrs"></a>RowNumber 関数 (レポート ビルダーおよび SSRS)
  指定されたスコープの実行中の行数を返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>構文  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *スコープ (scope)*  
 (`String`) 行数を評価するコンテキストを示すデータセット、データ領域、またはグループの名前か、NULL ([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] では `Nothing`) です。 `Nothing` は、最も外側のコンテキスト (通常はレポート データセット) を示します。  
  
## <a name="remarks"></a>コメント  
 `RowNumber` 同様に、指定したスコープ内の行のカウントの実行中の値を返します[RunningValue](report-builder-functions-runningvalue-function.md)集計関数の実行中の値を返します。 スコープを指定すると、行数を 1 にリセットするタイミングが指定されます。  
  
 *scope* には、式を指定することはできません。 *scope* には、コンテナー スコープを指定する必要があります。 一般的なスコープは、外側から内側の順に、レポート データセット、データ領域、行グループまたは列グループです。  
  
 列全体で値を増分するには、列グループの名前であるスコープを指定します。 行の下方向に向かって数を増分するには、行グループの名前であるスコープを指定します。  
  
> [!NOTE]  
>  行グループと列グループの両方を指定する複数の集計を含めた式はサポートされていません。  
  
 詳細については、「[集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)」および「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
## <a name="code-example"></a>コード例  
 Tablix データ領域の詳細行の `BackgroundColor` プロパティに使用できる式を次に示します。この式では、各グループの詳細行の色を交互に設定し、常に先頭が白になるようにしています。  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>参照  
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
