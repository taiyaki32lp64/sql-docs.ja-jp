---
title: DataControl オブジェクト (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a571e93a070c3ce07fbaf40a86b762c749042ec1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964401"
---
# <a name="datacontrol-object-rds"></a>DataControl オブジェクト (RDS)
データのクエリをバインド[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)を 1 つまたは複数のコントロール (たとえば、テキスト ボックス、取引先グリッド コントロール、またはコンボ ボックス) を表示する、**レコード セット**Web ページ上のデータ。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>コメント  
 クラス ID を**rds.DataControl**オブジェクトが BD96C556 65A3-11 D 00C04FC29E33 983A 0。  
  
> [!NOTE]
>  エラーが発生する場合、 [rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)または**rds.DataControl**オブジェクトから読み込み、正しいクラス ID を使用しているかどうかを確認できません クラスは、これらのオブジェクトの Id は、バージョン 1.0 および 1.1 から変更されました。 また、あるを使用する場合でも null 許容列を設定する必要があります、 **RDS DataControl**オブジェクト。  
  
 基本的なシナリオでのみ設定する必要があります、 **SQL**、 **Connect**、および**Server**のプロパティ、 **rds.DataControl**オブジェクトで、既定のビジネス オブジェクトの呼び出しに自動的には、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)します。  
  
 すべてのプロパティ、 **rds.DataControl**カスタム ビジネス オブジェクトがそれらの機能を置き換えるためには、省略可能です。  
  
> [!NOTE]
>  複数の結果を照会する場合、最初のみ[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)が返されます。 複数の結果セットが必要な場合のそれぞれを独自に割り当てる**DataControl**します。 複数の結果に対するクエリの例は、次になります。 `"Select * from Authors, Select * from Topics"`  
  
 追加する"DFMode = 20 です"を接続文字列を使用する場合、 **rds.DataControl**データを更新するときに、オブジェクトが、サーバーのパフォーマンスを向上させることができます。 この設定で、 **RDSServer.DataFactory**サーバー上のオブジェクトが少ないリソースを消費するモードを使用します。 ただし、次の機能では、この構成では使用できません。  
  
-   パラメーター化クエリを使用します。  
  
-   呼び出しの前に、パラメーターまたは列の情報の取得、 **Execute**メソッド。  
  
-   設定**更新プログラムを Transact**に**True**します。  
  
-   行の状態を取得します。  
  
-   呼び出す、[再同期](../../../ado/reference/ado-api/resync-method.md)メソッド。  
  
-   (明示的または自動) の更新を使用して、 [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)プロパティ。  
  
-   設定**コマンド**または[Recordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)プロパティ。  
  
-   使用して**adCmdTableDirect**します。  
  
 **Rds.DataControl**オブジェクトは、既定で非同期モードで実行されます。 アプリケーションの同期の実行が必要な場合は、設定、 [ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md)パラメーターと等しい**adcExecSync**と[FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md) パラメーター**adcFetchUpFront**次の例のようにします。  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 1 つを使用して、 **rds.DataControl** 1 つまたは複数のビジュアル コントロールに 1 つのクエリの結果をリンクするオブジェクト。 たとえば、名前、住所、出生、年齢、および優先順位の顧客のステータスなどのクエリ要求している顧客データをコードがあるとします。 1 つを使用する**rds.DataControl** ; 3 つの別のテキスト ボックスに、顧客の名前、年齢、およびリージョンを表示するオブジェクトチェック ボックスでの優先順位の顧客のステータスグリッド コントロール内のすべてのデータ。  
  
 使用して異なる**rds.DataControl**異なるビジュアル コントロールに複数のクエリの結果をリンクするオブジェクト。 たとえば、1 つのクエリ、顧客に関する情報を取得して、顧客が購入した商品に関する情報を取得する 2 番目のクエリを使用するとします。 3 つのテキスト ボックスとチェック ボックスを 1 つのグリッド コントロールで 2 番目のクエリ結果の最初のクエリの結果を表示するには。 既定のビジネス オブジェクトを使用する場合 (**RDSServer.DataFactory**)、次を行う必要があります。  
  
-   2 つ追加**rds.DataControl** Web ページへのオブジェクト。  
  
-   2 つの書き込み、クエリごとに 1 つ**SQL** 、2 つのプロパティ**rds.DataControl**オブジェクト。 1 つ**rds.DataControl**オブジェクトは、顧客情報を要求する SQL クエリが格納されます。 2 つ目は、顧客が購入した商品の一覧を要求するクエリが含まれます。  
  
-   各バインドされたコントロールのオブジェクト タグで、各ビジュアル コントロールに表示するデータの値を設定する DATAFLD 値を指定します。  
  
 数の数の制限はありません**rds.DataControl**オブジェクトを 1 つの Web ページで、オブジェクト タグを使用して埋め込むことができます。  
  
 定義するときに、 **rds.DataControl** Web ページ上のオブジェクト、0 以外の値を使用して、**高さ**と**幅**1 (を余分なスペースを含めることを避けるため) などの値。  
  
 Internet Explorer 4.0; の一部として含まれているリモート データ サービスのクライアント コンポーネントそのため、必要はありませんでコードベースのパラメーターを含む、 **rds.DataControl**オブジェクト タグ。  
  
 Internet Explorer 4.0 以降、アパートメント モデルのコントロールとしてマークされている場合にのみ、HTML コントロールおよび ActiveX® コントロールを使用してデータにバインドすることができます。  
  
> [!NOTE]
>  **Microsoft Visual Basic ユーザー** 、 **rds.DataControl**のスクリプトが安全と Web ベースのアプリケーションでのみ使用されます。 Visual Basic のクライアント アプリケーションには、その必要はありません。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [DataControl オブジェクト (RDS) のプロパティ、メソッド、およびイベント](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [DataControl オブジェクトの例 (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















