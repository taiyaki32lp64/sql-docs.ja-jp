---
title: OLE DB (ADO サービス コンポーネント) の Microsoft カーソル サービス |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e7e5b9a973e5ccf04f92a2162d88ee25b7fa5242
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926795"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>OLE DB の概要の Microsoft カーソル サービス
OLE DB 用の Microsoft カーソル サービスは、データ プロバイダーのカーソル サポート機能を補完します。 その結果、ユーザーは、すべてのデータ プロバイダーから比較的均一な機能を認識します。

 カーソル サービスでは、動的プロパティを使用できるようにし、特定のメソッドの動作が向上します。 たとえば、[最適化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)動的プロパティなどの特定の操作を容易に一時インデックスの作成ができるように、[検索](../../../ado/reference/ado-api/find-method-ado.md)メソッド。

 カーソル サービスを使用すると、常にバッチを更新するためのサポート。 データ プロバイダーが劣るカーソル、静的カーソルなどを指定できますのみときも、dynamic カーソルより高機能な種類のカーソルをシミュレートします。

## <a name="keyword"></a>Keyword
 このサービスのコンポーネントを呼び出す、[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)または[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを**adUseClient**します。

```vb
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>動的プロパティ
 次の動的プロパティを追加の OLE DB カーソル サービスが呼び出されたときに、 **Recordset**オブジェクトの[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション。 完全な一覧**接続**と**Recordset**オブジェクトの動的プロパティの一覧は、 [ADO Dynamic プロパティ インデックス](../../../ado/reference/ado-api/ado-dynamic-property-index.md)します。 関連付けられている OLE DB プロパティ名に、適切な場所はかっこ内に含ま ADO のプロパティ名の後にします。

 カーソル サービスが呼び出された後は、いくつかの動的プロパティへの変更を基になるデータ ソースに表示されません。 たとえば、設定、*コマンド タイムアウト*プロパティを**Recordset**は基になるデータ プロバイダーには表示されません。

```vb

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 基になるプロバイダーの動的プロパティを設定する必要がありますが、アプリケーションには、カーソル サービスが必要ですが場合、は、カーソルのサービスを呼び出す前にプロパティを設定します。 コマンド オブジェクトのプロパティの設定は常に、カーソルの場所に関係なく、基になるデータ プロバイダーに渡されます。 そのため、いつでもプロパティを設定するのにコマンド オブジェクトを使用することもできます。

> [!NOTE]
>  基になるデータ プロバイダーがサポートされている場合でも、DBPROP_SERVERDATAONINSERT 動的プロパティは、カーソル サービスによってサポートされていません。

|プロパティ名|説明|
|-------------------|-----------------|
|自動再計算 (DBPROP_ADC_AUTORECALC)|この値はどのくらいの頻度を示します Data Shaping Service で作成されたRecordsetの集計と計算列が計算されます。 既定値 (値 = 1) Data Shaping Service は、値が変更されたことを決定するたびに再計算されます。 値が 0 の場合、階層の最初にビルド時に計算または集計列が計算のみです。|
|バッチ サイズ (DBPROP_ADC_BATCHSIZE)|データ ストアに送信される前にバッチ処理できる update ステートメントの数を示します。 バッチ内の複数のステートメント、データに少ないラウンド トリップを格納します。|
|子の行をキャッシュする (DBPROP_ADC_CACHECHILDROWS)|Data Shaping Service で作成されたRecordsetは、この値は、後で使用できるキャッシュに、子のRecordsetが格納されているかどうかを示します。|
|カーソル エンジンのバージョン (DBPROP_ADC_CEVER)|使用されているカーソル サービスのバージョンを示します。|
|状態の変更 (DBPROP_ADC_MAINTAINCHANGESTATUS) の管理します。|複数のテーブルの結合で 1 つまたは複数の行の再同期に使用されるコマンドのテキストを示します。|
|[最適化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|インデックスを作成するかどうかを示します。 設定すると**True**、一時的な特定の操作の実行を向上させるためにインデックスの作成を承認します。|
|[名前を変更します。](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|名前を示します、 **Recordset**します。 現在内で参照されているまたはその後、データ シェイプのコマンドです。|
|[再同期コマンド](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|によって使用されるカスタム コマンド文字列を示します、[再同期](../../../ado/reference/ado-api/resync-method.md)メソッドと、[一意テーブル](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)プロパティが有効になります。|
|[一意のカタログ](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|参照されているテーブルを含むデータベースの名前を示します、**一意テーブル**プロパティ。|
|[一意のスキーマ](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|参照されるテーブルの所有者の名前を示します、**一意テーブル**プロパティ。|
|[一意テーブル](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|1 つのテーブルの名前を示します、**Recordset**挿入、更新、または削除によって変更可能な複数のテーブルから作成します。|
|更新基準 (DBPROP_ADC_UPDATECRITERIA)|どのフィールドを示す、**WHERE**句は、更新中に発生する競合を処理するために使用します。|
|[再同期の更新](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)(DBPROP_ADC_UPDATERESYNC)|示すかどうか、**Resync**メソッドが後に暗黙的に呼び出され、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)メソッド (とその動作)、**一意テーブル**プロパティが有効になります。|

 設定またはのインデックスとしてその名前を指定することで動的プロパティを取得することも、**プロパティ**コレクション。 たとえば、取得しての現在の値を出力、[最適化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)動的プロパティは、新しい値を次のように設定し。

```vb
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>組み込みのプロパティの動作
 OLE DB のカーソル サービスは、特定の組み込みプロパティの動作にも影響します。

|プロパティ名|説明|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|使用可能なカーソルの種類を補足するもの、 **Recordset**します。|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|使用できるロックの種類を補足するもの、**Recordset**します。 一括更新を可能にします。|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|1 つまたは複数のフィールド名を指定します、**Recordset**並べ替えられた各フィールドが昇順または降順で並べ替えられるかどうか、およびします。|

## <a name="method-behavior"></a>メソッドの動作
 OLE DB のカーソル サービスを有効またはの動作に影響、[Field](../../../ado/reference/ado-api/field-object.md)オブジェクトの[Append](../../../ado/reference/ado-api/append-method-ado.md)メソッドと**Recordset**オブジェクトの[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)、[Resync](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)、および[Save](../../../ado/reference/ado-api/save-method.md)メソッド。
