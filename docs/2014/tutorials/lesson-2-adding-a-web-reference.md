---
title: レッスン 2:Web 参照の追加 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a2c2b8b8-6b13-45ca-ab3b-1582447b6807
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: dd4b9edc8c054a7fa2ec84bdc8d892e5b5a903a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316007"
---
# <a name="lesson-2-adding-a-web-reference"></a>レッスン 2:Web 参照の追加
  Web サービスの探索とは、クライアントが Web サービスを検索し、そのサービス記述を取得する処理です。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の Web サービス探索処理では、事前に定義されたアルゴリズムに従って、Web サイトの問い合わせが行われます。 この処理の目的はサービス記述を見つけることです。サービス記述とは、WSDL (Web サービス記述言語) を使用する XML ドキュメントです。  
  
 サービス記述には、利用可能なサービスとこれらのサービスとの対話方法が記述されています。 サービス記述がない場合は、プログラムから Web サービスと対話することはできません。  
  
 アプリケーションには、Web サービスと通信する方法とランタイムで Web サービスを検出する方法を実装する必要があります。 これを実現するには、プロジェクトに Web サービス用の Web 参照を追加します。その結果、プロキシ クラスが生成されます。プロキシ クラスは、Web サービスとのインターフェイスとなり、Web サービスのローカル表記を提供します。 詳細については、次を参照してください。"する方法。XML Web サービス プロキシの生成"で、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]ドキュメント。  
  
### <a name="to-add-a-web-reference"></a>Web 参照を追加するには  
  
1.  **プロジェクト** メニューのをクリックして**サービス参照の追加**します。  
  
2.  **サービス参照の追加**ダイアログ ボックスで、をクリックして**詳細**します。  
  
3.  **サービス参照設定**ダイアログ ボックスで、をクリックして**Web 参照の追加**します。  
  
4.  **URL**のボックス、 **Web 参照の追加** ダイアログ ボックスなど、レポート サーバー Web サービスのサービスの説明を取得する URL を入力 http://localhost/reportserver/reportservice2010.asmx します。 をクリックし、**移動**Web サービスに関する情報を取得するボタンをクリックします。  
  
     \- - または -  
  
     レポート サーバー Web サービスがローカル コンピューターに存在する場合にクリックして、**の Web サービス、ローカル マシン**ブラウザー ウィンドウのリンク。 次に、表示された一覧から ReportService2010 Web サービスのリンクをクリックします。  
  
5.  **Web 参照名**ボックスに、これはこの Web 参照に使用する名前空間を ReportService2010 に Web 参照の名前を変更します。  
  
6.  クリックして**参照の追加**対象の Web サービスに Web 参照を追加します。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] により、サービス記述がダウンロードされ、アプリケーションとレポート サーバー Web サービス間のインターフェイスとなるプロキシ クラスが生成されます。 また、Web 参照が動作するように、 <xref:System.Web.Services> 名前空間への参照を追加する必要があります。  
  
7.  [プロジェクト] メニューで、次のようにクリックします。**参照の追加**します。  
  
8.  **参照の追加** ダイアログ ボックスで、 **.NET** タブで **System.Web.Services**、順にクリックします**OK**します。  
  
 詳細については、「[SOAP API へのアクセス](../reporting-services/report-server-web-service/accessing-the-soap-api.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レポート サーバー Web サービス](../reporting-services/report-server-web-service/report-server-web-service.md)   
 [レッスン 3:Web サービスにアクセスします。](../../2014/tutorials/lesson-3-accessing-the-web-service.md)   
 [Visual Basic または Visual C を使用してレポート サーバー Web サービスにアクセスする&#35; &#40;SSRS チュートリアル&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  
