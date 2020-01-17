---
title: 方法:空の SQL Server の単体テストを作成する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.createtest
ms.assetid: b6f3cd5a-3389-42d6-a93f-97b3ddf31b95
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2cd7a605fbe9d3075d4d67e1ce824664ef2747c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897129"
---
# <a name="how-to-create-an-empty-sql-server-unit-test"></a>方法:空の SQL Server の単体テストを作成する
データベース オブジェクトに単体テストを含めることで、データベース オブジェクトに加えた変更によって既存の機能が使用できなくなっていないかどうかを検証できます。 次に、任意のデータベース オブジェクト用に SQL Server 単体テストを作成する手順について説明します。 SQL Server Data Tools には、データベース関数、トリガー、およびストアド プロシージャの追加のサポートも含まれています。 詳細については、「[ソフト NUMA を使用するように関数、トリガー、ストアド プロシージャに対する SQL Server の単体テストを作成する方法](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)」を参照してください。  
  
最初の手順を使用して SQL Server の単体テストを作成すると、テスト プロジェクトが存在しない場合は自動的に作成されます。 テスト プロジェクトが既に存在する場合は、新しいテストをプロジェクトの 1 つに追加するか、新しいテスト プロジェクトを作成するかを選択できます。 テスト プロジェクトの詳細については、「[SQL Server の単体テストのテスト プロジェクトを作成する方法](../ssdt/how-to-create-a-test-project-for-sql-server-database-unit-testing.md)」を参照してください。  
  
SQL Server の単体テストを作成するには、次の 2 つの方法があります。  
  
-   新しいテスト クラス内に新しい SQL Server の単体テストを作成する。  
  
    指定したテスト クラス内の SQL Server のすべての単体テストでは、同じ TestInitialize スクリプトと TestCleanup スクリプトが使用されます。 他の単体テストとは別の TestInitialize スクリプトおよび TestCleanup スクリプトを使用する場合は、新しいテスト クラスを作成します。 詳しくは、「[SQL Server の単体テストのスクリプト](../ssdt/scripts-in-sql-server-unit-tests.md)」をご覧ください。  
  
-   既存テスト クラス内に新しい SQL Server の単体テストを作成する。  
  
    クラス内の他の単体テストと同じ TestInitialize スクリプトと TestCleanup スクリプトを使用する場合は、この方法を選択します。  
  
### <a name="to-create-a-sql-server-unit-test-inside-a-new-test-class"></a>新しいテスト クラス内に SQL Server の単体テストを作成するには、次の手順を実行します  
  
1.  **[テスト]** メニューの **[新しいテスト]** をクリックします。  
  
    **[新しいテストの追加]** ダイアログ ボックスが表示されます。  
  
2.  **[テンプレート]** の **[SQL Server 単体テスト]** をクリックします。  
  
3.  **[テスト名]** に、テストの名前を入力します。  
  
4.  **[テスト プロジェクトに追加]** で、このテストの追加先となる既存のテスト プロジェクトを選択します。 テスト プロジェクトが存在しない場合、または新しいテスト プロジェクトを作成する場合は、 **[新しい <language> テスト プロジェクトの作成]** を選択します。  
  
5.  **[OK]** をクリックします。  
  
    テスト プロジェクトが新しい場合、 **[新しいテスト プロジェクト]** ダイアログ ボックスが表示されます。 プロジェクト名を指定して、 **[OK]** をクリックします。  
  
    テスト プロジェクトが新しい場合または構成されていない場合は、 **[SQL Server テスト構成 - <ProjectName>]** ダイアログ ボックスが表示されます。 このダイアログ ボックスでは、テスト プロジェクトに関する次の情報を構成できます。  
  
    -   テストの実行に使用するデータベース接続。  
  
    -   テスト結果の検証、データベースの配置、およびデータの生成に使用するデータベース接続。  
  
    -   単体テストを実行する前の、データベース プロジェクトと関連するスキーマ変更の特定のプロジェクト構成への自動配置。  
  
    詳細については、「[ソフト NUMA を使用するようにSQL Server の単体テストの実行を構成する方法](../ssdt/how-to-configure-sql-server-unit-test-execution.md)」を参照してください。  
  
6.  プロジェクトの構成情報を指定し、 **[OK]** をクリックします。  
  
    \- - または -  
  
    **[キャンセル]** をクリックして、テスト プロジェクトを構成せずに単体テストを作成します。  
  
    **SQL Server 単体テスト デザイナー**に、空白のテストが表示されます。 テスト プロジェクトの作成に指定した言語によって、Visual Basic または Visual C\# のソース コード ファイルがテスト プロジェクトに追加されます。 このファイルには、単体テスト用に SQL Server Data Tools によって生成される SQL Server の単体テスト クラスが含まれます。 このテスト クラスには、SQL Server 単体テスト デザイナーを使用するか、テスト クラスの新しいテスト メソッドとしてのコードを通じて追加できる 1 つ以上の単体テストを含めることができます。  
  
    また、次の方法で新しいテストを追加することもできます。  
  
    -   **ソリューション エクスプローラー**でテスト プロジェクトを右クリックし、 **[追加]** をポイントして、 **[新しいテスト]** をクリックします。次に **[SQL Server 単体テスト]** を選択します。  
  
    -   SQL Server オブジェクト エクスプローラーで [単体テストの作成] をクリックします。  
  
    **ソリューション エクスプローラー**でこのファイルを選択すると、既定では、SQL Server 単体テスト デザイナーに表示されます。 コードを表示するか、コードをカスタマイズして単体テストに機能を追加するには、ファイルを選択して右クリックし、 **[コードの表示]** をクリックします。  
  
### <a name="to-create-a-sql-server-unit-test-inside-an-existing-test-class"></a>既存テスト クラス内に SQL Server の単体テストを作成するには  
  
1.  **SQL Server 単体テスト デザイナー**で、既存の SQL Server 単体テスト クラスを開きます。 **ソリューション エクスプローラー**で単体テストのソース コード ファイルをダブルクリックすることで、**SQL Server 単体テスト デザイナー**にアクセスできます。  
  
2.  ナビゲーション バーの正符号 ( **+** ) をクリックして、 **[単体テスト名を指定します]** ダイアログ ボックスを表示します。  
  
3.  名前を入力し、 **[OK]** をクリックします。  
  
    新しい SQL Server の単体テストは、ナビゲーション バーのドロップダウン リストで選択できるようになります。 また、テスト クラスの新しいテスト メソッドとしても追加されます。 コードでテスト メソッドを表示するには、クラス ファイルを選択して右クリックし、 **[コードの表示]** を選択します。 現在のテスト クラス ファイルの名前が、**SQL Server 単体テスト デザイナー**の上部にあるタブに表示されます。  
  
テスト プロジェクトを構成し、単体テストを作成した後、次の手順を実行します。  
  
-   Transact\-SQL スクリプトを追加します。  
  
-   事前テストと事後テストのアクションを定義します。  
  
-   スクリプトの結果を確認するためのテスト条件またはその他のアサート ステートメントを追加します。  
  
> [!NOTE]  
> 結果不確定のテスト条件は、すべてのテストに追加される既定の条件です。 このテスト条件は、テストの検証が実装されていないことを示すために含まれています。 このテスト条件は、他のテスト条件を追加した後に、テストから削除します。 詳細については、「[ソフト NUMA を使用するようにAdd Test Conditions to Database Unit Tests](https://msdn.microsoft.com/library/aa833242(VS.100).aspx)」(データベース単体テストにテスト条件を追加する方法) を参照してください。  
  
## <a name="see-also"></a>参照  
[方法:SQL Server の単体テストを実行する](../ssdt/how-to-run-sql-server-unit-tests.md)  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[単体テストの作成](https://msdn.microsoft.com/library/ms182523(VS.90).aspx)  
  
