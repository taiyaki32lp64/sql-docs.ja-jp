---
title: Min 関数 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: aa1ee96f-9fc4-4775-b9d4-c6187dc37e27
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c620c8cc4f3ddaaa0cddd261cf5c42f111763ed1
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287670"
---
# <a name="min-function-report-builder-and-ssrs"></a>Min 関数 (レポート ビルダーおよび SSRS)
  指定されたスコープのコンテキストで、式で指定された NULL 以外のすべての数値の中から最小値を返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>構文  
  
```  
  
Min(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *式 (expression)*  
 (`Variant`) この集計関数の実行対象の式です。  
  
 *スコープ (scope)*  
 (`String`) 省略可。 集計関数の適用先となるレポート アイテムを含むデータセット、グループ、またはデータ領域の名前です。 *scope* を指定しない場合、現在のスコープが使用されます。  
  
 *再帰*  
 (**列挙型**) 省略可。 `Simple` (既定値) または `RdlRecursive` です。 集計を再帰的に実行するかどうかを指定します。  
  
## <a name="return-type"></a>戻り値の型  
 式の型によって決まります。  
  
## <a name="remarks"></a>コメント  
 式で指定されたデータセットは、同じデータ型である必要があります。 複数の数値データ型のデータを同じデータ型に変換するには、`CInt`、`CDbl`、`CDec` などの変換関数を使用します。 詳細については、「 [データ型変換関数](https://go.microsoft.com/fwlink/?LinkId=96142)」を参照してください。  
  
 *scope* の値は文字列定数である必要があり、式にすることはできません。 外部の集計または他の集計を指定しない集計では、 *scope* は現在のスコープまたはコンテナー スコープを参照する必要があります。 集計の集計では、入れ子になった集計に、子のスコープを指定できます。  
  
 *Expression* には、入れ子になった集計関数への呼び出しを含めることができます。ただし、次に示すように、これには例外および条件があります。  
  
-   入れ子集計の*Scope* は、外部集計のスコープと同じであるか、そのスコープに含まれている必要があります。 式内のすべてのスコープについては、1 つのスコープがそれ以外のすべてのスコープに対する子であるようなリレーションシップが必要です。  
  
-   入れ子集計の*Scope* には、データセット名は使用できません。  
  
-   *式*する必要がありますが含まれていない`First`、 `Last`、 `Previous`、または`RunningValue`関数。  
  
-   *Expression* には、 *recursive*を指定する入れ子集計を含めることができません。  
  
 詳細については、「[集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)」および「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
 再帰的集計については、「[複数の再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例では、現在のスコープの合計のうち最小値が返されます。  
  
```  
=Min(Fields!OrderTotal.Value)  
```  
  
## <a name="see-also"></a>参照  
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
