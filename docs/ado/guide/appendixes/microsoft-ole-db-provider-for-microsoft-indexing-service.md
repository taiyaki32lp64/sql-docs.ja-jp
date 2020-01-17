---
title: Microsoft OLE DB Provider for Microsoft インデックス サービス |Microsoft ドキュメント
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a5a81514fd12117a9f43e2c33bf0cda579fb363d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926663"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Microsoft OLE DB Provider for Microsoft サービスの概要をインデックス作成
Microsoft OLE DB Provider for Microsoft インデックス サービスは、ファイル システムと Microsoft Indexing Service でインデックス付けされた Web データにプログラムでの読み取り専用アクセスを提供します。 ADO アプリケーションでは、コンテンツとファイルのプロパティ情報を取得する SQL クエリを発行できます。

 プロバイダーは、フリー スレッドし、UNICODE に対応します。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 このプロバイダーに接続するには、設定、**Provider =** への引数、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティ。

```vb
MSIDXS
```

 読み取り、[Provider](../../../ado/reference/ado-api/provider-property-ado.md)プロパティは同様に、この文字列を返します。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 文字列は、これらのキーワードで構成されます。

|Keyword|説明|
|-------------|-----------------|
|**Provider**|Microsoft インテックス サービス用の OLE DB プロバイダーを指定します。 通常これは、接続文字列で指定された唯一のキーワードです。|
|**Data Source**|インデックス サービスのカタログ名を指定します。 このキーワードが指定されていない場合は、既定のシステム カタログが使用されます。|
|**Locale Identifier**|32 ビットに固有の番号 (1033 など) に関連するユーザーの言語の基本設定を指定するを指定します。 このキーワードが指定されていない場合は、既定のシステム ロケールの識別子が使用されます。|

## <a name="command-text"></a>コマンド テキスト
 インデックス作成サービスの SQL クエリ構文では、SQL 92 に拡張機能の **SELECT** ステートメントとその **FROM** と **WHERE** 句。 ADO で使用およびとして操作可能な OLE DB 行セットを使用して、クエリの結果が返されます [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) オブジェクト。

 正確な単語や語句を検索したり、ワイルドカードのパターンや単語の語幹検索を使用できます。 検索ロジックは、ブール型の意思決定、重み付け語句は、またはその他の語の近接度に基づいて作成できます。 「フリー テキストを」一致する正確な単語ではなく、意味のものを検索することもできます。

 特定のコマンド構文は、インデックス サービスに関するドキュメントのクエリ言語で完全に記載されています。

 プロバイダーはストアド プロシージャの呼び出しまたは単純なテーブル名を受け付けません (たとえば、 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)プロパティが必ず**adCmdText**)。

## <a name="recordset-behavior"></a>レコード セットの動作
 次の表で使用できる機能の一覧、**Recordset**オブジェクトをこのプロバイダーに開きます。 静的カーソルの種類のみ (**adOpenStatic**) は使用できます。

 詳細については**Recordset**実行、プロバイダーの構成の動作、[Supports](../../../ado/reference/ado-api/supports-method.md)メソッドを列挙し、[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)のコレクション、**Recordset**をプロバイダーに固有の動的なプロパティが存在するかどうかを判断します。

 **標準の ADO レコード セットのプロパティの可用性:**

|プロパティ|可用性|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|読み取り/書き込み|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|読み取り/書き込み|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|読み取り専用|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|読み取り専用|
|[Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md)*|読み取り/書き込み|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|読み取り/書き込み|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|always **adUseServer**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|always **adOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|always **adEditNone**|
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|読み取り専用|
|[Assert](../../../ado/reference/ado-api/filter-property.md)|読み取り/書き込み|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|読み取り/書き込み|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|使用できません。|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|読み取り/書き込み|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|読み取り専用|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|読み取り/書き込み|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|読み取り専用|
|[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)|読み取り/書き込み|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|読み取り専用|
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|読み取り専用|

 \*この機能の順序で上に存在するプロバイダーのブックマークを有効にする必要があります、 **Recordset**します。

 **標準の ADO レコード セット メソッドの可用性:**

|方法|使用できるでしょうか。|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|いいえ|
|[Cancel](../../../ado/reference/ado-api/cancel-method-ado.md)|はい|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|いいえ|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|いいえ|
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|はい|
|[Close](../../../ado/reference/ado-api/close-method-ado.md)|はい|
|[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|いいえ|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|はい|
|[Move](../../../ado/reference/ado-api/move-method-ado.md)|はい|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|はい|
|[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)|はい|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|はい|
|[Resync](../../../ado/reference/ado-api/resync-method.md)|はい|
|[Supports](../../../ado/reference/ado-api/supports-method.md)|はい|
|[Update](../../../ado/reference/ado-api/update-method.md)|いいえ|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|いいえ|

 特定の実装の詳細と Microsoft インデックス サービスの機能について、Microsoft OLE DB プロバイダーを参照してください、 [OLE DB プログラマ ガイド](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx)、または Windows NT Server Web のサービスの Web ページを参照してくださいサイトです。

## <a name="see-also"></a>参照
 [CommandType プロパティ (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md) [ConnectionString プロパティ (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [Provider プロパティ (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [RecordSet オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [Supports メソッド](../../../ado/reference/ado-api/supports-method.md)
