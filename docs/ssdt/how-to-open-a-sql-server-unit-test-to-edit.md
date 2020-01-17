---
title: 方法:SQL Server の単体テストを開いて編集する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c6af1b12-54cd-42f9-b2ef-7164f8078323
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 52818b0d76ae5201fb9bf53376696fab54180cb2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035152"
---
# <a name="how-to-open-a-sql-server-unit-test-to-edit"></a>方法:SQL Server の単体テストを開いて編集する
SQL Server の単体テストを作成したら、**SQL Server 単体テスト デザイナー**を使用して Transact\-SQL ステートメントおよびテスト条件を追加します。 このデザイナーを使用して作成されたテストでは、Visual C# コードまたは Visual Basic コードが生成されます。 このコードが、テストの実行時に実行されます。  
  
作成されたテストで問題ない場合は、テストをそのまま実行できます。 この単体テストにさらに機能を追加する場合は、テストのコードを編集できます。 このコードは、テスト プロジェクト内の .cs ファイルまたは .vb ファイルにあります。 詳しくは、「[SQL Server の単体テストのファイル](../ssdt/sql-server-unit-test-files.md)」をご覧ください。 また、新しいテスト条件を作成して、テストをカスタマイズすることもできます。 詳細については、「[ソフト NUMA を使用するようにCreate Test Conditions for the Database Unit Test Designer (Visual Studio 2010)](https://msdn.microsoft.com/library/aa833409(VS.100).aspx)」(データベース単体テスト デザイナーのテスト条件を作成する方法) を参照してください。  
  
> [!NOTE]  
> .cs ファイルまたは .vb ファイルを編集してテスト メソッドを削除しても、そのテスト メソッドは **SQL Server 単体テスト デザイナー**に表示されたままです。 これは、テスト クラスの InitializeComponent メソッドにそのテストのメンバー変数が残っていることが原因です。 テストは、デザイナーには表示されますが、そのコードは既に存在しないため、実行することはできません。 このテストのテスト メソッドを再生成するには、エディターで Transact\-SQL を編集した後、.cs テスト ファイルまたは .vb テスト ファイルを保存するか、テスト プロジェクトをビルドし直してください。  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-solution-explorer"></a>ソリューション エクスプローラーから SQL Server の単体テストのソース コード ファイルを開くには  
  
-   **ソリューション エクスプローラー**で、SQL Server 単体テストを含むソース コード ファイルを右クリックし、 **[コードの表示]** をクリックします。  
  
    ファイルが開くと、単体テストのテスト メソッドが Visual Studio のメイン編集ウィンドウに表示されます。  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-the-test-view-window-visual-studio-2010"></a>[テスト ビュー] ウィンドウから SQL Server の単体テストのソース コード ファイルを開くには (Visual Studio 2010)  
  
1.  単体テストを実行します。 詳しくは、「[チュートリアル:SQL Server の単体テストの作成と実行](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)」の「SQL Server の単体テストの実行」セクションをご覧ください。  
  
2.  [テスト ビュー] ウィンドウで、テストを右クリックし、 **[テストを開く]** をクリックします。  
  
    ファイルが開くと、単体テストのテスト メソッドが Visual Studio のメイン編集ウィンドウに表示されます。  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-the-test-view-window-visual-studio-2012"></a>[テスト ビュー] ウィンドウから SQL Server の単体テストのソース コード ファイルを開くには (Visual Studio 2012)  
  
1.  単体テストを実行します。 詳しくは、「[チュートリアル:SQL Server の単体テストの作成と実行](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)」の「SQL Server の単体テストの実行」セクションをご覧ください。  
  
2.  [テスト エクスプローラー] ウィンドウで、単体テストのソース コード ファイルの名前をクリックします。  
  
    ファイルが開くと、単体テストのテスト メソッドが Visual Studio のメイン編集ウィンドウに表示されます。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server の単体テストを使用したデータベース コードの検証](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
