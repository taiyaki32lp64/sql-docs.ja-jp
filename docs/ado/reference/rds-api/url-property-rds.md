---
title: URL プロパティ (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c88b8029ee5d96986cf9b366bd8faee53ca1393b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963224"
---
# <a name="url-property-rds"></a>URL プロパティ (RDS)
相対パスまたは絶対 URL を含む文字列を示します。  
  
 設定することができます、 **URL**でデザイン時にプロパティ、 [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトのオブジェクト タグまたはスクリプト コードの実行時にします。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>パラメーター  
 *[サーバー]*  
 A**文字列**有効な URL を表す値です。  
  
 *DataControl*  
 オブジェクト変数を表す、 **DataControl**オブジェクト。  
  
## <a name="remarks"></a>コメント  
 通常、URL は、アクティブ サーバー ページ (.asp) ファイルを生成して返すを識別します。、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。 このため、ユーザーが取得できる、**レコード セット**をサーバー側を呼び出すことがなく[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)オブジェクト、またはカスタム ビジネス オブジェクトをプログラムします。  
  
 場合、 **URL**プロパティが設定されている、 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) URL で指定された場所の変更を送信します。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [URL プロパティの例 (VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)


