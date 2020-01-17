---
title: AddNew メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AddNew
- Recordset15::raw_AddNew
helpviewer_keywords:
- AddNew method [ADO]
ms.assetid: a9f54be9-5763-45d0-a6eb-09981b03bc08
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2f9efa8f5042fab603c794edada5aacab001936
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921324"
---
# <a name="addnew-method-ado"></a>AddNew メソッド (ADO)
更新可能なに対して新しいレコードを作成します。 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>パラメーター  
 *recordset*  
 A **Recordset**オブジェクト。  
  
 *FieldList*  
 任意。 1 つの名前または名前の配列または新しいレコードのフィールドの序数位置。  
  
 *値*  
 任意。 1 つの値、または新しいレコードのフィールドの値の配列。 場合*Fieldlist* 、配列は、*値*配列である必要があります、同じメンバーの数。 それ以外の場合、エラーが発生します。 フィールド名の順序は、各配列内のフィールド値の順序と一致する必要があります。  
  
## <a name="remarks"></a>コメント  
 使用して、 **AddNew**メソッドを作成し、新しいレコードを初期化します。 使用して、[サポート](../../../ado/reference/ado-api/supports-method.md)メソッド**adAddNew** (、 [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)値) を現在のレコードを追加できるかどうかを確認する**レコードセット**オブジェクト。  
  
 呼び出した後、 **AddNew**メソッドでは、新しいレコードが現在のレコードになり、を呼び出した後は、最新の状態、 [Update](../../../ado/reference/ado-api/update-method.md)メソッド。 新しいレコードが追加されますので、 **Recordset**への呼び出し**MoveNext**の末尾を越えた移動は次の更新プログラム、**レコード セット**、 **EOF** True です。 場合、 **Recordset**オブジェクトは、ブックマークをサポートしていない、別のレコードに移動すると、新しいレコードにアクセスすることはできません。 呼び出す必要があります、カーソルの種類に応じて、 [Requery](../../../ado/reference/ado-api/requery-method.md)メソッドを新しいレコードにアクセスできるようにします。  
  
 呼び出す場合**AddNew** ADO を呼び出し、現在のレコードを編集している間、または新しいレコードを追加するときに、 **Update**を保存する方法の変更し、新しいレコードを作成します。  
  
 動作、 **AddNew**メソッドの更新モードによって異なります、 **Recordset**オブジェクトとかどうかを渡す、 *Fieldlist*と*値*引数。  
  
 *即時更新モード*(をプロバイダーに変更を書き込みます、基になるデータ ソースを呼び出すと、**更新**メソッド) を呼び出すと、 **AddNew**メソッドなし引数のセット、 [EditMode](../../../ado/reference/ado-api/editmode-property.md)プロパティを**adEditAdd** (、 [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)値)。 プロバイダーは、ローカル フィールド値の変更をキャッシュします。 呼び出す、 **Update**メソッドは、データベースに新しいレコードをポストし、リセット、 **EditMode**プロパティを**adEditNone** (、 **EditModeEnum**値)。 渡す場合、 *Fieldlist*と*値*引数、ADO はすぐに、新しいレコードをデータベースに投稿 (ありません**Update**呼び出しが必要)、 **EditMode**プロパティの値が変更されない (**adEditNone**)。  
  
 *バッチ更新モード*(をプロバイダーが複数の変更をキャッシュし、呼び出すときにのみ、基になるデータ ソースに書き込む、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)メソッド) を呼び出すと、 **AddNew**メソッドの引数を設定せず、 **EditMode**プロパティを**adEditAdd**します。 プロバイダーは、ローカル フィールド値の変更をキャッシュします。 呼び出す、 **Update**メソッドは、現在、新しいレコードを追加**レコード セット**、プロバイダーが基になるデータベースへの変更を投稿またはリセットしていませんが、 **EditMode** **adEditNone**を呼び出すまで、 **UpdateBatch**メソッド。 渡す場合、 *Fieldlist*と*値*引数、ADO プロバイダーに送信、新しいレコードの記憶域のキャッシュとセット、 **EditMode**に**adEditAdd**; を呼び出す必要があります、 **UpdateBatch**メソッドを基になるデータベースに新しいレコードを投稿します。  
  
## <a name="example"></a>例  
 次の例では、配列としてフィールドの一覧と値のリストを追加する方法についてに含まれる値のリストとフィールドの一覧で AddNew メソッドを使用する方法を示します。  
  
```  
create table aa1 (intf int, charf char(10))  
insert into aa1 values (2, 'aa')  
  
Dim cn As New adodb.Connection  
Dim rs As New adodb.Recordset  
Dim cmd As New adodb.Command  
  
cn.ConnectionString = "Provider=SQLOLEDB;Data Source=alexverb2;uid=sa;pwd=foo$bar00;"  
  
cn.Open  
rs.Open "select * from xxx..aa1", cn, adOpenKeyset, adLockOptimistic  
  
Dim fieldsArray(1) As Variant  
fieldsArray(0) = "intf"  
fieldsArray(1) = "charf"  
Dim values(1) As Variant  
values(0) = 4  
values(1) = "as"  
rs.AddNew fieldsArray, values  
rs.Update  
```  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [AddNew メソッドの例 (VB)](../../../ado/reference/ado-api/addnew-method-example-vb.md)   
 [AddNew メソッドの例 (VBScript)](../../../ado/reference/ado-api/addnew-method-example-vbscript.md)   
 [AddNew メソッドの例 (vc++)](../../../ado/reference/ado-api/addnew-method-example-vc.md)   
 [CancelUpdate メソッド (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode プロパティ](../../../ado/reference/ado-api/editmode-property.md)   
 [Requery メソッド](../../../ado/reference/ado-api/requery-method.md)   
 [メソッドをサポートしています](../../../ado/reference/ado-api/supports-method.md)   
 [Update メソッド](../../../ado/reference/ado-api/update-method.md)   
 [UpdateBatch メソッド](../../../ado/reference/ado-api/updatebatch-method.md)
