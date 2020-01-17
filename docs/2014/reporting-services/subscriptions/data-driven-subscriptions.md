---
title: データ ドリブン サブスクリプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: ba009f62-0d4f-45e7-a27c-36fd5f0cd3a8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 90733af47898116236d94c9b9f6ccc6d9fc542ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100864"
---
# <a name="data-driven-subscriptions"></a>データ ドリブン サブスクリプション
  データ ドリブン サブスクリプションでは、実行時に外部データ ソースから取得した動的サブスクリプション データを使用できます。 サブスクリプションの定義時に指定した静的テキストや既定値を使用することもできます。 データ ドリブン サブスクリプションを使用すると、次のようなことが可能になります。  
  
-   サブスクライバーの変動が頻繁に生じても、それに対応してレポートを配信する。 たとえば、データ ドリブン サブスクリプションを使用して、サブスクライバーが毎月変わる大きな組織全体にレポートを配信したり、他の条件を使用して既存の一連のユーザーからグループのメンバーシップを決定することができます。  
  
-   実行時に取得したレポート パラメーター値に基づいてレポート出力をフィルター選択する。  
  
-   レポートを配信するたびにレポートの出力形式や配信オプションを変化させる。  
  
 データ ドリブン サブスクリプションは複数の要素で構成されます。 データ ドリブン サブスクリプションの固定的な要素は、サブスクリプションの作成時に定義され、次のような要素があります。  
  
-   サブスクリプションを定義するレポート (サブスクリプションは常に単一のレポートと関連付けられます)。  
  
-   レポートの配信に使用する配信拡張機能。 レポート サーバーの電子メール配信、ファイル共有配信、キャッシュの事前読み込みに使用する NULL 配信プロバイダー、カスタム配信拡張機能などを指定できます。 単一のサブスクリプションに対して複数の配信拡張機能を指定することはできません。  
  
-   サブスクライバー データ ソース。 サブスクリプションを定義するとき、サブスクライバー データが格納されているデータ ソースへの接続文字列を指定する必要があります。 サブスクライバー データ ソースを実行時に動的に指定することはできません。  
  
-   サブスクライバー データの選択に使用するクエリ。サブスクリプションの定義時に指定する必要があります。 クエリを実行時に変更することはできません。  
  
 データ ドリブン サブスクリプションに使用される動的な値は、サブスクリプションの処理時に取得されます。 サブスクリプションで使用される変数データには、サブスクライバー名、電子メール アドレス、使用するレポート出力形式のほか、各種レポート パラメーターの値があります。 データ ドリブン サブスクリプションで動的な値を使用するには、クエリから返されるフィールドを、特定の配信オプションおよびレポート パラメーターに対応付ける必要があります。 変数データは、サブスクリプションを処理するごとに、サブスクライバー データ ソースから取得されます。  
  
## <a name="requirements-for-using-data-driven-subscriptions"></a>データ ドリブン サブスクリプションを使用する場合の要件  
 データ ドリブン サブスクリプション機能は、すべてのエディションで利用できるわけではありません。 また、データ ソースの種類によっては、実行時にサブスクリプション データを取得できない場合もあります。 詳細な要件については、以下の情報を参考にしてください。  
  
-   データ ドリブン サブスクリプション機能をサポートする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションについては、「[SQL Server 2012 の各エディションがサポートする機能 ](https://go.microsoft.com/fwlink/?linkid=232473)」(https://go.microsoft.com/fwlink/?linkid=232473) を参照してください。  
  
-   サブスクリプション データについては、スキーマ情報をレポート サーバーに提供できるデータ ソースを選択します。 サポートされているデータ ソースの種類としては、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データ、Oracle、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ データ、ODBC データ ソース、OLE DB データ ソースなどがあります。 サブスクライバー データ ソース要件の詳細については、「 [サブスクライバー データに対して外部データ ソースを使用する &#40;データ ドリブン サブスクリプション&#41;](use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)」を参照してください。  
  
## <a name="working-with-data-driven-subscriptions"></a>データ ドリブン サブスクリプションの処理  
 以下のトピックでは、データ ドリブン サブスクリプションの詳細について説明します。  
  
|トピック|説明|  
|------------|-----------------|  
|[データ ドリブン サブスクリプションを作成、変更、および削除する](data-driven-subscriptions.md)|データ ドリブン サブスクリプションの作成、変更、および削除方法について説明します。|  
|[サブスクライバー データに対して外部データ ソースを使用する &#40;データ ドリブン サブスクリプション&#41;](use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)|データ ドリブン サブスクリプションに使用できるデータ ソースに関する情報を記載しています。|  
|[データ ドリブン サブスクリプションの作成 &#40;SSRS チュートリアル&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)|データ ドリブン サブスクリプションの作成方法について理解するための手順を記載しています。|  
|[レポートのキャッシュ &#40;SSRS&#41;](../report-server/caching-reports-ssrs.md)|データ ドリブン サブスクリプションと NULL 配信プロバイダーを使用して、キャッシュを事前に読み込む方法を説明しています。|  
  
## <a name="see-also"></a>参照  
 [サブスクリプションと配信 &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [[データ ドリブン サブスクリプションの作成] ページ &#40;レポート マネージャー&#41;](../create-data-driven-subscription-page-report-manager.md)   
 [キャッシュの事前読み込み &#40;レポート マネージャー&#41;](../report-server/preload-the-cache-report-manager.md)  
  
  
