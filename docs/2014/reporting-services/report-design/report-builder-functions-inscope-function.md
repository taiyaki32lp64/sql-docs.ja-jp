---
title: InScope 関数 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 84f9b681ee632e922f5ab349bf1a72fbea63f911
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105250"
---
# <a name="inscope-function-report-builder-and-ssrs"></a>InScope 関数 (レポート ビルダーおよび SSRS)
  アイテムの現在のインスタンスが、指定したスコープ内にあるかどうかを示します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>構文  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *スコープ (scope)*  
 (`String`) スコープを指定するデータセット、データ領域、またはグループの名前です。  
  
## <a name="return-type"></a>戻り値の型  
 `Boolean` を返します。  
  
## <a name="remarks"></a>コメント  
 `InScope`関数で指定されたスコープ内のメンバーシップのレポート アイテムの現在のインスタンスのスコープのテスト、*スコープ*パラメーター。  
  
 *Scope* には、式を指定することはできません。  
  
 `InScope` 関数は、通常、動的スコープを利用するデータ領域で使用されます。 たとえば、`InScope` をデータ領域のセル内のドリルスルー リンクに使用して、クリックされたセルに応じて異なるレポート名とパラメーター セットが返されるようにすることができます。 この例を以下に示します。  
  
-   次の式では、ドリルスルー リンクのレポート名として使用し、 `ProductDetail` グループ内のセルがクリックされた場合は `Month` レポートが開き、それ以外のセルがクリックされた場合は `ProductSummary` レポートが開くようにしています。  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   次の式では、詳細レポート パラメーターの `Omit` プロパティに使用し、`Product` グループ内のセルがクリックされた場合のみ、目的のレポートにパラメーターが渡されるようにしています。  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 詳細については、「[集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)」および「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例では、アイテムの現在のインスタンスが、 `Product` データセット、データ領域、またはグループのスコープにあるかどうかが示されます。  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>参照  
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
