---
title: SQL Server の単体テストの作成と定義 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.DatabaseMethodNameDialog
- sql.data.tools.unittesting.designer
ms.assetid: 3c082177-a2b1-4fde-8833-b49b2a351815
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b920803c317920c6336dbdde0990b4ad511cccb2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984593"
---
# <a name="creating-and-defining-sql-server-unit-tests"></a>SQL Server の単体テストの作成と定義
SQL Server の単体テストを実行すると、スキーマ内の 1 つ以上のデータベース オブジェクトに対する変更によって、データベース アプリケーションの既存の機能が損なわれていないかどうかを検証できます。 これらのテストは、ソフトウェア開発者が作成する単体テストを補完するものです。 両方の種類のテストを実行して、アプリケーションの動作を検証する必要があります。  
  
SQL Server の単体テストおよび Transact\-SQL スクリプトを任意のオブジェクトのテストに追加することにより、スキーマ内のそのオブジェクトの動作を検証できます。 また、特定の関数、トリガー、またはストアド プロシージャの動作を検証する場合は、Transact\-SQL スクリプトのスタブを自動的に生成することもできます。 スタブを生成したら、意味のある結果が得られるようにカスタマイズする必要があります。  
  
> [!NOTE]  
> SQL Server データベース プロジェクトを開いておかなくても、空のテストを作成し、そのテストにコードを追加して、実行することができます。 ただし、関数、トリガー、またはストアド プロシージャをテストする Transact\-SQL スタブは、テスト対象のオブジェクトを含むプロジェクトを開かないと自動的に生成することはできません。  
  
## <a name="common-tasks"></a>一般的なタスク  
次の表に、このシナリオをサポートする一般的なタスクの説明と、それらのタスクを正常に完了する方法の詳細へのリンクを示します。  
  
|一般的なタスク|関連する参照先|  
|----------------|----------------------|  
|**実践的な経験を得る**:入門編のチュートリアルに従い、シンプルな SQL Server 単体テストを作成および実行する方法を理解することができます。|-   [チュートリアル:SQL Server の単体テストの作成と実行](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)|  
|**SQL Server の単体テストの詳細を理解する**:SQL Server の単体テストを構成するファイルおよびスクリプトについて詳しく知ることができます。 また、単体テストでテスト条件と Transact\-SQL アサーションを使用する方法についても習得できます。|-   [SQL Server の単体テストのスクリプト](../ssdt/scripts-in-sql-server-unit-tests.md)<br />-   [SQL Server の単体テストのファイル](../ssdt/sql-server-unit-test-files.md)<br />-   [SQL Server の単体テストでのテスト条件の使用](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)<br />-   [SQL Server の単体テストでの Transact-SQL アサーションの使用](../ssdt/using-transact-sql-assertions-in-sql-server-unit-tests.md)|  
|**1 つ以上のテスト プロジェクトを作成する**:SQL Server の単体テストは、テスト プロジェクト内に作成する必要があります。 テスト プロジェクトを作成する前に SQL Server オブジェクト エクスプローラーを使用して SQL Server の単体テストを作成すると、テスト プロジェクトが自動的に作成されます。 たとえば、さまざまなテスト セット内で使用するデータ生成計画または配置構成が異なる場合は、複数のテスト プロジェクトを作成しておくこともできます。 テスト プロジェクトを作成するときに、そのプロジェクトに使用するテスト設定 (接続文字列など)、配置設定、およびデータ生成計画を構成できます。|-   [SQL Server の単体テストのテスト プロジェクトを作成する方法](../ssdt/how-to-create-a-test-project-for-sql-server-database-unit-testing.md)<br />-|  
|**単体テストの実行方法を構成する**:テストの実行対象のデータベースへの接続文字列、データ生成計画、配置設定を指定できます。 プロジェクトに SQL Server の単体テストを最初に追加する際にこれらの設定を構成しますが、後で変更することもできます。|-   [SQL Server の単体テストの実行を構成する方法](../ssdt/how-to-configure-sql-server-unit-test-execution.md)<br />-   [接続文字列とアクセス許可の概要](../ssdt/overview-of-connection-strings-and-permissions.md)|  
|**SQL Server の単体テストを作成する**:関数、トリガー、またはストアド プロシージャの動作を検証する SQL Server の単体テストの Transact\-SQL コード スタブを自動的に作成できます。 また、空の SQL Server の単体テストを作成し、他の種類のデータベース オブジェクトをテストするための Transact\-SQL コードを追加することもできます。|-   [関数、トリガー、ストアド プロシージャに対する SQL Server の単体テストを作成する方法](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)<br />-   [空の SQL Server の単体テストを作成する方法](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)|  
|**SQL Server の単体テストのコードを記述する**:単体テストの作成後は、データベース オブジェクトをテストするための Transact\-SQL コードを修正または記述します。 テストごとに、テストが成功するか失敗するかを判定するテスト条件を 1 つ以上定義します。 より複雑なテストでは、データベース プロジェクトの Visual Basic コードまたは Visual C\# コードを変更できます。 たとえば、1 つのトランザクションのスコープ内で実行される単体テストを記述できます。|-   [SQL Server の単体テストを開いて編集する方法](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md)<br />-   [SQL Server の単体テストにテスト条件を追加する方法](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)<br />-   [単一のトランザクションのスコープ内で実行する SQL Server の単体テストを作成する方法](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md)<br />-   [SQL Server 単体テスト デザイナーのキーボード ショートカット](../ssdt/keyboard-shortcuts-for-sql-server-unit-test-designer.md)|  
|**問題のトラブルシューティングを行う**:SQL Server に関する一般的な問題のトラブルシューティング方法についてさらに詳しく知ることができます。|-   [SQL Server のデータベース単体テストに関する問題のトラブルシューティング](../ssdt/troubleshooting-sql-server-database-unit-testing-issues.md)|  
  
## <a name="related-scenarios"></a>関連するシナリオ  
[SQL Server の単体テストの実行](../ssdt/running-sql-server-unit-tests.md)  
作成した SQL Server の単体テストは、[テスト ビュー] ウィンドウまたは SQL Server 単体テスト デザイナーから実行したり、Team Foundation ビルドを使用して実行したりできます。  
  
[シナリオ:データベース単体テストのカスタム条件の定義](https://msdn.microsoft.com/library/dd193282(VS.100).aspx)  
カスタムのテスト条件を作成すると、既定のテスト条件で検証できない動作をテストできます。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストを使用したデータベース コードの検証](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
