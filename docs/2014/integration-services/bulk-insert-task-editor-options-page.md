---
title: 一括挿入タスク エディター ([オプション] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.options.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: b3702811-3eb8-4b28-9190-5ae7a1a7bb6f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e7cb19e3ba2f58a39ffd87bdabc6eb1ad18a1d18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061188"
---
# <a name="bulk-insert-task-editor-options-page"></a>[一括挿入タスク エディター] ([オプション] ページ)
  **[一括挿入タスク エディター]** ダイアログ ボックスの **[オプション]** ページを使用すると、一括挿入操作のプロパティを設定できます。 一括挿入タスクにより、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のテーブルまたはビューに大量のデータがコピーされます。  
  
 一括挿入タスクについては、「[一括挿入タスク](control-flow/bulk-insert-task.md)」および「[「BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)」を参照してください。  
  
## <a name="options"></a>および  
 **CodePage**  
 データ ファイル内のデータのコード ページを指定します。  
  
 **[DataFileType]**  
 読み込み操作で使用するデータ型の値を指定します。  
  
 **BatchSize**  
 バッチ内の行数を指定します。 既定では、データ ファイル全体です。 **[BatchSize]** を 0 に設定すると、データは単一のバッチに読み込まれます。  
  
 **[LastRow]**  
 コピーする最後の行を指定します。  
  
 **[FirstRow]**  
 コピーを開始する最初の行を指定します。  
  
 **[一括挿入タスク エディター]**  
 |項目|定義|  
|----------|----------------|  
|**CHECK 制約**|テーブルおよび列に対する制約をチェックします。|  
|**[NULL を保持する]**|空の列に任意の既定値を挿入する代わりに、一括挿入操作中に NULL 値を保持します。|  
|**[ID 挿入を許可する]**|ID 列に既存の値を挿入します。|  
|**[テーブル ロック]**|一括挿入中にテーブルをロックします。|  
|**[トリガーを起動する]**|テーブル上のすべての挿入トリガー、更新トリガー、および削除トリガーを起動します。|  
  
 **SortedData**  
 一括挿入ステートメントに ORDER BY 句を指定します。 指定する列名は、挿入先テーブル内の有効な列でなければなりません。 既定値は `false` です。 これは、データが ORDER BY 句によって並べ替えられないことを意味します。  
  
 **[MaxErrors]**  
 一括挿入操作が取り消されるまでに発生が許可される最大エラー数を指定します。 0 の値は、許可されるエラー数が無制限であることを示します。  
  
> [!NOTE]  
>  一括読み込み操作でインポートできない行は、1 つのエラーとしてカウントされます。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [一括挿入タスク エディター &#40;[全般] ページ&#41;](general-page-of-integration-services-designers-options.md)   
 [一括挿入タスク エディター &#40;[接続] ページ&#41;](../../2014/integration-services/bulk-insert-task-editor-connection-page.md)   
 [[式] ページ](expressions/expressions-page.md)   
 [制御フロー](control-flow/control-flow.md)  
  
  
