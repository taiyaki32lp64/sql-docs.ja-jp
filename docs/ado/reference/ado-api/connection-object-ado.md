---
title: 接続オブジェクト (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 278e2d90ed20b99706f00acf72e2892941c42865
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933561"
---
# <a name="connection-object-ado"></a>Connection オブジェクト (ADO)
データ ソースへの接続を開くを表します。  
  
## <a name="remarks"></a>コメント  
 A**接続**オブジェクトは、データ ソースとの一意のセッションを表します。 クライアント/サーバー データベース システムでは、サーバーへの実際のネットワーク接続と同じ場合があります。 プロバイダー、いくつかのコレクション、メソッド、またはのプロパティでサポートされる機能によって、**接続**オブジェクトを使用できない可能性があります。  
  
 コレクション、メソッド、およびプロパティの使用、**接続**オブジェクトを次を行うことができます。  
  
-   開く前に、接続の構成、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)、 [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)、および[モード](../../../ado/reference/ado-api/mode-property-ado.md)プロパティ。 **ConnectionString**の既定のプロパティ、**接続**オブジェクト。  
  
-   設定、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを呼び出すクライアントを[OLE DB 用の Microsoft カーソル サービス](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)を一括更新をサポートしています。  
  
-   既定のデータベースとの接続の設定、 [DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)プロパティ。  
  
-   セットとの接続でのトランザクションの分離レベルが開かれて、 [IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)プロパティ。  
  
-   OLE DB プロバイダーの指定、[プロバイダー](../../../ado/reference/ado-api/provider-property-ado.md)プロパティ。  
  
-   を確立し、データ ソースに物理接続は切断後で、[オープン](../../../ado/reference/ado-api/open-method-ado-connection.md)と[閉じる](../../../ado/reference/ado-api/close-method-ado.md)メソッド。  
  
-   コマンドとの接続を実行して、 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)メソッドの実行を構成して、 [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)プロパティ。  
  
    > [!NOTE]
    >  コマンド オブジェクトを使用せずに、クエリを実行するクエリ文字列を渡す、 **Execute**のメソッド、**接続**オブジェクト。 ただし、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)コマンド テキストを保持し、再実行するか、またはクエリ パラメーターを使用する場合は、オブジェクトが必要です。  
  
-   プロバイダーは、それらをサポートしている場合は、入れ子になったトランザクションを含む、開いている接続でトランザクションを管理、 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)、 [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)、および[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)メソッドおよび[属性](../../../ado/reference/ado-api/attributes-property-ado.md)プロパティ。  
  
-   持つデータ ソースから返されたエラーを調べて、[エラー](../../../ado/reference/ado-api/errors-collection-ado.md)コレクション。  
  
-   使用される ADO 実装からバージョンを読み取る、[バージョン](../../../ado/reference/ado-api/version-property-ado.md)プロパティ。  
  
-   使用してデータベースに関するスキーマ情報を取得、 [OpenSchema](../../../ado/reference/ado-api/openschema-method.md)メソッド。  
  
 作成することができます**接続**他の定義済みのオブジェクトとは無関係にオブジェクト。  
  
 場合と同様、ネイティブ メソッドの名前付きコマンドまたはストアド プロシージャを実行することができます、**接続**オブジェクト、次のセクションで示すようにします。 名前付きコマンドは、ストアド プロシージャの場合と同じ名前で、「ネイティブ メソッドの呼び出し」を呼び出す、**接続**オブジェクトは常にストアド プロシージャではなく名前付きコマンドを実行します。  
  
> [!NOTE]
>  この機能を使用しない (でネイティブ メソッドがあるかのように、名前付きコマンドまたはストアド プロシージャを呼び出す、**接続**オブジェクト)、Microsoft® .NET Framework アプリケーションのため、機能の競合の基になる実装方法と、.NET Framework に com 相互運用します。  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>接続オブジェクトのネイティブ メソッドとしてコマンドを実行します。  
 コマンドを実行するコマンドを指定の名前を使用して、**コマンド**オブジェクト[名前](../../../ado/reference/ado-api/name-property-ado.md)プロパティ。 設定、 **ActiveConnection**のプロパティ、**コマンド**オブジェクトに接続します。 メソッドがあるかのように、コマンド名が使用されているステートメントを発行し、**接続**任意のパラメーターの前に、オブジェクトと**レコード セット**オブジェクトのかどうか、すべての行が返されます。 設定、 **Recordset**プロパティ、その結果をカスタマイズする**レコード セット**します。 以下に例を示します。  
  
```  
Dim cnn As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
...  
cnn.Open "..."  
cmd.Name = "yourCommandName"  
cmd.ActiveConnection = cnn  
...  
'Your command name, any parameters, and an optional Recordset.  
cnn. "parameter", rst  
```  
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>接続オブジェクトのネイティブ メソッドとしてストアド プロシージャを実行します。  
 ストアド プロシージャを実行するには、上のメソッドがあるかのように、ストアド プロシージャ名が使用されているステートメントを発行、**接続**任意のパラメーターの前に、オブジェクト。 ADO は、パラメーターの型の「最善の推測」になります。 以下に例を示します。  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 **接続**オブジェクトがスクリプトを実行します。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [接続オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [コマンド オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [エラーのコレクション (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [RecordSet オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
