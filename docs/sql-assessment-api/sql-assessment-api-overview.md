---
title: SQL Server Assessment API
description: SQL Server Assessment API の概要について説明します。
ms.prod: sql
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 11/04/2019
ms.openlocfilehash: 0315f181aad5c61b7d9c5fe7d46f3d81b27c9758
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73589136"
---
# <a name="sql-assessment-api"></a>SQL Assessment API

SQL Assessment API には、ベスト プラクティスのために SQL Server の構成を評価するメカニズムが用意されています。 この API は、SQL Server Team が推奨するベスト プラクティス ルールを含むルールセットと共に配布されます。 このルールセットは新しいバージョンのリリースと共に強化されますが、同時に、この API は高いカスタマイズ性と拡張性を備えたソリューションを提供する目的で構築されています。 そのため、ユーザーは既定のルールを調整し、独自のルールを作成できます。

SQL Assessment API は、SQL Server の構成が推奨されるベスト プラクティスに準拠していることを確認する場合に便利です。 初期評価後は、定期的にスケジュールされた評価によって構成の安定性を追跡できます。

この API を使用すると、Azure SQL Database Managed Instance と SQL Server バージョン 2012 以降を評価できます。 Linux 上の SQL がサポートされています。

## <a name="rules"></a>ルール

チェックとも呼ばれるルールは、JSON 形式のファイルで定義されます。 ルールセットの書式では、ルールセットの名前とバージョンを指定する必要があります。 そのため、カスタム ルールセットを使用すると、どのルールセットに由来する推奨事項かを簡単に把握できます。 

Microsoft が配布するルールセットは GitHub で入手できます。 詳細については、[サンプル リポジトリ](https://aka.ms/sql-assessment-api)を参照してください。

## <a name="sql-assessment-cmdlets-and-smo-extension"></a>SQL Assessment コマンドレットと SMO 拡張機能

SQL Assessment API は、[SQL Server 管理オブジェクト (SMO)](../relational-databases/server-management-objects-smo/installing-smo.md) 2019 年 7 月リリース バージョン以降および [SQL Server PowerShell モジュール](../powershell/download-sql-server-ps-module.md) 2019 年 7 月リリース バージョン以降に含まれています。

* [SMO のインストール](../relational-databases/server-management-objects-smo/installing-smo.md)

* [SQL Server PowerShell モジュールのインストール](../powershell/download-sql-server-ps-module.md)

SqlServer モジュールには、SQL Assessment API と連携する 2 つの新しいコマンドレットが追加されました。

* **Get-SqlAssessmentItem** - SQL Server オブジェクトの使用可能な評価チェックの一覧を提供します

* **Invoke-SqlAssessment** - 評価の結果を提供します

SMO Framework は、次のメソッドを備える SQL Assessment API 拡張機能によって補完されています。

* **GetAssessmentItems**  - 特定の SQL オブジェクトの使用可能なチェックを返します (IEnumerable<…>)

* **GetAssessmentResults**  - 同期的に評価を査定し、結果とエラー (ある場合) を返します (IEnumerable<…>)

* **GetAssessmentResultsList**  - 非同期的に評価を査定し、結果とエラー (ある場合) を返します (Task<…>)

## <a name="get-started-using-sql-assessment-cmdlets"></a>SQL Assessment コマンドレットの使用を開始する

選択した SQL Server オブジェクトに対して評価が実行されます。 既定のルールセットでは、2 種類のオブジェクトのみのチェックがあります。サーバーとデータベース (それらに加えて、API ではさらに 2 種類がサポートされます。Filegroup と AvailabilityGroup)。 SQL インスタンスとそのすべてのデータベースを評価する場合は、オブジェクトごとに SQL Assessment コマンドレットを個別に実行する必要があります。 または、変数またはパイプラインで SQL Assessment コマンドレットに評価用のオブジェクトを渡すことができます。

SqlServer オブジェクトと RegisteredServer オブジェクトは交換可能なので、いずれも SQL Assessment コマンドレットに渡すことができます。

以下の例を参照して始めてください。

1. ローカルの既定インスタンスで使用できるチェックの一覧を取得すると、チェックに慣れることができます。 この例では、Get-SqlInstance コマンドレットの出力を Get-SqlAssessmentItem コマンドレットにパイプして、それにインスタンス オブジェクトを渡します。

    ```powershell
    Get-SqlInstance -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

2. インスタンスのすべてのデータベースで使用できるチェックの一覧を取得します。 ここでは、Get-Item コマンドレットと Windows Powershel SQL Server プロバイダーで実装されたパスを使用してデータベースの一覧を取得し、それを Get-SqlDatabase コマンドレットにパイプしています。

    ```powershell
    Get-Item SQLSERVER:\SQL\localhost\default | Get-SqlAssessmentItem
    ```
    
    また、Get-SqlDatabase コマンドレットを使用して同じことを実行できます。

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

3. インスタンスのすべてのデータベースで使用できるチェックの一覧を取得します。 ここでは、Get-Item コマンドレットと Windows Powershel SQL Server プロバイダーで実装されたパスを使用してデータベースの一覧を取得し、それを Get-SqlDatabase コマンドレットにパイプしています。

    ```powershell
    Get-Item SQLSERVER:\SQL\localhost\default | Get-SqlAssessmentItem
    ```
    
    また、Get-SqlDatabase コマンドレットを使用して同じことを実行できます。

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

4. インスタンスの評価を呼び出し、結果を SQL テーブルに保存します。 この例では、Get-SqlInstance コマンドレットの出力を Invoke-SqlAssessment コマンドレットにパイプし、その結果を Write-SqlTableData コマンドレットにパイプします。 この例では、Invoke-Assessment コマンドレットが `-FlattenOutput` パラメーターを使用して実行されることに注意してください。 このパラメーターにより、Write-SqlTableData コマンドレットに適した出力になります。 後者の場合、このパラメーターを省略すると、エラーが発生します。

    ```powershell
    Get-SqlInstance -ServerInstance 'localhost' |
    Invoke-SqlAssessment -FlattenOutput |
    Write-SqlTableData -ServerInstance 'localhost' -DatabaseName SQLAssessmentDemo -SchemaName Assessment -TableName Results -Force
    ```

    次に、インスタンスのすべてのデータベースの評価を呼び出し、同じテーブルに結果を追加しましょう。

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' |
    Invoke-SqlAssessment -FlattenOutput |
    Write-SqlTableData -ServerInstance 'localhost' -DatabaseName SQLAssessmentDemo -SchemaName Assessment -TableName Results -Force
    ```

5. 推奨事項を詳しく理解するには、テーブルの説明とリンクに従います。

6. 環境と組織の要件に基づいてルールをカスタマイズします (以下を参照してください)。

7. 評価を定期的に実行するか、オンデマンドで進行状況を測定するようにタスクまたはジョブをスケジュールします。

## <a name="customizing-rules"></a>ルールのカスタマイズ

ルールは、カスタマイズおよび拡張できるように設計されています。 Microsoft のルールセットは、ほとんどの環境で機能するように設計されています。 ただし、すべての環境で機能する 1 つのルールセットを作成することは不可能です。 ユーザーは、独自の JSON ファイルを作成し、既存のルールをカスタマイズしたり、新しく追加したりすることができます。 カスタマイズの例と Microsoft がリリースした完全なルールセットは、[サンプル リポジトリ](https://aka.ms/sql-assessment-api)で入手できます。 カスタム JSON ファイルを使用して SQL Assessment コマンドレットを実行する方法の詳細については、Get-Help コマンドレットを使用します。

### <a name="options-available-with-rule-customization-feature"></a>ルールのカスタマイズ機能で使用できるオプション

#### <a name="enablingdisabling-certain-rules-or-groups-of-rules-using-tags"></a>特定のルールまたはルールのグループの有効化/無効化 (タグの使用)

実際の環境に該当しない場合、または問題を修正するためのスケジュールされた作業が完了するまで、特定のルールを無効にすることができます。

#### <a name="changing-threshold-parameters"></a>しきい値パラメーターの変更

各ルールにはしきい値があり、メトリックの現在の値と比較して問題が検出されます。 既定のしきい値が適切でない場合は、変更できます。

#### <a name="adding-more-rules-written-by-you-or-third-parties"></a>自分またはサード パーティが作成したルールの追加

SQL Assessment API の呼び出しにパラメーターとして 1 つ以上の JSON ファイルを追加することで、ルールセットをまとめることができます。 このようなファイルは、自分の組織で作成する場合と、サード パーティから取得する場合があります。 たとえば、Microsoft のルールセットの特定のルールを無効にする JSON ファイル、環境に役立つルールを含む業界専門家による別の JSON ファイル、その JSON ファイルのしきい値を変更する別の JSON ファイルがあります。

> [!IMPORTANT]  
>  信頼されていないソースから提供されたルールセットは、安全であることを十分に確認するまで使用しないことをお勧めします。

## <a name="next-steps"></a>次の手順

[SQL Server 管理オブジェクト (SMO)](../relational-databases/server-management-objects-smo/overview-smo.md) と [PowerShell](../powershell/download-sql-server-ps-module.md) に関する記事を参照してください。
