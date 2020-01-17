---
title: 方法:ターゲット プラットフォームを変更し、データベース プロジェクトを公開する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.publish.dialog
- sql.data.tools.publishdacproject
ms.assetid: 6012e120-5f72-4f4f-ae6e-f9a57ae1dea7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a2dd22b47da751294b60f57aaad246234004e946
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897363"
---
# <a name="how-to-change-target-platform-and-publish-a-database-project"></a>方法:ターゲット プラットフォームを変更し、データベース プロジェクトを公開する
SQL Server Data Tools (SSDT) データベース プロジェクトのターゲット SQL Server のバージョンは、サポートされている任意の SQL Server インスタンス (SQL Server 2005、2008、2008 R2、Microsoft SQL Server 2012、または SQL Azure) に変更することができます。 そうすることによって、データベース開発を 1 つのプロジェクトで行い、必要に応じて複数のバージョンの SQL Server インスタンスに発行することができます。  
  
SSDT では、ターゲット プラットフォームを認識し、コード内のエラー (たとえば、SQL Azure に発行するプロジェクトでサポートされていない機能を使用している場合など) を自動検出することで、このタスクを容易にしています。  
  
> [!WARNING]  
> 以下に示す手順では、「[接続されているデータベース開発](../ssdt/connected-database-development.md)」および「[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)」に示されているこれまでの手順で作成したエンティティを使用します。  
  
### <a name="to-change-a-projects-target-platform"></a>プロジェクトのターゲット プラットフォームを変更するには  
  
1.  **ソリューション エクスプローラー**でプロジェクトを右クリックし、 **[プロパティ]** をクリックします。 左側の **[プロジェクトの設定]** タブをクリックし、 **[プロジェクトの設定]** プロパティ ページを開きます。  
  
2.  このページの **[ターゲット プラットフォーム]** ボックスの一覧には、データベース プロジェクトの公開先としての指定が可能な、サポートされているすべての SQL Server プラットフォームが含まれています。 この手順では、 **SQL Azure**を選択します。  
  
### <a name="to-use-platform-validation-when-editing-scripts"></a>スクリプトの編集時にプラットフォームの検証を使用するには  
  
1.  ソリューション エクスプローラーで **Products** テーブルを右クリックし、 **[コードの表示]** をクリックして Transact\-SQL エディターで開きます。  
  
2.  `ON [PRIMARY]` ステートメントの末尾に、 `CREATE TABLE` を追加します。  
  
3.  **[エラー一覧]** ウィンドウに次のエラーが表示されることに注意してください。SQL70015:'ファイル グループ参照とパーティション構成' は、SQL Azure ではサポートされていません。  
  
    ターゲット プラットフォームに基づいて、スクリプトが自動的に検証されます。 ここでは、ファイル グループが SQL Azure でサポートされていないため、SSDT からエラーが返されます。 SQL Azure でサポートされていない Transact\-SQL ステートメントの一覧については、「[部分的にサポートされる Transact-SQL ステートメント (Microsoft Azure SQL Database)](https://msdn.microsoft.com/library/ee336267.aspx)」をご覧ください。  
  
4.  `ON` 句を削除します。 エラーが直ちに **[エラー一覧]** から消えます。  
  
### <a name="to-publish-a-database-project"></a>データベース プロジェクトを公開するには  
  
1.  SQL Azure インスタンスにアクセスできる場合は、スキップして次の手順に進むことができます。 それ以外の場合は、**ソリューション エクスプローラー**で **TradeDev** プロジェクトを右クリックし、 **[プロパティ]** をクリックして **[プロジェクトの設定]** プロパティ ページを開きます。 **[ターゲット プラットフォーム]** ボックスの一覧を使用して、プロジェクトの発行先となる SQL Server プラットフォームを選択します。  
  
2.  **ソリューション エクスプローラー**で **TradeDev** プロジェクトを右クリックし、 **[公開]** をクリックします。 SSDT により、プロジェクトのビルドが開始されます。 ビルド エラーがなければ、 **[データベースの公開]** ダイアログ ボックスが表示されます。  
  
3.  **[データベースの公開]** ダイアログ ボックスの **[編集]** をクリックし、ターゲットのデータベース接続を編集します。  
  
4.  **[接続のプロパティ]** ダイアログ ボックスで、SQL Server インスタンス名を指定し、認証に使用する資格情報を入力します。 **[データベースへの接続]** に、「 **NewTrade**」と入力します。 これにより、データベース プロジェクトを新しいデータベースに公開するように試行されます。 公開先の既存データベースを選択することもできます。 たとえば、既存の **TradeDev** データベースを選択すると、オフラインの **TradeDev** プロジェクトに含まれるオブジェクト (スクリプト) に対して加えた変更がすべて、ライブの **TradeDev** データベースに反映されます。  
  
    公開先のデータベースに変更を加えるアクセス許可を持っている場合は、 **[公開]** をクリックします。 運用データベースに対する書き込みアクセス許可を持っていない場合は、 **[スクリプトの生成]** をクリックし、Transact\-SQL 公開スクリプトを作成できます。これは DBA に渡すことができます。 DBA はスクリプトを実行し、スキーマがデータベース プロジェクトと同期するように、運用サーバーを更新します。  
  
5.  **[データ ツール操作]**  ウィンドウには、公開操作の進捗状況が表示され、エラーがあれば通知されます。 この新しいウィンドウでは、配置プレビュー、生成されたスクリプト、または必要に応じて公開のすべての結果も表示できます。  
  
6.  同じ設定を今後の公開操作に再利用できるように、公開設定をプロファイルに保存することもできます。 これには、 **[データベースの公開]** ダイアログ ボックスの **[プロファイルに名前を付けて保存]** をクリックします。 今後は、 **[プロファイルの読み込み]** をクリックすると既存の設定を再読み込みできます。  
  
7.  **[データ ツール操作]** ウィンドウのメッセージに注意してください。 **[公開プレビューを作成しています...]** の右にある [プレビューの表示] リンクをクリックします。の右にある [プレビューの表示] のリンクをクリックします。これにより、配置プレビュー レポートが表示されます。 プロジェクトの公開先のデータベース サーバーとプロジェクトのターゲット プラットフォームが一致しない場合は、SSDT による警告がこのレポートで発行されます。  たとえば、プロジェクトのターゲット プラットフォームが Microsoft SQL Server 2012 である場合に、プロジェクトを SQL Server 2008 R2 サーバー インスタンスに公開しようとすると、以下の警告が **[出力]** ウィンドウに表示されます。  
  
**A project which specifies Microsoft SQL Server 2012 as the target platform may experience compatibility issues with SQL Server 2008**    このようなプロジェクトに Microsoft SQL Server 2012 で導入されたエンティティ (たとえば、シーケンス オブジェクト) が含まれている場合、発行操作は失敗します。  
  
    The deployment will fail if object predicates use **CONTAINS** or **FREETEXT** over a newly created full-text index and transactional scripts are used. If the option to include transactional scripts is enabled during deployment, then procedures and views are defined inside a transaction while a full-text index is defined outside of a transaction at the end of the deploy script. Because of this ordering in the script, procedures or views using CONTAINS or FREETEXT will not be resolved against the full-text index, resulting in a deployment error.  
  
