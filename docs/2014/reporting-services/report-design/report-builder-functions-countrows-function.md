---
title: CountRows 関数 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5b1c403d-6afd-44c8-b5f6-5ecff2a29a45
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f3414498d0ce399607ab0faa1a438dad88efc35c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105279"
---
# <a name="countrows-function-report-builder-and-ssrs"></a>CountRows 関数 (レポート ビルダーおよび SSRS)
  NULL 値の行を含めて、指定されたスコープ内の行数を返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>構文  
  
```  
  
CountRows(scope, recursive)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *スコープ (scope)*  
 (`String`) カウントするレポート アイテムを含むデータセット、データ領域、またはグループの名前です。  
  
 *再帰*  
 (**列挙型**) 省略可。 `Simple` (既定値) または `RdlRecursive` です。 集計を再帰的に実行するかどうかを指定します。  
  
## <a name="return-type"></a>戻り値の型  
 `Integer` 値を返します。  
  
## <a name="remarks"></a>コメント  
 `CountRows` は、指定されたスコープ内のすべての行 (NULL 値を持つ行を含む) をカウントします。  
  
 *scope* の値には、式を指定することができません。また、この値では、現在のスコープまたはコンテナー スコープを参照する必要があります。  
  
 詳細については、「[集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)」および「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
 再帰的集計については、「[複数の再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例では、(式 `GroupbyCategory` に基づいた) `[Category]`という名前の行グループ内の行数を計算する式を示します。  
  
```  
="Number of rows: " & CountRows("GroupbyCategory")  
```  
  
## <a name="see-also"></a>関連項目  
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
