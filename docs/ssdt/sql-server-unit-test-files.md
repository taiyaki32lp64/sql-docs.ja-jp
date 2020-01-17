---
title: SQL Server の単体テストのファイル | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cee093c9-b97d-4fb0-b80f-806d071259dc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3dcefdc7b229f0d36f3c14349cc4af73c9f8eb2e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110657"
---
# <a name="sql-server-unit-test-files"></a>SQL Server の単体テストのファイル
マネージド コードの単体テストと同様に、SQL Server 単体テストはテスト プロジェクトに存在します。 **ソリューション エクスプローラー**のテスト プロジェクトの階層で、SQL Server 単体テストを構成するアイテムを確認できます。  
  
SQL Server 単体テストは、いくつかのファイルに含まれる複数のアイテムで構成されます。 次の表では、SQL Server 単体テストを構成するために相互作用するファイルを示します。  
  
|**[最近使ったファイル]**|**[説明]**|  
|------------|-------------------|  
|.cs または .vb|このソース コード ファイルには、[TestClass] 属性で修飾されたクラスが含まれます。 このクラスは、含まれる SQL Server 単体テストごとに 1 つのテスト メソッドが含まれています。 これらのメソッドは、[TestMethod] 属性で修飾されています。<br /><br />各テスト メソッドには、Transact\-SQL テスト スクリプトを実行するための適切なコードが含まれます。 このコードは、テスト メソッドを作成すると生成され、ユーザーが変更できます。<br /><br />**注:** このファイルを**ソリューション エクスプローラー**でダブルクリックすると、テスト クラスが SQL Server 単体テスト デザイナーで開かれます。 .cs または .vb ファイルを開いてソース コードを表示するには、**ソリューション エクスプローラー**でファイルを右クリックし、 **[コードの表示]** をクリックします。|  
|.resx|このリソース ファイルには、関連付けられた .cs ファイルまたは .vb ファイル内のすべてのテスト用の Transact\-SQL スクリプトが含まれています。 このスクリプトのグループには、事前テスト スクリプト、テスト スクリプト、事後テスト スクリプトが含まれます。 リソース ファイルに含まれる XML は編集できます。 リソース ファイルはテスト アセンブリにコンパイルされます。<br /><br />Transact\-SQL スクリプトは、**SQL Server 単体テスト デザイナー**を使用してコーディングする必要があります。 SQL Server 単体テストで使用されるスクリプトについて詳しくは、「[SQL Server の単体テストのスクリプト](../ssdt/scripts-in-sql-server-unit-tests.md)」をご覧ください。|  
|app.config|このファイルには、コマンド タイムアウトなどの他の SQL Server 単体テスト構成設定に加えて、テスト プロジェクト用のデータベース接続文字列が格納されています。詳しくは、「[SQL Server の単体テストのスクリプト](../ssdt/scripts-in-sql-server-unit-tests.md)」をご覧ください。|  
|SQLDatabaseSetup.cs または SQLDatabaseSetup.vb|このファイルには、テスト プロジェクト内のすべての SQL Server 単体テスト用にテスト環境を準備するクラスが含まれています。 app.config ファイルの構成設定に基づいて、テスト データベースに SQL Server データベース プロジェクトを配置する場合があります。|  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server の単体テストを使用したデータベース コードの検証](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[SQL Server の単体テストのスクリプト](../ssdt/scripts-in-sql-server-unit-tests.md)  
  
