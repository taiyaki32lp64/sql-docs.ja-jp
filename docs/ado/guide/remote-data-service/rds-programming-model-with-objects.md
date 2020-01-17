---
title: RDS のプログラミング モデルとオブジェクト |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 06bf7c811074ba70741fe77b06037f9f69c9cda4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922473"
---
# <a name="rds-programming-model-with-objects"></a>RDS のプログラミング モデルとオブジェクト
RDS の目標にアクセスし、IIS などの中間層を介して、データ ソースを更新することです。 プログラミング モデルでは、この目標を達成するために必要なアクティビティのシーケンスを指定します。 オブジェクト モデルでは、メソッドとプロパティが、プログラミング モデルに影響するオブジェクトを指定します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 RDS は、次の一連のアクションを実行する手段を提供します。  
  
-   サーバーで、呼び出されるプログラムを指定して、クライアントから参照する方法 (プロキシ) を取得 ([rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md))。  
  
-   サーバー プログラムを起動します。 データ ソースおよび発行するコマンドを識別するサーバーのプログラムにパラメーターを渡す (プロキシまたは[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md))。  
  
-   サーバーのプログラムを取得、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)ADO を使用して、通常、データ ソースからのオブジェクト。 必要に応じて、 **Recordset**オブジェクトは、サーバーで処理される ([RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md))。  
  
-   サーバー プログラム返します最終的な**レコード セット**オブジェクトをクライアント アプリケーション (プロキシ)。  
  
-   クライアントで、**レコード セット**ビジュアル コントロールで簡単に使用できる形式にオブジェクトが格納されます (ビジュアル コントロールと**rds.DataControl**)。  
  
-   変更、 **Recordset**オブジェクトがサーバーに送信され、データ ソースを更新するために使用 (**rds.DataControl**または**RDSServer.DataFactory**)。  
  
## <a name="see-also"></a>関連項目  
 [RDS オブジェクト モデルの概要](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory オブジェクト (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace オブジェクト (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS のシナリオ](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS チュートリアル](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RecordSet オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS の使用方法とセキュリティ](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


