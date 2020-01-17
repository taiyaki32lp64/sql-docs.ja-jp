---
title: SQL Server インポートの拡張機能
titleSuffix: Azure Data Studio
description: Azure Data Studio 用の SQL Server インポートの拡張機能をインストールして使用する
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 012c2c880e81c095e90086cf26ebffd6117d534e
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959121"
---
# <a name="sql-server-import-extension-preview"></a>SQL Server インポートの拡張機能 (プレビュー)

SQL Server インポートの拡張機能 (プレビュー) では、.txt ファイルと .csv ファイルが SQL テーブルに変換されます。 このウィザードでは、[Program Synthesis using Examples (PROSE)](https://microsoft.github.io/prose/) と呼ばれるマイクロソフト リサーチ フレームワークを利用して、最小のユーザー入力でファイルをインテリジェントに解析することができます。 これはデータ ラングリングのための強力なフレームワークであり、Microsoft Excel でフラッシュ フィルを強化するのと同じテクノロジです

この機能の SSMS バージョンの詳細については、[こちら](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard)の記事を参照してください。


## <a name="install-the-sql-server-import-extension"></a>SQL Server インポートの拡張機能をインストールする

1. 拡張機能マネージャーを開いて、使用可能な拡張機能にアクセスするには、拡張機能アイコンを選択するか、 **[表示]** メニューの **[拡張機能]** を選択します。
2. 使用可能な拡張機能を選択すると、その詳細が表示されます。

   ![拡張機能マネージャーをインポートする](media/sql-server-import-extension/import-wizard-install.png)

1. 必要な拡張機能を選択して**インストール**します。
2. **[再読み込み]** を選択して拡張機能を有効にします (拡張機能を初めてインストールするときにのみ必要です)。

## <a name="start-import-wizard"></a>インポート ウィザードを開始する

1. SQL Server インポートを開始するには、まず [サーバー] タブでサーバーへの接続を確立します。
2. 接続を確立したら、SQL テーブルにファイルをインポートするターゲット データベースにドリルダウンします。
3. データベースを右クリックし、 **[インポート ウィザード]** をクリックします。
    ![インポート ウィザードを開く](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>ファイルのインポート
1. 右クリックしてウィザードを起動すると、サーバーとデータベースは既に自動入力されています。 アクティブな接続が他にもある場合は、ドロップダウンで選択することができます。 
    
    **[参照]** をクリックしてファイルを選択します。 ファイル名に基づくテーブル名が自動的に入力されますが、それを自分で変更することもできます。

    既定では、スキーマは dbo になりますが、これは変更することができます。 **[次へ]** をクリックします。
    ![入力ファイル](media/sql-server-import-extension/import-wizard-input-file.png)
1. ウィザードでは、最初の 50 行に基づいてプレビューが生成されます。 データが正確に見えることを確認する以外に、このページに追加のアクションはありません。 **[次へ]** をクリックします。
    ![インポート ウィザードを開く](media/sql-server-import-extension/import-wizard-preview-data.png)
2. このページでは、列名またはデータ型に変更を加えたり、主キーかどうか、または null を許容するかどうかを変更したりできます。 変更は必要なだけ行うことができます。 **[データのインポート]** をクリックして続行します。
    ![インポート ウィザードを開く](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. このページには、選択したアクションの概要が表示されます。 ご利用のテーブルが正常に挿入されたかどうかを確認することもできます。 

    変更が必要な場合に **[完了]、[前へ]** の順にクリックすることも、別のファイルをすばやくインポートするために **[Import new file]\(新しいファイルのインポート\)** をクリックすることもできます。
    ![インポート ウィザードを開く](media/sql-server-import-extension/import-wizard-summary.png)
1. ご利用のターゲット データベースを更新するか、テーブル名に対して SELECT クエリを実行することにより、テーブルが正常にインポートされたかどうかを確認します。

## <a name="next-steps"></a>次の手順
- インポート ウィザードの詳細については、[こちら](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/)のブログの投稿を参照してください。
- PROSE の詳細については、[こちら](https://microsoft.github.io/prose/)のドキュメントを参照してください。
