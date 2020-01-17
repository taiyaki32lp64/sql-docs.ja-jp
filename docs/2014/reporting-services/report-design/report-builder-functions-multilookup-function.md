---
title: Multilookup 関数 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1fec079e-33b3-4e4d-92b3-6b4d06a49a77
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e6a60f1b47c7015fa0fca27cc7ce68bf4d04b15d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105212"
---
# <a name="multilookup-function-report-builder-and-ssrs"></a>Multilookup 関数 (レポート ビルダーおよび SSRS)
  名前と値のペアを含むデータセットから、指定された名前のセットに最初に一致した値のセットを返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>構文  
  
```  
  
Multilookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *source_expression*  
 (`VariantArray`) 現在のスコープ内で評価される式。参照する名前またはキーのセットを指定します。 たとえば、複数値パラメーターの場合、 `=Parameters!IDs.value`のように指定します。  
  
 *destination_expression*  
 (`Variant`) データセット内の各行に対して評価される式。照合する名前またはキーを指定します。 たとえば、`=Fields!ID.Value` のようにします。  
  
 *result_expression*  
 (`Variant`) データセット内の行に対して評価される式を*source_expression* = *destination_expression*、取得する値を指定します。 たとえば、`=Fields!Name.Value` のようにします。  
  
 *データセット (dataset)*  
 レポート内のデータセットの名前を指定する定数。 たとえば、"Colors" と指定します。  
  
## <a name="return"></a>戻り値  
 `VariantArray` を返します。一致する結果がなかった場合は、`Nothing` を返します。  
  
## <a name="remarks"></a>コメント  
 データセットで、名前と値の各ペアに 1 対 1 のリレーションシップが存在する場合、`Multilookup` を使用して一連の値を取得します。 `MultiLookup` は、一連の名前またはキーに対して `Lookup` を呼び出すことと同じです。 たとえば、主キー識別子に基づく複数値パラメーターの場合、テーブルのテキスト ボックス内の式で `Multilookup` を使用して、パラメーターまたはテーブルにバインドされていないデータセットから、関連付けられている値を取得することができます。  
  
 `Multilookup` を実行すると、次の処理が行われます。  
  
-   現在のスコープ内でソース式が評価され、variant オブジェクトの配列が生成されます。  
  
-   配列内の各オブジェクトに対して [Lookup 関数 &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-lookup-function.md) が呼び出され、返される配列に結果が追加されます。  
  
-   結果セットが返されます。  
  
 指定した名前に対応する、名前と値のペアを含むデータセットに 1 対 1 のリレーションシップが存在する場合、このデータセットから 1 つの値を取得するには、[Lookup 関数 &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-lookup-function.md) を使用します。 指定した名前に対応する、名前と値のペアを含むデータセットに 1 対多のリレーションシップが存在する場合、このデータセットから複数の値を取得するには、[LookupSet 関数 &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-lookupset-function.md) を使用します。  
  
 次の制限があります。  
  
-   `Multilookup` は、すべてのフィルター式が適用された後で評価されます。  
  
-   1 レベルの参照のみがサポートされます。 変換元、変換先、または結果の式に、Lookup 関数への参照を含めることはできません。  
  
-   変換元および変換先の式は、同じデータ型として評価される必要があります。  
  
-   変換元、変換先、結果の式には、レポート変数またはグループ変数への参照を含めることができません。  
  
-   `Multilookup` は、次のレポート アイテムを求める式として使用することはできません。  
  
    -   データ ソースの動的な接続文字列。  
  
    -   データセット内の計算フィールド。  
  
    -   データセット内のクエリ パラメーター。  
  
    -   データセット内のフィルター。  
  
    -   レポート パラメーター。  
  
    -   Report.Language プロパティ。  
  
 詳細については、「[集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)」および「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
## <a name="example"></a>例  
 "Category" というデータセットに、CategoryList フィールドが含まれているとします。このフィールドには、コンマ区切りのカテゴリの識別子のリスト ("2, 4, 2, 1" など) が含まれています。  
  
 CategoryNames データセットには、次の表に示すように、カテゴリ識別子とカテゴリ名が格納されています。  
  
|ID|名前|  
|--------|----------|  
|1|Accessories|  
|2|Bikes|  
|3|Clothing|  
|4|コンポーネント|  
  
 識別子のリストに対応する名前を参照するには、`Multilookup` を使用します。 まず、リストを文字列の配列に分割する必要があります。次に、`Multilookup` を呼び出してカテゴリ名を取得し、結果を連結して文字列にします。  
  
 Category データセットにバインドされているデータ領域内のテキスト ボックスに次の式を置いた場合、"Bikes, Components, Bikes, Accessories" と表示されます。  
  
```  
=Join(MultiLookup(Split(Fields!CategoryList.Value,","),  
   Fields!CategoryID.Value,Fields!CategoryName.Value,"Category")),  
   ", ")  
```  
  
## <a name="example"></a>例  
 ProductColors データセットに、次の表に示すように色の識別子のフィールドである ColorID と、色の値のフィールドである Color が含まれているとします。  
  
|ColorID|色|  
|-------------|-----------|  
|1|[赤]|  
|2|[青]|  
|3|[緑]|  
  
 複数値パラメーターである *MyColors* が、使用可能な値について、データセットにバインドされていないとします。 このパラメーターの既定値は、2 および 3 に設定されています。 次の式をテーブル内のテキスト ボックスに置いた場合、パラメーターの複数選択された値がコンマ区切りの一覧として連結され、"Blue, Green" と表示されます。  
  
```  
=Join(MultiLookup(Parameters!MyColors.Value,Fields!ColorID.Value,Fields!Color.Value,"ProductColors"),", ")  
```  
  
## <a name="see-also"></a>参照  
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
