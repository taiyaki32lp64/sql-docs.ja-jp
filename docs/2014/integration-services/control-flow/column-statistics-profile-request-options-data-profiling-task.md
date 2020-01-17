---
title: '[列統計プロファイル要求] のオプション (データ プロファイル タスク) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 87205984-507a-49f3-b27c-36a0075c234d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e07bd6ead9ce0dfc20249f5db50a8b0b78ba242a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832769"
---
# <a name="column-statistics-profile-request-options-data-profiling-task"></a>[列統計プロファイル要求] のオプション (データ プロファイル タスク)
  **[プロファイル要求]** ページの **[要求プロパティ]** ペインを使用すると、要求ペインで選択した **[列統計プロファイル要求]** のオプションを設定できます。 列統計プロファイルは、最小、最大、平均値、および数値の列、および最低限の標準偏差、最大などの統計を報告`datetime`列。 このプロファイルを使用すると、無効な日付などのデータの問題を特定できます。 たとえば、履歴の日付の列をプロファイルし、将来の日付の最大値を検出できます。  
  
> [!NOTE]  
>  このトピックで説明するオプションは、 **[データ プロファイル タスク エディター]** の **[プロファイル要求]** ページに表示されます。 エディターのこのページの詳細については、「[Data Profiling Task Editor &#40;Profile Requests Page&#41;](data-profiling-task-editor-profile-requests-page.md)」(データ プロファイル タスク エディター &#40;[プロファイル要求] ページ&#41;)を参照してください。  
  
 データ プロファイル タスクの使用方法の詳細については、「[データ プロファイル タスクのセットアップ](data-profiling-task.md)」を参照してください。 Data Profile Viewer を使用してデータ プロファイル タスクの出力を分析する方法の詳細については、「 [Data Profile Viewer (Data Profile Viewer)](data-profile-viewer.md)」を参照してください。  
  
## <a name="request-properties-options"></a>[要求プロパティ] のオプション  
 **[要求プロパティ]** ペインに表示される **[列統計プロファイル要求]** のオプション グループは次のとおりです。  
  
-   **[データ]** ( **[TableOrView]** オプション、 **[Column]** オプションなど)  
  
-   **全般**  
  
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
 このオプションは、列統計プロファイルには適用されません。  
  
### <a name="general-options"></a>[全般] のオプション  
 **RequestID**  
 このプロファイル要求を識別するわかりやすい名前を入力します。 通常、自動生成された値を変更する必要はありません。  
  
## <a name="see-also"></a>参照  
 [データ プロファイル タスク エディター ([全般] ページ)](../general-page-of-integration-services-designers-options.md)   
 [単一テーブル クイック プロファイル フォーム (データ プロファイル タスク)](single-table-quick-profile-form-data-profiling-task.md)  
  
  
