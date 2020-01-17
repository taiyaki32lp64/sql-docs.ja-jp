---
title: テスト リポジトリ (OracleToSQL) の使用 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: da99b63c986029a1791793fbbd33910bb95d4b7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086805"
---
# <a name="using-test-repositories-oracletosql"></a>テスト リポジトリの使用 (OracleToSQL)
SSMA テスト リポジトリ ストア SSMA テスター テスト_ケースとテストの結果を後で使用します。 リポジトリのデータは、SQL Server テーブルに保存されます**TestCaseRepository**と**RunTestCaseResultRepository**スキーマ**ssma_oracle_utilities** の**ssmatesterdb**データベース。  
  
次のボタンは、リポジトリのテスト ケース ダイアログ ボックスを使用できます。  
  
-   をクリックして、**更新**テスト_ケースまたはテスト結果の一覧を更新するボタンをクリックします。  
  
-   をクリックして、**閉じます**リポジトリのテスト ケース ダイアログ ボックスを閉じるボタンをクリックします。  
  
## <a name="test-cases-repository"></a>テスト_ケースのリポジトリ  
クリックして、テスト_ケースのリポジトリを表示する **テスト\_ケース.** から、 **テスター** メニュー。 SSMA は、表示、 **テスト\_ケース リポジトリ** ダイアログ ウィンドウに保存されているテスト\_ケースの一覧で、 **テスト\_ケース** ページ。  
  
グリッドには、各テスト・ケースに関する次の情報が表示されます。  
  
-   名前:テスト_ケース名。  
  
-   作成されます。テスト_ケースの作成日。  
  
-   変更日。テスト ケース最終更新日。  
  
-   説明:テスト_ケースの説明。  
  
次のボタンが [テスト_ケース] ページで。  
  
-   をクリックして、**追加**テスト_ケース ウィザードを実行し、新しいテストを作成するボタンをクリックします。  
  
-   をクリックして、**削除**をリポジトリから、選択したテストを削除します。テスト_ケースが削除されると、関連するすべてのテスト結果も削除されます。  
  
-   をクリックして、**編集**テスト_ケース ウィザードを実行し、選択したテストを変更するボタンをクリックします。  
  
-   をクリックして、**実行**ボタンをクリックする、[を実行しているテスト_ケースは (OracleToSQL)](https://msdn.microsoft.com/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02)ダイアログし、選択したテストを実行します。  
  
## <a name="test-results-repository"></a>テストの結果リポジトリ  
テストの結果リポジトリを表示することができます、**テスト結果**のページ、**テスト_ケース リポジトリ**ウィンドウ。 クリックして開きます**テスト結果.** から、**テスター**メニュー。  
  
2 つのフィルターを使用して、**テスト結果**ページ。  
  
-   テスト_ケース名フィルター:テスト_ケース名によってテストの結果を選択することができます。 このフィルターの**すべてのテスト_ケース**値により、すべてのテスト_ケースのテスト結果を表示します。  
  
-   実行日のテスト ケース フィルター:テストの結果の保存日付をフィルターします。このフィルターの**すべて期間**保存の任意の日付のテスト結果を表示する値を使用できます。  
  
テスト結果の詳細については、次の情報がグリッドに表示されます。  
  
-   名前:テスト_ケース名。  
  
-   保存。保存のテスト ケースの日付。  
  
-   結果:テストの実行 (このセルのツールヒントには、テストの実行の完全な概要が表示されます) の概要。  
  
次のボタンは、テスト結果 ページで入手できます。  
  
-   をクリックして、**ビュー**ボタンをクリックする[テスト_ケースのレポートを表示する&#40;OracleToSQL&#41; ](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)の現在のテスト_ケースの結果。  
  
-   をクリックして、**削除** ボタンを選択したテスト結果を削除するには  
  
## <a name="see-also"></a>関連項目  
[テスト_ケースを実行している&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[移行されたデータベース オブジェクトのテスト&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
