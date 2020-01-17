---
title: 使用可能なサンプルのコンソール スクリプト FilesExecuting SSMA コンソール |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ad75b648-d119-4119-98f0-d18f058be68d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d6fea9a78928e2944cba1571737008965d679759
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938383"
---
# <a name="working-with-the-sample-console-script-filesexecuting-the-ssma-console-accesstosql"></a>サンプルのコンソール スクリプト FilesExecuting (AccessToSQL) SSMA コンソールの操作
いくつかのサンプル ファイルは、ユーザーの参照と使用状況の製品と共に提供されています。 このセクションでは、エンドユーザーのニーズに合わせてこれらのスクリプトを簡単にカスタマイズする方法について説明します。  
  
## <a name="sample-console-script-files"></a>サンプルのコンソール スクリプト ファイル  
さまざまなシナリオをカバーする次のサンプル コンソール スクリプト ファイルがユーザーの参照用に用意されています。  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   このサンプルでは、利用可能な接続の別のモードをソースとターゲット データベースにして、ユーザーは、必要に応じて、どのモードを選択できます。 このサンプルには、サーバーの定義が含まれています。  
  
    -   ユーザーは、必要なソースとターゲット サーバーの定義に値を変更するだけで、必要なデータベースに接続できます。 例ではすべての値が用意されています、変数の値にある、 **VariableValueFileSample.xml**します。 その他のすべての接続パラメーターは、ユーザーの作業サーバー接続ファイルから削除できます。  
  
    -   ソースとターゲット サーバーに接続する方法の詳細については、次を参照してください。[サーバー接続ファイルを作成する&#40;AccessToSQL&#41; ](../../ssma/access/creating-the-server-connection-files-accesstosql.md)します。  
  
-   **VariableValueFileSample.xml:** スクリプト ファイルのサンプルのコンソールで使用されているすべての変数と`ServersConnectionFileSample.xml`このファイルで照合されています。 ユーザーがサンプルの変数を置き換えるだけです、サンプルのコンソール スクリプトを実行するには、ユーザーに値は定義されているものとスクリプト ファイルと共に追加のコマンドライン引数としてこのファイルを渡します。  
  
    変数値ファイルの詳細については、次を参照してください。[変数値ファイルの作成&#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)します。  
  
-   **AssessmentReportGenerationSample.xml:** このサンプルで使用できるユーザー分析のために変換し、データの移行を始める前にこの xml 評価レポートを生成できます。  
  
    `generate-assessment-report`コマンド、ユーザーが mandatorily 変数の値を変更する必要があります (参照**VariableValueFileSample.xml**) で、`object-name`属性をユーザーによって使用されているデータベース名。 指定すると、オブジェクトの種類に応じて、`object-type`値を変更する必要があります。  
  
    場合、ユーザーが複数のオブジェクトを評価する必要があります/データベースは複数を指定できます`metabase-object`ノードに示すように、`generate-assessment-report`サンプルのコンソール スクリプト ファイルのコマンドの例 4。  
  
    レポートを生成する方法の詳細については、次を参照してください。[レポートを生成する&#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)します。  
  
    > [!NOTE]  
    > -   コンソール アプリケーションに渡される変数値ファイルのコマンドライン引数を使用すると、し VariableValueFileSample.xml が指定したユーザーに更新された値。  
    > -   サーバー接続ファイルのコマンドライン引数は、コンソール アプリケーションに渡される、ServersConnectionFileSample.xml が適切なサーバー パラメーターの値で更新されることを確認します。  
  
-   **ConversionAndDataMigrationSample.xml:** このサンプルでは、データの移行に変換する、エンド ツー エンドの移行を実行するユーザーができるようにします。 変更が必要とされる必須の属性値の一覧は、次に示します。  
  
    |コマンド名|説明|属性|  
    |----------------|---------------|-------------|  
    |`map-schema`|ターゲット スキーマにソース データベースのスキーマ マッピングです。|`source-schema:` 変換に必要となる、ソース データベースを指定します。<br /><br />`sql-server-schema`:ターゲット データベースへの移行を指定します|  
    |`convert-schema`|ソースからターゲット スキーマへのスキーマの変換を実行します。<br /><br />場合、ユーザーが複数のオブジェクトを評価する必要があります/データベースは複数を指定できます`metabase-object`ノードに示すように、`convert-schema`サンプルのコンソール スクリプト ファイルのコマンドの例 4。|`object-name`:ソース データベースを指定/オブジェクト名を変換する必要があります。 対応することを確認します`object-type`で指定されているオブジェクトの種類に応じて変化は、 `object-name`|  
    |`synchronize-target`|ターゲット オブジェクトは、ターゲット データベースと同期されます。<br /><br />場合、ユーザーが複数のオブジェクトを評価する必要があります/データベース彼複数を指定できます`metabase-object`ノードに示すように、`synchronize-target`サンプルのコンソール スクリプト ファイルのコマンドの例 3。|`object-name:` Sql server データベースを指定/オブジェクト名を作成する必要があります。 対応することを確認します`object-type`で指定されているオブジェクトの種類に応じて変化は、 `object-name`|  
    |`migrate-data`|ソース データをターゲットに移行します。<br /><br />場合、ユーザーが複数のオブジェクトを評価する必要があります/データベースは複数を指定できます`metabase-object`ノードに示すように、`migrate-data`サンプルのコンソール スクリプト ファイルのコマンドの例 2。|`object-name:` ソース データベースを指定します]、[テーブル名を移行する必要があります。 対応することを確認します`object-type`で指定されているオブジェクトの種類に応じて変化は、 `object-name`|  
  
## <a name="see-also"></a>参照  
[変数値ファイルを作成する&#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
[サーバー接続ファイルを作成する&#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
[レポートを生成する&#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)  
  
