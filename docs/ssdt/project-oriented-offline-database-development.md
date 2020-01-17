---
title: プロジェクト指向のオフライン データベース開発 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.dbprojectwizard.general
- sql.data.tools.dbprojectwizard.summary
ms.assetid: e61e830d-9fcd-45e7-b7b4-93a42155dd56
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 59bff166871160525504e65a52648c97518a7ca7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110784"
---
# <a name="project-oriented-offline-database-development"></a>プロジェクト指向のオフライン データベース開発
このセクションでは、データベース プロジェクトの作成、ビルド、デバッグ、および公開を行うために SQL Server Data Tools (SSDT) で提供されている機能について説明します。  
  
SSDT を使用すると、サーバー インスタンスに接続しなくても、プロジェクト内のオブジェクトの定義 (スクリプト) を追加、修正、または削除することで、オフラインのデータベース プロジェクトを作成し、スキーマの変更を実装できます。 テーブル デザイナーまたは Transact\-SQL エディターを使用することで、これらをすべて実現できます。 同じプロジェクトで、Transact\-SQL オブジェクトおよび CLR オブジェクトを記述およびデバッグすることもできます。 スキーマ比較を使用すると、プロジェクトが運用データベースと同期されていることを確認し、比較用に開発サイクルの各段階でプロジェクトに対するスナップショットを作成できます。 チームベースの環境でデータベース プロジェクトの作業を行う際には、すべてのファイルをバージョン管理できます。 データベース プロジェクトを開発、テスト、およびデバッグした後で、運用環境に公開するプロジェクトは、許可されたユーザーに渡すことができます。  
  
> [!NOTE]  
> このセクションの操作方法に関するトピックには、順番に完了する一連のタスクが含まれています。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|---------|---------------|  
|[データベース プロジェクトへのインポート](../ssdt/import-into-a-database-project.md)|ライブ データベース、.dacpac、またはスクリプトからのオブジェクトのインポートについて説明します。|  
|[[データベース参照の追加] ダイアログ ボックス](../ssdt/add-database-reference-dialog-box.md)|データベース参照を追加するさまざまな方法について説明します。|  
|[[更新の確認] ダイアログ ボックス](../ssdt/check-for-updates-dialog-box.md)|製品の更新プログラムを SQL Server Data Tools で確認する方法について説明します。|  
|[データベース プロジェクトの設定](../ssdt/database-project-settings.md)|データベースの特性およびビルド構成を制御するための各種のプロジェクト設定について説明します。|  
|[方法: SQL Server データベース プロジェクトのオブジェクトを参照する](../ssdt/how-to-browse-objects-in-a-sql-server-database-project.md)|Visual Studio の SQL Server オブジェクト エクスプローラーには、専用の [プロジェクト] ノードが用意されました。このノードの下で、ソリューション内のすべての SQL Server データベース プロジェクトが SQL Server Management Studio のような階層構造でグループ化されます。|  
|[[データ ツール操作] ウィンドウ](../ssdt/data-tools-operations-window.md)|**[データ ツール操作]** ウィンドウについて説明します。このウィンドウには、一部の操作の進捗状況が表示され、エラーがあれば通知が表示されます。|  
|[Transact-SQL エディターのオプション](../ssdt/transact-sql-editor-options.md)|Transact\-SQL オプションについて説明します。|  
|[方法: 新しいデータベース プロジェクトを作成する](../ssdt/how-to-create-a-new-database-project.md)|データベース プロジェクトを作成し、既存のデータベース スキーマをインポートします。|  
|[方法: スキーマ比較を使用して各種のデータベース定義を比較する](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)|データベースのスキーマとプロジェクトを比較して同期します。|  
|[方法: ローカル データベースでビルドおよび配置を行う](../ssdt/how-to-build-and-deploy-to-a-local-database.md)|ローカルのオンデマンド SQL Server インスタンスを使用します。このインスタンスは、データベース プロジェクトをデバッグする際にアクティブ化されます。|  
|[方法: ターゲット プラットフォームを変更し、データベース プロジェクトを公開する](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)|プロジェクトのターゲットとなる SQL Server プラットフォームを、サポートされている任意の SQL Server インスタンスに変更し、構文を検証します。|  
|[方法: プロジェクトのスナップショットを作成する](../ssdt/how-to-create-a-snapshot-of-a-project.md)|データベース スキーマの読み取り専用プロキシを作成し、望ましくない変更がプロジェクトに適用された場合はソース プロジェクトを元に戻します。|  
|[方法: プロジェクトで Microsoft SQL Server 2012 のオブジェクトを使用する](../ssdt/how-to-use-microsoft-sql-server-2012-objects-in-your-project.md)|新しいシーケンス オブジェクトをプロジェクトに追加します。|  
|[方法: CLR データベース オブジェクトを使用する](../ssdt/how-to-work-with-clr-database-objects.md)|SQL Server Data Tools データベース プロジェクトで CLR オブジェクトを作成および公開します。|  
|[方法: Visual Studio 2010 のデータベース プロジェクトを SQL Server のデータベース プロジェクトに変換してターゲットを別のプラットフォームに変更する](../ssdt/how-to-convert-visual-studio-2010-database-projects-to-ssql-server-projects.md)|Visual Studio 2010 で作成された SQL Server データベース、CLR オブジェクト、およびデータ層アプリケーションの各既存プロジェクトを SQL Server Data Tools データベース プロジェクトに変換します。|  
|[方法: 配置前スクリプトまたは配置後スクリプトを指定する](../ssdt/how-to-specify-predeployment-or-postdeployment-scripts.md)|データベースの配置前または配置後に実行するスクリプトの使用方法について説明します。|  
  
## <a name="related-sections"></a>関連項目  
[テーブルとリレーションシップの管理およびエラーの修正](../ssdt/manage-tables-relationships-and-fix-errors.md)  
  
