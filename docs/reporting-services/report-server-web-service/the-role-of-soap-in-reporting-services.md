---
title: Reporting Services における SOAP の役割 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- SOAP [Reporting Services], role in Reporting Services
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: f229c3ef-f2ca-448f-98f1-b8df350b9992
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4f03388971728750866480a5b0a6ec9626f92a1c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63069890"
---
# <a name="the-role-of-soap-in-reporting-services"></a>Reporting Services における SOAP の役割
  レポート サーバー Web サービスでは、Simple Object Access Protocol (SOAP) メッセージングを使用し、ネットワーク経由でテキストベースのコマンドを送信します。 これらのコマンドは XML テキスト形式であり、HTTP を使用して World Wide Web 経由で送信されます。 レポート サーバー Web サービスでは、通信プロトコルとして SOAP を使用することで、アプリケーションとコンポーネントが開放型で広く普及しているインフラストラクチャを使用してレポート サーバーとデータを交換できるようにしています。 SOAP 標準は www.w3.org/TR/SOAP で定義されています。  
  
 クライアント アプリケーションは、SOAP に対応しており、SOAP 要求を送信できる限り、SOAP クライアントして動作できます。 レポート マネージャーはそのような SOAP クライアントの 1 つです。 レポート マネージャーは、すべてのレポートとレポート関連コンテンツが格納されているレポート サーバー データベースへのインターフェイスを提供します。 エンド ユーザーはアプリケーションを使用して、レポート サーバー名前空間のレポートとフォルダーを参照し、管理できます。 レポート マネージャーはレポート サーバー Web サービス インフラストラクチャ上に構築されています。  
  
 レポート サーバーは SOAP サーバーとして動作します。SOAP サーバーは、SOAP クライアントから要求を受け取り、適切な応答を作成できる SOAP 対応サービスです。 サーバーは要求を処理し、クライアントにエンコードされた応答を送り返します。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の SOAP メッセージは、クライアントで行われた要求の種類によってさまざまな形式を取ります。 次の例は、レポート サーバー データベースからアイテムを削除する簡単な SOAP クライアント要求を表しています。  
  
```  
<soap:Envelope xmlns:soap="https://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItem xmlns="https://www.microsoft.com/sql/ReportingServer">  
            <item>/Samples/Report1</item>  
        </DeleteItem>  
    </soap:Body>  
</soap:Envelope>  
```  
  
 SOAP 自体は、メッセージを **Envelope** 要素に入れるよう要求します。メッセージは一括して **Body** 要素内に入ります。 この例では、Body には <xref:ReportService2010.ReportingService2010.DeleteItem%2A> メソッドの呼び出しが入っています。このメソッドは、削除するアイテムのパスを表す文字列パラメーターを取ります。 すべての SOAP 操作をメソッドにカプセル化する [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] クライアント プロキシ クラスを作成できます。 次の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] メソッドは上記の SOAP の例を表しています。  
  
```  
public void DeleteItem(string item);  
```  
  
 サーバーからの応答は次のようになります。  
  
```  
<soap:Envelope xmlns:soap="https://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItemResponse xmlns="https://www.microsoft.com/sql/ReportingServer" />  
    </soap:Body>  
</soap:Envelope>  
```  
  
 <xref:ReportService2010.ReportingService2010.DeleteItem%2A> メソッドに戻り値はないため、空の応答が返されます。  
  
## <a name="see-also"></a>参照  
 [SOAP API へのアクセス](../../reporting-services/report-server-web-service/accessing-the-soap-api.md)   
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Reporting Services Report Server](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)   
 [レポート サーバー web サービス](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
