---
title: SQL Server (OracleToSQL) に Oracle のデータの移行 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Oracle Data Migration, Client-Side Migration
- Oracle Data Migration,Server-Side Migration
ms.assetid: e23c5268-41ed-4e55-9fe7-a11376202a13
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: c37f9c8e39a8a9dd87eabecba445b5ce7cef9028
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264679"
---
# <a name="migrating-oracle-data-into-sql-server-oracletosql"></a>SQL Server (OracleToSQL) に Oracle のデータの移行
変換されたオブジェクトが正常に同期後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、oracle からデータを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
> [!IMPORTANT]  
> 使用されているエンジンがサーバー側のデータ移行のエンジンの場合は、次に、データを移行する前にする必要がありますインストールする、SSMA Oracle 拡張パックし、SSMA を実行しているコンピューター上の Oracle プロバイダーの。 SQL Server エージェント サービスも実行している必要があります。 拡張機能パックをインストールする方法の詳細については、次を参照してください[サーバー コンポーネントのインストール (OracleToSQL)。](https://msdn.microsoft.com/33070e5f-4e39-4b70-ae81-b8af6e4983c5)  
  
## <a name="setting-migration-options"></a>移行オプションの設定  
移行する前にデータを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、プロジェクトの移行オプションの確認、**プロジェクト設定** ダイアログ ボックス。  
  
-   このダイアログ ボックスを使用して、移行のバッチ サイズ、テーブルのロック、制約チェック、null 値の処理、および id 値の処理などのオプションを設定できます。 プロジェクトの移行設定の詳細については、次を参照してください。[プロジェクトの設定 (移行) (OracleToSQL)](https://msdn.microsoft.com/fcd6b988-633b-4b2b-9f36-6368b5e86b60)します。  
  
-   **移行エンジン**で、**プロジェクト設定**ダイアログ ボックスで、2 つの種類のデータ移行のエンジンを使用して、移行プロセスを実行できます。  
  
    1.  クライアント側のデータ移行のエンジン  
  
    2.  サーバー側のデータ移行のエンジン  
  
**クライアント側のデータの移行:**  
  
-   クライアント側でデータ移行を開始するには、選択、**クライアント側のデータ移行のエンジン**オプション、**プロジェクト設定** ダイアログ ボックス。  
  
-   **プロジェクト設定**、**クライアント側のデータ移行のエンジン**オプションを設定します。  
  
    > [!NOTE]  
    > **クライアント側のデータ移行のエンジン**SSMA アプリケーション内に存在し、拡張機能パックの可用性に依存しません。  
  
**サーバー側のデータの移行:**  
  
-   サーバー側のデータ移行中には、エンジンは、ターゲット データベースに存在します。 拡張機能パックによってインストールされます。 拡張機能パックをインストールする方法の詳細については、次を参照してください[SQL サーバー上のサーバー コンポーネントのインストール。](installing-ssma-components-on-sql-server-oracletosql.md)  
  
-   サーバー側での移行を開始するには、選択、**サーバー側のデータ移行のエンジン**オプション、**プロジェクト設定** ダイアログ ボックス。  
  
## <a name="migrating-data-to-sql-server"></a>SQL Server へのデータの移行  
移行データは、Oracle のテーブルから行のデータを移動する一括読み込み操作[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]トランザクション内のテーブル。 読み込まれた行の数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各トランザクションでは、プロジェクトの設定で構成されます。  
  
移行のメッセージを表示するには、出力ウィンドウが表示されているを確認します。 それから、**ビュー**メニューの **出力**します。  
  
**データを移行するには**  
  
1.  次のことを検証します。  
  
    -   Oracle プロバイダーは、SSMA を実行しているコンピューターにインストールされます。  
  
    -   変換後のオブジェクトを同期している、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
2.  Oracle メタデータ エクスプ ローラーでは、移行するデータを含むオブジェクトを選択します。  
  
    -   すべてのスキーマのデータを移行する場合は、横にチェック ボックスを選択します**スキーマ**します。  
  
    -   データを移行または個々 のテーブルの省略は、まずスキーマを展開し、**テーブル**、選択するか、テーブルの横にあるチェック ボックスをオフにします。  
  
3.  データを移行するには、2 つのケースが生じます。  
  
    **クライアント側のデータの移行:**  
  
    -   実行するため**クライアント側のデータ移行**を選択、**クライアント側のデータ移行のエンジン**オプション、**プロジェクト設定** ダイアログ ボックス。  
  
    **サーバー側のデータの移行:**  
  
    -   サーバー側でのデータの移行を行う前に確認します。  
  
        1.  SSMA for Oracle の拡張機能パックがのインスタンスにインストールされている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
        2.  SQL Server エージェント サービスは、SQL Server のインスタンスで実行されています。  
  
    -   実行するため**サーバー側のデータ移行**を選択、**サーバー側のデータ移行のエンジン**オプション、**プロジェクト設定** ダイアログ ボックス。  
  
4.  右クリック**スキーマ**Oracle メタデータ エクスプ ローラーでクリック**Migrate Data**します。 個々 のオブジェクトまたはオブジェクトのカテゴリのデータを移行することもできます。オブジェクトまたはその親フォルダーを右クリックします。選択、 **Migrate Data**オプション。  
  
    > [!NOTE]  
    > SSMA for Oracle の拡張機能パックがのインスタンスにインストールされていないかどうかは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、場合**サーバー側のデータ移行のエンジン**が選択されている、ターゲット データベースにデータを移行する際に、次のエラーが発生しました。' SQL Server のデータ移行の SSMA コンポーネントが見つかりません、サーバー側のデータの移行を可能にすることはできません。 拡張機能パックが正しくインストールされているかどうかを確認してください '。 クリックして**キャンセル**データ移行を終了します。  
  
5.  **Oracle への接続**ダイアログ ボックスが接続の資格情報を入力し、クリックして**Connect**します。 Oracle に接続する方法の詳細については、次を参照してください[Oracle に接続する&#40;OracleToSQL。&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)  
  
    ターゲット データベースに接続するため[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で接続の資格情報を入力、 **SQL サーバーへの接続** ダイアログ ボックスをクリックします**Connect**します。 接続の詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[SQL サーバーへの接続](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    メッセージが表示されます、**出力**ウィンドウ。 移行の完了時に、**データ移行レポート**が表示されます。 すべてのデータが移行されない場合、エラーを含む行をクリックし、順にクリックします**詳細**します。 レポートが完了したら、クリックして**閉じる**します。 データ移行レポートの詳細については、次を参照してください[データ移行レポート (SSMA 一般的)。](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> SQL Express エディションは、対象データベースとして使用される、クライアント側のデータの移行のみが許可されているし、サーバー側のデータ移行はサポートされていません。  
  
## <a name="see-also"></a>参照  
[SQL Server にデータベースを移行する Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
