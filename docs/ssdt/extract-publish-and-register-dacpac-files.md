---
title: .dacpac ファイルの抽出、発行、および登録 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.DacTableChooser
- sql.data.tools.DacPublishDialog
- sql.data.tools.DacPropertiesDialog
- sql.data.tools.publishdacproject
- sql.data.tools.DacExtractDialog
ms.assetid: ed900f93-d3df-40f5-8e62-4d722595e041
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2aee0f145c2ef2b82b929a8f6358a764a10050f5
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154799"
---
# <a name="extract-publish-and-register-dacpac-files"></a>.dacpac ファイルの抽出、発行、および登録
このトピックでは、SQL Server オブジェクト エクスプローラーで接続されているデータベースを右クリックして実行できる 4 つの手順について説明します。  
  
-   データ層アプリケーションの公開  
  
-   データ層アプリケーションの抽出  
  
-   データ層アプリケーションの登録  
  
-   データ層アプリケーションの登録解除  
  
## <a name="publish-data-tier-application"></a>データ層アプリケーションの公開  
.dacpac をデータベースに公開できます。 公開操作では、ソース .dacpac ファイルのスキーマに合わせてデータベース スキーマの増分更新を行います。 データベースがサーバーに存在しない場合は、公開操作によって作成されます。  
  
この操作は、[データベース] ノードを選択して利用することもできます。  
  
.dacpac ファイルを選択します。 .dacpac ファイルを指定したら、 **[DAC のプロパティ]** ボタンが有効になります。 **[DAC のプロパティ]** ダイアログ ボックスには、.dacpac ファイルに関する情報が表示されます。  
  
データベース名が接続文字列に含まれていない場合は、データベース サーバーへの接続文字列を指定して、データベース名を指定します。  
  
**[公開]** ボタンと **[スクリプトの生成]** ボタンが使用できるようになりました。 スクリプトを生成すると、スクリプトはドキュメント ウィンドウに表示され、必要に応じて保存できます。 データベースに直接公開することを選択する場合は、更新の概要と使用した実際のスクリプトを **[データ ツール操作]** ウィンドウから表示できます。  
  
**[データ層アプリケーションとして登録する]** チェック ボックスをオンにすると、結果のデータベースはサーバー メタデータにデータ層アプリケーションとして登録されます。 公開するデータベースが登録される場合、データベースのスキーマが現在登録されている dacpac と異なると、公開に失敗する可能性があります。  
  
**[公開の詳細設定]** ダイアログ ボックスでは、その他の公開の構成を利用できます。このダイアログ ボックスには、 **[詳細設定]** ボタンをクリックしてアクセスできます。  
  
## <a name="extract-data-tier-application"></a>データ層アプリケーションの抽出  
データベースから .dacpac を抽出できます。 抽出では、データベース スキーマに加えて、ユーザー テーブルのデータが含まれる可能性があるライブ SQL Server または Azure SQL Database から、データベース スナップショット ファイル (.dacpac) が作成されます。  
  
作成する .dacpac ファイルを指定します。 **[DAC のプロパティ]** ボタンをクリックすると、 **[DAC のプロパティ]** ダイアログ ボックスが表示され、.dacpac ファイルのプロパティを指定できます。  
  
必要に応じて、抽出プロセスの構成を変更します。 **[設定の抽出]** セクションで、スキーマの抽出のみを実行するか、スキーマを抽出してテーブル データを含めるかを選択できます。 スキーマとデータを抽出する場合は、データを抽出するテーブルを選択できます。  
  
## <a name="register-data-tier-application"></a>データ層アプリケーションの登録  
データベースは、データ層アプリケーション (DAC) としてインスタンス内に登録できます。 これにより、データベース スキーマの現在の状態がシステム メタデータに保存されます。  
  
**[データ層アプリケーションの登録]** ダイアログ ボックスで、登録した DAC のプロパティを指定します。  
  
## <a name="unregister-data-tier-application"></a>データ層アプリケーションの登録解除  
登録解除により、登録したデータ層アプリケーションのメタデータをインスタンスから削除できます。 登録を解除しても、登録したデータベースは削除されません。  
  
## <a name="see-also"></a>参照  
[接続されているデータベース開発](../ssdt/connected-database-development.md)  
  
