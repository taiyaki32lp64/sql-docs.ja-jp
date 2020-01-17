---
title: プロパティをフィルター処理 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ff06bc27e765945d1cca74b5f8401e0caadf6b17
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918635"
---
# <a name="filter-property"></a>Filter プロパティ
内のデータのフィルターを示します、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値

設定または取得を**バリアント**値で、次の項目の 1 つ含めることができます。  
  
-   **条件の文字列。** 1 つ以上の各句を使用して、連結から成る文字列**AND**または**OR**演算子。  
  
-   **ブックマークの配列。** 一意のブックマークの配列値内のレコードを指す、 **Recordset**オブジェクト。  
  
-   A [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)値。  
  
## <a name="remarks"></a>コメント

使用して、**フィルター**プロパティ内のレコードを選択して画面を**Recordset**オブジェクト。 フィルター処理された**Recordset**現在のカーソルになります。 その他の値を返すプロパティが現在に基づいて**カーソル**など、影響は[AbsolutePosition プロパティ (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)、 [AbsolutePage プロパティ (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)、 [RecordCount プロパティ (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)、および[PageCount プロパティ (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)します。 設定、**フィルター**プロパティを特定の新しい値に新しい値を満たす最初のレコードを現在のレコードを移動します。
  
フォーム内の句の条件の文字列から成る*FieldName-演算子-値*(たとえば、 `"LastName = 'Smith'"`)。 個々 の句を連結して複合句を作成することができます**AND** (たとえば、 `"LastName = 'Smith' AND FirstName = 'John'"`) または**OR** (たとえば、 `"LastName = 'Smith' OR LastName = 'Jones'"`)。 条件文字列の場合は、次のガイドラインを使用します。

-   *FieldName*から有効なフィールド名にする必要があります、 **Recordset**します。 フィールド名にスペースが含まれている場合は、角かっこで名前を囲む必要があります。  
  
-   演算子は、次のいずれかを指定する必要があります: \<、>、 \<=、> =、<>、=、または**など**します。  
  
-   値は、フィールドの値を比較する、値 (たとえば、'Smith' を 8/24/95 #、12.345、または 50.00 ドル)。 文字列と日付にはシャープ記号 (#) では、単一引用符を使用します。 数値の場合は、小数点、ドル記号、および科学的表記法を使用できます。 演算子は場合**など**値は、ワイルドカードを使用できます。 アスタリスク (*) とパーセント記号 (%)ワイルドカードを許可、および最後の文字の文字列である必要があります。 値を NULL にすることはできません。  
  
> [!NOTE]
>  フィルター値には、単一引用符 (') を含めるには、2 つの単一引用符を使用して、1 つを表します。 たとえば、O'Malley でフィルター処理、条件の文字列があります`"col1 = 'O''Malley'"`します。 先頭と末尾のフィルター値の両方に単一引用符を含めるには、シャープ記号文字列を囲む (#)。 たとえば、'1' でフィルター処理、条件の文字列があります`"col1 = #'1'#"`します。  
  
-   間の優先順位がないとします。 句は、かっこで囲まれてグループ化できます。 ただし、OR で結合句をグループ化とし、次のコード スニペットのようにして、別の句をグループに参加することはできません。  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   このフィルターを構築する代わりに、  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   **など**句では、先頭とパターンの末尾にワイルドカードを使用することができます。 たとえば、使用することができます`LastName Like '*mit*'`します。 または**など**パターンの末尾にのみ、ワイルドカードを使用することができます。 たとえば、`LastName Like 'Smit*'` のようにします。  
  
 フィルター定数容易に解決するにはこれらのレコードのみを表示、たとえば、許可することで、バッチ更新モード時に競合レコードの最後の中に影響を受けた[UpdateBatch メソッド](../../../ado/reference/ado-api/updatebatch-method.md)メソッドの呼び出し。  
  
設定、**フィルター**プロパティ自体が基になるデータの競合により失敗します。 たとえば、レコードは既に別のユーザーによって削除されたときに、このエラーが発生することができます。 このような場合は、プロバイダーは警告を返します、[エラー コレクション (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)コレクションが、プログラムの実行は停止しません。 要求されたすべてのレコードの競合がある場合にのみ、実行時にエラーが発生します。 使用して、 [Status プロパティ (ADO Recordset)](../../../ado/reference/ado-api/status-property-ado-recordset.md)が競合しているレコードを検索するプロパティ。  
  
設定、**フィルター**プロパティを長さ 0 の文字列 ("") を使用して同じ効果があります、 **adFilterNone**定数。
  
たびに、**フィルター**プロパティを設定すると、現在のレコードの位置を内のレコードのフィルター処理されたサブセットの最初のレコードに移動、 **Recordset**します。 同様に、ときに、**フィルター**で最初のレコードを現在のレコードの位置が移動プロパティをオフになって、**レコード セット**します。

ものとします、**レコード セット**sql_variant 型など、いくつかのバリアント型のフィールドの基にフィルターされます。 エラー (が DISP_E_TYPEMISMATCH 80020005 または) のサブタイプの条件の文字列で使用されるフィールドとフィルターの値が一致しないときに発生します。 たとえば、あるとします。

- A **Recordset**オブジェクト (rs) には、sql_variant 型の列 (C) が含まれています。
- この列のフィールドに、I4 型の 1 の値が割り当てられています。 条件の文字列に設定されている`rs.Filter = "C='A'"`フィールド。

この構成では、ランタイム処理中にエラーが生成されます。 ただし、`rs.Filter = "C=2"`同じ適用フィールドでは、エラーは生成されません。 フィールドは、現在のレコード セットからフィルター処理します。

参照してください、[ブックマーク プロパティ (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)プロパティについては、Filter プロパティを使用する配列をビルドすることができます、ブックマークの値。

フィルター条件文字列の形式で、永続化の内容に影響を与えるだけ**Recordset**します。 条件の文字列の例は`OrderDate > '12/31/1999'`します。 ブックマーク、またはからの値を使用して配列が作成されたフィルター、 **FilterGroupEnum**、永続化の内容には影響しません**Recordset**します。 これらの規則は、クライアント側またはサーバー側のカーソルで作成されたレコード セットに適用されます。
  
> [!NOTE]
>  フィルター選択された行と列のフラグを適用する場合、変更**レコード セット**バッチ更新モード、結果として得られる**レコード セット**のキー フィールドに基づくフィルター処理された場合は空です、テーブルの単一キーと、変更は、キー フィールドの値で行われました。 結果として得られる**Recordset**は空にする、次のステートメントのいずれかが true の場合。  
  
-   フィルター処理は、単一キー テーブルの非キー フィールドに基づいていました。  
  
-   フィルター処理は、複数キー テーブル内のフィールドに基づいていました。  
  
-   単一キー テーブルの非キー フィールドに対しては、変更が行われました。  
  
-   複数キー テーブル内のフィールドに対しては、変更が行われました。  
  
次の表の効果**行と列が**のフィルター処理と変更のさまざまな組み合わせでします。 左側の列には、変更が表示されます。 非キー フィールドを単一キー テーブル内のキー フィールドまたは複数キー テーブルのキー フィールドのいずれかのいずれかで変更できます。 最上位の行では、フィルター選択条件を示します。 フィルター処理できますに基づいて任意の非キー フィールドで、単一キーのテーブルでは、または複数キー テーブルのキー フィールドのいずれかのキー フィールド。 交差するセルは、結果を表示します。 A **+** プラス記号は、適用されることを意味**行と列が**空でない結果**Recordset**します。 A **-** 負符号は、空**Recordset**します。  
  
||非キー|1 つのキー|複数のキー|
|-|--------------|----------------|-------------------|
|**非キー**|+|+|+|
|**1 つのキー**|+|-|なし|
|**複数のキー**|+|なし|+|
|||||
  
## <a name="applies-to"></a>適用対象

[Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目

[Filter および RecordCount プロパティの例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)
[Filter および RecordCount プロパティの例 (vc++)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)
[Clear メソッド (ADO)](../../../ado/reference/ado-api/clear-method-ado.md) 
[Optimize プロパティ-動的 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
