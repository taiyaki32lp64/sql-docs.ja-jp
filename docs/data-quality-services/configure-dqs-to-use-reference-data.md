---
title: 参照データを使用する DQS の構成
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.administration.rdsconfiguration.f1
- sql13.dqs.administration.configuration.createDirectRDS.f1
- sql13.dqs.admin.config.rds.f1
ms.assetid: fae745e7-57a7-4cbc-8979-56ea8e392e4e
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 8dfc5a65659efe71fd3389a770af06f360f980bd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255649"
---
# <a name="configure-dqs-to-use-reference-data"></a>参照データを使用する DQS の構成

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  このトピックでは、データのクレンジングに参照データを使用するように [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) を構成する方法について説明します。 Azure Marketplace またはダイレクトオンラインサードパーティ参照データプロバイダーから参照データを使用することもできます。  

> [!IMPORTANT]
> この記事では、以前は Azure DataMarket から利用できたサード パーティ参照データ サービスについて説明します。 DataMarket および Data Services (Melissa アドレス データなどを含む) は、2016 年 12 月 31 日以降廃止となりました。 その結果、DataMarket から指定されたサービスを使用して、この記事に示されている例を実行できなくなりました。 サード パーティ参照データ プロバイダーからオンラインで直接利用可能な参照データ サービスは引き続き使用できます。

## <a name="before-you-begin"></a>開始する前に  
  
###  <a name="Prerequisites"></a>応募  
 Marketplace の参照データを使用するには、Marketplace の有効なアカウント キーを所有している必要があります。 Marketplace アカウントキーの作成の詳細については、「[アカウントの作成](https://go.microsoft.com/fwlink/?LinkId=212936)」 (https://go.microsoft.com/fwlink/?LinkId=212936)を参照してください。 Marketplace のアカウント キーは、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 内で作成することもできます。 **のホーム画面で、** [管理] **の下の** [構成] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] をクリックし、 **[参照データ]** タブの **[DataMarket のアカウント ID を作成]** をクリックします。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 DQS で参照データ サービス設定を構成するには、DQS_MAIN データベースの dqs_administrator ロールが必要です。  
  
##  <a name="Marketplace"></a>Marketplace から参照データを使用するように DQS を構成する  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、 **[管理]** の下の **[構成]** をクリックします。  
  
3.  組織でインターネットへの接続にプロキシ サーバーを使用している場合には、 **[参照データ]** タブの **[ネットワークの設定]** の下の **[プロキシ サーバー]** と **[ポート]** ボックスに適切な値を入力します。  
  
4.  
  **[DataMarket のアカウント ID]** ボックスに Marketplace のアカウント キーを指定し、 **[DataMarket のアカウント ID を検証]** アイコンをクリックしてアカウント キーを検証します。 指定した Marketplace アカウント キーが有効かどうかを示すメッセージが表示されます。  
  
 指定した Marketplace のアカウント キーによってサブスクライブされた Marketplace の参照データ サービスを、DQS で使用する準備が整いました。  
  
##  <a name="ThirdParty"></a>ダイレクトオンラインサードパーティ参照データプロバイダーから参照データを使用するように DQS を構成する  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、 **[管理]** の下の **[構成]** をクリックします。  
  
3.  組織でインターネットへの接続にプロキシ サーバーを使用している場合には、 **[参照データ]** タブの **[ネットワークの設定]** の下の **[プロキシ サーバー]** と **[ポート]** ボックスに適切な値を入力します。  
  
4.  
  **[ダイレクト オンライン サード パーティの参照データ サービス プロバイダーの設定]** 領域の **[新しい参照データ サービス プロバイダーの追加]** アイコンをクリックします。  
  
5.  
  **[新しいダイレクト オンライン サード パーティの参照データ サービス プロバイダーを作成]** ダイアログ ボックスで次の詳細情報を指定します。  
  
    1.  
  **[名前]** ボックスに、新しいダイレクト参照データ サービス プロバイダーの名前を入力します。  
  
    2.  (省略可) **[説明]** ボックスに、新しいダイレクト参照データ サービス プロバイダーの説明を入力します。  
  
    3.  
  **[カテゴリ]** ボックスに、新しいダイレクト参照データ サービス プロバイダーによって提供されるデータのカテゴリを入力します。  
  
    4.  [スキーマ] ボックスに、ダイレクト参照データ サービス プロバイダーが使用するフィールドの文字列 (列名) を定義するスキーマを指定します。 フィールド名にスペースを含めることはできず、フィールドはコンマで区切る必要があります。 (例: `FirstName, LastName, City, State`)。  
  
    5.  
  **[URI]** ボックスに、ダイレクト参照データ サービス プロバイダーの URI を入力します。 DQS ではセキュリティで保護された URI ("https://" で始まるアドレス) だけが使用できます。  
  
    6.  
  **[最大バッチ サイズ]** ボックスに、クレンジングのために参照データ サービス プロバイダーに送られるバッチごとのレコードの最大数を入力します。 クレンジング アクティビティ用に、最大で 100 のバッチごとのレコード数を指定できます。  
  
    7.  
  **[アカウント ID]** ボックスに、参照データ サービス プロバイダーのサブスクライバーのアカウント ID を入力します。  
  
6.  
  **[OK]** をクリックしてデータを保存し、 **[新しいダイレクト オンライン サード パーティの参照データ サービス プロバイダーを作成]** ダイアログ ボックスを閉じます。 新しく追加されたダイレクト オンライン サード パーティの参照データ プロバイダーが DQS の **[ダイレクト参照データ サービス プロバイダー グリッド]** に表示されます。  
  
 新しく構成されたダイレクト オンライン サード パーティ参照データ サービス プロバイダーの参照データ サービスを DQS で使用する準備が整いました。  
  
##  <a name="FollowUp"></a>補足情報: 参照データを使用するように DQS を構成した後  
 必要なナレッジ ベース ドメインを、構成したデータ プロバイダーから提供される参照データにマップする必要があります。 方法については、「[参照データにドメインまたは複合ドメインをアタッチする](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)」をご覧ください。  
  
  
