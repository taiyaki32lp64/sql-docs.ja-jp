---
title: 手順 1:サーバー プログラム (RDS チュートリアル) を指定する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6cecddfe127bba43852412b6d804254f35103def
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922113"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>手順 1:サーバー プログラムを指定する (RDS チュートリアル)
最も一般的な場合に、使用、 [rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)オブジェクト[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)既定のサーバー プログラムを指定するメソッド[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)、または独自のカスタム サーバー プログラム (ビジネス オブジェクト)。 サーバーのプログラムが、サーバーとサーバーのプログラムへの参照でインスタンス化または*プロキシ*が返されます。  
  
 このチュートリアルでは、既定のサーバー プログラムを使用します。  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="see-also"></a>関連項目  
 [手順 2:サーバーのプログラム (RDS チュートリアル) を呼び出す](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [RDS のチュートリアル (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
