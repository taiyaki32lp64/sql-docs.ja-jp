---
title: 一般にバックアップの更新が必要になるアクション | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], actions requiring a backup
- restoring [SQL Server replication], actions requiring a backup
- backups [SQL Server replication], actions requiring a backup
ms.assetid: a5975bf4-183e-42e3-b7d1-ad02f89d2e1d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 184bda56568cfcedbc07183bd2be7fdde7a789e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705031"
---
# <a name="common-actions-requiring-an-updated-backup"></a>一般にバックアップの更新が必要になるアクション
  定期的なログ バックアップを実行する場合は、レプリケーション関連の変更をログ バックアップでキャプチャする必要があります。 ログ バックアップを実行しない場合は、レプリケーション スキーマまたはトポロジを変更した後でパブリケーション、ディストリビューション、サブスクリプション、 **msdb**、および **master** の各データ ベースのバックアップを実行してください。  
  
## <a name="publication-database"></a>パブリケーション データベース  
 以下の処理の後で、パブリケーション データベースをバックアップしてください。  
  
-   パブリケーションの新規作成。  
  
-   フィルター選択を含む、任意のパブリケーション プロパティの変更。  
  
-   既存のパブリケーションへのアーティクル追加。  
  
-   1 つのパブリケーション全体にわたる、サブスクリプションの再初期化。  
  
-   パブリッシュされたテーブルでのスキーマの変更。  
  
-   [sp_addscriptexec &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql) による要求時スクリプトの実行。  
  
-   任意のアーティクル プロパティの変更。  
  
-   任意のパブリケーションの削除。  
  
-   任意のアーティクルの削除。  
  
-   レプリケーションの無効化。  
  
## <a name="distribution-database"></a>ディストリビューション データベース  
 以下の処理の後で、ディストリビューション データベースをバックアップしてください。  
  
-   レプリケーション エージェント プロファイルの作成または変更。  
  
-   レプリケーション エージェント プロファイルのパラメーターの変更。  
  
-   任意のプッシュ サブスクリプションについての、レプリケーション エージェント プロパティ (スケジュールを含む) の変更。  
  
-   自動 ID 範囲管理機能による新しい ID 範囲の割り当て。  
  
## <a name="subscription-database"></a>サブスクリプション データベース  
 以下の処理の後で、サブスクリプション データベースをバックアップしてください。  
  
-   任意のサブスクリプション プロパティの変更。  
  
-   パブリッシャーにあるマージ サブスクリプションの優先順位の変更。  
  
-   任意のサブスクリプションの削除。  
  
-   レプリケーションの無効化。  
  
## <a name="msdb-database"></a>msdb データベース  
 以下の処理の後で、適切なノードで **msdb** システム データベースをバックアップしてください。  
  
-   レプリケーションの有効化または無効化。  
  
-   ディストリビューション データベースの追加または削除 (ディストリビューターで)。  
  
-   データベースのパブリッシュを有効化または無効化 (パブリッシャーで)。  
  
-   レプリケーション エージェント プロファイルの作成または変更 (ディストリビューターで)。  
  
-   任意のレプリケーション エージェント パラメーターの変更 (ディストリビューターで)。  
  
-   任意のプッシュ サブスクリプションについて、レプリケーション エージェント プロパティ (スケジュールを含む) の変更 (ディストリビューターで)。  
  
-   任意のプル サブスクリプションについて、レプリケーション エージェント プロパティ (スケジュールを含む) の変更 (サブスクライバーで)。  
  
-   変換可能なサブスクリプションを使用するトランザクション パブリケーションに関連する DTS パッケージの作成 (ディストリビューターおよびサブスクライバーで)。  
  
-   変換可能なサブスクリプションの追加または削除 (ディストリビューターおよびサブスクライバーで)。  
  
## <a name="master-database"></a>master データベース  
 以下の処理の後で、適切なノードで **master** システム データベースをバックアップしてください。  
  
-   レプリケーションの有効化または無効化。  
  
-   ディストリビューション データベースの追加または削除 (ディストリビューターで)。  
  
-   データベースのパブリッシュを有効化または無効化 (パブリッシャーで)。  
  
-   任意のデータベースについて、先頭のパブリケーションの追加、または末尾のパブリケーションの削除 (パブリッシャーで)。  
  
-   任意のデータベースについて、先頭のサブスクリプションの追加、または末尾のサブスクリプションの削除 (サブスクライバーで)。  
  
-   ディストリビューション パブリッシャーのパブリッシャーの有効化または無効化 (パブリッシャーおよびディストリビューターで)。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server データベースのバックアップと復元](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Back Up and Restore Replicated Databases (レプリケートされたデータベースのバックアップと復元)](back-up-and-restore-replicated-databases.md)  
  
  
