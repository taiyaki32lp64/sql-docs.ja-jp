---
title: SQL Server の単体テストを使用したデータベース コードの検証 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 003713e2-de6b-4277-a0a8-7d1f2f4ffb39
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b3e720389f790282f1ad7a33302e2d277128178f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140951"
---
# <a name="verifying-database-code-by-using-sql-server-unit-tests"></a>SQL Server の単体テストを使用したデータベース コードの検証
SQL Server の単体テストを使用すると、データベースのベースラインとなる状態を確立した後、データベース オブジェクトに対してそれ以降行う変更を検証することができます。  
  
データベースのベースラインとなる状態を確立するには、データベース オブジェクトで動作するテスト プロジェクトを作成し、Transact\-SQL テストのセットを記述します。 このような単体テストを使用すると、分離した開発環境でオブジェクトが予想どおりに機能するかどうかを確認できます。 SQL Server 単体テストは、SQL Server データベース プロジェクトを使用したオフライン データベース開発に適しています (詳細については、「[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)」を参照してください)。 ベースラインとなる一連の SQL Server 単体テストが用意できたら、変更をバージョン管理にチェックインする前に、これらのテストを使用してデータベースが正しく動作しているかどうかを検証できます。  
  
任意のデータベース オブジェクトに対する変更を検証するテストを作成できます。 さらに、データベースの関数、トリガー、およびストアド プロシージャをテストする Transact\-SQL コードのスタブを自動的に生成できます。  
  
> [!NOTE]  
> SQL Server 単体テストは、データベース プロジェクトを開いていなくても、作成および実行できます。 ただし、プロジェクトの特定のデータベース オブジェクトをテストするテスト スクリプトを自動生成する場合は、テスト対象のオブジェクトを含むデータベース プロジェクトを開く必要があります。  
  
自分またはチーム メンバーがデータベース スキーマを変更した場合は、これらのテストを使用し、変更によって既存の機能が使用できなくなったかどうかを検証できます。 ソフトウェア開発者が作成するソフトウェア単体テストを補完する SQL Server 単体テストを作成します。 この両方のテストを実行して、アプリケーション全体の動作を検証する必要があります。  
  
単体テストでは、成功が予想されるときにプロシージャが成功し、失敗が予想されるときにプロシージャが失敗することを検証できます。 適切なエラーが発生することを検証するテストは、ネガティブ テストとも呼ばれます。  
  
## <a name="visual-studio-editions-support-for-sql-server-unit-tests"></a>SQL Server 単体テストに関する Visual Studio エディションのサポート  
2012 年 12 月の SQL Server Data Tools の更新プログラムで追加された SQL Server 単体テスト機能により、Visual Studio 2010 Professional および Visual Studio 2012 Professional 以上のエディションで SQL Server 単体テストを作成、変更、および実行できます。  
  
SQL Server Data Tools の最新の更新プログラムがインストールされていることを確認するには、「[[更新の確認] ダイアログ ボックス](../ssdt/check-for-updates-dialog-box.md)」を参照してください。  
  
Visual Studio 2010 および Visual Studio 2012 の SQL Server Data Tools 統合シェルでは、SQL Server 単体テストがサポートされません。  
  
## <a name="common-tasks"></a>一般的なタスク  
次の表に、このシナリオをサポートする一般的なタスクの説明と、それらのタスクを正常に完了する方法の詳細へのリンクを示します。  
  
|一般的なタスク|関連する参照先|  
|----------------|----------------------|  
|**実践的な経験を得る**: 入門編のチュートリアルに従い、シンプルな SQL Server 単体テストを作成および実行する方法を理解することができます。 このチュートリアルには、ネガティブ SQL Server 単体テストの例が含まれています。|[チュートリアル:SQL Server の単体テストの作成と実行](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)|  
|**SQL Server 単体テストを定義する:** SQL Server 単体テストを独自のプロジェクトに作成する必要があります。 そのプロジェクトの設定を構成し、テストごとに 1 つ以上のテスト条件を定義します。|[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)<br /><br />[SQL Server の単体テストでのテスト条件の使用](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)|  
|**SQL Server の単体テストを実行する:** 1 つまたは複数の単体テストを定義したら、単体テストを実行し、問題をデバッグして、テスト結果を調査します。|[SQL Server の単体テストの実行](../ssdt/running-sql-server-unit-tests.md)|  
|**テストのグループを管理する (Visual Studio 2010):** 通常同時に実行する必要があるテストの場合は、テストをグループ化することもできます。 テスト リストは引き続きサポートされますが、新しいテスト グループの場合は、代わりにテスト カテゴリを検討する必要があります。 たとえば、特定の*スキーマ*のトリガーまたはすべてのオブジェクトについて、テスト カテゴリを作成することもできます。|[テスト カテゴリの定義によるテストのグループ化](https://msdn.microsoft.com/library/dd286595(VS.100).aspx)<br /><br />[テスト リストの定義によるテストのグループ化](https://msdn.microsoft.com/library/dd286584(VS.100).aspx)|  
|**テスト プロジェクトとテストをバージョン管理にチェックインする:** テストを実行し、正常に動作するかどうかを検証したら、テスト プロジェクトと関連するすべてのファイルをバージョン管理にチェックインして、チームのすべてのメンバーがテストを実行できるようにする必要があります。 SQL Server データベース プロジェクトと一緒にテスト プロジェクトをバージョン管理にチェックインすることで、データベースとデータベース テストの両方の互換性のあるバージョンを簡単に復元できます。|[バージョン管理へのファイルの追加](https://msdn.microsoft.com/library/ms181374(VS.100).aspx)<br /><br />[[チェックイン] ウィンドウと [保留中の変更] ウィンドウの使用](https://msdn.microsoft.com/library/ms245462(VS.100).aspx)|  
|**カスタムのテスト条件を定義する:** 既定のテスト条件のセットでは対応できない動作をテストする必要がある場合は、カスタムのテスト条件を作成できます。 カスタムのテスト条件は、その新しい条件を使用するテストを実行するチーム メンバー全員に配布する必要があります。|[シナリオ: SQL Server の単体テストのカスタム テスト条件の定義](https://msdn.microsoft.com/library/dd193282(VS.100).aspx)|  
|**既存の単体テストを更新する:** 以前のバージョンの Visual Studio で作成されたデータベース単体テストがある場合は、今回のリリースで正常にビルドおよび実行されるように、アップグレードする必要があります。<br /><br />**注:** 以前のバージョンの Visual Studio のデータベース プロジェクトとデータベース単体テスト プロジェクトの両方を含むソリューションを開くと、データベース プロジェクトをアップグレードするように求めるメッセージが表示されます。 手動でアップグレードする必要のあるデータベース単体テスト プロジェクトについては、アップグレードするように求められることはありません。|[データベース単体テストを含む以前のテスト プロジェクトをアップグレードする](../ssdt/upgrade-an-older-test-project-containing-database-unit-tests.md)|  
|**機能拡張:** 機能拡張を作成することで SQL Server Data Tools の機能を拡張できます。|[SQL Server の単体テストのカスタム テスト条件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)|  
|**問題のトラブルシューティングを行う:** SQL Server 単体テストに関する一般的な問題のトラブルシューティング方法についてさらに詳しく知ることができます。|[SQL Server のデータベース単体テストに関する問題のトラブルシューティング](../ssdt/troubleshooting-sql-server-database-unit-testing-issues.md)|  
  
## <a name="related-scenarios"></a>関連するシナリオ  
[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)  
データベース単体テストは、SQL Server データベース プロジェクトを使用するオフライン プロジェクト開発と組み合わせて使用すると、特に高い効果が得られます。  
  
## <a name="see-also"></a>参照  
[SQL Server Data Tools](../ssdt/sql-server-data-tools.md)  
  
