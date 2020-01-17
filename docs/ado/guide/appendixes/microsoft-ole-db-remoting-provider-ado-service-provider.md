---
title: Microsoft OLE DB のリモート処理 Provider (サービス プロバイダーの ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5c60567da677564c168f0601625686bdfb8b3d67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926598"
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Microsoft OLE DB リモート処理のプロバイダーの概要
Microsoft OLE DB リモート処理プロバイダーにより、リモート コンピューター上のデータ プロバイダーを呼び出すため、クライアント コンピューター上のローカル ユーザーです。 リモート コンピューター上のローカル ユーザーをした場合と同様に、リモート コンピューターのデータ プロバイダーのパラメーターを指定します。 次に、リモート コンピューターにアクセスするリモート処理のプロバイダーによって使用されるパラメーターを指定します。 ローカル ユーザーをした場合と、リモート コンピューターをアクセスできます。

> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。

## <a name="provider-keyword"></a>プロバイダーのキーワード
 OLE DB リモート処理プロバイダーを起動するには、接続文字列で、次のキーワードと値を指定します。 (プロバイダー名に空白を注意してください)。

```vb
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>その他のキーワード
 このサービス プロバイダーが呼び出されたときに次の他のキーワードが関連します。

|Keyword|説明|
|-------------|-----------------|
|**Data Source**|リモート データ ソースの名前を指定します。 処理のための OLE DB リモート プロバイダーに渡されます。<br /><br /> このキーワードは等しく、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトの[Connect](../../../ado/reference/rds-api/connect-property-rds.md)プロパティ。|

## <a name="dynamic-properties"></a>動的プロパティ
 このサービス プロバイダーが呼び出されたときに、次の動的なプロパティに追加されます、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション。

|動的なプロパティ名|説明|
|---------------------------|-----------------|
|**DFMode**|DataFactory のモードを示します。 目的のバージョンを指定する文字列、 [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)サーバー上のオブジェクト。 特定のバージョンの要求への接続を開く前に、このプロパティを設定、 **DataFactory**します。 要求されたバージョンが利用できない場合は試行前のバージョンを使用します。 前のバージョンがない場合は、エラーが発生します。 場合**DFMode**が利用可能なバージョンより小さい、エラーが発生します。 このプロパティは、接続の確立後は読み取り専用です。<br /><br /> 有効な文字列値は次のいずれかを指定できます。<br /><br /> -「25」、バージョン 2.5 (既定値)<br />-「21」、バージョン 2.1<br />-「20」-version 2.0<br />-「15」のバージョン 1.5|
|**コマンドのプロパティ**|MS リモート プロバイダーによって、サーバーに送信されるコマンド (行セット) のプロパティの文字列に追加される値を示します。 この文字列の既定値は、vt_empty です。|
|**現在 DFMode**|実際のバージョンの数を示す、 **DataFactory**サーバー。 バージョンが要求されたかどうかに表示するには、このプロパティを確認、 **DFMode**プロパティが受け入れられます。<br /><br /> 長整数型の有効な値は次のいずれかを指定できます。<br /><br /> -25 バージョン 2.5 (既定値)<br />-21 バージョン 2.1<br />-20 version 2.0<br />-15 version 1.5<br /><br /> 追加する"DFMode = 20 です。"を接続文字列を使用する場合、 **MSRemote**データを更新するときに、プロバイダーがサーバーのパフォーマンスを向上させることができます。 この設定で、 **RDSServer.DataFactory**サーバー上のオブジェクトが少ないリソースを消費するモードを使用します。 ただし、次の機能では、この構成では使用できません。<br /><br /> -パラメーター化クエリを使用します。<br />-呼び出しの前にパラメーターまたは列の情報の取得、 **Execute**メソッド。<br />-設定**更新プログラムを Transact**に**True**します。<br />-行のステータスを取得します。<br />-呼び出し、**再同期**メソッド。<br />-(明示的または自動) の更新を使用して、 **Update Resync**プロパティ。<br />-設定**コマンド**または**Recordset**プロパティ。<br />-を使用して**adCmdTableDirect**します。|
|**ハンドラー**|機能を拡張するサーバー側のカスタマイズのプログラム (またはハンドラー) の名前を示します、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)コンマで区切った、ハンドラーによって使用される任意のパラメーターすべて (「,」)。 **文字列**値です。|
|**インターネット タイムアウト。**|要求と、サーバーの間を移動するを待機するミリ秒の最大数を示します。 (既定値は 5 分です)。|
|**リモート プロバイダー**|リモート サーバーで使用するデータ プロバイダーの名前を示します。|
|**リモート サーバー**|この接続で使用されるサーバー名との通信プロトコルを示します。 このプロパティは、 [rds.DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト[Server](../../../ado/reference/rds-api/server-property-rds.md)プロパティ。|
|**更新プログラムを transact します。**|設定すると**True**、この値をすることを示します[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)が実行されますが、サーバーで、トランザクション内で行われます。 このブール型の動的プロパティの既定値は**False**します。|

 接続文字列のキーワードとしてその名前を指定することで書き込み可能な動的プロパティを設定することもできます。 たとえば、設定、**インターネット タイムアウト**動的プロパティを指定することで、5 秒に。

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 設定またはのインデックスとしてその名前を指定することによって動的なプロパティを取得することがありますも、**プロパティ**プロパティ。 次の例では、取得し、現在の値を出力する方法を示しています、**インターネット タイムアウト**動的プロパティは、および新しい値に設定します。

```vb
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>コメント
 Ado 2.0 では、OLE DB リモート処理プロバイダーのみで指定、 *ActiveConnection*のパラメーター、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト**オープン**メソッド。 ADO 2.1 以降では、プロバイダーが指定することもに、 *ConnectionString*のパラメーター、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト**オープン**メソッド。

 同等の**rds.DataControl**オブジェクト[SQL](../../../ado/reference/rds-api/sql-property.md)プロパティは使用できません。 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト**オープン**メソッド*ソース*引数が代わりに使用されます。

 **注**"...; を指定します。リモート プロバイダー MS リモートを = です。 ..."4 層のシナリオを作成します。 3 つのレベルを超えたシナリオでは、テストされていないと、必要はありません。

## <a name="example"></a>例
 この例のクエリを実行する、**作成者**のテーブル、 **Pubs**という名前のサーバー上のデータベース*通常*します。 リモート データ ソースとリモート サーバーの名前が提供されている、[オープン](../../../ado/reference/ado-api/open-method-ado-connection.md)のメソッド、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト、および SQL クエリがで指定された、[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)のメソッド、[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。 A **Recordset**オブジェクトが返された、編集、およびデータ ソースを更新するために使用します。

```vb
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=https://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>関連項目
 [OLE DB のリモート処理のプロバイダーの概要](https://msdn.microsoft.com/4083b72f-68c4-4252-b366-abb70db5ca2b)
