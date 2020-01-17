---
title: レコード セット オブジェクト (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e76bc993b6f3fed781b8458bc7cf4a70081cd167
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931365"
---
# <a name="recordset-object-ado"></a>Recordset オブジェクト (ADO)
ベース テーブル、またはコマンドの実行の結果からレコードのセット全体を表します。 いつでもでも、 **Recordset**オブジェクトとして現在のレコード セット内で 1 つのレコードのみを参照します。  
  
## <a name="remarks"></a>コメント  
 使用する**Recordset**プロバイダーからデータを操作するオブジェクト。 ほぼすべてを使用してデータを操作する ADO を使用して、 **Recordset**オブジェクト。 すべて**Recordset**オブジェクトから成るレコード (行) とフィールド (列)。 プロバイダーによってサポートされている機能に応じていくつか**Recordset**メソッドまたはプロパティを使用できない可能性があります。  
  
 ADODB します。レコード セットが作成するために使用する必要があります、ProgID、 **Recordset**オブジェクト。 古い ADOR を参照する既存のアプリケーション。レコード セットの ProgID を再コンパイルせずに作業が続行されますが、新しい開発は、ADODB を参照する必要があります。レコード セット。  
  
 ADO で定義されている 4 つのカーソルの種類があります。  
  
-   **動的カーソル**内の移動のすべての種類は、表示、追加、変更、および他のユーザーによって削除することができます、 **Recordset**ブックマーク; に依存しないし、プロバイダーがサポートしている場合は、ブックマークを使用します。します。  
  
-   **キーセット カーソル**Behaves ことが表示されないレコード他のユーザーはその点を除いて、動的カーソルなどの追加、およびその他のユーザーを削除するレコードにアクセスできなくなります。 他のユーザーによるデータの変更も表示されます。 常にブックマークをサポートし、により、すべての種類内の移動のため、 **Recordset**します。  
  
-   **静的カーソル**一連のレコードを使用してデータを検索またはレポートを生成するための静的コピーを提供します; ブックマークは常に許可し、したがってすべての種類内の移動のでは、 **Recordset**します。 追加、変更、または他のユーザーによって削除は表示されません。 これは、唯一の種類のクライアント側を開いたときに許可されているカーソル**Recordset**オブジェクト。  
  
-   **順方向専用カーソル**を前方スクロールのみすることができます、 **Recordset**します。 追加、変更、または他のユーザーによって削除は表示されません。 これを単一のパスのみを作成する必要がある状況でパフォーマンスが向上する**レコード セット**します。  
  
 設定、 [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)プロパティを開始する前に、**レコード セット**、カーソルの種類を選択するか、渡す、 *CursorType*引数を[を開く](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッド。 一部のプロバイダーは、すべてのカーソルの種類でサポートされていません。 プロバイダーのマニュアルを確認します。 カーソルの種類を指定しない場合、ADO は、既定で順方向専用カーソルを開きます。  
  
 場合、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティに設定されて**adUseClient**を開く、 **Recordset**、 **UnderlyingValue** プロパティ[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクトが返されたでご利用いただけません**Recordset**オブジェクト。 作成することができます (OLE DB と組み合わせてで Microsoft SQL Server 用 Microsoft ODBC プロバイダー) などの一部のプロバイダーを併用すると、 **Recordset**以前に定義されたとは無関係にオブジェクト[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトとの接続文字列を渡すことによって、**オープン**メソッド。 ADO が作成されますが、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトが、オブジェクト変数にそのオブジェクトを割り当てていません。 ただし、複数開いている場合**Recordset** 、同じ接続経由でオブジェクトを明示的に作成し、開く必要があります、**接続**オブジェクトこの割り当て、**接続**。オブジェクト変数にオブジェクト。 開くときに、このオブジェクトの変数を使用しないかどうか、**レコード セット**オブジェクトの場合、ADO が新たに作成**接続**ごとに新しいオブジェクト**Recordset**同じを渡す場合にも、接続文字列。  
  
 数だけ作成できます**Recordset**に応じてオブジェクトします。  
  
 開くと、**レコード セット**、最初のレコードを現在のレコードが配置されている (該当する場合)、 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)と[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)プロパティに設定されます**False**. レコードがない場合、 **BOF**と**EOF**プロパティの設定は**True**します。  
  
 使用することができます、 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 **MoveLast**、 **MoveNext**、および**MovePrevious**メソッドは、[移動](../../../ado/reference/ado-api/move-method-ado.md)メソッド。および[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)、 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)、および[フィルター](../../../ado/reference/ado-api/filter-property.md)プロパティ プロバイダーが、関連するサポートするいると仮定すると、現在のレコードの位置を変更するには機能。 順方向専用**Recordset**オブジェクトのみをサポート、 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)メソッド。 使用する場合、**移動**各レコードにアクセスする方法 (または列挙、**レコード セット**)、使用することができます、 **BOF**と**EOF**プロパティ先頭または末尾のを超えて移動したかどうかの判断、 **Recordset**します。  
  
 機能を使用する前に、 **Recordset**オブジェクトを呼び出す必要があります、**サポート**機能がサポートされているか使用可能であることを確認するオブジェクトのメソッド。 機能を使用する必要があるときに、**サポート**メソッドが false を返します。 たとえば、使用することができます、 **MovePrevious**メソッド場合にのみ`Recordset.Supports(adMovePrevious)`返します**True**します。 それ以外の場合、エラーが発生する、ため、 **Recordset**オブジェクトが閉じられている可能性があり、インスタンスで使用できなくなった機能が表示されます。 興味のある機能がサポートされていない場合**サポート**も false に戻ります。 対応するプロパティまたはメソッドの呼び出しを避ける必要があります、ここで、 **Recordset**オブジェクト。  
  
 **レコード セット**オブジェクトは、2 種類の更新をサポートできます: イミディ エイト ウィンドウとバッチ処理します。 即時更新では、データに対するすべての変更直ちに書き込まれます、基になるデータ ソースを呼び出すと、 [Update](../../../ado/reference/ado-api/update-method.md)メソッド。 パラメーターとして値の配列を渡すことも、 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)と**更新**メソッドを同時に、レコード内のいくつかのフィールドを更新します。  
  
 1 つ以上のレコードへの変更をキャッシュし、使用してデータベースに 1 回の呼び出しで送信するプロバイダーはプロバイダーでは、バッチ更新をサポートする場合、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)メソッド。 これに加えられた変更を適用されます、 **AddNew**、 **Update**、および[削除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)メソッド。 呼び出した後、 **UpdateBatch**メソッドが使用できる、[状態](../../../ado/reference/ado-api/status-property-ado-recordset.md)それらを解決するために、データの競合を確認するプロパティ。  
  
> [!NOTE]
>  クエリの実行を使用せずに、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト、クエリ文字列を渡す、**オープン**のメソッド、**レコード セット**オブジェクト。 ただし、**コマンド**コマンド テキストを保持し、再実行するか、またはクエリ パラメーターを使用する場合は、オブジェクトが必要です。  
  
 [モード](../../../ado/reference/ado-api/mode-property-ado.md)プロパティへのアクセス権限を制御します。  
  
 **フィールド**コレクションがの既定のメンバー、 **Recordset**オブジェクト。 その結果、次の 2 つのコード ステートメントは同等です。  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 ときに、**レコード セット**のみ、プロセス間でオブジェクトが渡される、**行セット**値は、マーシャ リングとのプロパティ、**レコード セット**オブジェクトは無視されます。 います、中に、**行セット**、新しく作成されたにアンパック**レコード セット**オブジェクトで、既定値にもそのプロパティを設定します。  
  
 **Recordset**オブジェクトがスクリプトを実行します。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [レコード セット オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [フィールド コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
