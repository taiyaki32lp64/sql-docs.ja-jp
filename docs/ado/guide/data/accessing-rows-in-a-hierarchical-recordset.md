---
title: 階層レコード セット内の行へのアクセス |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e73b2ca96cc5e7eb7683b72aa19fd59a318b8596
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926355"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>階層レコード セット (例) 内の行へのアクセス
次の例を示しています手順では、アクセス許可の行に必要な階層構造で[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **レコード セット**オブジェクトから、**作成者**と**titleauthor**作成者 ID によって関連テーブル

2.  外側のループでは、各著者の姓と名、状態、および識別情報が表示されます。

3.  追加された**レコード セット**の各行がから取得した、[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)コレクションに割り当てられていると*最初*します。

4.  内側のループで、追加された各列から 4 つのフィールドを表示します**Recordset**します。

 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)プロパティに設定されて**false**わかりやすくするための表示できるように章では、明示的にで変更、外側のループの各反復処理します。 コード例をより効率的にするために、割り当てが 1 回だけ実行されるように、手順 2. で最初の行の前に、手順 3. で割り当てを移動できます。 設定し、 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)プロパティを**true**ように*最初*に対応する章が暗黙的に、自動的に変更されるたびに*rst*を新しい行に移動します。

## <a name="example"></a>例

```
Sub datashape()
   Dim cnn As New ADODB.Connection
   Dim rst As New ADODB.Recordset
   Dim rstTitleAuthor As New ADODB.Recordset

   cnn.Provider = "MSDataShape"
   cnn.Open    "Data Provider=MSDASQL;" & _
               "Data Source=SRV;Integrated Security=SSPI;Database=Pubs"
' STEP 1
   rst.StayInSync = FALSE
   rst.Open    "SHAPE  {select * from authors} "  & _
               "APPEND ({select * from titleauthor} " & _
               "RELATE au_id TO au_id) AS chapTitleAuthor", _
               cnn
' STEP 2
   While Not rst.EOF
      Debug.Print    rst("au_fname"), rst("au_lname"), _
                     rst("state"), rst("au_id")
' STEP 3
      Set rstTitleAuthor = rst("chapTitleAuthor").Value
' STEP 4
      While Not rstTitleAuthor.EOF
         Debug.Print rstTitleAuthor(0), rstTitleAuthor(1), _
                     rstTitleAuthor(2), rstTitleAuthor(3)
         rstTitleAuthor.MoveNext
      Wend
      rst.MoveNext
   Wend
End Sub
```

## <a name="see-also"></a>関連項目
 [データ シェイプの概要](../../../ado/guide/data/data-shaping-overview.md)[オブジェクトをフィールド](../../../ado/reference/ado-api/field-object.md) [Fields コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md) [Shape の正式文法](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft のデータ シェイプの OLE DB のサービス(サービス プロバイダーの ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [レコード セット オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [プロバイダーに必要なデータの整形](../../../ado/guide/data/required-providers-for-data-shaping.md)[図形の APPEND 句](../../../ado/guide/data/shape-append-clause.md)[図形内のコマンド一般的な](../../../ado/guide/data/shape-commands-in-general.md) [Shape COMPUTE 句](../../../ado/guide/data/shape-compute-clause.md) [Visual Basic for Applications の関数](../../../ado/guide/data/visual-basic-for-applications-functions.md)
