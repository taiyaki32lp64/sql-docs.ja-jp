---
title: '(外部の) ナレッジ参照データを使用してデータをクレンジングする '
description: SQL Server の Data Quality Services (DQS) を使用して、参照データプロバイダーからのナレッジを使用してデータをクレンジングする方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 158009e9-8069-4741-8085-c14a5518d3fc
author: swinarko
ms.author: sawinark
ms.openlocfilehash: fc0135ed4e4956d6bd98fc0b467a5b6d0a25a013
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557907"
---
# <a name="cleanse-data-using-external-knowledge-reference-data---data-quality-services-dqs"></a>(外部の) ナレッジ参照データを使用してデータをクレンジングする-Data Quality Services (DQS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  このトピックでは、参照データ プロバイダーから提供されるナレッジを使用してデータをクレンジングする方法について説明します。 クレンジング アクティビティを実行する手順は、参照データ プロバイダーから提供されるナレッジを使ってデータをクレンジングする場合も「[DQS &#40;内部&#41; ナレッジを使用したデータのクレンジング](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)」で説明した手順とすべて同じですが、このトピックでは、[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) での参照データ サービスを使ったデータ クレンジングに固有の情報を示します。  

> [!IMPORTANT]
> この記事では、以前は Azure DataMarket から利用できたサード パーティ参照データ サービスについて説明します。 DataMarket および Data Services (Melissa アドレス データなどを含む) は、2016 年 12 月 31 日以降廃止となりました。 その結果、DataMarket から指定されたサービスを使用して、この記事に示されている例を実行できなくなりました。 サード パーティ参照データ プロバイダーからオンラインで直接利用可能な参照データ サービスは引き続き使用できます。
 
 DQS の参照データ サービス機能を使用してデータをクレンジングする場合、DQS のクレンジング プロセスで、マップされたドメイン値がバッチ要求として参照データ サービス プロバイダーに送信されます。 参照データ サービスから、次の情報を含む応答が返されます。  
  
-   修正案  
  
-   Confidence  
  
-   マップされたドメインに関する追加情報。 参照データでは、この追加データを使用してソースを標準化、解析、または強化することもできます。 この情報は応答の追加フィールドに記載されています。  
  
 参照データ サービスから応答を受け取った後、DQS のクレンジング アクティビティで次の処理が行われます。  
  
-   ドメインを参照データ サービスにマップするときに指定した **[自動修正しきい値]** と **[最小信頼度]** の値に基づいて、ドメイン値が信頼レベルに応じて自動的に修正または提案されます。  
  
    > [!NOTE]  
    >  参照データ サービスのナレッジを使用してデータをクレンジングするときは、 **[全般設定]** タブの **[構成]** セクションで指定したしきい値ではなく、参照データ サービスにドメインをマップするときに指定したしきい値が適用されます。 参照データのクレンジングのしきい値の指定については、「[参照データへのドメインまたは複合ドメインのアタッチ](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)」の手順 9 をご覧ください。  
  
-   ドメイン値が " **提案**"、" **新規**"、" **無効**"、" **修正済み**"、および " **適切**" に分類されます。  
  
-   追加データがソースに追加され、クレンジングされたデータと一緒に情報をエクスポートできるようになります。  
  
## <a name="before-you-begin"></a>開始する前に  
  
###  <a name="Prerequisites"></a>応募  
 DQS のナレッジ ベース内の必要なドメインを適切な参照データ サービスにマップしておく必要があります。 また、クレンジングするデータの種類に関するナレッジがナレッジ ベースに含まれている必要があります。 たとえば、米国の住所が格納されたソース データをクレンジングする場合は、米国の住所に関する高品質データを提供する参照データ サービス プロバイダーにドメインをマップする必要があります。 詳細については、「 [参照データへのドメインまたは複合ドメインのアタッチ](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)」を参照してください。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 データ クレンジングを実行するには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_kb_operator ロールが必要です。  
  
##  <a name="Cleanse"></a>参照データのナレッジを使用してデータをクレンジングする  
 ここでは、Azure Marketplace の Melissa Data service を使用して、前のトピック「[ドメインまたは複合ドメインを参照データにアタッチする](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)」でマップしたドメインを使用する例についても説明します。 ここでは、同じドメインを使用して、いくつかのサンプルの米国の住所をクレンジングします。 データをクレンジングする手順は、「[DQS &#40;内部&#41; ナレッジを使用したデータのクレンジング](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)」で説明されているものと同じです。 処理中に注意が必要な箇所には説明を補足しています。  
  
1.  データ品質プロジェクトを作成し、 **[クレンジング]** アクティビティを選択します。 「 [Create a Data Quality Project](../data-quality-services/create-a-data-quality-project.md)」を参照してください。  
  
2.  
  **[マップ]** ページで、 **Address Line**、 **City**、 **State**、および **Zip**の 4 つのドメインをソース データの適切な列にマップします。 
  **[次へ]** をクリックします。  
  
    > [!NOTE]  
    >  
  **Address Verification** 複合ドメイン内の 4 つのドメインをすべてマップしているため、データ クレンジングは、個々のドメイン レベルではなく、複合ドメイン レベルで実行されます。  
  
3.  
  **[最適化]** ページで、 **[開始]** をクリックしてコンピューター支援型のクレンジング プロセスを実行します。 クレンジング プロセスが完了したら、 **[次へ]** をクリックします。  
  
    > [!NOTE]  
    >  
  **[最適化]** ページには、参照データ サービスにアタッチされているドメインに関する情報が次の 2 とおりの方法で表示されます。  
    >   
    >  -   [**開始**] ボタンの下に "Domains \<Domain1>, \<Domain2>" というメッセージが表示され,...\<Domainn> は、参照データサービスプロバイダーを使用してクレンジングされます。 " この例の場合、"ドメイン Address Verification を、参照データ サービス プロバイダーを使用してクレンジングします" というメッセージが表示されます。  
    > -   アイコン (![ドメインが RDS にアタッチ](../data-quality-services/media/dqs-rdsindicator.JPG "RDS にドメインがアタッチされている")されている) が、参照データサービスプロバイダーにアタッチされているドメインに対して**プロファイラー**領域に表示されます。 この例の場合、 **Address Verification** 複合ドメインに対してこのアイコンが表示されます。  
  
4.  
  **[結果の管理と表示]** ページで、ドメイン値を確認します。 参照データ サービスでは、値に対する提案が複数ある場合、参照データ サービスにドメインをマップするときに **[提案された候補]** ボックスで指定した提案の最大数に応じて表示できます。 たとえば、次の米国の住所に対しては 2 つの提案が表示されます。  
  
     **元の値:**  
  
    |Address Line|City|State|Zip|  
    |------------------|----------|-----------|---------|  
    |1 msft way|レドモンド||98052|  
  
     **推奨される値:**  
  
    |Address Line|City|State|Zip|  
    |------------------|----------|-----------|---------|  
    |1 Microsoft Way|レドモンド|WA|98052|  
    |PO Box 1|レドモンド|WA|98073|  
  
     ![Reference Data Services の使用によるクレンジング](../data-quality-services/media/dqs-rdscleansing.JPG "Reference Data Services の使用によるクレンジング")  
  
    > [!NOTE]  
    >  複合ドメインについては、さらに、コンピューター支援型のクレンジング プロセスで修正された個々のドメインが別の色で強調表示されます。 たとえば、この例では、 **Address Line** ドメインと **State** ドメインが修正されているため、それらのドメインがシアンで強調表示されます。  
  
5.  すべてのドメイン値の確認が完了したら、 **[次へ]** をクリックしてデータをエクスポートします。  
  
6.  
  **[エクスポート]** ページに、各ドメインのクレンジング アクティビティに関する通常の情報 (ソース、理由、信頼度、およびステータス) に加え、住所データに関して Melissa Data 参照データ サービスから提供された追加の情報が表示されます。これには、住所の経度と緯度、郡の名前、住所タイプ (高層ビルや番地) などが含まれます。  
  
7.  目的のエクスポート先 (SQL Server、CSV、または Excel) にデータをエクスポートし、 **[完了]** をクリックしてプロジェクトを閉じます。  
  
    > [!IMPORTANT]  
    >  Excel の 64 ビット版を使用している場合、クレンジングされたデータは Excel ファイルにエクスポートできません。SQL Server データベースまたは .csv ファイルにのみエクスポートできます。  
  
  
