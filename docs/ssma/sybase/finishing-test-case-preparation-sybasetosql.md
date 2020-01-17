---
title: テスト_ケース準備 (SybaseToSQL) の終了 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Settings
ms.assetid: 8b2a49b0-4296-4f3f-9e56-323aa6a6fa8e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c3085d17804866015a78e93556dd5373d3a1b8cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029141"
---
# <a name="finishing-test-case-preparation-sybasetosql"></a>テスト ケースの準備の終了 (SybaseToSQL)
ウィザードの最後のページには、テスト_ケースの説明と、テストに含まれるオブジェクトに関する情報が表示されます。 さらに、このページで設定できますテストの実行オプション。  
  
**テスト_ケース情報**セクションには、テスト ケースの名前と説明が表示されます。  
  
**テスト オブジェクト**セクションには、名前付きオブジェクトの種類によってグループ化されたテスト済みのオブジェクトの一覧が含まれています。  
  
**分析対象のオブジェクトの影響を受ける**セクションには、テスト対象のオブジェクトの実行後にデータ変更と比較するオブジェクトの名前付きの一覧が表示されます。  
  
## <a name="test-case-settings"></a>テスト_ケースの設定  
**テスト_ケース設定**セクションの次の実行テスト オプションを設定できます。  
  
### <a name="stop-test-execution-after-first-failure"></a>最初のエラーの後にテストの実行を停止します。  
テストの実行中にエラーが発生した場合、テストを中断することを指定します。  
  
-   選択した場合**はい**エラーが発生した場合は、実行が中断をテストします。  
  
-   選択した場合**いいえ**、エラーが発生したテストの実行が続行されます。  
  
### <a name="perform-data-rollback"></a>データのロールバックを実行します。  
テストの実行後、データの自動ロールバックを有効にします。  
  
-   選択した場合**はい**テストの実行後のデータの変更が失われます。  
  
-   選択した場合**いいえ**、すべてのテスト実行データの変更は保存されます。  
  
### <a name="auxiliary-tables-saving-mode"></a>補助テーブルの保存モード  
テストの実行中に作成された補助テーブルの保存モードを定義します。 内の補助テーブルの説明を参照して、[テスト_ケースを実行している&#40;SybaseToSQL&#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md)トピック。  
  
-   選択した場合**常に保存**、後で使用するための補助テーブルのデータを格納する常にします。  
  
-   選択した場合**テーブルの比較が失敗した場合の保存**、補助テーブルのデータは、エラーが発生する場合にのみ格納されます。  
  
-   選択した場合**をいつでも削除**、常に補助テーブルがテストの実行の後に削除されます。  
  
-   選択した場合**テーブルの比較が失敗した場合にユーザーを依頼**エラーが発生した場合、ユーザーが必要な操作を選択できます。  
  
をクリックして、**完了**に準備されたテスト_ケースを保存するボタン[を使用してテスト リポジトリ&#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)。  
  
## <a name="see-also"></a>関連項目  
[テスト リポジトリの使用&#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[テスト_ケースを実行している&#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[移行されたデータベース オブジェクトのテスト&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
