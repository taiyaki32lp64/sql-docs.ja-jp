---
title: テスト_ケース準備 (OracleToSQL) の終了 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: bc5693c71ac6061f12ee90386b3c135a45a14e09
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266075"
---
# <a name="finishing-test-case-preparation-oracletosql"></a>テスト ケースの準備の終了 (OracleToSQL)
ウィザードの最後のページには、テスト_ケースの説明と、テストに含まれるオブジェクトに関する情報が表示されます。 さらに、このページで設定できますテストの実行オプション。  
  
**テスト_ケース情報**セクションには、テスト ケースの名前と説明が表示されます。  
  
**オブジェクトを選択するテスト**セクションには、名前付きオブジェクトの種類によってグループ化されたテスト済みのオブジェクトの一覧が含まれています。  
  
**オブジェクトの影響を受けるでテストを分析すること**セクションには、テスト対象のオブジェクトの実行後にデータ変更と比較するオブジェクトの名前付きの一覧が表示されます。  
  
## <a name="test-case-settings"></a>テスト_ケースの設定  
**テスト_ケース設定**セクションの次の実行テスト オプションを設定できます。  
  
### <a name="stop-test-execution-after-first-failure"></a>最初のエラーの後にテストの実行を停止します。  
テストの実行中にエラーが発生した場合、テストを中断することを指定します。  
  
-   選択した場合**はい**エラーが発生した場合は、実行が中断をテストします。  
  
-   選択した場合**いいえ**、エラーが発生したテストの実行が続行されます。  
  
### <a name="perform-data-rollback"></a>データのロールバックを実行します。  
テストの実行後にデータの自動ロールバックが可能です。  
  
-   選択した場合**はい**テストの実行後のデータの変更が失われます。  
  
-   選択した場合**いいえ**、すべてのテスト実行データの変更は保存されます。  
  
### <a name="auxiliary-tables-saving-mode"></a>補助テーブルの保存モード  
テストの実行中に作成された補助テーブルの保存モードを定義します。 内の補助テーブルの説明を参照して、[テスト_ケースを実行している&#40;OracleToSQL&#41; ](../../ssma/oracle/running-test-cases-oracletosql.md)トピック。  
  
-   選択した場合**常に保存**、後で使用するための補助テーブルのデータを格納する常にします。  
  
-   選択した場合**テーブルの比較が失敗した場合の保存**、補助テーブルのデータは、エラーが発生する場合にのみ格納されます。  
  
-   選択した場合**をいつでも削除**、常に補助テーブルがテストの実行の後に削除されます。  
  
-   選択した場合**テーブルの比較が失敗した場合にユーザーを依頼**エラーが発生した場合、ユーザーが必要な操作を選択できます。  
  
をクリックして、**完了**に準備されたテスト_ケースを保存するボタン[を使用してテスト リポジトリ (OracleToSQL)](https://msdn.microsoft.com/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4)します。  
  
## <a name="see-also"></a>関連項目  
[テスト リポジトリの使用&#40;OracleToSQL&#41;](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[テスト_ケースを実行している&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[移行されたデータベース オブジェクトのテスト&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
