---
title: RDS のプログラミング モデルの詳細 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d7251e3a403168e8383e636a8e6b5f712b9f7bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922527"
---
# <a name="rds-programming-model-in-detail"></a>RDS のプログラミング モデルの詳細
以下は、RDS のプログラミング モデルの主な要素です。  
  
-   RDS.DataSpace  
  
-   RDSServer.DataFactory  
  
-   RDS.DataControl  
  
-   event  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 クライアント アプリケーションには、サーバーおよび起動するサーバーのプログラムを指定する必要があります。 代わりに、アプリケーションでは、サーバー プログラムへの参照を受信し、サーバー プログラム自体の場合と同様に、参照を扱うことができます。  
  
 RDS オブジェクト モデルでのこの機能を実現する、 [rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)オブジェクト。  
  
 プログラム識別子を持つサーバー プログラムを指定または*ProgID*します。 サーバーを使用して、 *ProgID*およびサーバー コンピューターのレジストリを開始する実際のプログラムに関する情報を検索します。  
  
 RDS は、インターネットまたはイントラネット; の間でリモート サーバーでサーバーのプログラムがあるかによって内部的に区別ローカル エリア ネットワーク; 上のサーバーまたは、すべてのサーバーではなくが代わりに、ローカルのダイナミック リンク ライブラリ (DLL) にします。 情報のクライアントとサーバー間で交換され、クライアント アプリケーションに返される参照の型の具体的な違いは、この区別を決定します。 ただしの観点から、このような区別特殊は意味がありません。 重要なは、使用可能なプログラムの参照を受け取ります。  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 RDS は、データ ソースと戻り値に対して SQL クエリを実行できるか、既定のサーバー プログラムを提供します、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトまたは、**レコード セット**オブジェクトし、データ ソースを更新します。  
  
 RDS オブジェクト モデルでのこの機能を実現する、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)オブジェクト。  
  
 また、このオブジェクトでは、空の作成方法の**レコード セット**オブジェクトをプログラムで入力することができます ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md))、および変換するための別のメソッドを**レコード セット**を Web ページを構築するテキスト文字列にオブジェクト ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md))。  
  
 標準の接続の一部とのコマンドの動作をオーバーライドする、ADO を使用した、 **RDSServer.DataFactory**で、 **DataFactory**ハンドラーと、接続が含まれているカスタマイズ ファイルは、次のコマンドをおよびセキュリティ パラメーター。  
  
 サーバーのプログラムとも呼ばれます、*ビジネス オブジェクト*します。 複雑なデータ アクセスや妥当性検査を実行できる、独自のカスタム ビジネス オブジェクトを記述することができます。 インスタンスを作成するには、カスタム ビジネス オブジェクトを記述する場合でも、 **RDSServer.DataFactory**オブジェクトをそのメソッドの一部を使用して、独自のタスクを実行します。  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 RDS の機能を結合するための手段を提供する、 **rds.DataSpace**と**RDSServer.DataFactory**も簡単に使用するビジュアル コントロールを有効にして、 **Recordset**データ ソースからクエリによって返されるオブジェクト。 RDS は、自動的にサーバー上の情報にアクセスしてビジュアル コントロールで表示可能な限り行う、最も一般的なケースを試行します。  
  
 RDS オブジェクト モデルでのこの機能を実現する、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト。  
  
 **Rds.DataControl**は 2 つの側面があります。 1 つの側面は、データ ソースに関連します。 コマンドと接続情報を使用して設定した場合、 **Connect**と**SQL**のプロパティ、 **rds.DataControl**が自動的に使用されている、 **rds.DataSpace**既定値への参照を作成する**RDSServer.DataFactory**オブジェクト。 **RDSServer.DataFactory**を使用して、 **Connect**プロパティの値をデータ ソースへの接続を使用、 **SQL**プロパティの値を取得、 **レコード セット**データ ソース、および戻り値から、 **Recordset**オブジェクトを**rds.DataControl**します。  
  
 2 つ目の側面に関連の表示に返される**Recordset**ビジュアル コントロール内の情報。 ビジュアルなコントロールに関連付けることができます、 **rds.DataControl** (バインディングと呼ばれるプロセス) 内で関連付けられている情報にアクセスできると**レコード セット**Microsoft® Internet Explorer で Web ページ上のクエリの結果を表示するオブジェクト。 各**rds.DataControl**オブジェクトは 1 つにバインド**Recordset** (たとえば、テキスト ボックス、コンボ ボックス、グリッド コントロールとなど) 1 つまたは複数のビジュアル コントロールへの 1 つのクエリの結果を表すオブジェクト。 1 つ以上あります**rds.DataControl**各ページ上のオブジェクト。 各**rds.DataControl**オブジェクトが別のデータ ソースに接続できるし、別のクエリの結果が含まれます。  
  
 **Rds.DataControl**オブジェクトに移動、並べ替え、および関連付けられている行をフィルター処理の独自のメソッドもあります**Recordset**オブジェクト。 これらのメソッドと同様に、ADO 上のメソッドとして同じ**Recordset**オブジェクト。  
  
## <a name="events"></a>イベント  
 RDS では、独自のイベントは、ADO イベント モデルとは無関係の 2 つサポートしています。 [OnReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md)イベントが呼び出されるたびに、 **rds.DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)プロパティの変更を非同期操作が正常に完了したら、通知を終了すると、またはエラーが発生しました。 [OnError](../../../ado/reference/rds-api/onerror-event-rds.md)イベントは、その非同期操作中にエラーが発生した場合でもエラーが発生するたびに呼び出されます。  
  
> [!NOTE]
>  Microsoft Internet Explorer では、RDS の 2 つの追加イベント:**詳細**、ことを示します、**レコード セット**機能ですがまだ、行を取得するには、 **詳細について**、ことを示します、 **Recordset**行の取得が完了します。  
  
## <a name="see-also"></a>関連項目  
 [RDS のプログラミング モデルとオブジェクト](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory オブジェクト (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace オブジェクト (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS のシナリオ](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS チュートリアル](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS の使用方法とセキュリティ](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



