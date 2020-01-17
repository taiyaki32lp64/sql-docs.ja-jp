---
title: SQL Server Profiler の拡張機能
titleSuffix: Azure Data Studio
description: Azure Data Studio 用の SQL Server Profiler の拡張機能 (プレビュー) をインストールして使用する
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 4fcb16d2ec3c267dc2927f22a029709a434416c9
ms.sourcegitcommit: 76fb3ecb79850a8ef2095310aaa61a89d6d93afd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2020
ms.locfileid: "75776513"
---
# <a name="sql-server-profiler-extension-preview"></a>SQL Server Profiler の拡張機能 (プレビュー)

SQL Server Profiler の拡張機能 (プレビュー) は、拡張イベントを使用して構築されていることを除けば、SQL Server Management Studio (SSMS) プロファイラーに類似したシンプルな SQL Server トレース ソリューションです。 SQL Server Profiler は、非常に使いやすく、最も一般的なトレース構成に合わせて適切な既定値を備えています。 UX は、イベントを参照するため、および関連付けられた Transact-SQL (T-SQL) テキストを表示するために最適化されています。 Azure Data Studio 用の SQL Server Profiler では、使いやすい UX で T-SQL 実行アクティビティを収集するための適切な既定値も想定されています。 この拡張機能は、現在プレビューの段階にあります。

**一般的な SQL Profiler のユースケース:**

- 問題の原因を特定するため、問題の発生したクエリを順次実行する。
- 実行速度の遅いクエリを検出し、その原因を診断する。
- 問題の原因となる一連の Transact-SQL ステートメントをキャプチャする。
- ワークロードを調整するため、SQL Server のパフォーマンスを監視する。
- 問題を診断するために、さまざまなパフォーマンス カウンターの関連を調べる。


## <a name="install-the-sql-server-profiler-extension"></a>SQL Server Profiler の拡張機能をインストールする

1. 拡張機能マネージャーを開いて、使用可能な拡張機能にアクセスするには、拡張機能アイコンを選択するか、 **[表示]** メニューの **[拡張機能]** を選択します。
2. 使用可能な拡張機能を選択すると、その詳細が表示されます。

   ![プロファイラー拡張機能マネージャー](media/extensions/sql-server-profiler-extension/profiler-extension.png)

1. 必要な拡張機能を選択して**インストール**します。
2. **[再読み込み]** を選択して拡張機能を有効にします (拡張機能を初めてインストールするときにのみ必要です)。

## <a name="start-profiler"></a>Profiler の開始

1. Profiler を起動するには、まず [サーバー] タブでサーバーへの接続を確立します。
2. 接続を確立したら、**Alt + P** キーを押して Profiler を起動します。
3. Profiler を起動するには、**Alt + S** キーを押します。これで、拡張イベントの表示を開始できます。
    ![プロファイラー拡張機能マネージャー](media/extensions/sql-server-profiler-extension/view-profiler.png)    
1. Profiler を停止するには、**Alt + S** キーを押します。このホットキーはトグルです。

## <a name="next-steps"></a>次のステップ

Profiler と拡張イベントの詳細については、[拡張イベント](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)に関するページを参照してください。





