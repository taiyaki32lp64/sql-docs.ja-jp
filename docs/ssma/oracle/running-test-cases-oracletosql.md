---
title: テスト_ケース (OracleToSQL) を実行している |。Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 79d3905c130e37c973a79a40369f97ae8f30ac5b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266549"
---
# <a name="running-test-cases-oracletosql"></a>テスト ケースの実行 (OracleToSQL)
SSMA のテスト担当者がテスト_ケースを実行すると、テスト用に選択されたオブジェクトを実行し、検証結果に関するレポートを作成します。 結果が両方のプラットフォームで同一の場合、テストは成功しました。 Oracle の間でオブジェクトの対応と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SSMA プロジェクトを現在のスキーマ マッピングの設定に従って決定されます。  
  
成功したテストのために必要な要件では、Oracle のすべてのオブジェクトが変換され、ターゲット データベースに読み込まれることです。 また、両方のプラットフォーム上のテーブルの内容を同期できるようにテーブルのデータを移行する必要があります。  
  
## <a name="run-test-case"></a>テスト_ケースを実行します。  
準備済みのテスト_ケースを実行します。  
  
1.  をクリックして、**実行**ボタンをクリックします。  
  
2.  **Connect to Oracle**  ダイアログ ボックスで、接続情報を入力し、順にクリックします**Connect**します。  
  
テストが完了したら、テスト_ケースのレポートが作成されます。 をクリックして、**レポート**を表示するボタン、[テスト_ケース レポート](viewing-test-case-reports-oracletosql.md)します。 テスト (テスト ケース レポート) の結果がで自動的に格納されている、[テストの結果リポジトリ](using-test-repositories-oracletosql.md)後で使用します。  
  
## <a name="test-case-execution-steps"></a>テスト_ケースの実行ステップ  
  
### <a name="prerequisites"></a>必須コンポーネント  
SSMA のテスト担当者は、テストの実行を開始する前に、テストのすべての前提条件が満たされたかどうかを確認します。 いくつかの条件が満たされない場合、エラー メッセージが表示されます。  
  
### <a name="initialization"></a>初期化  
この手順では、SSMA テスト担当者は、Oracle サーバーの SSMATESTER_ORACLE スキーマで補助オブジェクト (テーブル、トリガー、およびビュー) を作成します。 影響を受けるオブジェクトの検証用に選択したトレースの変更が可能です。  
  
検証済みのテーブルは USER_TABLE、ということを想定しています。 このようなテーブルでは、Oracle では、次の補助オブジェクトが作成されます。  
  
||||  
|-|-|-|  
|名前|型|説明|  
|USER_TABLE$ Trg|トリガー (trigger)|検証済みのテーブルで変更の監査をトリガーします。|  
|USER_TABLE$ AUD|テーブル|テーブルな行を削除し、上書きを保存する場所です。|  
|USER_TABLE$ AUDID|テーブル|追加または変更された行が保存されているテーブル。|  
|USER_TABLE|ビュー|テーブルの変更の簡略化された表現。|  
|USER_TABLE $ 新規|ビュー|行の挿入と上書きの簡略化された表現。|  
|USER_TABLE$ NEW_ID|ビュー|挿入および変更された行の id です。|  
|USER_TABLE$ 古い|ビュー|行の削除と上書きの簡略化された表現。|  
  
次のオブジェクトで検証済みのテーブルのスキーマに作成されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
||||  
|-|-|-|  
|名前|型|説明|  
|USER_TABLE$ Trg|トリガー (trigger)|検証済みのテーブルで変更の監査をトリガーします。|  
  
次のオブジェクトを作成および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ssmatesterdb データベースにします。  
  
||||  
|-|-|-|  
|名前|型|説明|  
|USER_TABLE$ Aud|テーブル|テーブルな行を削除し、上書きを保存する場所です。|  
|USER_TABLE$AudID|テーブル|追加または変更された行が保存されているテーブル。|  
|USER_TABLE|ビュー|テーブルの変更の簡略化された表現。|  
|USER_TABLE$new|ビュー|行の挿入と上書きの簡略化された表現。|  
|USER_TABLE$new_id|ビュー|挿入および変更された行の id です。|  
|USER_TABLE$old|ビュー|行の削除と上書きの簡略化された表現。|  
  
### <a name="test-object-calls"></a>オブジェクトの呼び出しをテストします。  
この手順では、SSMA テスト担当者は、テスト用に選択した各オブジェクトを呼び出し、結果を比較しますをレポートが表示されます。  
  
### <a name="finalization"></a>終了処理  
SSMA のテスト担当者がで作成された補助オブジェクトをクリーンアップ、終了処理中に、**初期化**手順。  
  
## <a name="next-step"></a>次の手順  
[テスト_ケースのレポートを表示する&#40;OracleToSQL&#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>関連項目  
[選択し、テストするオブジェクトを構成する&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[影響を受けるオブジェクトの選択と構成&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[移行されたデータベース オブジェクトのテスト&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
