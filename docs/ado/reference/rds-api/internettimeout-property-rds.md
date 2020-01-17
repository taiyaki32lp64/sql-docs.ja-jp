---
title: InternetTimeout プロパティ (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InternetTimeout property [ADO]
ms.assetid: 4d1c8892-4bbc-4e71-bf4b-ba52c0ea9549
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eaaa72c302c9218810ce653ea59fe5ff29a54ef0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963874"
---
# <a name="internettimeout-property-rds"></a>InternetTimeout プロパティ (RDS)
要求がタイムアウトするまで待機するミリ秒数を示します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**長い**タイムアウトになる要求までのミリ秒数を表す値です。  
  
## <a name="remarks"></a>コメント  
 このプロパティは、HTTP または HTTPS プロトコルで送信された要求のみに適用されます。  
  
 3 層環境での要求は、実行するのに数分をかかります。 このプロパティを使用して、実行時間の長い要求の待機時間を指定します。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[DataSpace オブジェクト (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)|  
  
## <a name="see-also"></a>関連項目  
 [InternetTimeout プロパティの例 (VB)](../../../ado/reference/rds-api/internettimeout-property-example-vb.md)   
 [InternetTimeout プロパティの例 (VC++)](../../../ado/reference/rds-api/internettimeout-property-example-vc.md)   
 

