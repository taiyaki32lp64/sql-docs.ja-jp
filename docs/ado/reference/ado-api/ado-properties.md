---
title: ADO のプロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- properties [ADO]
- ADO properties
ms.assetid: 0ac0d1a7-6c7a-4f4c-b115-428935e0f98b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3ddf4e26d015067c0b5bf06f6e2adeecd39f041
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920892"
---
# <a name="ado-properties"></a>ADO のプロパティ

|||  
|-|-|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|現在のレコードがどのページが存在することを示します。|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|現在のレコードの序数位置を示す、 **Recordset**オブジェクト。|  
|[ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md)|示す、**コマンド**作成、関連付けられているオブジェクトを**レコード セット**オブジェクト。|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|先を示します**接続**オブジェクトの指定した**コマンド**、 **Recordset**、または**レコード**オブジェクトが現在属しています。|  
|[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)|フィールドの値の実際の長さを示します。|  
|[Attributes](../../../ado/reference/ado-api/attributes-property-ado.md)|オブジェクトの 1 つまたは複数の特性を示します。|  
|[BOF、EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|**BOF**レコード セット オブジェクトの最初のレコードの前に、現在のレコードの位置があることを示します。<br /><br /> **EOF**レコード セット オブジェクトの最後のレコードの後に、現在のレコードの位置があることを示します。|  
|[Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md)|ブックマークの現在のレコードを一意に識別することを示します、**レコード セット**オブジェクトまたは現在のレコードを設定、**レコード セット**オブジェクトを有効なブックマークで識別されるレコード。|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|レコードの数を示す、 **Recordset**メモリにローカルにキャッシュされたオブジェクト。|  
|[」の章](../../../ado/reference/ado-api/chapter-property-ado.md)|OLE DB の設定を取得または**章**オブジェクトとの間で、 **ADORecordsetConstruction**オブジェクト。|  
|[CharSet](../../../ado/reference/ado-api/charset-property-ado.md)|文字セットを示します、テキストの内容**Stream**変換する必要があります。|  
|[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)|入力として使用するストリームを示す、**コマンド**オブジェクト。|  
|[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)|プロバイダーに対して発行するコマンドのテキストを示します。|  
|[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)|試行を終了し、エラーが発生する前に、コマンドの実行中に待機する時間を示します。|  
|[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)|型を示す、**コマンド**オブジェクト。|  
|[ConnectionString プロパティ](../../../ado/reference/ado-api/connectionstring-property-ado.md)|データ ソースへの接続を確立するための情報を示します。|  
|[ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)|試行を終了し、エラーが発生する前に、接続を確立中に待機する時間を示します。|  
|[Count](../../../ado/reference/ado-api/count-property-ado.md)|コレクション内のオブジェクトの数を示します。|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|カーソル サービスの場所を示します。|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|使用するカーソルの種類を示す、 **Recordset**オブジェクト。|  
|[DataMember](../../../ado/reference/ado-api/datamember-property.md)|によって参照されるオブジェクトから取得するデータ メンバーの名前を示します、 **DataSource**プロパティ。|  
|[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md)|として表されるデータを格納しているオブジェクトを示す、 **Recordset**オブジェクト。|  
|[DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)|既定のデータベースを示す、**接続**オブジェクト。|  
|[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)|データ容量を示します、**フィールド**オブジェクト。|  
|[[説明]](../../../ado/reference/ado-api/description-property.md)|について説明します、**エラー**オブジェクト。|  
|[言語仕様](../../../ado/reference/ado-api/dialect-property.md)|構文と、プロバイダーが解析に使用する一般的な規則を示します、 **CommandText**または**CommandStream**プロパティ。|  
|[[方向]](../../../ado/reference/ado-api/direction-property.md)|示すかどうか、**パラメーター**入力パラメーター、出力パラメーター、またはその両方を表すパラメーターがストアド プロシージャからの戻り値の場合、または。|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|現在のレコードの編集状態を示します。|  
|[EOS](../../../ado/reference/ado-api/eos-property.md)|現在の位置がストリームの末尾にあるかどうかを示します。|  
|[[フィルター]](../../../ado/reference/ado-api/filter-property.md)|内のデータのフィルターを示します、 **Recordset**します。|  
|[HelpContext、HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)|ヘルプ ファイルと関連付けられているトピックを示します、**エラー**オブジェクト。<br /><br /> **ヘルプ コンテキスト Id**として、コンテキスト ID を返します、**長い**トピックでは、ヘルプ ファイル内の値。<br /><br /> **HelpFile**を返します、**文字列**ヘルプ ファイルの完全に解決されたパスに評価される値。|  
|[Index](../../../ado/reference/ado-api/index-property.md)|有効なインデックスを現在の名前を示します、 **Recordset**オブジェクト。|  
|[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)|分離のレベルを示します、**接続**オブジェクト。|  
|[アイテム](../../../ado/reference/ado-api/item-property-ado.md)|名前または序数で、コレクションの特定のメンバーを示します。|  
|[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)|テキストの行区切り記号として使用する文字をバイナリ示します**Stream**オブジェクト。|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|編集中に、レコードに置かれたロックの種類を示します。|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|どのレコードがサーバーにマーシャ リングするかを示します。|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|返されるレコードの最大数を示す、 **Recordset**クエリから。|  
|[モード](../../../ado/reference/ado-api/mode-property-ado.md)|データを変更する使用可能なアクセス許可を示します、**接続**、**レコード**、または**Stream**オブジェクト。|  
|[名前](../../../ado/reference/ado-api/name-property-ado.md)|オブジェクトの名前を示します。|  
|[NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)|特定のプロバイダー固有のエラー コードを示します**エラー**オブジェクト。|  
|[数値](../../../ado/reference/ado-api/number-property-ado.md)|一意に識別する番号を示します、**エラー**オブジェクト。|  
|[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)|内の数値の小数点以下桁数を示す、**パラメーター**または**フィールド**オブジェクト。|  
|[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)|値を示す、**フィールド**変更が行われる前に、レコードに存在します。|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|データのページの数を示します、 **Recordset**オブジェクトが含まれています。|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|1 つのページを表すレコードの数を示します、 **Recordset**します。|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|OLE DB のコンテナーを設定します**行**上のオブジェクト、 **ADORecordConstruction**オブジェクト、行の親が ADO に変換されるよう**レコード**オブジェクト。|  
|[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)|親を指す絶対 URL 文字列を示す**レコード**、現在の**レコード**オブジェクト。|  
|[[Position]](../../../ado/reference/ado-api/position-property-ado.md)|内の現在位置を示す、 **Stream**オブジェクト。|  
|[Precision](../../../ado/reference/ado-api/precision-property-ado.md)|内の数値の有効桁数の度を示す、**パラメーター**オブジェクトまたは数値の**フィールド**オブジェクト。|  
|[準備](../../../ado/reference/ado-api/prepared-property-ado.md)|コンパイル済みのバージョンのコマンドを実行する前に保存するかどうかを示します。|  
|[Provider](../../../ado/reference/ado-api/provider-property-ado.md)|プロバイダーの名前を示します、**接続**オブジェクト。|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|内のレコードの数を示す、 **Recordset**オブジェクト。|  
|[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)|型を示す**レコード**オブジェクト。|  
|[行](../../../ado/reference/ado-api/row-property-ado.md)|OLE DB の設定を取得または**行**オブジェクトとの間で、 **ADORecordConstruction**オブジェクト。|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|OLE DB の設定を取得または**RowPosition**オブジェクトとの間で、 **ADORecordsetConstruction**オブジェクト。|  
|[行セット](../../../ado/reference/ado-api/rowset-property-ado.md)|OLE DB の設定を取得または**行セット**オブジェクトとの間で、 **ADORecordsetConstruction**オブジェクト。|  
|[ソース (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)|オブジェクトまたはアプリケーション エラーの発生源の名前を示します。|  
|[ソース (ADO Record)](../../../ado/reference/ado-api/source-property-ado-record.md)|によって表されるエンティティを示す、**レコード**オブジェクト。|  
|[ソース (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)|内のデータ ソースを示す、 **Recordset**オブジェクト|  
|[SQLState](../../../ado/reference/ado-api/sqlstate-property.md)|特定の SQL 状態を示す**エラー**オブジェクト。|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|すべての該当するオブジェクトのオブジェクトの状態がオープンかクローズかどうかを示します。 オブジェクトの現在の状態の接続、実行すると、または取得するかどうか、非同期メソッドを実行しているすべての該当するオブジェクトを示します。|  
|[状態 (ADO Field)](../../../ado/reference/ado-api/status-property-ado-field.md)|状態を示します、**フィールド**オブジェクト。|  
|[状態 (ADO Recordset)](../../../ado/reference/ado-api/status-property-ado-recordset.md)|バッチ更新やその他の一括操作に関する現在のレコードの状態を示します。|  
|[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)|階層構造内に示します**レコード セット**オブジェクトかどうか、基になる子レコードへの参照 (、 *」の章*)、親の行の位置が変わったときに変更します。|  
|[Stream プロパティ](../../../ado/reference/ado-api/stream-property.md)|OLE DB の設定を取得または**Stream**オブジェクトとの間で、 **ADOStreamConstruction**オブジェクト。|  
|[型](../../../ado/reference/ado-api/type-property-ado.md)|操作の種類またはデータ型を示す、**パラメーター**、**フィールド**、または**プロパティ**オブジェクト。|  
|[型 (ADO Stream)](../../../ado/reference/ado-api/type-property-ado-stream.md)|含まれているデータの型を示す、 **Stream** (バイナリまたはテキスト)。|  
|[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)|データベースに現在の値を示す、**フィールド**オブジェクト。|  
|[[値]](../../../ado/reference/ado-api/value-property-ado.md)|割り当てられている値を示します、**フィールド**、**パラメーター**、または**プロパティ**オブジェクト。|  
|[バージョン](../../../ado/reference/ado-api/version-property-ado.md)|ADO のバージョン番号を示します。|  
  
## <a name="see-also"></a>関連項目  
 [ADO の API リファレンス](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO のコレクション](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO の動的プロパティ](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO の列挙定数](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [付録 B: ADO エラー](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO イベント](../../../ado/reference/ado-api/ado-events.md)   
 [ADO メソッド](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO オブジェクト モデル](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO のオブジェクトとインターフェイス](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)
