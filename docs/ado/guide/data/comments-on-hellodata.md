---
title: HelloData に関するコメント |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c4897f82ff8562c031ec3522f47cddebfb56eb2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925807"
---
# <a name="comments-on-hellodata"></a>HelloData に関するコメント
HelloData アプリケーションが一般的な ADO アプリケーションの基本的な操作手順: を取得する、確認、編集、およびデータを更新します。 アプリケーションを起動するときに、最初のボタンをクリックします。**データの取得**します。 これは、実行、 **GetData**サブルーチンです。  
  
## <a name="getdata"></a>GetData  
 **GetData**モジュール レベルの変数に有効な接続文字列を配置*m_sConnStr*します。 接続文字列の詳細については、次を参照してください。[接続文字列を作成する](../../../ado/guide/data/creating-a-connection-string.md)します。  
  
 Visual Basic を使用して、エラー ハンドラーを割り当てる**OnError**ステートメント。 ADO のエラー処理の詳細については、次を参照してください。[エラー処理](../../../ado/guide/data/error-handling.md)します。 新しい**接続**オブジェクトを作成すると、および**CursorLocation**プロパティに設定されて**adUseClient** HelloData 例では、作成されるため、 *切断されたレコード セット*します。 つまり、データ ソースからデータがフェッチされた、データ ソースとの物理的な接続が切断されているが、まだ、ローカルでキャッシュされているデータを使用することができ、すぐに、 **Recordset**オブジェクト。  
  
 接続を開いた後は、SQL 文字列を変数 (sSQL) に割り当てます。 新しいインスタンスを作成し、 **Recordset**オブジェクト、`m_oRecordset1`します。 次のコード行で開く、**レコード セット**既存**接続**で渡し`sSQL`のソースとして、**レコード セット**します。 SQL 文字列を判断に役立つよう ADO のソースとして渡されますが、 **Recordset**を渡すことによって、コマンドのテキストの定義は、 **adCmdText** への最後の引数で**レコード セットを開いて**メソッド。 この行もの設定、 **LockType**と**CursorType**に関連付けられている、**レコード セット**します。  
  
 次の行のコード セット、 **MarshalOptions**プロパティを等しく**adMarshalModifiedOnly**します。 **MarshalOptions**どのレコードを中間層 (または Web サーバー) にマーシャ リングすることを示します。 マーシャ リングの詳細については、COM ドキュメントを参照してください。 使用すると**adMarshalModifiedOnly**クライアント側のカーソル ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**)、変更されているレコードだけ、クライアントは、中間層に書き戻されます。 設定**MarshalOptions**に**adMarshalModifiedOnly**より少ない行がマーシャ リングされるため、パフォーマンスを向上させることができます。  
  
 次に、切断、**レコード セット**を設定してその**ActiveConnection**プロパティを等しく**Nothing**します。 詳細については、"切断と再接続 Recordset"セクションを参照してください[更新およびデータの永続化](../../../ado/guide/data/updating-and-persisting-data.md)します。  
  
 データ ソースへの接続を閉じて、既存を破棄して**接続**オブジェクト。 これは、使用、リソースを解放します。  
  
 最後の手順を設定するのには、**レコード セット**として、 **DataSource**からデータを簡単に表示できる Microsoft DataGrid コントロール、フォームのための**レコード セット**で、フォームです。  
  
 2 番目のボタンをクリックします。**を調べるデータ**します。 これを実行、 **ExamineData**サブルーチンです。  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData さまざまなメソッドとプロパティを使用して、 **Recordset**内のデータに関する情報を表示するオブジェクト、**レコード セット**します。 使用してレコードの数を報告、 **RecordCount**プロパティ。 ループ処理、**レコード セット**の値を表示し、 **AbsolutePosition**フォームの表示のテキスト ボックス内のプロパティ。 値は、ループの中にも、**ブックマーク**3 番目のレコードのプロパティは、バリアント型の変数に配置されます*vBookmark*、後で使用します。  
  
 ルーチンは、以前に格納するブックマーク変数を使用する 3 番目のレコードに直接移動します。 ルーチンの呼び出し、 **WalkFields**サブルーチンは、ループ、**フィールド**のコレクション、 **Recordset**それぞれに関する詳細を表示および**フィールド**コレクション。  
  
 最後に、 **ExamineData**を使用して、**フィルター**のプロパティ、 **Recordset**レコードだけの画面に、 **CategoryId**と等しい2 です。 このフィルターを適用した結果は、フォームの表示のグリッドにすぐに表示されます。  
  
 示すように機能の詳細については、 **ExamineData**サブルーチンを参照してください[データを調べる](../../../ado/guide/data/examining-data.md)します。  
  
 次に、3 番目のボタンをクリックして**データの編集**します。 これは、実行、 **EditData**サブルーチンです。  
  
## <a name="editdata"></a>EditData  
 コードを入力した場合、 **EditData**サブルーチン、**レコード セット**にフィルターがまだ**CategoryId**フィルタ条件を満たす項目のみが実行されるため、2 と等しく表示されます。 最初のループ、**レコード セット**で表示される各項目の価格になり、**レコード セット**を 10% です。 値、**価格**フィールドを設定して変更が、**値**そのフィールドが新しい有効な金額と同等のプロパティ。  
  
 注意して、 **Recordset**がデータ ソースから切断されています。 加えられた変更**EditData**データのローカルにキャッシュされたコピーに対してのみ実行されます。 詳細については、次を参照してください。[データを編集](../../../ado/guide/data/editing-data.md)します。  
  
 4 番目のボタンをクリックするまで変更は、データ ソースで行われません**更新データ**します。 これは、実行、 **UpdateData**サブルーチンです。  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData が最初に適用されているフィルターを削除、 **Recordset**します。 コードを削除し、戻します`m_oRecordset1`として、 **DataSource** Microsoft バインド DataGrid がフォーム上のように、フィルター処理されていない**レコード セット**グリッドに表示されます。  
  
 後方に移動することができるかどうかを確認し、 **Recordset**を使用して、**サポート**メソッドを**adMovePrevious**引数。  
  
 最初のレコードを使用するルーチンに移動、 **MoveFirst**メソッドを使用して、フィールドの元と現在の値を表示し、 **OriginalValue**と**値**プロパティ、**フィールド**オブジェクト。 と共にこれらのプロパティ、 **UnderlyingValue**プロパティ (使用されていないここ) は、後ほど[更新およびデータの永続化](../../../ado/guide/data/updating-and-persisting-data.md)します。  
  
 次に、新しい**接続**オブジェクトを作成し、データ ソースへの接続を再確立するために使用します。 再接続する、**レコード セット**設定、新しいデータ ソースに**接続**として、 **ActiveConnection**の**Recordset**します。 コードでは、サーバーに更新を送信する**UpdateBatch**上、**レコード セット**します。  
  
 バッチ更新が成功すると、モジュール レベルのフラグ変数`m_flgPriceUpdated`が True に設定します。 後でクリーンアップする場合、データベースに加えられたすべての変更は通知します。  
  
 最後に、コードに移動の最初のレコード、 **Recordset**し、元と現在の値を表示します。 呼び出した後は、値が同じ**UpdateBatch**します。  
  
 データを更新する方法の詳細については、対象とした場合の対処を含むデータ中にサーバーの変更を**レコード セット**は、切断されているを参照してください[更新およびデータの永続化](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
## <a name="formunload"></a>Form_Unload  
 **Form_Unload**いくつかの理由のサブルーチンが重要です。 最初に、これはサンプル アプリケーションであるため、form_unload をアプリケーションが終了する前にデータベースに加えられた変更します。 次に、コードは、コマンドを実行して、開いているから直接方法**接続**オブジェクトを使用して、 **Execute**メソッド。 最後に、データ ソースに対する行を返すクエリ (UPDATE クエリ) を実行する例を示します。
