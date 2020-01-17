---
title: '[統計の更新タスク] (メンテナンス プラン) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.statistics.f1
helpviewer_keywords:
- Updates Statistics Task dialog box
ms.assetid: 22902fd0-eb39-4f18-af94-3fcb69d2a3a4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d63b9d5d864dc9027eaf6b19a4e4964895699feb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115511"
---
# <a name="update-statistics-task-maintenance-plan"></a>[統計の更新タスク] \(メンテナンス プラン)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[統計の更新タスク]** ダイアログ ボックスを使用して、テーブルおよびインデックスのデータに関する [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 情報を更新します。 このタスクでは、データベース内のユーザー テーブルに定義されている各インデックスの分布統計のサンプル データを取り直します。 分布統計は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを処理する際のテーブル内の移動の最適化に使用されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、分布統計を自動的に作成するために、各インデックスに対応するテーブルのデータを定期的にサンプリングしています。 サンプリングするサイズは、テーブルに含まれる行数とデータ更新の頻度に基づいて決められます。 このオプションを使用すると、サンプリングされるテーブル データの比率を指定して、サンプリングを追加実行することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、この情報を使用してより適切なクエリ プランを作成します。  
  
このタスクで `UPDATE STATISTICS` ステートメントが実行されます。  
  
## <a name="options"></a>オプション  
 **[接続]**  
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
 > メンテナンス プランは、互換性レベルが 80 以上に設定されているデータベースに対してのみ実行されます。 互換性レベルが 70 以下に設定されているデータベースは表示されません。  
  
 **オブジェクト**  
 **[選択]** グリッドでテーブル、ビュー、または両方を表示するように制限します。  
  
 **[選択]**  
 このタスクの対象とするテーブルまたはインデックスを指定します。 [オブジェクト] ボックスで **[テーブルとビュー]** が選択されている場合は、このオプションは利用できません。  
  
 **[すべての既存の統計]**  
 列とインデックスの統計を両方とも更新します。  
  
 **[列統計のみ]**  
 列統計のみを更新します。  
  
 **[インデックス統計のみ]**  
 インデックス統計のみを更新します。  
  
 **[スキャンの種類]**  
 更新された統計情報を収集するスキャンの種類です。  
  
 **[フル スキャン]**  
 統計を収集する際、テーブルまたはビューのすべての行を読み取ります。  
  
 **[サンプル対象]**  
 大きなテーブルやビューの統計を収集するときにサンプリングする、テーブルまたはインデックス付きビューの割合や行数を指定します。  
  
 **[T-SQL の表示]**  
 選択したオプションに基づき、このタスクでサーバーに対して実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを表示します。  
  
> [!NOTE]  
> 影響を受けるオブジェクトが大量にある場合は、表示にかなりの時間を要する場合があります。  
  
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
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] のインスタンスに接続します。  
  
 **[特定のユーザー名とパスワードを使用する]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続します。 このオプションは利用できません。  
  
 **User name**  
 認証に使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。 このオプションは利用できません。  
  
 **パスワード**  
 認証に使用するパスワードを指定します。 このオプションは利用できません。  
  
## <a name="see-also"></a>参照  
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)    
 [sp_updatestats](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)    
 [Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)
