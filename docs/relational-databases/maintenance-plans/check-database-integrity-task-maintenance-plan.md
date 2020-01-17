---
title: データベースの整合性確認タスク (メンテナンス プラン) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.maintplanproperties.integrity.f1
- sql13.swb.maint.integrity.f1
helpviewer_keywords:
- Check Database Integrity Task dialog box
ms.assetid: 3534494a-5dfe-4738-b49a-e7fabd731c47
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 68bdea5d7c63f8d4781dadd8250a14f258c0866f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083924"
---
# <a name="check-database-integrity-task-maintenance-plan"></a>[データベースの整合性確認タスク]\(メンテナンス プラン)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **[データベースの整合性確認タスク]** ダイアログを使用すると、 `DBCC CHECKDB`[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行することにより、ユーザーおよびシステム テーブルの割り当ておよび構造の整合性、データベース内のインデックスを確認できます。 `DBCC` を実行することにより、データベース整合性に問題があった場合にレポートし、システム管理者またはデータベースの所有者によって対処できます。  
  
## <a name="options"></a>オプション  
 **[接続]**  
 このタスクを実行するときに使用するサーバー接続を選択します。  
  
 **[新規作成]**  
 このタスクを実行するときに使用する新しいサーバー接続を作成します。 **[新しい接続]** ダイアログ ボックスについては、後で説明します。  
  
 **データベース**  
 このタスクで操作するデータベースを指定します。  
  
-   **[すべてのデータベース]**  
  
     すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ( **tempdb**を除く) を対象として、メンテナンス タスクを実行するメンテナンス プランを生成します。  
  
-   **[すべてのシステム データベース]**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム データベース ( **tempdb**を除く) を対象として、メンテナンス タスクを実行するメンテナンス プランを生成します。 ユーザーが作成したデータベースではメンテナンス タスクは実行されません。  
  
-   **[すべてのユーザー データベース]**  
  
     ユーザーが作成したすべてのデータベースを対象として、メンテナンス タスクを実行するメンテナンス プランを生成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム データベースではメンテナンス タスクは実行されません。  
  
-   **[これらのデータベース]**  
  
     選択されたデータベースだけを対象として、メンテナンス タスクを実行するメンテナンス プランを生成します。 このオプションをオンにする場合は、少なくとも 1 つのデータベースが一覧内で選択されている必要があります。  
  
    > [!NOTE]  
    >  メンテナンス プランは、互換性レベルが 80 以上に設定されているデータベースに対してのみ実行されます。 互換性レベルが 70 以下に設定されているデータベースは表示されません。  
  
 **[インデックスを含める]**  
 すべてのインデックス ページおよびテーブル データ ページの整合性を確認します。  
  
 **[Physical only] (物理のみ)**  
 ページの物理構造の整合性、レコード ヘッダー、およびデータベースの割り当ての一貫性にチェックを限定します。 このオプションは、大規模なデータベースの DBCC CHECKDB の実行時間を大幅に短縮することがあるため、実稼働システムで頻繁に使用する場合にお勧めします。  
  
 **[Tablock] (Tablock)**  
 DBCC CHECKDB が、内部データベースのスナップショットを使用せずに、ロックを取得します。 これにはデータベースの短期の排他 (X) ロックも含まれます。 このオプションを使用すると、負荷の高いデータベースでの DBCC CHECKDB の実行速度が速くなることがありますが、DBCC CHECKDB の実行中はデータベースでのコンカレンシーが低下します。  
  
 **[T-SQL の表示]**  
 選択したオプションに基づき、このタスクでサーバーに対して実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを表示します。  
  
> [!NOTE]  
>  影響を受けるオブジェクトが大量にある場合は、表示にかなりの時間を要する場合があります。  
  
## <a name="new-connection-dialog-box"></a>[新しい接続] ダイアログ ボックス  
 **[接続名]**  
 新しい接続の名前を入力します。  
  
 **[サーバー名の選択または入力]**  
 このタスクを実行するときに接続するサーバーを選択します。  
  
 **[更新]**  
 使用できるサーバーの一覧を表示します。  
  
 **[サーバーにログオンするための情報の入力]**  
 サーバーの認証情報を指定します。  
  
 **[Windows NT の統合セキュリティを使用する]**  
 Windows 認証を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続します。  
  
 **[特定のユーザー名とパスワードを使用する]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続します。 このオプションは利用できません。  
  
 **User name**  
 認証に使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。 このオプションは利用できません。  
  
 **パスワード**  
 認証に使用するパスワードを指定します。 このオプションは利用できません。  
  
## <a name="see-also"></a>参照  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
  
