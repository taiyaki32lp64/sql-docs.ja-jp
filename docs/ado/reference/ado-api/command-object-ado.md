---
title: コマンド オブジェクト (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbce299e2e9f67b705f940480913c7d8ac367d0d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919794"
---
# <a name="command-object-ado"></a>Command オブジェクト (ADO)
データ ソースに対して実行する特定のコマンドを定義します。  
  
## <a name="remarks"></a>コメント  
 使用して、**コマンド**データベースを照会して、レコードを取得するオブジェクト、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト、データベースの構造を操作したり、一括操作を実行します。 プロバイダーの機能をいくつかに応じて**コマンド**参照されている場合、コレクション、メソッド、またはプロパティすると、エラーが発生する可能性があります。  
  
 コレクション、メソッド、およびプロパティの使用、**コマンド**オブジェクトを次を行うことができます。  
  
-   コマンド (たとえば、SQL ステートメント) の実行可能ファイルのテキストの定義、 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)プロパティ。 または、コマンドまたはクエリ構造よりも単純なその他の文字列 (たとえば、XML テンプレートのクエリ) を定義してコマンドを[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)プロパティ。  
  
-   必要に応じてで使用されるコマンド言語を示す、 **CommandText**または**CommandStream**で、[言語](../../../ado/reference/ado-api/dialect-property.md)プロパティ。  
  
-   パラメーター化クエリまたはストアド プロシージャの引数と定義[パラメーター](../../../ado/reference/ado-api/parameter-object.md)オブジェクトと[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)コレクション。  
  
-   使用してプロバイダーをパラメーター名を渡す必要があるかどうかを示す、 [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md)プロパティ。  
  
-   コマンドを実行し、返す、 **Recordset**オブジェクトで該当する場合、 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)メソッド。  
  
-   コマンドの種類を指定、 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)パフォーマンスを最適化するために実行する前にプロパティ。  
  
-   プロバイダーを実行する前に、コマンドの準備済み (またはコンパイル済み) のバージョンを保存するかどうかを制御、[準備](../../../ado/reference/ado-api/prepared-property-ado.md)プロパティ。  
  
-   プロバイダーがコマンドの実行を待機する秒数を設定、 [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)プロパティ。  
  
-   開いている接続を関連付ける、**コマンド**オブジェクトを設定してその[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)プロパティ。  
  
-   設定、[名前](../../../ado/reference/ado-api/name-property-ado.md)プロパティを識別するために、**コマンド**オブジェクトに関連付けられているメソッドとして[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。  
  
-   渡す、**コマンド**オブジェクトを[ソース](../../../ado/reference/ado-api/source-property-ado-recordset.md)のプロパティを**レコード セット**データを取得します。  
  
-   プロバイダーに固有の属性へのアクセス、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション。  
  
> [!NOTE]
>  クエリの実行を使用せずに、**コマンド**オブジェクト、クエリ文字列を渡す、 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)のメソッド、**接続**オブジェクトまたは、 [を開く](../../../ado/reference/ado-api/open-method-ado-recordset.md)のメソッド、 **Recordset**オブジェクト。 ただし、**コマンド**コマンド テキストを保持し、再実行するか、またはクエリ パラメーターを使用する場合は、オブジェクトが必要です。  
  
 作成する、**コマンド**以前に定義されたとは無関係にオブジェクト**接続**オブジェクト、設定、 **ActiveConnection**プロパティを有効な接続文字列にします。 ADO が作成されますが、**接続**オブジェクトが、これはそのオブジェクトに割り当てませんオブジェクト変数です。 ただし、複数を関連付ける場合**コマンド**同じ接続では、オブジェクトを明示的に作成し、開く、**接続**オブジェクトこの割り当て、 **の接続。** オブジェクト変数にオブジェクト。 確認、**接続**に割り当てる前に、オブジェクトが正常に開かれた、 **ActiveConnection**のプロパティ、**コマンド**オブジェクトを割り当てるため、閉じられた**接続**オブジェクト、エラーが発生します。 設定しない場合、 **ActiveConnection**のプロパティ、**コマンド**ADO 新たに作成しますが、このオブジェクトの変数にオブジェクト**接続**オブジェクトごとに**コマンド**オブジェクト、同じ接続文字列を使用する場合でもです。  
  
 実行する、**コマンド**、呼び出すことの[名前](../../../ado/reference/ado-api/name-property-ado.md)プロパティに関連付けられている**接続**オブジェクト。 **コマンド**必要があります、 **ActiveConnection**プロパティに設定、**接続**オブジェクト。 場合、**コマンド**はその値を引数としてメソッドに渡すパラメーターがあります。  
  
 2 つ以上の場合**コマンド**オブジェクトが同じ接続し、いずれかで実行される**コマンド**オブジェクトが出力パラメーターを使用してストアド プロシージャであり、エラーが発生します。 各を実行する**コマンド**オブジェクト、個別の接続を使用して、またはその他のすべての接続を切断**コマンド**接続からのオブジェクト。  
  
 **パラメーター**コレクションがの既定のメンバー、**コマンド**オブジェクト。 その結果、次の 2 つのコード ステートメントは同等です。  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   **コマンド**オブジェクトは、スクリプトを実行することはありません。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [コマンド オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Parameters コレクション (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
