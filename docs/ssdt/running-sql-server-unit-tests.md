---
title: SQL Server の単体テストの実行 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.testconfig
ms.assetid: febcc87f-eb18-4c12-ba30-82ef0d49aaa3
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67f49ab119e43ed59fc6bee5f9f10ede55143618
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088494"
---
# <a name="running-sql-server-unit-tests"></a>SQL Server の単体テストの実行
コードの品質を向上および維持するために、データベース オブジェクトの動作を検証する SQL Server 単体テストを作成して実行した後、そのテストをバージョン管理にチェックインできます。 データベース スキーマを変更するときは、SQL Server 単体テストとソフトウェア単体テストの両方を実行し、変更によって既存の機能が損なわれないことを確認します。 個々のテストを実行することも、テスト リストと呼ばれるテストのグループを実行することもできます。 詳しくは、「[Using Test Lists](http://msdn.microsoft.com/library/ms182461(VS.100).aspx)」(テスト リストの使用) (Visual Studio 2010) をご覧ください。  
  
## <a name="ways-to-run-sql-server-unit-tests"></a>SQL Server 単体テストを実行する方法  
次に示すように、インストールされているソフトウェアに応じて異なる複数の方法で、SQL Server 単体テストを実行できます。  
  
-   Visual Studio 2010 の **[テスト ビュー]** ウィンドウを使ってテストを実行します。 詳しくは、「[SQL Server 単体テストを実行する方法](../ssdt/how-to-run-sql-server-unit-tests.md)」および「[方法: Microsoft Visual Studio から自動テストを実行する (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182470(VS.100).aspx)」をご覧ください。 Visual Studio 2012 の場合は、「[方法: Microsoft Visual Studio から自動テストを実行する (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182470.aspx)」をご覧ください。  
  
-   コマンド プロンプトで MSTest.exe コマンドを使用してテストを実行します。 詳しくは、「[方法: MSTest を使用してコマンド ラインから自動テストを実行する (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182487(VS.100).aspx)」または「[方法: MSTest を使用してコマンド ラインから自動テストを実行する (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182487.aspx)」をご覧ください。  
  
-   **ソリューション エクスプローラー**からテスト プロジェクトを実行することで、テストを実行します。 詳しくは、「[方法: Microsoft Visual Studio から自動テストを実行する (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182470(VS.100).aspx)」または「[方法: Microsoft Visual Studio から自動テストを実行する (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182470.aspx)」をご覧ください。  
  
-   **[テスト結果]** ウィンドウからテストを再実行します。 詳しくは、「[方法: テストを再実行する (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182472(VS.100).aspx)」をご覧ください。  
  
-   **[テスト リスト エディター]** ウィンドウから個々のテストまたはテスト リスト (Visual Studio 2010) を実行します。 詳しくは、「[方法: Microsoft Visual Studio から自動テストを実行する (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182470(VS.100).aspx)」または「[方法: Microsoft Visual Studio から自動テストを実行する (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182470.aspx)」をご覧ください。  
  
-   Team Foundation ビルドでプロジェクトをビルドするときにテストを実行します。 詳しくは、「[方法: アプリケーションのビルド後にスケジュールされているテストを構成および実行する (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182465(VS.100).aspx)」または「[方法: アプリケーションのビルド後にスケジュールされているテストを構成および実行する (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182465.aspx)」をご覧ください。  
  
順序指定テストを使用して、特定の順序で SQL Server 単体テストを実行できます。 詳しくは、「[方法: 順序指定テストを作成する (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182631(VS.100).aspx)」または「[方法: 順序指定テストを作成する (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182631.aspx)」をご覧ください。  
  
## <a name="interpreting-tests-results"></a>テスト結果の解釈  
テストを実行した後、**[テスト結果]** ウィンドウにテストの合格または不合格が示されます。 詳しくは、「[SQL Server の単体テストの結果の解釈](../ssdt/interpreting-sql-server-unit-test-results.md)」をご覧ください。 予期しないエラーを診断する方法について詳しくは、「[データベース オブジェクトをデバッグする方法](../ssdt/how-to-debug-database-objects.md)」をご覧ください。  
  
## <a name="topics-in-this-section"></a>このセクションのトピック  
このセクションのトピックは次のとおりです。  
  
-   [データベース オブジェクトをデバッグする方法](../ssdt/how-to-debug-database-objects.md)  
  
-   [Team Foundation ビルドから SQL Server の単体テストを実行する方法](../ssdt/how-to-run-sql-server-unit-tests-from-team-foundation-build.md)  
  
-   [SQL Server 単体テストを実行する方法](../ssdt/how-to-run-sql-server-unit-tests.md)  
  
-   [SQL Server の単体テストの結果の解釈](../ssdt/interpreting-sql-server-unit-test-results.md)  
  
## <a name="related-scenarios"></a>関連するシナリオ  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
データベース オブジェクトの動作を検証するように単体テストを定義し、各テスト プロジェクトを異なるデータ生成計画、配置構成、および接続文字列と関連付けることができます。  
  
[SQL Server の単体テストのカスタム テスト条件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
カスタムのテスト条件を作成して、既定のテスト条件で検証できない条件をテストできます。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストを使用したデータベース コードの検証](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  