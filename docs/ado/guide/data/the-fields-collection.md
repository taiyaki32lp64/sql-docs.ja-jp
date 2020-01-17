---
title: Fields コレクション |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 197a57b8a9b9ea2927a057733992a02c731a335a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923934"
---
# <a name="the-fields-collection"></a>Fields コレクション
**フィールド**コレクションは、ADO の組み込みコレクションの 1 つです。 コレクションは、単位として参照される項目の順序付けされたセットです。 ADO のコレクションの詳細については、次を参照してください。 [、ADO オブジェクト モデル](../../../ado/guide/data/ado-objects-and-collections.md)します。  
  
 **フィールド**コレクションに含まれる、**フィールド**オブジェクトのすべてのフィールド (列)、**レコード セット**します。 すべての ADO のコレクションのような**カウント**と**項目**プロパティだけでなく**Append**と**更新**メソッド。 **CancelUpdate**、**削除**、**再同期**、および**Update**メソッドはその他の ADO のコレクションを使用できません。  
  
## <a name="examining-the-fields-collection"></a>フィールド コレクションを調べる  
 検討してください、**フィールド**サンプルのコレクション**レコード セット**このセクションで導入されました。 サンプル**Recordset** SQL ステートメントから派生しました  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 そのため、必要があることがわかります、**レコード セット フィールド**コレクションには、3 つのフィールドが含まれています。  
  
```  
'BeginWalkFields  
    Dim objFields As ADODB.Fields  
    Dim intLoop As Integer  
  
    objRs.Open strSQL, strConnStr, adOpenForwardOnly, adLockReadOnly, adCmdText  
  
    Set objFields = objRs.Fields  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
    Next  
'EndWalkFields  
```  
  
 このコードは単純に数を判断します**フィールド**内のオブジェクト、**フィールド**コレクションを使用して、**カウント**プロパティとの値を返す、コレクション内のループ**名前**プロパティごとに**フィールド**オブジェクト。 さらに多くを使用する**フィールド**プロパティ、フィールドに関する情報を取得します。 クエリの詳細については、**フィールド**を参照してください[フィールド オブジェクトを](../../../ado/guide/data/the-field-object.md)します。  
  
## <a name="counting-columns"></a>列のカウント  
 ご想像のとおり、**カウント**プロパティの実際の数を返します**フィールド**内のオブジェクト、**フィールド**コレクション。 ループの値で始まり、0 個のメンバーとをコーディングするため、ゼロから始まる番号のコレクションのメンバーは、常にする必要があります、**カウント**から 1 を引いたプロパティ。 Microsoft Visual Basic を使用しているをチェックせずにコレクションのメンバーをループ処理する場合、**カウント**プロパティを使用して、**ごとにしています.[次へ]** コマンド。  
  
 場合、**カウント**プロパティが 0 で、コレクション内のオブジェクトはありません。  
  
## <a name="getting-to-the-field"></a>フィールドを取得します。  
 任意の ADO のコレクションと同様、**項目**プロパティは、コレクションの既定のプロパティ。 個人が返されます**フィールド**名前で指定されたオブジェクトまたはインデックスに渡されます。 そのため、次のステートメントは、サンプルの同等**Recordset**:  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 これらのメソッドと同じ場合は、最適なでしょうか。 場合によって異なります。 取得するインデックスを使用して、**フィールド**コレクションからは、高速にアクセスするため、**フィールド**文字列検索を実行する必要なく、直接します。 その一方の順序**フィールド**、コレクション内で認識する必要があります、し、順序を変更への参照、**フィールドの**インデックスが常に変更する必要があります。 少し遅くなりますが、名前を使用して、**フィールド**の順序に依存しないために、柔軟性が、**フィールド**コレクション。  
  
## <a name="using-the-refresh-method"></a>Refresh メソッドを使用します。  
 いくつか他 ADO のコレクションを使用するとは異なり、**更新**メソッドを**フィールド**コレクションが表示される影響を与えません。 基になるデータベース構造からの変更を取得する、いずれかを使用する必要があります、 **Requery**メソッド、または、**レコード セット**オブジェクトは、ブックマークをサポートしていません、 **MoveFirst**メソッドで、もう一度、プロバイダーに対して実行するコマンドが発生します。  
  
## <a name="adding-fields-to-a-recordset"></a>フィールドをレコード セットに追加します。  
 **Append**メソッドを使用するフィールドの追加を**Recordset**します。  
  
 使用することができます、 **Append**を生成するメソッド、**レコード セット**データ ソースへの接続を開くことがなくプログラムを使用します。 実行時エラーが発生、 **Append**でメソッドが呼び出される、**フィールド**、オープンのコレクション**レコード セット**か、または、**レコード セット**場所、 **ActiveConnection**プロパティが設定されています。 のみフィールドを追加できる、**レコード セット**が開いていないと、データ ソースに接続されていません。 ただし、新たに追加の値を指定**フィールド**、 **Recordset**を開いておく必要があります。  
  
 開発者には、一時的に一部のデータを格納またはいくつかのデータをユーザー インターフェイスのデータ バインドに参加できるように、サーバーから送信されているように機能する場所を多くの場合、必要があります。 ADO (と組み合わせて、 [OLE DB 用の Microsoft カーソル サービス](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)) により、開発者は、空のビルド**Recordset**列情報を指定して、呼び出すことによってオブジェクト**を開く**. 次の例では、3 つの新しいフィールドは、新しいに追加されます**Recordset**オブジェクト。 **レコード セット**を開くと、2 つの新しいレコードを追加すると、および**レコード セット**ファイルに保存されます。 (の詳細については**Recordset**永続化を参照してください[更新およびデータの永続化](../../../ado/guide/data/updating-and-persisting-data.md))。  
  
```  
'BeginFabricate  
    Dim objRs As ADODB.Recordset  
    Set objRs = New ADODB.Recordset  
  
    With objRs.Fields  
        .Append "StudentID", adChar, 11, adFldUpdatable  
        .Append "FullName", adVarChar, 50, adFldUpdatable  
        .Append "PhoneNmbr", adVarChar, 20, adFldUpdatable  
    End With  
  
    With objRs  
        .Open  
  
        .AddNew  
        .Fields(0) = "123-45-6789"  
        .Fields(1) = "John Doe"  
        .Fields(2) = "(425) 555-5555"  
        .Update  
  
        .AddNew  
        .Fields(0) = "123-45-6780"  
        .Fields(1) = "Jane Doe"  
        .Fields(2) = "(615) 555-1212"  
        .Update  
    End With  
  
    objRs.Save App.Path & "FabriTest.adtg", adPersistADTG  
  
    objRs.Close  
'EndFabricate  
```  
  
 使用状況、**フィールドの追加**メソッドは、の間で異なれば、**レコード セット**オブジェクトと**レコード**オブジェクト。 詳細については、**レコード**オブジェクトを参照してください[レコードとストリーム](../../../ado/guide/data/records-and-streams.md)します。  
  
## <a name="see-also"></a>参照  
 [階層レコードセットの作成](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)
