---
title: Previous 関数 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 540bf8367ba32fbebe4e27ee6e2cd3e1aa01ae0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105199"
---
# <a name="previous-function-report-builder-and-ssrs"></a>Previous 関数 (レポート ビルダーおよび SSRS)
  アイテムの、指定されたスコープ内の直前のインスタンスに対応する値または指定された集計値を返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>構文  
  
```  
  
Previous(expression, scope)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *式 (expression)*  
 (`Variant` または `Binary`) データを識別し、直前の値を取得するための式 (`Fields!Fieldname.Value` や `Sum(Fields!Fieldname.Value)` など) です。  
  
 *スコープ (scope)*  
 (`String`) 省略可。 グループまたはデータ領域、または null の名前 (`Nothing`で[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])、によって指定された以前の値を取得する対象のスコープを指定する*式*します。  
  
## <a name="return-type"></a>戻り値の型  
 `Variant` または `Binary` 値を返します。  
  
## <a name="remarks"></a>コメント  
 `Previous` 関数は、すべての並べ替えおよびフィルター処理が適用された後、指定されたスコープで評価された式の直前の値を返します。  
  
 場合*式*集計が含まれていない、`Previous`既定値は、レポート アイテムの現在のスコープに機能します。  
  
 詳細グループで、直前の詳細行のフィールド参照の値を指定するには `Previous` を使用します。  
  
> [!NOTE]  
>  `Previous`関数では、詳細グループでフィールドへの参照のみがサポートしています。 たとえば、詳細グループのテキスト ボックスの場合、 `=Previous(Fields!Quantity.Value)` では、直前の行から `Quantity` フィールドのデータが返されます。 この式が先頭行にある場合は、NULL ([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] では `Nothing`) が返されます。  
  
 場合*式*既定のスコープを使用する集計関数を含んで`Previous`集計関数の呼び出しに指定されたスコープの直前のインスタンス内のデータを集計します。  
  
 場合*式*、既定以外のスコープを指定する集計関数が含まれています、*スコープ*のパラメーター、`Previous`関数で指定されたスコープのコンテナー スコープを指定する必要があります集計関数の呼び出し。  
  
 関数は、 `Level`、 `InScope`、`Aggregate`と`Previous`では使用できません、*式*パラメーター。 集計関数に *recursive* パラメーターを指定することはサポートされていません。  
  
 詳細については、「[集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)」および「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="description"></a>説明  
 次のコード例は、データ領域の既定のデータ行に配置されると、直前の行の `LineTotal` フィールドの値が表示されます。  
  
### <a name="code"></a>コード  
  
```  
=Previous(Fields!LineTotal.Value)  
```  
  
### <a name="description"></a>説明  
 次の例では、特定の月日の売上合計と、前年のその月日の値を計算する式を示します。 この式は、子グループ `GroupbyDay`に属する行内のセルに追加されます。 その親グループは `GroupbyMonth`で、このグループの親グループは `GroupbyYear`です。 この式では、GroupbyDay (既定のスコープ) の結果、次に `GroupbyYear` (親グループ `GroupbyMonth`の親) の結果が表示されます。  
  
 たとえば、親グループが `Year`、その子グループが `Month`、そのまた子グループが `Day` という名前のデータ領域 (入れ子レベル 3) の場合、 グループ `=Previous(Sum(Fields!Sales.Value,"Day"),"Year")` に関連付けられた行内の式 `Day` は、前年の同じ月日の売上高の値を返します。  
  
### <a name="code"></a>コード  
  
```  
=Sum(Fields!Sales.Value) & " " & Previous(Sum(Fields!Sales.Value,"GroupbyDay"),"GroupbyYear")  
```  
  
## <a name="see-also"></a>関連項目  
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
