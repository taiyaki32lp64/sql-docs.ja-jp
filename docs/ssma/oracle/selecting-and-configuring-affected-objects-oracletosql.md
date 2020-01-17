---
title: 影響を受けるオブジェクト (OracleToSQL) の選択と構成 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Columns Comparison Settings
- Selection of Affected Objects
ms.assetid: 545eeda2-9829-4187-a858-619a96b4b71d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: c06fb621cab581e934ba4655ed6507149d109c60
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266503"
---
# <a name="selecting-and-configuring-affected-objects-oracletosql"></a>影響を受けるオブジェクトの選択と構成 (OracleToSQL)
このページでは、テーブルを選択することができ、SSMA 前の手順で選択したオブジェクトの実行の結果を検証するときに、外部キーを変更とを比較する必要があります。 また、検証パラメーターをカスタマイズできます。  
  
## <a name="selection-of-affected-objects"></a>影響を受けるオブジェクトの選択  
ウィンドウの左側にある Oracle オブジェクト ツリーでテーブルと外部キーをチェックで変更が同一になるのと比較する必要があります。  
  
SSMA のテスト担当者は、これらのオブジェクトのいずれかを確認できない場合、というラベルの付いたリンクが表示されます**いくつかの選択したオブジェクトがエラーを含む**オブジェクト ツリーの下。 なぜこれらのオブジェクトを比較できない理由を表示して、不適切なオブジェクトの選択を解除する、このリンクをクリックします。  
  
## <a name="table"></a>テーブル  
[テーブル] タブには、選択したテーブルのグリッド ビューが含まれています。 グリッドには、選択したテーブルの詳細については、次の情報が含まれています。  
  
-   列名  
  
-   データ型  
  
-   有効桁数  
  
-   Scale  
  
-   Rule  
  
-   既定  
  
-   同一。  
  
-   [可]  
  
## <a name="sql"></a>Sql  
SQL タブには、「テーブル作成」にはが含まれています。 SQL のテーブルを選択します。  
  
## <a name="data"></a>data  
[データ] タブには、選択したテーブル内のデータが表示されます。  
  
## <a name="properties"></a>Properties  
[プロパティ] タブには、選択したテーブルのプロパティが表示されます。 次のフィールド、[プロパティ] タブの下。  
  
-   作成または最後に変更  
  
-   オブジェクト名  
  
## <a name="columns-comparison-settings"></a>列の比較の設定  
テーブルの列に対して比較の規則の確立**列比較**ページ。 次の設定を行うことができます。  
  
### <a name="use-during-test-comparisons"></a>テストの比較の際に使用  
この列は、テスト結果の検証に参加するかどうかを決定します。  
  
-   選択した場合**True**SSMA は Oracle の SQL Server 内の列の内容を含むテストの実行後にこの列の内容を比較します。 
  
-   選択した場合**False**列は、結果の検証から除外されます。  
  
### <a name="use-custom-scale"></a>カスタムのスケールを使用します。  
数値データ型の列の場合は、比較のためのカスタム スケールを設定できます。  
  
-   選択した場合**True**、に従って数値は丸められます、**を比較するスケール**値の前に、比較されます。  
  
-   選択した場合**False**、数値比較を正確になります。  
  
### <a name="comparing-scale"></a>スケールを比較します。  
  
-   使用可能な場合にのみ、**使用のカスタム スケール**にオプションが設定されている**True**します。 これは、数値比較の有効桁数です。  
  
### <a name="date-time-comparing"></a>日付時刻を比較します。  
定義する方法、日付/時刻値が比較されます。  
  
-   選択した場合**全体の日付の比較**、両方のプラットフォームからの値の完全な比較を実行します。  
  
-   選択した場合**日付のみを比較**、時刻部分は無視されます。  
  
-   選択した場合**時刻のみを比較**日付の部分は無視されます。  
  
-   選択した場合**無視ミリ秒**結果は秒単位までと比較されます。  
  
-   選択した場合**を無視する日付とミリ秒**秒の時間部分でのみ比較し、無視の小数部になります。  
  
### <a name="ignore-strings-case"></a>文字列の大文字小文字を区別します。  
比較の大文字小文字の区別を制御します。  
  
-   選択した場合**True**、大文字と小文字を区別しない比較になります。  
  
-   選択した場合**False**大文字と小文字のアカウントは、比較します。  
  
## <a name="comparing-sql"></a>SQL の比較  
SSMA テスターによって生成された SELECT ステートメントを表示することができます、**を比較する SQL**ページ。 テスト担当者 - 行ごとにこれらのステートメントの結果セットが比較されます。 [次へ]、Oracle の結果セットの各行を SQL Server で生成された結果セットの次の行と等しいことがあります。
  
カスタム検証を提供するこれらの SELECT ステートメントを編集することができます。 Oracle では、SQL Server のステートメントで、変更を保存するには、使用、**適用**これに応じて拡大縮小、ソースとターゲット SQL では、下ボタンします。  
  
## <a name="next-step"></a>次の手順  
[呼び出し順序のカスタマイズ&#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
## <a name="see-also"></a>関連項目  
[テスト_ケースの準備の終了&#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
[テスト_ケースを実行している&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[移行されたデータベース オブジェクトのテスト&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
