---
title: Azure Data Lake Analytics タスク | Microsoft Docs
description: Data Lake Analytics タスクを使用して、U-SQL ジョブを Azure Data Lake Analytics サービスに送信できます。
ms.custom: ''
ms.date: 06/27/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: yanancai
ms.author: yanacai
ms.openlocfilehash: ab9a357e8215310b21fa2e401067f49176aeefd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947356"
---
# <a name="azure-data-lake-analytics-task"></a>Azure Data Lake Analytics タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Data Lake Analytics タスクを使用して、U-SQL ジョブを Azure Data Lake Analytics サービスに送信できます。 このタスクは、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。

一般的な背景については、[「Azure Data Lake Analytics」](https://azure.microsoft.com/services/data-lake-analytics/)をご覧ください。

## <a name="configure-the-task"></a>タスクの構成

パッケージに Data Lake Analytics タスクを追加するには、タスクを SSIS ツールボックスからデザイナー キャンバスにドラッグします。 次に、タスクをダブルクリックするか、タスクを右クリックして **[編集]** を選択します。 **[Azure Data Lake Analytics Task Editor]\(Azure Data Lake Analytics タスク エディター\)** ダイアログ ボックスが開きます。 プロパティは、SSIS デザイナーを使用して、またはプログラムによって設定できます。

## <a name="general-page-configuration"></a>全般ページの構成

**[全般]** ページを使ってタスクを構成し、タスクが送信する U-SQL スクリプトを指定します。 U-SQL 言語について詳しくは、[U-SQL 言語のリファレンス](/u-sql/)をご覧ください。

### <a name="basic-configuration"></a>[基本構成]

タスクの名前と説明を指定できます。

### <a name="u-sql-configuration"></a>U-SQL の構成

U-SQL の構成には、**SourceType** と、**SourceType** の値に基づく動的なオプションの、2 つの設定があります。 

**SourceType** は U-SQL スクリプトのソースを指定します。 スクリプトは、SSIS パッケージの実行中に、Data Lake Analytics アカウントに送信されます。 このプロパティのオプションは次のとおりです。

|[値]|[説明]|  
|-----------|-----------------|  
|**DirectInput (直接入力)**|インライン エディターを使用して U-SQL スクリプトを指定します。 この値を選択すると、動的オプション **[USQLStatement]** が表示されます。|  
|**[FileConnection]**|U-SQL スクリプトを含むローカルな .usql ファイルを指定します。 この値を選択すると、動的オプション **[FileConnection]** が表示されます。|  
|**変数**|U-SQL スクリプトを含む SSIS 変数を指定します。 この値を選択すると、動的オプション **[SourceVariable]** が表示されます。|

**SourceType 動的オプション**では、U-SQL クエリのスクリプトの内容を指定します。 

|[SourceType]|動的オプション|  
|-----------|-----------------|  
|**SourceType = DirectInput**|送信する U-SQL クエリを、オプション ボックスに直接入力します。または、参照ボタン [...] をクリックし、 **[Enter U-SQL Query]\(U-SQL クエリの入力\)** ダイアログ ボックスで U-SQL クエリを入力します。|  
|**SourceType = FileConnection**|既存のファイル接続マネージャーを選択するか、<**新しい接続…** > を選択して新しいファイル接続を作成します。 関連情報については、「[ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)」と「[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)」をご覧ください。|  
|**SourceType = Variable**|既存の変数を選択するか、\<**新しい変数...** > を選択して新しい変数を作成します。 関連情報については、「[Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」と「[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)」をご覧ください。|


### <a name="job-configuration"></a>ジョブの構成
ジョブの構成では、U-SQL ジョブの送信のプロパティを指定します。

- **AzureDataLakeAnalyticsConnection:** U-SQL スクリプト送信先の Data Lake Analytics アカウントを指定します。 定義済みの接続マネージャーの一覧から接続を選択します。 新しい接続を作成するには、<**新しい接続**> を選択します。 関連情報については、「[Azure Data Lake Analytics 接続マネージャー](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)」をご覧ください。

- **JobName:** U-SQL ジョブの名前を指定します。 
- **AnalyticsUnits:** U-SQL ジョブの分析ユニット数を指定します。
- **Priority:** U-SQL ジョブの優先順位を指定します。 これは 0 から 1000 までの値に設定できます。 数値が小さいほど、優先順位は高くなります。
- **RuntimeVersion:** U-SQL ジョブの Data Lake Analytics ランタイム バージョンを指定します。 既定では、"default" に設定されます。 通常、このプロパティを変更する必要はありません。
- **Synchronous:** このブール値では、タスクがジョブの実行の完了を待つかどうかを指定します。 値を true に設定する場合、タスクはジョブの完了後に**成功**とマークされます。 値を false に設定する場合、タスクはジョブが準備フェーズを通過した後に**成功**とマークされます。

  |[値]|[説明]|
  |-----------|-----------------|
  |True|タスクの結果は、U-SQL ジョブの実行結果に基づきます。 ジョブの成功 > タスクの成功。 ジョブの失敗 > タスクの失敗。 タスクの成功または失敗 > タスクの完了。|
  |False|タスクの結果は、U-SQL ジョブの送信と準備の結果に基づきます。 ジョブの送信に成功し、準備フェーズを通過した > タスクの成功。 ジョブの送信に失敗、または準備フェーズでジョブが失敗した > タスクの失敗。 タスクの成功または失敗 > タスクの完了。|

- **TimeOut:** ジョブ実行のタイムアウト時間を秒単位で指定します。 タイムアウトしたジョブはキャンセルされ、失敗としてマークされます。 **Synchronous** が false に設定されている場合、このプロパティは使用できません。

## <a name="parameter-mapping-page-configuration"></a>パラメーター マッピング ページの構成

**[Azure Data Lake Analytics Task Editor]\(Azure Data Lake Analytics タスク エディター\)** ダイアログ ボックスの **[パラメーター マッピング]** ページを使用して、U-SQL スクリプトのパラメーター (U-SQL 変数) に変数をマップします。

- **[変数名]:** **[追加]** を選択してパラメーター マッピングを追加したら、システム変数またはユーザー定義の変数を一覧から選択します。 または、<**新しい変数...** > を選択して、 **[変数の追加]** ダイアログ ボックスを使用して新しい変数を追加できます。 関連情報については、「[Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」をご覧ください。  

- **[パラメーター名]:** U-SQL スクリプトのパラメーター/変数名を指定します。 パラメーター名が \@ 記号で始まっていることを確認します (例: \@Param1)。 

U-SQL スクリプトにパラメーターを渡す方法の例を次に示します。

**U-SQL スクリプトのサンプル**
```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

入力と出力のパスは **\@in** および **\@out** パラメーターで定義されています。 U-SQL スクリプトの **\@in** および **\@out** パラメーターの値は、パラメーター マッピングの構成に従って動的に渡されます。

|[変数名]|[パラメーター名]|
|-------------|--------------|
|ユーザー :Variable1|\@in|
|ユーザー :Variable2|\@out| 

## <a name="expression-page-configuration"></a>式ページの構成

[全般] ページの構成のすべてのプロパティをプロパティ式として割り当てて、実行時のプロパティの動的な更新を有効にできます。 関連情報については、「[パッケージでプロパティ式を使用する](../../integration-services/expressions/use-property-expressions-in-packages.md)」をご覧ください。

## <a name="see-also"></a>参照
- [Azure Data Lake Analytics 接続マネージャー](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)
- [Azure Data Lake Store ファイル システム タスク](../../integration-services/control-flow/azure-data-lake-store-file-system-task.md)
- [Azure Data Lake Store 接続マネージャー](../../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)

