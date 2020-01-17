---
title: 手順 4:サーバーは、レコード セット (RDS チュートリアル) を返します |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server returns Recordset
ms.assetid: 3d1855c4-419c-4810-b5ea-6c874b5e2905
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bd243b21b7003c524c3483f5b8d7bb92be1e18d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922066"
---
# <a name="step-4-server-returns-the-recordset-rds-tutorial"></a>手順 4:サーバーがレコード セットを返す (RDS チュートリアル)
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 RDS を取得して、変換**レコード セット**をクライアントに送信できる形式にオブジェクト (つまり、*マーシャ リング*、**レコード セット**)。 変換と送信方法の正確な形式は、サーバーがインターネットまたはイントラネットをローカル エリア ネットワーク上またはダイナミック リンク ライブラリは、かどうかによって異なります。 ただし、この詳細は重要です。その RDS に問題がすべて送信、**レコード セット**クライアントに送り返します。  
  
 クライアント側で、**レコード セット**オブジェクトが返され、ローカル変数に代入します。  
  
```vb
Sub RDSTutorial4()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>関連項目  
 [手順 5:DataControl が使用可能に (RDS チュートリアル)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)   
 [RDS のチュートリアル (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
