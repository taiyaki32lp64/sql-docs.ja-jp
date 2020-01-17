---
title: サーバー プロパティ (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d196a60986734c5717be9711af1fa28accee414
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963472"
---
# <a name="server-property-rds"></a>Server プロパティ (RDS)
インターネット インフォメーション サービス (IIS) の名前との通信プロトコルを示します。  
  
 設定することができます、 **Server**のオブジェクト タグでは、デザイン時プロパティ、[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト、またはスクリプト コードの実行時にします。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
 **HTTP**  
  
 デザイン時の構文  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 実行時の構文  
  
```  
  
DataControl  
.Server="https://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 デザイン時の構文  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 実行時の構文  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 デザイン時の構文  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 実行時の構文  
  
```  
  
DataControl.Server="computername"  
```  
  
 **インプロセス**  
  
 デザイン時の構文  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 実行時の構文  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>パラメーター  
 *awebsrvr*または*computername*  
 A**文字列**サーバーは、サーバーがローカル コンピューターの場合、リモート コンピューター、または空の文字列がある場合、インターネットまたはイントラネットのパス、またはコンピューターの名前を表す値です。  
  
 *port*  
 任意。 IIS を実行しているサーバーに接続するために使用するポート。 Internet Explorer で、ポート番号を設定 (上、**ビュー**  メニューのをクリックして**オプション**を選び、**接続** タブ) または IIS でします。  
  
 *DataControl*  
 オブジェクト変数を表す、 **rds.DataControl**オブジェクト。  
  
## <a name="remarks"></a>コメント  
 サーバーの場所は、場所、 **rds.DataControl** (つまり、クエリまたは更新) 要求を処理します。 によって既定では、すべての要求の処理、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)オブジェクト、 [MSDFMAP します。ハンドラー](../../../ado/guide/remote-data-service/datafactory-customization.md)コンポーネント、および[MSDFMAP します。INI](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)指定したサーバー上のファイル。 古いと新しい設定を調整するサーバーを変更するときに注意する**MSDFMAP します。INI**ファイル。 非互換性は、別の失敗を 1 つのサーバーで成功した要求を引き起こす可能性が。 サーバー プロパティが空の文字列に設定されている場合""、これらのオブジェクトは、ローカル コンピューターで使用されます。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [サーバー プロパティの例 (VBScript)](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [接続プロパティ (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [SQL プロパティ](../../../ado/reference/rds-api/sql-property.md)   
 [SubmitChanges メソッド (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


