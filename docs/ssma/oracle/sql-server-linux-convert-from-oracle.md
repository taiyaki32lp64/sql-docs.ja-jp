---
title: Linux 上の SQL Server への Oracle HR スキーマの移行 |Microsoft Docs
description: サンプルの Oracle スキーマを SQL Server on Linux に変換します。
author: shamikg
ms.author: shamikg
manager: shamikg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: ssma
ms.openlocfilehash: 1926c13b739de8294966fd6ce84df3d1e02a676e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266518"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>SQL Server Migration Assistant を使った Linux 上の SQL Server 2017 への Oracle スキーマを移行します。

このチュートリアルでは、Windows 上の Oracle の SQL Server Migration Assistant (SSMA) を使用、Oracle のサンプルを変換する**HR**スキーマ[SQL Server 2017 on Linux](../../linux/sql-server-linux-overview.md)します。

> [!div class="checklist"]
> * ダウンロードして Windows での SSMA のインストール
> * 移行を管理する SSMA プロジェクトを作成します。
> * Oracle への接続
> * 移行レポートを実行します。
> * サンプル HR スキーマを変換します。
> * データを移行します。

## <a name="prerequisites"></a>必須コンポーネント

- Oracle 12c の (12.2.0.1.0) を持つインスタンス、 **HR**スキーマがインストールされています。
- Linux 上の SQL Server の作業用インスタンス

> [!NOTE]
> SQL Server on Windows をターゲットに同じ手順を使用できますで Windows を選択する必要があります、**移行先**プロジェクトの設定。

## <a name="download-and-install-ssma-for-oracle"></a>ダウンロードし、SSMA for Oracle をインストールします。

SQL Server Migration Assistant のいくつかのエディションは、ソース データベースによって、使用できます。  現在のバージョンをダウンロード[SQL Server Migration Assistant for Oracle](https://aka.ms/ssmafororacle)し、[ダウンロード] ページの手順を使用してインストールします。

> [!NOTE]
> この時点で、 **SSMA for Oracle の拡張機能パック**は linux では、サポートされていませんが、このチュートリアルでは必要はありません。

## <a name="create-and-set-up-project"></a>作成し、セットアップ プロジェクト

新しい SSMA プロジェクトを作成するのにには、次の手順を使用します。

1. SSMA for Oracle を開き、選択**新しいプロジェクト**から、**ファイル**メニュー。

1. プロジェクトの名前を付けます。

1. "SQL Server 2017 (Linux) - プレビュー"を選択、**移行先**フィールド。

SSMA for Oracle では、既定では、Oracle のサンプル スキーマを使用しません。 HR スキーマを有効にするには、次の手順を使用します。

1. SSMA では、選択、**ツール**メニュー。

1. 選択**プロジェクト設定の既定の**を選び、**システム オブジェクトの読み込み**します。

1. 確認**HR**がチェックされ、選択**OK**。

## <a name="connect-to-oracle"></a>Oracle への接続

次に SSMA を Oracle に接続します。

1. ツールバーの**Connect to Oracle**します。

1. サーバー名、ポート、Oracle SID、ユーザー名、およびパスワードを入力します。

   ![Oracle への接続](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. 続いて、 **[接続]** をクリックします。 数分後は、SSMA for Oracle は、データベースに接続し、そのメタデータを読み取ります。

## <a name="create-a-report"></a>レポートを作成します。

次の手順を使用すると、移行レポートを生成できます。

1. **Oracle メタデータ エクスプ ローラー**サーバーのノードを展開します。

1. 展開**スキーマ**を右クリックして**HR**、選択および**レポートの作成**です。

   ![Oracle メタデータ エクスプ ローラーは、レポートを作成します。](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. すべての警告とエラーに関連付けられた変換の一覧を表示するレポートを新しいブラウザー ウィンドウが開きます。

   > [!NOTE]
   > このチュートリアルの一覧から何もする必要はありません。 Oracle データベースの次の手順を実行する場合は、データベースの変換の重要な問題に対処するレポートをレビューする必要があります。

   ![移行のサンプル レポート](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>SQL Server への接続

次に**SQL サーバーへの接続**適切な接続情報を入力します。  まだデータベース名を使用する場合は、存在、SSMA for Oracle が自動的に作成します。

![SQL Server への接続](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>スキーマを変換します。

右クリックして**HR**で**Oracle メタデータ エクスプ ローラー**スキーマの変換を選択します。

![スキーマを変換します。](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>データベースを同期します。

次に、データベースを同期します。

1. 変換が完了すると、使用、 **SQL Server メタデータ エクスプ ローラー**前の手順で作成したデータベースに移動します。

1. データベースを右クリックして**データベースと同期する**、[ok] をクリックします。

   ![データベースと同期します。](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>データを移行します。

最後の手順では、データを移行します。

1. **Oracle メタデータ エクスプ ローラー**を右クリックして**HR**を選択し、 **Migrate Data**します。

1. データ移行の手順では、Oracle と SQL Server 資格情報を再入力することが必要です。

1. 完了したら、次のスクリーン ショットのようになりますが、データ移行レポートを確認します。

   ![データ移行レポート](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>次の手順

複雑な Orcale スキーマ、変換プロセスの詳細の時間、テスト、およびクライアント アプリケーションへの変更、します。 このチュートリアルの目的では、全体的な移行プロセスの一部として、Oracle の SSMA を使用する方法を説明します。

このチュートリアルでは、以下の使用方法を学習しました:
> [!div class="checklist"]
> * Windows での SSMA をインストールします。
> * 新しい SSMA プロジェクトを作成します。
> * 評価し、Oracle からの移行の実行

次に、SSMA を使用する他の方法の詳細します。

> [!div class="nextstepaction"]
>[SQL Server Migration Assistant のドキュメント](../sql-server-migration-assistant.md)
