---
title: データの一括インポートの準備 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], about bulk importing
- BULK INSERT statement, guidelines
- BULK INSERT statement, restrictions
- bcp utility [SQL Server], guidelines
- bcp utility [SQL Server], restrictions
- hidden characters
- OPENROWSET function, BCP guidelines
ms.assetid: a82ef43c-d006-4c71-bfca-f001a3ba1ba0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 95deda34b673161bf63c29a912564f39425583a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011863"
---
# <a name="prepare-to-bulk-import-data-sql-server"></a>データの一括インポートの準備 (SQL Server)
  データ ファイルのみからデータを一括インポートするには、 **bcp** コマンド、BULK INSERT ステートメント、または OPENROWSET(BULK) 関数を使用します。  
  
> [!NOTE]  
>  テキスト ファイル以外のオブジェクトからデータを一括インポートするカスタム アプリケーションを記述することもできます。 メモリ バッファーからデータを一括インポートするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (ODBC) アプリケーション プログラミング インターフェイス (API) または OLE DB **IRowsetFastLoad** インターフェイスのいずれかの bcp 拡張機能を使用します。  C# のデータ テーブルからデータを一括インポートするには、ADO.NET 一括コピー API ( **SqlBulkCopy**) を使用します。  
  
> [!NOTE]  
>  リモート テーブルへのデータの一括インポートはサポートされていません。  
  
 データ ファイルから [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスにデータを一括インポートするときは、次のガイドラインに従ってください:  
  
-   使用しているユーザー アカウントに必要な権限を取得する。  
  
     **bcp** ユーティリティ、BULK INSERT ステートメント、INSERT ...SELECT * FROM OPENROWSET(BULK...) ステートメントのいずれかで使用するユーザー アカウントには、テーブル操作に必要な権限がテーブルの所有者によって割り当てられている必要があります。 各方法に必要な権限の詳細については、「[bcp ユーティリティ](../../tools/bcp-utility.md)」、「[OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)」、および「[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)」を参照してください。  
  
-   一括ログ復旧モデルを使用する。  
  
     このガイドラインは、完全復旧モデルを使用するデータベースに関するものです。 一括ログ復旧モデルは、インデックスなしテーブル ( *ヒープ*) に対して一括操作を実行する場合に便利です。 一括ログ復旧では行の挿入がログに記録されないため、一括ログ復旧モデルを使用することで、トランザクション ログの領域が不足する状況を回避できます。 一括ログ復旧モデルの詳細については、「[復旧モデル &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)」を参照してください。  
  
     一括インポート操作の直前に一括ログ復旧モデルが使用されるようにデータベースを変更することをお勧めします。 一括インポート操作が終了したらすぐに、データベースを完全復旧モデルに戻します。 詳細については、「[データベースの復旧モデルの表示または変更 &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)」を参照してください。  
  
    > [!NOTE]  
    >  一括インポート操作時のログ記録を最小限にする方法の詳細については、「[一括インポートで最小ログ記録を行うための前提条件](prerequisites-for-minimal-logging-in-bulk-import.md)」を参照してください。  
  
-   データの一括インポート後にバックアップを行う。  
  
     単純復旧モデルを使用するデータベースの場合は、一括インポート操作後に完全バックアップまたは差分バックアップを行うことをお勧めします。 詳細については、「[データベースの完全バックアップの作成 &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md)」または「[データベースの差分バックアップの作成 &#40;SQL Server&#41;](../backup-restore/create-a-differential-database-backup-sql-server.md)」を参照してください。  
  
     一括ログ復旧モデルまたは完全復旧モデルの場合、ログ バックアップで十分です。 詳細については、「[トランザクション ログ バックアップ &#40;SQL Server&#41;](../backup-restore/transaction-log-backups-sql-server.md)」を参照してください。  
  
-   大量一括インポートのパフォーマンスを向上するために、テーブル インデックスを削除する。  
  
     このガイドラインは、テーブル内の既存のデータ量に比べて大量のデータをインポートするときに関するものです。 この場合、一括インポート操作を実行する前にテーブルからインデックスを削除すると、パフォーマンスが大幅に向上します。  
  
    > [!NOTE]  
    >  テーブル内の既存のデータ量に比べて少量のデータを読み込む場合は、インデックスを削除すると逆効果です。 インデックスの再構築に必要な時間が、一括インポート操作で節約される時間よりも長くなることがあります。  
  
-   データ ファイルにある隠し文字を検索して取り除く。  
  
     多くのユーティリティやテキスト エディターで隠し文字を表示できます。隠し文字は、通常データ ファイルの末尾にあります。 一括インポート操作のとき、ASCII データ ファイルに隠し文字があると、"予期しない NULL が見つかりました" というエラーが発生することがあります。 隠し文字をすべて検索して削除することにより、この問題を回避することができます。  
  
## <a name="see-also"></a>参照  
 [bcp ユーティリティを使用した一括データのインポートとエクスポート &#40;SQL Server&#41;](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)   
 [BULK INSERT または OPENROWSET#40;BULK...&#41; を使用した一括データのインポート #40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [bcp ユーティリティ](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [一括インポートまたは一括エクスポートのデータ形式 &#40;SQL Server&#41;](data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
