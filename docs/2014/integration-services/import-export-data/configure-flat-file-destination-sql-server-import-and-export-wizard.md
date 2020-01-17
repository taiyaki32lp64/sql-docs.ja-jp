---
title: フラット ファイルの変換先の構成 (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6504e4f5eee83d670b4843fb8d956b23a84d4aad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62893033"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>[フラット ファイルの変換先の構成] (SQL Server インポートおよびエクスポート ウィザード)
  使用して、**フラット ファイル変換先の構成**ページで、変換先のフラット ファイルの書式設定オプションを指定し、続行する前に結果をプレビューします。  
  
 このウィザードの詳細については、次を参照してください。 [SQL Server インポートおよびエクスポート ウィザード](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)します。 ウィザードを正常に実行するために必要なアクセス許可と同様に、ウィザードを開始するためのオプションについては、次を参照してください。 [、SQL Server インポートおよびエクスポート ウィザードを実行](start-the-sql-server-import-and-export-wizard.md)します。  
  
 SQL Server インポートおよびエクスポート ウィザードの目的は、変換元から変換先にデータをコピーすることです。 また、このウィザードでは、変換先データベースと変換先テーブルも作成できます。 ただし、複数のデータベースやテーブルまたは他の種類のデータベース オブジェクトをコピーする必要がある場合は、データベース コピー ウィザードを使用してください。 詳細については、「 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)」を参照してください。  
  
## <a name="options"></a>および  
 **変換元フラット ファイル**  
 変換先ファイルの名前です。  
  
 **[行区切り記号]**  
 行の区切り記号の一覧から選択します。  
  
|値|説明|  
|-----------|-----------------|  
|**{CR}{LF}**|行は、復帰と改行の組み合わせで区切られます。|  
|**{CR}**|行は、復帰で区切られます。|  
|**{LF}**|行は、改行で区切られます。|  
|**[セミコロン {;}]**|行は、セミコロンで区切られます。|  
|**[コロン {:}]**|行は、コロンで区切られます。|  
|**[コンマ {,}]**|行は、コンマで区切られます。|  
|**[タブ {t}]**|行は、タブで区切られます。|  
|**[縦棒 {&#124;}]**|行は、縦棒で区切られます。|  
  
 **列区切り記号**  
 列の区切り記号の一覧から選択します。  
  
|値|説明|  
|-----------|-----------------|  
|**{CR}{LF}**|列は、キャリッジ リターン-ライン フィードの組み合わせで区切られます。|  
|**{CR}**|列は、復帰で区切られます。|  
|**{LF}**|列は、改行で区切られます。|  
|**[セミコロン {;}]**|列は、セミコロンで区切られます。|  
|**[コロン {:}]**|列は、コロンで区切られます。|  
|**[コンマ {,}]**|列はコンマで区切られます。|  
|**[タブ {t}]**|列は、タブで区切られます。|  
|**[縦棒 {&#124;}]**|列は、縦棒で区切られます。|  
  
 **プレビュー**  
 表示、**データのプレビュー**選択した形式の結果が変換先フラット ファイルのオプション ダイアログ ボックス。  
  
 **変換を編集します。**  
 行を削除、行を追加し、変換先ファイルを使用して列を構成、**列マッピング** ダイアログ ボックス。  
  
  
