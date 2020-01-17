---
title: レポート (OracleToSQL) の生成 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Report Generation in Oracle Console, synchronize-target
- Report Generation in Oracle Console,refresh-from-database
- Report Generation in Oracle Console,write-summary-report-to
ms.assetid: ccad6262-01e1-447a-bd2b-c105154c80ce
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 971d7e8dde2ae56da02205b50b2f6576a875bd70
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264456"
---
# <a name="generating-reports-oracletosql"></a>レポートの生成 (OracleToSQL)
オブジェクト ツリーのレベルでの SSMA コンソールのコマンドを使用して実行される特定のアクティビティ レポートが生成されます。  
  
レポートを生成するのにには、次の手順を使用します。  
  
1.  指定、**書き込みで概要レポート-を**パラメーター。 (指定した) 場合に、ファイル名として、関連するレポートが格納されているまたはでフォルダーを指定します。 ファイル名は、where、次の表で説明したようにシステム定義済み **&lt;n&gt;** は、同じコマンドを実行するたびに 1 桁の数字をインクリメントする一意のファイル数です。  
  
    レポートの vis-比べて-vis コマンドは次のとおりです。  
  
    ||||  
    |-|-|-|  
    |**Sl.No.**|**Command**|**レポートのタイトル**|  
    |@shouldalert|generate-assessment-report|AssessmentReport&lt;n&gt;します。XML|  
    |2|変換とスキーマ|SchemaConversionReport&lt;n&gt;します。XML|  
    |3|データの移行|DataMigrationReport&lt;n&gt;します。XML|  
    |4|convert-sql-statement|ConvertSQLReport&lt;n&gt;します。XML|  
    |5|同期ターゲット|TargetSynchronizationReport&lt;n&gt;します。XML|  
    |6|データベースからの更新|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > レポートの出力は、評価レポートと異なります。 前者はコマンドの実行中のパフォーマンス上のレポート、後者は、プログラムによる使用量の XML レポート。  
  
    コマンド オプションの出力からのレポート (上記の Sl. No. 2 ~ 4) を参照してください、 [SSMA コンソールを実行する&#40;OracleToSQL&#41; ](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)セクションです。  
  
2.  レポートの詳細度の設定を使用して、出力レポートに必要な詳細の程度を示します。  
  
    ||||  
    |-|-|-|  
    |**Sl.No.**|**コマンドとパラメーター**|**出力の説明**|  
    |1|詳細な ="false"|アクティビティの集計レポートを生成します。|  
    |2|詳細な ="true"|各アクティビティの概要と詳細の状態レポートを生成します。|  
  
    > [!NOTE]  
    > 上記で指定したレポートの詳細度の設定は生成評価レポート、convert スキーマ、データの移行、sql ステートメントの変換コマンド。  
  
3.  エラー報告の設定を使用してエラーの報告に必要な詳細の程度を示します。  
  
    ||||  
    |-|-|-|  
    |**Sl.No.**|**コマンドとパラメーター**|**出力の説明**|  
    |1|レポート エラー ="false"|エラーの詳細はありません/警告/情報メッセージ。|  
    |2|report-errors="true"|エラーの詳細/警告/情報メッセージ。|  
  
    > [!NOTE]  
    > 上記で指定したエラー報告の設定は生成評価レポート、convert スキーマ、データの移行、sql ステートメントの変換コマンド。  
  
**例:**  
  
```  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-type>"  
  
   verbose="<true/false>"  
  
   report-erors="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   assessment-report-folder="<folder-name>"  
  
   assessment-report-overwrite="<true/false>"/>  
```  
  
### <a name="synchronize-target"></a>同期ターゲット:  
コマンドは、**同期ターゲット**が**レポートでエラーを**パラメーターで、同期操作のエラー レポートの場所を指定します。 次に、名前のファイル**TargetSynchronizationReport&lt;n&gt;します。XML**が指定した場所に作成、 **&lt;n&gt;** は、同じコマンドを実行するたびに 1 桁の数字をインクリメントする一意のファイル数です。  
  
**注:** フォルダーのパスを指定した場合、' レポートでエラーを 'パラメーターは、コマンド' 同期ターゲット ' の省略可能な属性になります。  
  
```  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**オブジェクト名:** 同期 (含めることもできます個々 のオブジェクト名またはグループ オブジェクトの名前) と見なされるオブジェクトを指定します。  
  
**エラー:** 同期エラーを警告またはエラーとして指定するかどうかを指定します。 エラー時の使用可能なオプション:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   フェールオーバー スクリプト  
  
### <a name="refresh-from-database"></a>データベースから更新します。  
コマンドは、**データベースからの更新**が**レポートでエラーを**パラメーターで、更新操作のエラー レポートの場所を指定します。 次に、名前のファイル**SourceDBRefreshReport&lt;n&gt;します。XML**が指定した場所に作成、 **&lt;n&gt;** は、同じコマンドを実行するたびに 1 桁の数字をインクリメントする一意のファイル数です。  
  
**注:** フォルダーのパスを指定した場合、' レポートでエラーを 'パラメーターは、コマンド' 同期ターゲット ' の省略可能な属性になります。  
  
```  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**オブジェクト名:** 最新の更新 (含めることもできます個々 のオブジェクト名またはグループ オブジェクトの名前) と見なされるオブジェクトを指定します。  
  
**エラー:** 更新エラーを警告またはエラーとして指定するかどうかを指定します。 エラー時の使用可能なオプション:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   フェールオーバー スクリプト  
  
## <a name="see-also"></a>関連項目  
[SSMA コンソール (Oracle) の実行](https://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
