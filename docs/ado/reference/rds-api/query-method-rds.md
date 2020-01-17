---
title: クエリ メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f646d5ebee63981c882f5e1ece147be0ff1677e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963824"
---
# <a name="query-method-rds"></a>Query メソッド (RDS)
返す有効な SQL クエリ文字列を使用して、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *レコード セット*  
 オブジェクト変数を表す、 **Recordset**オブジェクト。  
  
 *DataFactory*  
 オブジェクト変数を表す、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)オブジェクト。  
  
 *Connection*  
 A**文字列**をサーバーの接続情報を含む値です。 これに似ています、 [Connect](../../../ado/reference/rds-api/connect-property-rds.md)プロパティ。  
  
 *クエリ*  
 A**文字列**SQL クエリを格納しています。  
  
## <a name="remarks"></a>コメント  
 クエリでは、データベース サーバーの SQL 言語を使用する必要があります。 実行されたクエリにエラーがある場合、結果の状態が返されます。 **クエリ**メソッドでは、構文のチェックを行いません、**クエリ**文字列。  
  
## <a name="applies-to"></a>適用対象  
 [DataFactory オブジェクト (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>関連項目  
 [DataFactory オブジェクト、クエリ メソッド、および CreateObject メソッドの例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


