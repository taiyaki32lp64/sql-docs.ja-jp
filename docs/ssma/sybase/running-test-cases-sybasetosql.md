---
title: テスト_ケース (SybaseToSQL) を実行している |。Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 73047e0741d4dee12ecec3e83df308e3f7abd343
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021023"
---
# <a name="running-test-cases-sybasetosql"></a>テスト ケースの実行 (SybaseToSQL)
SSMA のテスト担当者がテスト_ケースを実行すると、テスト用に選択されたオブジェクトを実行し、検証結果に関するレポートを作成します。 結果が両方のプラットフォームで同一の場合、テストは成功しました。 Sybase の間でオブジェクトの対応と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SSMA プロジェクトを現在のスキーマ マッピングの設定に従って決定されます。  
  
成功したテストのために必要な要件では、Sybase のすべてのオブジェクトが変換され、ターゲット データベースに読み込まれることです。 また、両方のプラットフォーム上のテーブルの内容を同期できるようにテーブルのデータを移行する必要があります。  
  
## <a name="run-test-case"></a>テスト_ケースを実行します。  
準備済みのテスト_ケースを実行します。  
  
1.  をクリックして、**実行**ボタンをクリックします。  
  
2.  **Sybase への接続** ダイアログ ボックスで、接続情報を入力し、順にクリックします**Connect**します。  
  
テストが完了したら、テスト_ケースのレポートが作成されます。 をクリックして、**レポート**を表示するボタン、[テスト_ケースのレポートを表示する&#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)します。 テスト (テスト ケース レポート) の結果がで自動的に格納されている、[テスト リポジトリを使用して&#40;SybaseToSQL&#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md)後で使用します。  
  
## <a name="test-case-execution-steps"></a>テスト_ケースの実行ステップ  
  
### <a name="prerequisites"></a>必須コンポーネント  
SSMA のテスト担当者は、テストの実行を開始する前に、テストのすべての前提条件が満たされたかどうかを確認します。 いくつかの条件が満たされない場合、エラー メッセージが表示されます。  
  
### <a name="initialization"></a>初期化  
この手順では、SSMA テスト担当者は補助両方のオブジェクト (テーブル、トリガー、およびビュー)、Sybase でを作成しますおよび[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 テーブルの比較モードがある場合、検証の選択の影響を受けるテーブルで行われた変更をトレースできる**のみが変更され**します。  
  
検証済みのテーブルは USER_TABLE、ということを想定しています。 このようなテーブルでは、Sybase で、次の補助オブジェクトが作成されます。  
  
SSMATESTER2005db または SSMATESTER2008db データベースと、Sybase では、次のオブジェクトが作成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ssmatesterdb_syb データベースにします。  
  
|名前|型|説明|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|トリガー|検証済みのテーブルで変更の監査をトリガーします。|  
|USER_TABLE$ Aud|テーブル|テーブルな行を削除し、上書きを保存する場所です。|  
|USER_TABLE$AudID|テーブル|追加または変更された行が保存されているテーブル。|  
|USER_TABLE|表示|テーブルの変更の簡略化された表現。|  
|USER_TABLE$new|表示|行の挿入と上書きの簡略化された表現。|  
|USER_TABLE$new_id|表示|挿入および変更された行の id です。|  
|USER_TABLE$old|表示|行の削除と上書きの簡略化された表現。|  
  
次のオブジェクトは、Sybase で検証済みのテーブルのデータベースに作成し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
|名前|型|説明|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|トリガー|検証済みのテーブルで変更の監査をトリガーします。|  
  
### <a name="test-object-calls"></a>オブジェクトの呼び出しをテストします。  
この手順では、SSMA テスト担当者は、テスト用に選択した各オブジェクトを呼び出し、結果を比較しますをレポートが表示されます。  
  
### <a name="finalization"></a>終了処理  
SSMA のテスト担当者がで作成された補助オブジェクトをクリーンアップ、終了処理中に、**初期化**手順。  
  
## <a name="next-step"></a>次の手順  
[テスト_ケースのレポートを表示する&#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>関連項目  
[選択し、テストするオブジェクトを構成する&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[影響を受けるオブジェクトの選択と構成&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[移行されたデータベース オブジェクトのテスト&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
