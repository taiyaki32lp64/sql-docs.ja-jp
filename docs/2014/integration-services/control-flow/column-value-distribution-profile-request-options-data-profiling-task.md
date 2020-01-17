---
title: '[列の値分布プロファイル要求] のオプション (データ プロファイル タスク) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c1e5f5de-04f5-4d00-a9f0-55817186bdf9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5a79ba9f2ff211ed4bf56e749acba7f1d4601643
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832427"
---
# <a name="column-value-distribution-profile-request-options-data-profiling-task"></a>[列の値分布プロファイル要求] のオプション (データ プロファイル タスク)
  **[プロファイル要求]** ページの **[要求プロパティ]** ペインを使用すると、要求ペインで選択した **[列の値分布プロファイル要求]** のオプションを設定できます。 列の値分布プロファイルは、選択された列に含まれるすべての異なる値と、それぞれの値が表す行のテーブル内での比率を報告します。 また、テーブル内の指定された比率を超えている行の値も報告できます。 このプロファイルを使用すると、列に含まれる個別の値の数が正しくないなどのデータの問題を特定できます。 たとえば、米国の州の列をプロファイルし、50 個を超える個別の値を検出できます。  
  
> [!NOTE]  
>  このトピックで説明するオプションは、 **[データ プロファイル タスク エディター]** の **[プロファイル要求]** ページに表示されます。 エディターのこのページの詳細については、「[Data Profiling Task Editor &#40;Profile Requests Page&#41;](data-profiling-task-editor-profile-requests-page.md)」(データ プロファイル タスク エディター &#40;[プロファイル要求] ページ&#41;)を参照してください。  
  
 データ プロファイル タスクの使用方法の詳細については、「[データ プロファイル タスクのセットアップ](data-profiling-task.md)」を参照してください。 Data Profile Viewer を使用してデータ プロファイル タスクの出力を分析する方法の詳細については、「 [Data Profile Viewer (Data Profile Viewer)](data-profile-viewer.md)」を参照してください。  
  
## <a name="request-properties-options"></a>[要求プロパティ] のオプション  
 **[要求プロパティ]** ペインに表示される **[列の値分布プロファイル要求]** のオプション グループは次のとおりです。  
  
-   **[データ]** ( **[TableOrView]** オプション、 **[Column]** オプションなど)  
  
-   **全般**  
  
-   **Options**  
  
### <a name="data-options"></a>[データ] のオプション  
 **[ConnectionManager]**  
 プロファイル対象のテーブルまたはビューを含む [!INCLUDE[vstecado](../../includes/vstecado-md.md)] データベースに接続するには、.NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) を使用する既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続マネージャーを選択します。  
  
 **[TableOrView]**  
 プロファイル対象の列を含む既存のテーブルまたはビューを選択します。  
  
 詳細については、このトピックの「[TableorView] のオプション」を参照してください。  
  
 **[Column]**  
 プロファイル対象の既存の列を選択します。 すべての列をプロファイルするには、 **[(\*)]** を選択します。  
  
 詳細については、このトピックの「[列] のオプション」を参照してください。  
  
#### <a name="tableorview-options"></a>[TableOrView] のオプション  
 **[スキーマ]**  
 選択したテーブルが属するスキーマを指定します。 このオプションは読み取り専用です。  
  
 **Table**  
 選択したテーブルの名前を表示します。 このオプションは読み取り専用です。  
  
#### <a name="column-options"></a>[列] のオプション  
 **IsWildCard**  
 **[(\*)]** ワイルドカードが選択されているかどうかを示します。 **[(\*)]** を選択してすべての列をプロファイルする場合、このオプションは **[True]** に設定されます。 個々の列をプロファイル対象として選択した場合、このオプションは **[False]** になります。 このオプションは読み取り専用です。  
  
 **[ColumnName]**  
 選択した列の名前を表示します。 **[(\*)]** を選択してすべての列をプロファイルする場合、このオプションは空白になります。 このオプションは読み取り専用です。  
  
 **[StringCompareOptions]**  
 文字列値を比較するためのオプションを選択します。 このプロパティのオプションを次の表に示します。 このオプションの既定値は **[Default]** です。  
  
> [!NOTE]  
>  **[ColumnName]** に **[(\*)]** ワイルドカードを使用する場合、 **[CompareOptions]** は読み取り専用で、 **[Default]** に設定されます。  
  
|値|説明|  
|-----------|-----------------|  
|**[Default]**|ソース テーブル内の列の照合順序に基づいてデータを並べ替えて比較します。|  
|**[BinarySort]**|文字ごとに定義されているビット パターンに基づいてデータを並べ替えて比較します。 バイナリ並べ替え順では、大文字と小文字が区別され、アクセントが区別されます。 また、バイナリは最速の並べ替え順です。|  
|**[DictionarySort]**|関連する言語またはアルファベットの辞書で定義されている並べ替えおよび比較ルールに基づいてデータを並べ替えて比較します。|  
  
 **[DictionarySort]** を選択した場合は、次の表に示すオプションの任意の組み合わせも選択できます。 既定では、これらの追加オプションは選択されていません。  
  
|値|説明|  
|-----------|-----------------|  
|**IgnoreCase**|比較時に、大文字と小文字を区別するかどうかを示します。 このオプションを設定した場合、文字列比較で大文字と小文字は区別されません。 たとえば、"ABC" は "abc" と同一になります。|  
|**IgnoreNonSpace**|比較で、通常の文字と分音文字付きの文字を区別するかどうかを指定します。 このオプションを設定した場合、比較で分音文字は無視されます。 たとえば、"&#xE5;" は "a" と同じ文字になります。|  
|**IgnoreKanaType**|日本語の比較で、2 種類のかな文字である、ひらがなとカタカナを区別するかどうかを指定します。 このオプションを設定した場合、文字列比較でひらがなとカタカナは区別されません。|  
|**IgnoreWidth**|比較で、1 バイト文字と、それと同じ文字を表記した 2 バイト文字を区別するかどうかを指定します。 このオプションを設定した場合、文字列比較で 1 バイト表記と 2 バイト表記は同一文字として扱われます。|  
  
### <a name="general-options"></a>[全般] のオプション  
 **RequestID**  
 このプロファイル要求を識別するわかりやすい名前を入力します。 通常、自動生成された値を変更する必要はありません。  
  
### <a name="options"></a>および  
 **[ValueDistributionOption]**  
 すべての列の値の分布を計算するかどうかを指定します。 このオプションの既定値は **[FrequentValues]** です。  
  
|値|説明|  
|-----------|-----------------|  
|**[AllValues]**|すべての列の値の分布が計算されます。|  
|**[FrequentValues]**|**[FrequentValueThreshold]** で指定した最小値を頻繁に超える値の分布のみが計算されます。 **[FrequentValueThreshold]** を満たさない値は出力レポートから除外されます。|  
  
 **[FrequentValueThreshold]**  
 0 ～ 1 の値を使用して、列の値が報告されるしきい値を指定します。 **[ValueDistributionOption]** で **[AllValues]** を選択した場合、このオプションは無効になります。 このオプションの既定値は 0.001 です。  
  
## <a name="see-also"></a>関連項目  
 [データ プロファイル タスク エディター ([全般] ページ)](../general-page-of-integration-services-designers-options.md)   
 [単一テーブル クイック プロファイル フォーム (データ プロファイル タスク)](single-table-quick-profile-form-data-profiling-task.md)  
  
  
