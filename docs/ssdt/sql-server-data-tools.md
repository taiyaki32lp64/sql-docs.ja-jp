---
title: SQL Server Data Tools | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.errortask.generichelp
ms.assetid: 5f08f15a-851d-4026-a557-28b3c6492efe
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7bd026b76a7ce6e891c4267ad2c11b4e869a4d35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110695"
---
# <a name="sql-server-data-tools"></a>SQL Server Data Tools
SQL Server Data Tools (SSDT) は、Visual Studio で行うデータベース開発のあらゆるフェーズにわたるユビキタスな宣言モデルを導入することにより、データベース開発の形態を一変させました。 SSDT の Transact\-SQL デザイン機能を使用して、データベースのビルド、デバッグ、メンテナンス、およびリファクタリングを実行できます。 この作業は、データベース プロジェクトに対して、あるいはオンプレミスまたはオフプレミスで接続されているデータベース インスタンスに対して直接、行うことができます。  
  
使い慣れた Visual Studio ツールをデータベース開発でも使用できます。 コード ナビゲーション、IntelliSense、C# および Visual Basic に匹敵する言語サポート、プラットフォーム固有の検証、デバッグ、および宣言的な編集などのツールが Transact\-SQL エディターにも用意されています。 SSDT には、データベース プロジェクトまたは接続されているデータベース インスタンスのテーブルを作成または編集するためのビジュアル テーブル デザイナーも提供されています。 チームベースの環境でデータベース プロジェクトの作業を行う際には、すべてのファイルにバージョン管理を使用できます。 プロジェクトを発行する際には、SQL Database および SQL Server を含め、サポートされているすべての SQL プラットフォームに発行できます。 SSDT にはプラットフォーム検証機能があるため、スクリプトは指定されたターゲットで確実に動作します。  
  
Visual Studio の SQL Server オブジェクト エクスプローラーには、SQL Server Management Studio と同様のデータベース オブジェクトを表示する機能があります。 SQL Server オブジェクト エクスプローラーを使用すると、簡単なデータベースの管理や設計の作業を行うことができます。 テーブル、ストアド プロシージャ、型、関数などの作成、編集、名前変更、および削除が簡単にできます。 さらに、SQL Server オブジェクト エクスプローラーのコンテキスト メニューを使用することにより、テーブル データの編集、スキーマの比較、またはクエリの実行もできます。  
  
次のトピックやセクションでは、データベース開発で SSDT がどのように役立つかを説明します。 方法を説明するトピックは、データベース プロジェクトで遭遇する一連のタスクを完了できるように案内します。 これらのタスクは、Northwind Traders という食料品を輸出入する架空の会社を使って、チュートリアルのように記述されており、順番に従って実行します。  
  
|トピック/セクション|[説明]|  
|-------------------|---------------|  
|[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)|このセクションのトピックでは、データベース プロジェクトの作成、ビルド、デバッグ、および発行を行うための SQL Server Data Tools の機能について説明します。|  
|[コマンド ライン ツールを使用したプロジェクト指向のデータベース開発](../ssdt/project-oriented-database-development-using-command-line-tools.md)|このセクションのトピックでは、プロジェクト指向の各種データベース開発シナリオを実現に導くコマンド ライン ツールについて説明します。|  
|[接続されているデータベース開発](../ssdt/connected-database-development.md)|このセクションのトピックでは、接続されているデータベースのデザインおよび照会を行うための SQL Server Data Tools の機能について説明します。|  
|[1 つ以上のテーブルのデータを参照データベースのデータと比較して同期する](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)|ソース データベースとターゲット データベースのデータを比較する方法、一致する値を指定する方法、ターゲットを更新してデータベースを同期したり、更新スクリプトを Transact\-SQL エディターまたはファイルにエクスポートしたりする方法について説明します。|  
|[Transact-SQL エディターを使用したスクリプトの編集と実行](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)|このセクションのトピックでは、スクリプトの編集およびデバッグに役立つ豊富な機能が用意されている Transact\-SQL エディターの使用方法について説明します。|  
|[テーブルとリレーションシップの管理およびエラーの修正](../ssdt/manage-tables-relationships-and-fix-errors.md)|このセクションのトピックが説明するタスク<br /><br />-   テーブル デザイナーを使用してテーブルをデザインし、テーブルのリレーションシップを管理します。<br />-   よくある構文エラーやセマンティック エラーを修正します。|  
|[SQL Server の単体テストを使用したデータベース コードの検証](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)|SQL Server の単体テストを使用して、データベースのベースラインとなる状態を確立した後、データベース オブジェクトに対してそれ以降行う変更を検証する方法について説明します。|  
|[データベース機能の拡張](../ssdt/extending-the-database-features.md)|機能拡張を作成して、単体テストやデータベース コード分析などの機能を拡張することができます。|  
|[SQL Server Data Tools に必要な権限](../ssdt/required-permissions-for-sql-server-data-tools.md)|SQL Server Data Tools を使用するために必要なアクセス権限について説明します。|  
|[DAC Framework の互換性](../ssdt/dac-framework-compatibility.md)|DAC Framework との互換性の問題について説明します。|  
  

  
