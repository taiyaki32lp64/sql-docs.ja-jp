---
title: アドレス帳のデータ バインディング オブジェクト |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43623bc100fdfe071fcd00926117400a3c96eebe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922972"
---
# <a name="address-book-data-binding-object"></a>アドレス帳のデータ バインディング オブジェクト
アドレス帳アプリケーションを使用して、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)クライアント HTML ページで、アプリケーションの SQL Server データベースからデータを (この場合は、DHTML テーブル) 内のビジュアル オブジェクトにバインドするオブジェクト。 VBScript プログラムのイベント ドリブン ロジックを使用して、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)に。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
-   データベース クエリを実行、更新、データベースに送信し、データ グリッドを更新します。  
  
-   データ グリッドの前に、次に、最初に移動または最後のレコードにできます。  
  
 次のコード定義、 **rds.DataControl**コンポーネント。  
  
```vb
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 オブジェクト タグの定義、 **rds.DataControl**プログラムでコンポーネント。 タグには、2 種類パラメーターにはが含まれています。  
  
-   汎用の OBJECT タグに関連付けられているものとします。  
  
-   固有のもの、 **rds.DataControl**オブジェクト。  
  
## <a name="generic-object-tag-parameters"></a>汎用オブジェクト タグ パラメーター  
 次の表では、オブジェクト タグに関連付けられているパラメーターについて説明します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|***CLASSID***|システムに埋め込まれたオブジェクトの種類を識別する一意の 128 ビットの数。 この識別子は、ローカル コンピューターのシステム レジストリに保持されます。 (のクラス id、 **rds.DataControl**オブジェクトを参照してください[rds.DataControl オブジェクト](../../../ado/reference/rds-api/datacontrol-object-rds.md))。|  
|***ID***|コードでの識別に使用される埋め込みオブジェクトのドキュメント全体に対する識別子を定義します。|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>RDS.DataControl タグ パラメーター  
 次の表に固有のパラメーター、 **rds.DataControl**オブジェクト。 (の完全な一覧については、 **rds.DataControl**オブジェクトとパラメーターを使用すると、その実装を参照してください[rds.DataControl オブジェクト](../../../ado/reference/rds-api/datacontrol-object-rds.md))。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|[サーバー](../../../ado/reference/rds-api/server-property-rds.md)|HTTP を使用している場合、値は、前に、サーバー コンピューターの名前は`https://`します。|  
|[CONNECT](../../../ado/reference/rds-api/connect-property-rds.md)|必要な接続情報を提供、 **rds.DataControl** SQL サーバーに接続します。|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|設定または取得するために使用するクエリ文字列を返します、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。|  
  
## <a name="see-also"></a>関連項目  
 [アドレス帳のコマンド ボタン](../../../ado/guide/remote-data-service/address-book-command-buttons.md)


