---
title: '[インデックスの再構築タスク] (メンテナンス プラン) | Microsoft Docs'
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.reindex.f1
- reindex
helpviewer_keywords:
- Rebuild Index Task dialog box
ms.assetid: 33e2940b-139f-4563-b0cb-5683f08bd879
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34bd5a607998c6e37f688ccbadcd4d612d3daea7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807037"
---
# <a name="rebuild-index-task-maintenance-plan"></a>[インデックスの再構築タスク]\(メンテナンス プラン)
  **[インデックスの再構築タスク]** ダイアログ ボックスを使用すると、データベースのテーブルに新しい FILL FACTOR でインデックスを再作成できます。 FILL FACTOR は、後で拡張できるように、インデックスの各ページの空き領域の量を決定します。 FILL FACTOR が適用されるのはインデックスの作成時だけであるため、テーブルにデータが追加されるにつれて、各ページの空き容量は徐々に減少します。 データ ページおよびインデックス ページを再編成すると、再び空き領域を確保できます。  
  
 **[インデックスの再構築タスク]** では、ALTER INDEX ステートメントが使用されます。  
  
## <a name="options"></a>および  
 **Connection**  
 このタスクを実行するときに使用するサーバー接続を選択します。  
  
 **[新規作成]**  
 このタスクを実行するときに使用する新しいサーバー接続を作成します。 **[新しい接続]** ダイアログ ボックスについては、後で説明します。  
  
 **データベース**  
 このタスクで操作するデータベースを指定します。  
  
-   **[すべてのデータベース]**  
  
     すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース (tempdb を除く) を対象として、メンテナンス タスクを実行するメンテナンス プランを生成します。  
  
-   **[すべてのシステム データベース]**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム データベース (tempdb を除く) を対象として、メンテナンス タスクを実行するメンテナンス プランを生成します。 ユーザーが作成したデータベースではメンテナンス タスクは実行されません。  
  
-   **[すべてのユーザー データベース]**  
  
     ユーザーが作成したすべてのデータベースを対象として、メンテナンス タスクを実行するメンテナンス プランを生成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム データベースではメンテナンス タスクは実行されません。  
  
-   **[これらのデータベース]**  
  
     選択されたデータベースだけを対象として、メンテナンス タスクを実行するメンテナンス プランを生成します。 このオプションをオンにする場合は、少なくとも 1 つのデータベースが一覧内で選択されている必要があります。  
  
    > [!NOTE]  
    >  メンテナンス プランは、互換性レベルが 80 以上に設定されているデータベースに対してのみ実行されます。 互換性レベルが 70 以下に設定されているデータベースは表示されません。  
  
 **オブジェクト**  
 **[選択]** グリッドでテーブル、ビュー、または両方を表示するように制限します。  
  
 **[選択]**  
 このタスクの対象とするテーブルまたはインデックスを指定します。 [オブジェクト] ボックスで **[テーブルとビュー]** が選択されている場合は、このオプションは利用できません。  
  
 **空き領域量が既定のページを再構成します。**  
 データベース内のテーブルに定義されているインデックスを削除し、インデックスの作成時に指定された FILL FACTOR を使用して、新しいインデックスを再作成します。  
  
 **ページの割合をごとの空き領域を変更します。**  
 データベース内のテーブルに定義されているインデックスを削除し、指定した割合の空き領域が各インデックス ページに確保されるように自動的に計算される FILL FACTOR の値を使用してインデックスを再作成します。 指定するパーセント値を大きくすると、インデックス ページに確保される空き領域が増えて、より多くのデータをインデックスに追加できるようになります。 有効値は、0 ～ 100 です。  
  
 **[tempdb の結果を並べ替える]**  
 使用して、`SORT_IN_TEMPDB`オプションは、インデックスの作成中に生成された中間の並べ替え結果が一時的に格納場所が決まります。 並べ替え操作が必要ない場合、または並べ替えをメモリ上で実行できる場合、 `SORT_IN_TEMPDB`オプションは無視されます。  
  
 **インデックスの再作成中にオンラインのインデックスを保持します。**  
 `ONLINE` オプションを使用すると、インデックス操作の実行中に、ユーザーは基になるテーブルまたはクラスター化インデックス データ、および任意の関連付けられた非クラスター化インデックスにアクセスできます。  
  
> [!NOTE]  
>  オンラインでのインデックス操作は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
 **[T-SQL の表示]**  
 選択したオプションに基づき、このタスクでサーバーに対して実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを表示します。  
  
> [!NOTE]  
>  影響を受けるオブジェクトが大量にある場合は、表示にかなりの時間を要する場合があります。  
  
## <a name="new-connection-dialog-box"></a>[新しい接続] ダイアログ ボックス  
 **[接続名]**  
 新しい接続の名前を入力します。  
  
 **[サーバー名の選択または入力]**  
 このタスクを実行するときに接続するサーバーを選択します。  
  
 **更新**  
 使用できるサーバーの一覧を表示します。  
  
 **[サーバーにログオンするための情報の入力]**  
 サーバーの認証情報を指定します。  
  
 **[Windows NT の統合セキュリティを使用する]**  
 Windows 認証を使用して [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続します。  
  
 **[特定のユーザー名とパスワードを使用する]**  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 認証を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続します。 このオプションは利用できません。  
  
 **ユーザー名**  
 認証に使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。 このオプションは利用できません。  
  
 **Password**  
 認証に使用するパスワードを指定します。 このオプションは利用できません。  
  
## <a name="see-also"></a>関連項目  
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [インデックスの SORT_IN_TEMPDB オプション](../indexes/indexes.md)   
 [オンライン インデックス操作のガイドライン](../indexes/guidelines-for-online-index-operations.md)   
 [オンライン インデックス操作の動作原理](../indexes/how-online-index-operations-work.md)   
 [オンラインでのインデックス操作の実行](../indexes/perform-index-operations-online.md)  
  
  
