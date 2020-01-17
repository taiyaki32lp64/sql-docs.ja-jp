---
title: ADO メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, methods
- methods [ADO]
ms.assetid: a38c5670-ba28-44f3-bd5b-fcb46880e904
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8df204daeda82f809cf50246590141729e3608e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920923"
---
# <a name="ado-methods"></a>ADO メソッド

|||  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|更新可能なに対して新しいレコードを作成します。 **Recordset**オブジェクト。|  
|[追加](../../../ado/reference/ado-api/append-method-ado.md)|コレクションにオブジェクトを追加します。 コレクションが場合**フィールド**、新しい**フィールド**それをコレクションに追加する前に、オブジェクトを作成することがあります。|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|大きなテキストまたはバイナリ データにデータを追加します。**フィールド**、または、**パラメーター**オブジェクト。|  
|[BeginTrans、CommitTrans、および rollbacktrans の例](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|内のトランザクション処理の管理、**接続**オブジェクトの次のようにします。<br /><br /> **BeginTrans** -新しいトランザクションを開始します。<br /><br /> **CommitTrans** - 変更を保存し、現在のトランザクションを終了します。 新しいトランザクションを開始する場合もします。<br /><br /> **RollbackTrans** - 変更内容をキャンセルし、現在のトランザクションを終了します。 新しいトランザクションを開始する場合もします。|  
|[Cancel](../../../ado/reference/ado-api/cancel-method-ado.md)|実行をキャンセルする保留中、非同期メソッド呼び出し。|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|保留中のバッチ更新をキャンセルします。|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|現在のまたは新しい行に加えられた変更内容をキャンセル、**レコード セット**オブジェクト、または**フィールド**のコレクションを**レコード**オブジェクトを呼び出す前に、 **Update**メソッド。|  
|[Clear](../../../ado/reference/ado-api/clear-method-ado.md)|すべてを削除、**エラー**オブジェクトから、**エラー**コレクション。|  
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|複製を作成します**Recordset**既存のオブジェクト**Recordset**オブジェクト。 必要に応じて、複製が読み取り専用であることを指定します。|  
|[閉じる](../../../ado/reference/ado-api/close-method-ado.md)|開いているオブジェクトとすべての依存オブジェクトを閉じます。|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|2 つのブックマークを比較し、これらの相対値を示す値を返します。|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|ファイルまたはディレクトリと、その内容を別の場所にコピーします。|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|指定した数の文字またはバイトのコピー (に応じて**型**) で、 **Stream**間**Stream**オブジェクト。|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|新たに作成**パラメーター**を指定したプロパティを持つオブジェクト。|  
|[削除 (ADO Parameters コレクション)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|オブジェクトを削除、**パラメーター**コレクション。|  
|[(ADO Fields コレクション) の削除します。](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|オブジェクトを削除、**フィールド**コレクション。|  
|[削除 (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|現在のレコードまたはレコードのグループを削除します。|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|ファイルまたはディレクトリとそのすべてのサブディレクトリを削除します。|  
|[実行 (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)|クエリや、SQL ステートメントで指定されたストアド プロシージャの実行、 **CommandText**プロパティ。|  
|[実行 (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|指定されたクエリ、SQL ステートメント、ストアド プロシージャ、またはプロバイダー固有のテキストを実行します。|  
|[検索](../../../ado/reference/ado-api/find-method-ado.md)|検索、**レコード セット**を指定した条件を満たす行のできます。|  
|[フラッシュ](../../../ado/reference/ado-api/flush-method-ado.md)|内容を強制的、 **Stream**を基になるオブジェクトへの ADO のバッファーに残っている、 **Stream**が関連付けられています。|  
|[get_OLEDBCommand メソッド](../../../ado/reference/ado-api/get-oledbcommand-method.md)|まず ADO コマンドで設定する ole DB コマンドのパラメーター情報を伝達する、基になる ole DB コマンドを返します。|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|返します、 **Recordset**ファイルとこれによって表されるディレクトリにサブディレクトリを表す行を持つ**レコード**します。|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|大きなテキストまたはバイナリ データの内容の一部またはすべてを返します**フィールド**オブジェクト。|  
|[GetDataProviderDSO メソッド](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Shape プロバイダーから基になる ole DB データ ソース オブジェクトを取得します。|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|複数のレコードを取得、 **Recordset**オブジェクトを配列にします。|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|返します、 **Recordset**を文字列として。|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|既存のファイルの内容を読み込み、 **Stream**します。|  
|[Move](../../../ado/reference/ado-api/move-method-ado.md)|現在のレコードの位置を移動、 **Recordset**オブジェクト。|  
|[MoveFirst、MoveLast、MoveNext、MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|First、last に移動します。 次に、または前のレコードを、指定した**レコード セット**オブジェクトと、そのレコードを現在のレコード。|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|ファイルまたはディレクトリとその内容を別の場所に移動します。|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|現在のクリア**レコード セット**オブジェクトし、[次へ] を返します**レコード セット**一連のコマンドを進めることで。|  
|[開く (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)|データ ソースへの接続を開きます。|  
|[開く (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)|既存を開く**レコード**オブジェクト、または新しいファイルまたはディレクトリを作成します。|  
|[開く (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|カーソルを開きます。|  
|[開く (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)|開く、 **Stream**バイナリまたはテキスト データのストリームを操作するオブジェクト。|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|プロバイダーからデータベース スキーマ情報を取得します。|  
|[put_OLEDBCommand メソッド](../../../ado/reference/ado-api/put-oledbcommand-method.md)|このメソッドは演算を実行しない - 常に S_OK を返します。|  
|[読み取り](../../../ado/reference/ado-api/read-method.md)|指定したからのバイト数を読み取り、 **Stream**オブジェクト。|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|テキストから指定数の文字を読み取ります**Stream**オブジェクト。|  
|[[更新]](../../../ado/reference/ado-api/refresh-method-ado.md)|プロバイダーをコレクションから、使用可能なオブジェクトを反映するように、特定のオブジェクトを更新します。|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|データを更新、**レコード セット**オブジェクトをオブジェクトの基になるクエリを再実行しています。|  
|[Resync](../../../ado/reference/ado-api/resync-method.md)|現在のデータを更新します**レコード セット**オブジェクト、または**フィールド**のコレクションを**レコード**基になるデータベースからのオブジェクト。|  
|[および](../../../ado/reference/ado-api/save-method.md)|保存、**レコード セット**ファイルまたは**Stream**オブジェクト。|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|バイナリ コンテンツを保存、 **Stream**ファイル。|  
|[シーク](../../../ado/reference/ado-api/seek-method.md)|インデックスを検索、 **Recordset**を指定した値と一致して、その行に現在の行位置を変更する行をすばやく検索します。|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|ストリームの末尾の位置を設定します。|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|テキスト ストリームを読み取るときに、1 つの行全体をスキップします。|  
|[Stat](../../../ado/reference/ado-api/stat-method.md)|開いているストリームに関する統計情報を取得します。|  
|[サポート](../../../ado/reference/ado-api/supports-method.md)|指定したかどうかを判断します**Recordset**オブジェクトは、特定の種類の機能をサポートしています。|  
|[Update](../../../ado/reference/ado-api/update-method.md)|現在の行に加えた変更を保存、**レコード セット**オブジェクト、または**フィールド**のコレクションを**レコード**オブジェクト。|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|すべての保留中のバッチ更新プログラムをディスクに書き込みます。|  
|[書き込み](../../../ado/reference/ado-api/write-method.md)|バイナリ データを書き込みます、 **Stream**オブジェクト。|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|指定したテキスト文字列を書き込みます、 **Stream**オブジェクト。|  
  
## <a name="see-also"></a>関連項目  
 [ADO の API リファレンス](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO のコレクション](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO の動的プロパティ](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO の列挙定数](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [付録 B: ADO エラー](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO イベント](../../../ado/reference/ado-api/ado-events.md)   
 [ADO オブジェクト モデル](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO オブジェクトとインターフェイス](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO のプロパティ](../../../ado/reference/ado-api/ado-properties.md)
