---
title: レポート データ ソースの作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: bd6662c7-ffbe-479d-8944-3dc858340998
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 77cc99e74a1ee9d5d4be08bf7f9ce8d39288bd5b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076339"
---
# <a name="create-a-report-data-source"></a>レポート データ ソースの作成
  Power View が多次元モデルに接続するためには、共有レポート データ ソース定義 (.rsds ファイル) を SharePoint ライブラリに作成する必要があります。 .rsds ファイルは、多次元モデルへの接続に使用する Analysis Services サーバー インスタンスの名前、接続の種類、接続文字列、および資格情報の名前を指定します。 ユーザーが .rsds ファイルをクリックすると、新しい空白の Power View レポート (.rdlx ファイル) がブラウザーで開きます。  
  
 .rsds 接続を作成するには、SQL Server 2012 (以降) Reporting Services および SharePoint 2010 または SharePoint 2013 の Reporting Services アドインがインストールされている必要があります。  
  
## <a name="create-a-report-data-source-rsds-connection-to-a-multidimensional-model"></a>多次元モデルへのレポート モデル ソース (.rsds) 接続を作成する  
 開始する前に以下を調べます。  
  
-   多次元モードで実行中の Analysis Services サーバー インスタンスの名前。  
  
-   接続先の多次元データベースの名前。  
  
-   キューブの名前 (複数存在する場合)。  
  
-   (オプション) パースペクティブ名。  
  
-   (オプション) ロケール識別子  
  
#### <a name="to-create-a-shared-report-data-source-rsds-file-sharepoint-2010"></a>共有レポート データ ソース (.rsds) ファイルを作成するには (SharePoint 2010)  
  
1.  ライブラリ リボンで、 **[ドキュメント]** タブをクリックします。  
  
2.  **［新しいドキュメント］**  >  **［レポート データ ソース］** をクリックします。  
  
    > [!NOTE]  
    >  メニューに **[レポート データ ソース]** アイテムが表示されない場合は、このライブラリに対してレポート データ ソースのコンテンツ タイプが有効化されていません。 詳細については、次を参照してください。[追加レポート サーバー コンテンツ タイプをライブラリに&#40;Reporting Services SharePoint 統合モードで&#41;](../../reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)します。  
  
3.  **[データ ソースのプロパティ]** ページの **[名前]** に、接続 .rsds ファイルの名前を入力します。  
  
4.  **[データ ソースの種類]** で **[Power View 用 Microsoft BI セマンティック モデル]** をクリックします。  
  
5.  **[接続文字列]** で、Analysis Services サーバー名、データベース名、キューブ名、およびオプションの設定を指定します。  
  
     接続文字列: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>'`  
  
    > [!NOTE]  
    >  複数のキューブがある場合は、キューブの名前を指定する必要があります。  
  
     (オプション) 特定のディメンションまたはメジャー グループのみがクライアントに表示されている場合、ユーザーに選択ビューを提供するパースペクティブをキューブに含めることができます。 パースペクティブを指定するには、次のように、キューブのプロパティにパースペクティブ名を値として入力します。 `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<perspectivename>'`  
  
     (オプション) キューブには、モデル内でさまざまな言語に指定されたメタデータとデータの翻訳を含めることができます。 翻訳 (データとメタデータ) を表示するには、接続文字列に"Locale Identifier"プロパティを追加する必要があります。 `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>'; Locale Identifier=<identifier number>`  
  
6.  **[資格情報]** で、外部データ ソースにアクセスする際にレポート サーバーが資格情報を取得する方法を指定します。  
  
    -   レポートを開いたユーザーの資格情報を使用してデータにアクセスする場合は、 **[Windows 認証 (統合)]** を選択します。 SharePoint サイトまたはファームでフォーム認証を使用する場合や、信頼済みアカウントを使用してレポート サーバーに接続する場合は、このオプションを選択しないでください。 このレポートのサブスクリプションまたはデータ処理をスケジュールする場合は、このオプションを選択しないでください。 Kerberos 認証が有効なドメインに参加している場合、またはレポート サーバーと同一のコンピューターにデータ ソースがある場合に、このオプションは最適です。 Kerberos 認証が無効になっている場合、Windows 資格情報は別のコンピューター 1 台にしか渡すことができません。 つまり、外部データ ソースが別のコンピューターにあり、別の接続が必要な場合、意図したデータを取得できずにエラーが発生します。  
  
    -   ユーザーがレポートを実行するたびに資格情報の入力を要求する場合は、 **[資格情報を要求する]** をクリックします。 このレポートのサブスクリプションまたはデータ処理をスケジュールする場合は、このオプションを選択しないでください。  
  
    -   1 組の資格情報を使用してデータにアクセスする場合は、 **[保存された資格情報]** を選択します。 資格情報は暗号化されてから保存されます。 保存されている資格情報の認証方法を指定するオプションを選択できます。 保存された資格情報が Windows ユーザー アカウントに属する場合は、[データ ソースへの接続時に Windows 資格情報として使用する] をクリックします。 データベース サーバーの実行コンテキストを設定する場合は、 **[実行コンテキストをこのアカウントに設定する]** をクリックします。  
  
    -   接続文字列で資格情報を指定する場合や、最小特権アカウントを使用してレポートを実行する場合は、 **[資格情報は必要ありません]** をクリックします。  
  
7.  **[接続テスト]** をクリックして検証します。  
  
8.  データ ソースをアクティブにする場合は、 **[このデータ ソースを有効にする]** を選択します。 データ ソースが構成されていてもアクティブでない場合は、ユーザーがレポートを作成しようとするとエラー メッセージが表示されます。  
  
  
