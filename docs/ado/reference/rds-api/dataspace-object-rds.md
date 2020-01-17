---
title: DataSpace オブジェクト (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbd27490e20e8c615ba934299e80f55eb06a5481
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964354"
---
# <a name="dataspace-object-rds"></a>DataSpace オブジェクト (RDS)
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 中間層にあるカスタム ビジネス オブジェクトにクライアント側プロキシを作成します。  
  
 リモート データ サービスには、クライアント側コンポーネントは、中間層にあるビジネス オブジェクトと通信できるように、ビジネス オブジェクトのプロキシが必要があります。 パッケージ化、アンパッケージ処理、およびトランスポート (マーシャ リング) のアプリケーションのプロキシを容易に[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)プロセスやコンピューターの境界を越えてデータ。  
  
 リモート データ サービスを使用して、 **rds.DataSpace**オブジェクトの[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)ビジネス オブジェクトのプロキシを作成します。 中間層ビジネス オブジェクトの対応のインスタンスが作成されるたびに、ビジネス オブジェクトのプロキシが動的に作成されます。 リモート データ サービスには、次のプロトコルがサポートされています。HTTP、HTTPS (HTTP Secure Sockets)、DCOM、およびインプロセス (クライアント コンポーネントと同じコンピューター上にビジネス オブジェクト)。  
  
> [!NOTE]
>  RDS の「ステートレス」方法で動作時に、 **rds.DataSpace**オブジェクトが HTTP または HTTPS プロトコルを使用します。 つまり、サーバーに応答が返された後にクライアント要求に関する内部情報は破棄されます。  
  
> [!NOTE]
>  ビジネス オブジェクトは、ビジネス オブジェクトのプロキシの有効期間にわたって存在に見えますが、ビジネス オブジェクトは、要求に応答が送信されるまでの間だけに実際に存在します。 要求が発行されたとき (つまり、メソッドが呼び出されるビジネス オブジェクトで)、プロキシ サーバーへの新しい接続を開くし、サーバーは、ビジネス オブジェクトの新しいインスタンスを作成します。 ビジネス オブジェクトは、要求に応答して、サーバーが、ビジネス オブジェクトを破棄して、接続を閉じます。  
  
> [!NOTE]
>  この動作により、ビジネス オブジェクトのプロパティまたは変数を使用して、1 つの要求からデータを渡すことはできません。 ファイルやメソッドの引数、状態データを永続化など、他のメカニズムを採用する必要があります。  
  
 クラス ID を**rds.DataSpace**オブジェクトが BD96C556 65A3-11 D 00C04FC29E36 983A 0。  
  
 **DataSpace**オブジェクトがスクリプトを実行します。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [DataSpace オブジェクト (RDS) のプロパティ、メソッド、およびイベント](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [DataSpace オブジェクトおよび CreateObject メソッドの例 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


