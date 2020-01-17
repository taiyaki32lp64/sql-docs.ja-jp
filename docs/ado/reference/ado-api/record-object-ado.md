---
title: Record オブジェクト (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5ffc515350bfff4307da382c05aae50ed1930802
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917360"
---
# <a name="record-object-ado"></a>Record オブジェクト (ADO)
行を表す、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)またはデータ プロバイダー、あるいはファイルやディレクトリなどの半構造化データ プロバイダーによって返されるオブジェクト。  
  
## <a name="remarks"></a>コメント  
 A**レコード**オブジェクトは、データの 1 つの行を表しており、1 つの行といくつかの概念の類似性を持つ**Recordset**します。 プロバイダーの機能に応じて**レコード**オブジェクトは、1 つの行ではなく、プロバイダーから直接返される可能性があります**Recordset**ときに 1 行のみを選択する SQL クエリの例は、実行されます。 または、**レコード**から直接オブジェクトを取得できる、 **Recordset**オブジェクト。 または、**レコード**Microsoft Exchange の OLE DB プロバイダーなどの半構造化データに、プロバイダーから直接返されることができます。  
  
 関連付けられているフィールドを表示することができます、**レコード**でのオブジェクト、[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)コレクションに、**レコード**オブジェクト。 ADO では、オブジェクトの値を持つ列を含む**Recordset**、 **SafeArray**とでスカラー値、**フィールド**のコレクション**レコード**オブジェクト。  
  
 場合、**レコード**オブジェクト内の行を表します、**レコード セット**はその元に返すことのできる**レコード セット**で、[ソース](../../../ado/reference/ado-api/source-property-ado-record.md)プロパティ。  
  
 **レコード**オブジェクトも使用できますで半構造化データ プロバイダーなど、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)、ツリー構造の名前空間をモデル化します。 ツリー内の各ノードは、**レコード**関連付けられている列を持つオブジェクト。 列には、そのノードとその他の関連情報の属性を表すことができます。 **レコード**オブジェクトは、リーフ ノードとツリー構造内の非リーフ ノードの両方を表すことができます。 非リーフ ノードは、それらの内容として他のノードがリーフ ノードには、このような内容はありません。 通常、リーフ ノードにはデータのバイナリ ストリームが含まれてし、非リーフ ノードはそれらに関連付けられている既定のバイナリ ストリームにもあります。 プロパティを**レコード**オブジェクトは、ノードの種類を識別します。  
  
 **レコード**オブジェクトは、編成されたデータを階層的に移動するのも、別の方法を表します。 A**レコード**オブジェクトは、大規模なツリー構造内の特定のサブツリーのルートを表すために作成され、新しい可能性があります**レコード**子ノードを表すオブジェクトを開くことができます。  
  
 (たとえば、ファイルまたはディレクトリ) のリソースは、絶対 URL で一意に識別できます。 A[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトが暗黙的に作成されに設定、**レコード**オブジェクトと、**レコード**が絶対 URL を使用して開きます。 A**接続**オブジェクト明示的に設定する、**レコード**オブジェクトを使用して、 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)プロパティ。 ファイルとディレクトリを使用してアクセスできる、**接続**オブジェクトの定義、*コンテキスト*を**レコード**操作が発生する可能性があります。  
  
 データの変更とナビゲーション メソッド、**レコード**オブジェクトには、絶対 URL を使用してリソースを検索、相対 URL もそのまま使用または**接続**開始点として、オブジェクト コンテキスト。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
 A**接続**オブジェクトが互いに関連付けられている**レコード**オブジェクト。 そのため、**レコード**オブジェクトの操作を呼び出すことによって、トランザクションの一部をすることができます**接続**オブジェクトのトランザクション メソッドです。  
  
 **レコード**オブジェクトは、ADO のイベントをサポートしないし、通知には応答しません。  
  
 メソッドとプロパティの使用、**レコード**オブジェクトを次を行うことができます。  
  
-   設定または取得、関連付けられている**接続**オブジェクトを[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)プロパティ。  
  
-   アクセス許可を示す、[モード](../../../ado/reference/ado-api/mode-property-ado.md)プロパティ。  
  
-   によって表されるリソースが含まれている場合に、ディレクトリの URL を返す、**レコード**で、 [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)プロパティ。  
  
-   絶対 URL で、相対 URL を指定または**レコード セット**元となる、**レコード**は派生した、[ソース](../../../ado/reference/ado-api/source-property-ado-record.md)プロパティ。  
  
-   現在の状態を示す、**レコード**で、[状態](../../../ado/reference/ado-api/state-property-ado.md)プロパティ。  
  
-   種類を示す**レコード** - *単純*、*コレクション*、または*構造化ドキュメント*- で、 [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)プロパティ。  
  
-   使用して、非同期操作の実行を停止、[キャンセル](../../../ado/reference/ado-api/cancel-method-ado.md)メソッド。  
  
-   関連付けを解除、**レコード**でデータ ソースから、[閉じる](../../../ado/reference/ado-api/close-method-ado.md)メソッド。  
  
-   コピーしたファイルまたはディレクトリで表される、**レコード**で別の場所に、 [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)メソッド。  
  
-   削除、ファイルまたはディレクトリとサブディレクトリをによって表される、**レコード**で、 [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)メソッド。  
  
-   開く、 **Recordset**によって表されるエンティティのファイルとサブディレクトリを表す行を格納している、**レコード**で、 [GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)メソッド。  
  
-   移動 (変更)、ファイルまたはディレクトリとサブディレクトリ、によって表される、**レコード**で別の場所に、 [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)メソッド。  
  
-   関連付ける、**レコード**に既存のデータ ソース、または新しいファイルまたはディレクトリを作成、[オープン](../../../ado/reference/ado-api/open-method-ado-record.md)メソッド。  
  
 **レコード**オブジェクトがスクリプトを実行します。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Record オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [フィールド コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [レコードとストリーム](../../../ado/guide/data/records-and-streams.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
