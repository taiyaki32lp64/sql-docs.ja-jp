---
title: レポート (MySQLToSQL) の生成 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Generating reports
ms.assetid: 1c0202e8-546d-4cb3-a37f-1d2e35d53839
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a5b94ef545285cd7dfa4597820da00552b9f3930
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103010"
---
# <a name="generating-reports-mysqltosql"></a>レポートの生成 (MySQLToSQL)
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
  
    コマンド オプションの出力からのレポート (上記の Sl. No. 2 ~ 4) を参照してください、 [SSMA コンソールを実行する&#40;MySQLToSQL&#41; ](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)セクションです。  
  
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
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-type>"  
  
   verbose="<true/false>"  
  
   report-erors="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   assessment-report-folder="<folder-name>"  
  
   assessment-report-overwrite="<true/false>"  
  
/>  
```  
  
### <a name="synchronize-target"></a>同期ターゲット:  
コマンドは、**同期ターゲット**が**レポートでエラーを**パラメーターで、同期操作のエラー レポートの場所を指定します。 次に、名前のファイル**TargetSynchronizationReport&lt;n&gt;します。XML**が指定した場所に作成、 **&lt;n&gt;** は、同じコマンドを実行するたびに 1 桁の数字をインクリメントする一意のファイル数です。  
  
**注:** フォルダーのパスを指定した場合、' レポートでエラーを 'パラメーターは、コマンド' 同期ターゲット ' の省略可能な属性になります。  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/report-each-as-warning/fail-script>"  
  
   report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**オブジェクト名:** 同期 (含めることもできます個々 のオブジェクト名またはグループ オブジェクトの名前) と見なされるオブジェクトを指定します。  
  
**エラー:** 同期エラーを警告またはエラーとして指定するかどうかを指定します。 エラー時の使用可能なオプション:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   フェールオーバー スクリプト  
  
### <a name="refresh-from-database"></a>データベースから更新します。  
コマンドは、**データベースからの更新**が**レポートでエラーを**パラメーターで、更新操作のエラー レポートの場所を指定します。 次に、名前のファイル**SourceDBRefreshReport&lt;n&gt;します。XML**が指定した場所に作成、 **&lt;n&gt;** は、同じコマンドを実行するたびに 1 桁の数字をインクリメントする一意のファイル数です。  
  
**注:** フォルダーのパスを指定した場合、' レポートでエラーを 'パラメーターは、コマンド' 同期ターゲット ' の省略可能な属性になります。  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="<report-total-as-warning/report-each-as-warning/fail-script>"  
  
   report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**オブジェクト名:** 最新の更新 (含めることもできます個々 のオブジェクト名またはグループ オブジェクトの名前) と見なされるオブジェクトを指定します。  
  
**エラー:** 更新エラーを警告またはエラーとして指定するかどうかを指定します。 エラー時の使用可能なオプション:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   フェールオーバー スクリプト  
  
## <a name="see-also"></a>関連項目  
[SSMA コンソール (MySQL) の実行](https://msdn.microsoft.com/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
