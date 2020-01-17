---
title: SubmitChanges メソッド (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 783ad55a2355759f7625d536272f5243cd1c61c4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963287"
---
# <a name="submitchanges-method-rds"></a>SubmitChanges メソッド (RDS)
保留中のローカル キャッシュと更新の変更を送信する[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)で指定されたデータ ソースに、 [Connect](../../../ado/reference/rds-api/connect-property-rds.md)プロパティまたは[URL](../../../ado/reference/rds-api/url-property-rds.md)プロパティ。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 オブジェクト変数を表す、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト。  
  
 *DataFactory*  
 オブジェクト変数を表す、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)オブジェクト。  
  
 *Connection*  
 A**文字列**で作成された接続を表す値、 **rds.DataControl**オブジェクトの[Connect](../../../ado/reference/rds-api/connect-property-rds.md)プロパティ。  
  
 *レコード セット*  
 オブジェクト変数を表す、 **Recordset**オブジェクト。  
  
## <a name="remarks"></a>コメント  
 [Connect](../../../ado/reference/rds-api/connect-property-rds.md)、 [Server](../../../ado/reference/rds-api/server-property-rds.md)、および[SQL](../../../ado/reference/rds-api/sql-property.md)を使用するには、プロパティを設定する必要があります、 **SubmitChanges**メソッドを**RDS.DataControl**オブジェクト。  
  
 呼び出す場合、 [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md)メソッドを呼び出した後**SubmitChanges**同じ**Recordset**オブジェクト、 **CancelUpdate**変更がコミット済みの呼び出しは失敗します。  
  
 成功または失敗するすべての変更、変更、および変更のすべての変更されたレコードだけが送信されます。  
  
 使用することができます**SubmitChanges**既定値でのみ**RDSServer.DataFactory**オブジェクト。 カスタム ビジネス オブジェクトには、このメソッドを使用できません。  
  
 場合、 **URL**プロパティが設定されている、 **SubmitChanges** URL で指定された場所の変更を送信します。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[DataFactory オブジェクト (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>関連項目  
 [SubmitChanges メソッドの例 (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [アドレス帳のコマンド ボタン](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate メソッド (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh メソッド (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)



