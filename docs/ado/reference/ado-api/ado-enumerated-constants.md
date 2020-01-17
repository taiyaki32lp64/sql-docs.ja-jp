---
title: ADO の列挙定数 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADO]
ms.assetid: c97ed131-1a93-463c-9e61-22f029b0c474
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a2b02498905b73f321d7585b5c91adfbfd1b4b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921028"
---
# <a name="ado-enumerated-constants"></a>ADO の列挙定数
デバッグに役立つ、ADO 列挙体には、各定数の値が一覧表示します。 ただし、この値は、参考し、ADO の 1 つのリリース別に変更があります。 コードは、各列挙型定数の実際の値ではなく、名前にのみ依存する必要があります。  
  
|||  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|RDS の**Recordset**オブジェクト、データを取得する非同期のスレッドの実行の優先順位を指定します。|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|タイミングを指定します、 **MSDataShape**プロバイダーが階層構造での集計と計算列を再計算**Recordset**します。|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|オプティミスティックを持つデータ ソースの行の更新中に競合を検出するために使用できるフィールドに指定する**Recordset**オブジェクト。|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|指定するかどうか、 **UpdateBatch**メソッドの後に、暗黙的な**再同期**メソッドの操作であれば、その操作のスコープ。|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|操作の対象となるレコードを指定します。|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|操作の開始位置を示すブックマークを指定します。|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|コマンド引数を解釈する方法を指定します。|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|ブックマークによって表される 2 つのレコードの相対位置を指定します。|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|データを変更する使用可能なアクセス許可を指定します、**接続**を開いて、**レコード**の値を指定するか、**モード**のプロパティ、 **レコード**と**Stream**オブジェクト。|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|指定するかどうか、**オープン**のメソッド、**接続**後にオブジェクトを返す必要があります (同期) (非同期)、接続が確立される前に、または。|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|ODBC データ ソースへの接続を開くときに、不足しているパラメーターを要求する ダイアログ ボックスを表示するかどうかを指定します。|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|動作を指定します、 **CopyRecord**メソッド。|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|カーソル エンジンの場所を指定します。|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|どのような機能を指定します、**サポート**メソッドをテストする必要があります。|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|使用するカーソルの種類を指定します、 **Recordset**オブジェクト。|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|データ型を指定します、**フィールド**、**パラメーター**、または**プロパティ**します。|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|レコードの編集状態を指定します。|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|ADO の実行時エラーの種類を指定します。|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|イベントの発生の原因となった理由を指定します。|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|イベントの実行の現在の状態を指定します。|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|プロバイダーがコマンドを実行する方法を指定します。|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|参照されている特別なフィールドを指定します、**フィールド**のコレクションを**レコード**オブジェクト。|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|1 つまたは複数の属性を指定します、**フィールド**オブジェクト。|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|状態を示す、**フィールド**オブジェクト。|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|フィルター処理するレコードのグループを指定します、 **Recordset**します。|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|取得するレコードの数を指定します、 **Recordset**します。|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|トランザクションの分離のレベルを指定します、**接続**オブジェクト。|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|テキストの行区切り記号として使用される文字を指定します**Stream**オブジェクト。|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|編集中に、レコードに適用されるロックの種類を指定します。|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|サーバーに返されるレコードを指定します。|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|動作を指定します、**レコード**オブジェクト**MoveRecord**メソッド。|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|オブジェクトがオープンかクローズは、コマンドを実行またはデータのフェッチで、データ ソースに接続するかどうかを指定します。|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|属性を指定します、**パラメーター**オブジェクト。|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|指定するかどうか、**パラメーター**入力パラメーター、出力パラメーター、またはその両方を表す場合、またはパラメーターがストアド プロシージャからの戻り値。|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|保存先となる形式を指定します、 **Recordset**します。|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|内のレコード ポインターの現在位置を示す、 **Recordset**します。|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|属性を指定します、**プロパティ**オブジェクト。|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|指定、**レコード**オブジェクト**オープン**メソッド既存かどうか**レコード**は開かれている、または新しい**レコード**作成する必要があります。|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|開くのためのオプションを指定します、**レコード**します。 OR 演算子を使用して、これらの値を組み合わせることができます。|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|バッチ更新およびその他の一括操作に関して、レコードの状態を指定します。|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|型を指定**レコード**オブジェクト。|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|呼び出して、基になる値を上書きするかどうかを示す**再同期**します。|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|ファイルを作成または上書きを保存するときにするかどうかを指定します、 **Stream**オブジェクト。 値は、AND 演算子と組み合わせることができます。|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|スキーマの種類を指定します**Recordset**を**OpenSchema**メソッドを取得します。 内のレコードの検索の方向を指定します、 **Recordset**します。|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|内のレコードの検索の方向を指定します、 **Recordset**します。 型を指定**シーク**を実行します。|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|型を指定**シーク**を実行します。 開くのためのオプションを指定します、 **Stream**オブジェクト。 値は、AND 演算子と組み合わせることができます。|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|開くのためのオプションを指定します、 **Stream**オブジェクト。 値は、AND 演算子と組み合わせることができます。 ストリーム全体、または次の行をから読み取る必要があるかどうかを指定します、 **Stream**オブジェクト。|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|ストリーム全体、または次の行をから読み取る必要があるかどうかを指定します、 **Stream**オブジェクト。 格納されたデータの種類を指定します、 **Stream**オブジェクト。|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|格納されたデータの種類を指定します、 **Stream**オブジェクト。 書き込まれる文字列に行区切り記号を追加するかどうかを指定します、 **Stream**オブジェクト。|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|書き込まれる文字列に行区切り記号を追加するかどうかを指定します、 **Stream**オブジェクト。 取得するときに、形式を指定します、 **Recordset**を文字列として。|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|取得するときに、形式を指定します、 **Recordset**を文字列として。 トランザクション属性を指定します、**接続**オブジェクト。|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|トランザクション属性を指定します、**接続**オブジェクト。|  
  
## <a name="see-also"></a>関連項目  
 [ADO の API リファレンス](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO のコレクション](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO の動的プロパティ](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [付録 B: ADO エラー](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO イベント](../../../ado/reference/ado-api/ado-events.md)   
 [ADO メソッド](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO オブジェクト モデル](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO オブジェクトとインターフェイス](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO のプロパティ](../../../ado/reference/ado-api/ado-properties.md)
