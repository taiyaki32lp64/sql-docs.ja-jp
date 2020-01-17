---
title: Lookup 関数 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: e60e5bab-b286-4897-9685-9ff12703517d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 333c75f3ca10d1ed6ecd738a3dc76a32a53305c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579582"
---
# <a name="report-builder-functions---lookup-function"></a>レポート ビルダー関数 - Lookup 関数
  名前と値のペアを含むデータセットから、指定された名前に最初に一致した値を返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>構文  
  
```  
  
Lookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *source_expression*  
 (**Variant**) 現在のスコープ内で評価される式。参照する名前またはキーを指定します。 たとえば、`=Fields!ProdID.Value` のようになります。  
  
 *destination_expression*  
 (**Variant**) データセット内の各行に対して評価される式。照合する名前またはキーを指定します。 たとえば、 `=Fields!ProductID.Value`のようにします。  
  
 *result_expression*  
 (**Variant**) *source_expression* = *destination_expression*であるデータセットの行で評価され、取得する値を指定する式。 たとえば、`=Fields!ProductName.Value` のようになります。  
  
 *データセット (dataset)*  
 レポート内のデータセットの名前を指定する定数。 たとえば、"Products" などです。  
  
## <a name="return"></a>戻り値  
 **Variant**を返します。一致する結果がなかった場合は、 **Nothing** を返します。  
  
## <a name="remarks"></a>Remarks  
 指定したデータセットで、名前と値のペアについて 1 対 1 のリレーションシップが存在する場合、 **Lookup** を使用して値を取得します。 たとえば、テーブル内の ID フィールドに対して **Lookup** を使用して、データ領域にバインドされていないデータセットから対応する Name フィールドを取得することができます。  
  
 **Lookup** を実行すると、次の処理が行われます。  
  
-   ソースの式を現在のスコープ内で評価します。  
  
-   フィルターを適用した後で、指定されたデータセットの照合順序に基づき、指定されたデータセットの各行に対して変換先の式を評価します。  
  
-   変換元の式と変換先の式が最初に一致したときに、データセット内のその行に対して結果式を評価します。  
  
-   結果式の値を返します。  
  
 1 対多のリレーションシップがある場合、1 つの名前フィールドまたはキー フィールドに対応する複数の値を取得するには、[LookupSet 関数 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookupset-function.md) を使用します。 一連の値に対して **Lookup** を呼び出すには、[Multilookup 関数 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-builder-functions-multilookup-function.md) を使用します。  
  
 次の制限があります。  
  
-   **Lookup** は、すべてのフィルター式が適用された後で評価されます。  
  
-   1 レベルの参照のみがサポートされます。 変換元、変換先、または結果の式に、Lookup 関数への参照を含めることはできません。  
  
-   変換元および変換先の式は、同じデータ型として評価される必要があります。 戻り値の型は、評価された結果式のデータ型と同じです。  
  
-   変換元、変換先、結果の式には、レポート変数またはグループ変数への参照を含めることができません。  
  
-   **Lookup** は、次のレポート アイテムを求める式として使用することはできません。  
  
    -   データ ソースの動的な接続文字列。  
  
    -   データセット内の計算フィールド。  
  
    -   データセット内のクエリ パラメーター。  
  
    -   データセット内のフィルター。  
  
    -   レポート パラメーター。  
  
    -   Report.Language プロパティ。  
  
 詳細については、「[集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)」および「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、製品の識別子である ProductID のフィールドを含むデータセットにテーブルがバインドされているとします。 別のデータセットである "Product" には、対応する製品識別子 ID と、製品名を表す Name が含まれています。  
  
 次の式では、 **Lookup** を使用して "Product" データセットの各行に含まれる ID と ProductID の値を比較し、一致が見つかった場合には、その行の Name フィールドの値を返します。  
  
```  
=Lookup(Fields!ProductID.Value, Fields!ID.Value, Fields!Name.Value, "Product")  
```  
  
## <a name="see-also"></a>参照  
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
