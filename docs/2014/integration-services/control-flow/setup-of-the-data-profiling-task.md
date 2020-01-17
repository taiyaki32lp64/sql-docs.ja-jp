---
title: データ プロファイル タスクのセットアップ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], configuring
ms.assetid: fe050ca4-fe45-43d7-afa9-99478041f9a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1d2378426a3cd55b6df183cac7782d63578e2ed0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62830223"
---
# <a name="setup-of-the-data-profiling-task"></a>データ プロファイル タスクのセットアップ
  ソース データのプロファイルを確認する前に、まずデータ プロファイル タスクを設定して実行します。 このタスクは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ内に作成します。 データ プロファイル タスクを構成するには、[データ プロファイル タスク エディター] を使用します。 このエディターを使用すると、プロファイルの出力先と計算するプロファイルを選択できます。 タスクを設定したら、パッケージを実行してデータ プロファイルを計算します。  
  
## <a name="requirements-and-limitations"></a>要件と制限  
 データ プロファイル タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されているデータでのみ機能します。 サードパーティまたはファイル ベースのデータ ソースでは機能しません。  
  
 さらに、データ プロファイル タスクが含まれているパッケージを実行するには、tempdb データベースに対する Read/Write 権限 (CREATE TABLE 権限を含む) があるアカウントを使用する必要があります。  
  
## <a name="data-profiling-task-in-a-package"></a>パッケージのデータ プロファイル タスク  
 データ プロファイル タスクでは、プロファイルの構成と計算済みのプロファイルを含む出力ファイルの作成のみが実行されます。 この出力ファイルを確認するには、スタンドアロンのビューアー プログラムである Data Profile Viewer を使用する必要があります。 出力を個別に表示する必要があるために、他のタスクが含まれていないパッケージでデータ プロファイル タスクを使用する場合があります。  
  
 ただし、パッケージ内の唯一のタスクとしてデータ プロファイル タスクを使用する必要はありません。 より複雑なパッケージのワークフローやデータ フローでデータ プロファイルを実行する必要がある場合は、次のオプションを使用します。  
  
-   タスクの出力ファイルに基づく条件ロジックをパッケージの制御フローに実装するには、データ プロファイル タスクの後にスクリプト タスクを挿入します。 このスクリプト タスクを使用して、出力ファイルに対してクエリを実行できます。  
  
-   データが読み込まれて変換された後にデータ フローでデータをプロファイルするには、変更されたデータを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに一時的に保存する必要があります。 これで、保存したデータをプロファイルすることができます。  
  
 詳細については、「 [パッケージ ワークフローでデータ プロファイル タスクを使用する](incorporate-a-data-profiling-task-in-package-workflow.md)」をご覧ください。  
  
## <a name="setup-of-the-task-output"></a>タスク出力の設定  
 データ プロファイル タスクがパッケージに追加されたら、タスクで計算するプロファイルの出力を設定します。 プロファイルの出力を設定するには、[データ プロファイル タスク エディター] の **[全般]** ページを使用します。 **[全般]** ページでは、出力先の指定以外に、データのクイック プロファイルも実行できます。 **[クイック プロファイル]** を選択すると、データ プロファイル タスクにより、一部またはすべての既定のプロファイルを既定の設定のまま使用してテーブルまたはビューがプロファイルされます。  
  
 詳細については、「[データ プロファイル タスク エディター &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)」および「[単一テーブル クイック プロファイル フォーム &#40;データ プロファイル タスク&#41;](data-profiling-task.md)」をご覧ください。  
  
> [!IMPORTANT]  
>  出力ファイルには、データベースに関する機密データやデータベースに格納されているデータが含まれる場合があります。 このファイルの安全性を高める方法の推奨事項については、「 [パッケージで使用されるファイルへのアクセス](../access-to-files-used-by-packages.md)」をご覧ください。  
  
## <a name="selection-and-configuration-of-the-profiles-to-be-computed"></a>計算するプロファイルの選択と構成  
 出力ファイルを設定したら、計算するデータ プロファイルを選択する必要があります。 データ プロファイル タスクでは、8 つの異なるデータ プロファイルを計算できます。 これらのプロファイルのうち 5 つは個々の列を分析し、残りの 3 つは複数の列または列とテーブル間のリレーションシップを分析します。 単一のデータ プロファイル タスクで、複数のテーブルまたはビューの複数の列または列の組み合わせに対して複数のプロファイルを計算することができます。  
  
 次の表では、各プロファイルで計算されるレポートとプロファイルで有効なデータ型について説明します。  
  
|計算内容|特定できる問題|使用するプロファイル|  
|----------------|-------------------------|----------------------|  
|選択された列に含まれる文字列値の長さごとの、その長さと、テーブル内におけるその長さの行の比率。|**無効な文字列値** - たとえば、米国州コードとして 2 文字を使用する列をプロファイルし、3 文字以上の値を検出できます。|**列長分布-** これらのデータ型のいずれかの列に対して有効です。<br /><br /> 文字データ型 : `char`、`nchar`、`varchar`、および `nvarchar`|  
|文字列型の列に含まれる指定された比率の値に対応する一連の正規表現。<br /><br /> また、新しい値を検証するために将来使用できる正規表現も見つけます。|**無効な文字列値または形式が正しくない文字列値** - たとえば、米国郵便番号列のパターン プロファイルでは、\d{5}-\d{4}、\d{5}、\d{9} という正規表現が生成されます。 出力にその他の正規表現が示された場合、データに無効な値または形式が正しくない値が含まれています。|**列パターン プロファイル-** これらのデータ型のいずれかの列に対して有効です。<br /><br /> 文字データ型 : `char`、`nchar`、`varchar`、および `nvarchar`|  
|選択した列の NULL 値の比率。|**予想外に高い、列の NULL 値の比率** - たとえば、米国郵便番号を想定している列をプロファイルし、許容範囲を超える欠落した郵便番号の比率を検出できます。|**列 Null 比率-** これらのデータ型の列に対して有効です。<br /><br /> 任意のデータ型。 これには、`image`、`text`、`xml`、ユーザー定義型、およびバリアント型が含まれます。|  
|数値型列の最小値、最大値、平均値、標準偏差や、`datetime` 列の最小値、最大値などの統計。|**無効な数値および日付** - たとえば、履歴の日付の列をプロファイルし、将来の日付の最大値を検出できます。|**列統計プロファイル-** これらのデータ型のいずれかの列に対して有効です。<br /><br /> 数値データ型 : 整数型 (`bit` は除く)、`money`、`smallmoney`、`decimal`、`float`、`real`、および `numeric`<br /><br /> 日付および時刻データ型 : `datetime`、`smalldatetime`、`timestamp`、`date`、`time`、`datetime2`、および `datetimeoffset`<br />注:日付と時刻データ型を使用する列の場合、プロファイルでは最小値と最大値だけが計算されます。|  
|選択された列に含まれる値ごとの、その値と、テーブル内におけるその値の行の比率。 または、テーブル内の指定された比率を超えている値。|**列に含まれる個別の値の数が正しくない** - たとえば、米国の州を含む列をプロファイルし、50 個を超える個別の値を検出できます。|**列の値の配布-** これらのデータ型のいずれかの列に対して有効です。<br /><br /> 数値データ型 : 整数型 (`bit` は除く)、`money`、`smallmoney`、`decimal`、`float`、`real`、および `numeric`<br /><br /> 文字データ型 : `char`、`nchar`、`varchar`、および `nvarchar`<br /><br /> 日付および時刻データ型 : `datetime`、`smalldatetime`、`timestamp`、`date`、`time`、`datetime2`、および `datetimeoffset`|  
|列または列のセットが、選択したテーブルのキーまたは近似キーであるかどうか。|**キーとなる可能性がある列の重複値** - たとえば、Customers テーブルの名前列と住所列をプロファイルし、名前と住所の組み合わせは一意である必要があるにもかかわらず重複している値を検出できます。|**候補キー プロファイル** - 列または列のセットが、選択したテーブルのキーとして適しているかどうかを報告する複数列のプロファイルです。 次のいずれかのデータ型の列に対して有効です。<br /><br /> 整数データ型 : `bit`、`tinyint`、`smallint`、`int`、および `bigint`<br /><br /> 文字データ型 : `char`、`nchar`、`varchar`、および `nvarchar`<br /><br /> 日付および時刻データ型 : `datetime`、`smalldatetime`、`timestamp`、`date`、`time`、`datetime2`、および `datetimeoffset`|  
|ある列 (依存列) の値が別の列または列のセット (決定列) の値にどの程度依存しているか。|**依存列に含まれる無効な値** - たとえば、米国郵便番号を含む列と米国の州を含む列の間の依存関係をプロファイルできます。 郵便番号によって州が一意に決定されますが、 このプロファイルでは、この依存関係の違反を検出できます。|**機能の依存関係を**これらのデータ型のいずれかの列に対して有効です。<br /><br /> 整数データ型 : `bit`、`tinyint`、`smallint`、`int`、および `bigint`<br /><br /> 文字データ型 : `char`、`nchar`、`varchar`、および `nvarchar`<br /><br /> 日付および時刻データ型 : `datetime`、`smalldatetime`、`timestamp`、`date`、`time`、`datetime2`、および `datetimeoffset`|  
|列または列のセットが、選択したテーブル間の外部キーとして適しているかどうか。<br /><br /> つまり、このプロファイルは、2 つの列間または列のセット間の値の重複を報告します。|**無効な値** - たとえば、Sales テーブルの ProductID 列をプロファイルするとします。 プロファイルでは、この列に Products テーブルの ProductID 列には存在しない値が含まれていることを検出できます。|**値包含プロファイル** - 次のいずれかのデータ型の列に対して有効です。<br /><br /> 整数データ型 : `bit`、`tinyint`、`smallint`、`int`、および `bigint`<br /><br /> 文字データ型: `char`、 `nchar`、`varchar`と `nvarchar`<br /><br /> 日付および時刻データ型 : `datetime`、`smalldatetime`、`timestamp`、`date`、`time`、`datetime2`、および `datetimeoffset`|  
  
 計算するプロファイルを選択するには、[データ プロファイル タスク エディター] の **[プロファイル要求]** ページを使用します。 詳細については、「[[データ プロファイル タスク エディター] &#40;[プロファイル要求] ページ&#41;](data-profiling-task-editor-profile-requests-page.md)」をご覧ください。  
  
 **[プロファイル要求]** ページでは、データ ソースの指定とデータ プロファイルの構成も行います。 タスクを構成する際は、次の点を考慮してください。  
  
-   構成を容易にし、十分に理解していないデータの特性を検出しやすくするために、個々の列名の代わりにワイルドカード **(\*)** を使用できます。 このワイルドカードを使用すると、タスクによって、適切なデータ型のすべての列をプロファイルするため、処理の速度が低下する場合があります。  
  
-   選択したテーブルまたはビューが空の場合、データ プロファイル タスクではプロファイルが計算されません。  
  
-   選択した列のすべての値が NULL の場合、データ プロファイル タスクでは列の NULL 比プロファイルのみが計算されます。 空の列については列長分布プロファイル、列パターン プロファイル、列統計プロファイル、または列の値分布プロファイルは計算されません。  
  
 利用可能な各データ プロファイルには、独自の構成オプションがあります。 オプションの詳細については、次のトピックを参照してください。  
  
-   [[候補キー プロファイル要求] のオプション (データ プロファイル タスク)](candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [[列長分布プロファイル要求] のオプション (データ プロファイル タスク)](column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [[列の NULL 比プロファイル要求] のオプション (データ プロファイル タスク)](column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [[列パターン プロファイル要求] のオプション (データ プロファイル タスク)](column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [[候補キー プロファイル要求] のオプション (データ プロファイル タスク)](column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [[列の値分布プロファイル要求] のオプション (データ プロファイル タスク)](column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [[機能依存プロファイル要求] のオプション (データ プロファイル タスク)](functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [[値包含プロファイル要求] のオプション &#40;データ プロファイル タスク&#41;](value-inclusion-profile-request-options-data-profiling-task.md)  
  
## <a name="execution-of-the-package-that-contains-the-data-profiling-task"></a>データ プロファイル タスクを含むパッケージの実行  
 データ プロファイル タスクを設定したら、このタスクを実行できるようになります。 実行すると、データ プロファイルが計算され、XML 形式のこの情報がファイルまたはパッケージ変数に出力されます。 この XML の構造は、DataProfile.xsd スキーマに基づきます。 このスキーマは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] やその他のスキーマ エディター、XML エディター、またはメモ帳などのテキスト エディターで開くことができます。 データ品質情報に関するこのスキーマは、次の目的に役立ちます。  
  
-   組織内および組織間でデータ品質情報を交換する。  
  
-   データ品質情報を処理するカスタム ツールを作成する。  
  
 ターゲットの名前空間は、スキーマで [https://schemas.microsoft.com/sqlserver/2008/DataDebugger/](https://schemas.microsoft.com/sqlserver/2008/DataDebugger/) として識別されます。  
  
## <a name="next-step"></a>次の手順  
 [Data Profile Viewer](data-profile-viewer.md).  
  
  
