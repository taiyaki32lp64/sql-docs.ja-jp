---
title: SQL Server - Azure SQL DB への Sybase ASE データの移行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migrating data,Client Side Data Migration
- Migrating data,Server Side Data Migration
ms.assetid: 54a39f5e-9250-4387-a3ae-eae47c799811
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 28a07c08fd801a9d5fdcdde4206f7aa6fe7b926f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028837"
---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-db--sybasetosql"></a>移行の Sybase ASE データの SQL Server - Azure SQL DB (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) のデータベース オブジェクトを正常に読み込んだ後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB では、データを移行する ASE から[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。  
  
> [!IMPORTANT]  
> 使用されているエンジンがサーバー側のデータ移行のエンジンの場合は、データを移行する前にする必要がありますインストールする、SSMA for Sybase ASE 拡張パックおよび SSMA を実行しているコンピューター上の Sybase ASE プロバイダー。 SQL Server エージェント サービスも実行している必要があります。 拡張機能パックをインストールする方法の詳細については、次を参照してください[SQL サーバー (SybaseToSQL) での SSMA コンポーネントのインストール。](https://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
## <a name="setting-migration-options"></a>移行オプションの設定  
移行する前にデータを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB、プロジェクトの移行オプションの確認、**プロジェクト設定** ダイアログ ボックス。  
  
-   このダイアログ ボックスを使用して、移行のバッチ サイズ、テーブルのロック、制約チェック、null 値の処理、および id 値の処理などのオプションを設定できます。 プロジェクトの移行設定の詳細については、次を参照してください。[プロジェクトの設定 (移行) (Sybase)](https://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924)します。  
  
    詳細については**データ移行の設定の拡張**を参照してください[データ移行の設定](data-migration-settings-sybasetosql.md)  
  
-   **移行エンジン**で、**プロジェクト設定**ダイアログ ボックスで可視の 2 種類のデータ移行のエンジンを使用して、移行プロセスを実行できます。  
  
    1.  クライアント側のデータ移行のエンジン  
  
    2.  サーバー側のデータ移行のエンジン  
  
**クライアント側のデータの移行:**  
  
-   クライアント側でデータ移行を開始するには、オプションを選択**クライアント側のデータ移行のエンジン**で、**プロジェクト設定** ダイアログ ボックス。  
  
-   **プロジェクト設定**、**クライアント側のデータ移行のエンジン**オプションは既定で設定します。  
  
    > [!NOTE]  
    > クライアント側のデータ移行のエンジンは、SSMA アプリケーション内に存在して、そのためは、拡張機能パックの可用性に依存しません。  
  
**サーバー側のデータの移行:**  
  
-   サーバー側のデータ移行中には、エンジンは、ターゲット データベースに存在します。 拡張機能パックによってインストールされます。 拡張機能パックをインストールする方法の詳細については、次を参照してください[SQL サーバー (SybaseToSQL) での SSMA コンポーネントのインストール。](https://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
-   サーバー側での移行を開始するには、選択、**サーバー側のデータ移行のエンジン**オプション、**プロジェクト設定**ダイアログ。  
  
> [!NOTE]  
> ターゲット データベースのみとして Azure SQL DB を使用するときに**クライアント側のデータ移行**は許可されてサーバー側のデータ移行はサポートされていません。  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-db"></a>SQL Server または Azure SQL DB にデータの移行  
移行データは、一括読み込み操作をトランザクションで SQL Server テーブルに、ASE のテーブルから行のデータを移動します。 各トランザクションでは、SQL Server または Azure SQL DB に読み込まれる行の数は、プロジェクトの設定で構成されます。  
  
移行のメッセージを表示するには、出力ウィンドウが表示されているを確認します。 それ以外の場合、選択**出力**から、**ビュー**メニュー。  
  
**データを移行するには**  
  
1.  次のことを検証します。  
  
    -   ASE のプロバイダーは、SSMA を実行しているコンピューターにインストールされます。  
  
    -   ターゲット データベース (SQL Server または Azure SQL DB) と、変換されたオブジェクトを同期しました。  
  
2.  Sybase メタデータ エクスプ ローラーでは、移行するデータを含むオブジェクトを選択します。  
  
    -   すべてのスキーマのデータを移行する場合は、横にチェック ボックスを選択します**スキーマ**します。  
  
    -   データを移行または個々 のテーブルの省略は、まずスキーマを展開し、**テーブル**、選択するか、テーブルの横にあるチェック ボックスをオフにします。  
  
3.  データを移行するには、2 つのケースが生じます。  
  
    **クライアント側のデータの移行:**  
  
    実行するため**クライアント側のデータ移行**を選択、**クライアント側のデータ移行のエンジン**オプション、**プロジェクト設定** ダイアログ ボックス。  
  
    **サーバー側のデータの移行:**  
  
    -   サーバー側のデータ移行を実行する前に確認します。  
  
        1.  SSMA for Sybase の拡張機能パックは、SQL Server のインスタンスにインストールされます。  
  
        2.  SQL Server のインスタンスで SQL Server エージェント サービスが実行されています。  
  
    -   実行するため**サーバー側のデータ移行**を選択、**サーバー側のデータ移行のエンジン**オプション、**プロジェクト設定** ダイアログ ボックス。  
  
4.  右クリック**スキーマ**Sybase メタデータ エクスプ ローラーでクリック**Migrate Data**します。 個々 のオブジェクトまたはオブジェクトのカテゴリのデータを移行することもできます。オブジェクトまたはその親フォルダーを右クリックして、 **Migrate Data**オプション。  
  
    > [!NOTE]  
    > SSMA for Sybase の拡張機能パックは、SQL Server のインスタンスにインストールされていない場合、**サーバー側のデータ移行のエンジン**が選択されている、ターゲット データベースにデータを移行する際に、次のエラーが発生しました。' SQL Server のデータ移行の SSMA コンポーネントが見つかりません、サーバー側のデータの移行を可能にすることはできません。 拡張機能パックが正しくインストールされているかどうかを確認してください '。 クリックして**キャンセル**データ移行を終了します。  
  
5.  **Sybase ASE への接続**ダイアログ ボックスが接続の資格情報を入力し、クリックして**Connect**します。 Sybase ASE への接続に関する詳細については、次を参照してください[Sybase への接続&#40;SybaseToSQL。&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    ターゲット データベースが SQL Server の場合で接続の資格情報を入力し、 **SQL サーバーへの接続** ダイアログ ボックスをクリックします**Connect**します。 SQL Server に接続する方法の詳細については、次を参照してください[SQL Server(SybaseToSQL) への接続。](https://msdn.microsoft.com/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)  
  
    ターゲット データベースが Azure SQL DB の場合は、[接続の資格情報を入力してください。、 **Azure SQL DB への接続**] ダイアログ ボックスをクリックします**Connect**します。 Azure SQL DB に接続する方法の詳細については、次を参照してください[Azure SQL DB に接続する&#40;SybaseToSQL。&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    メッセージが表示されます、**出力**ウィンドウ。 移行の完了時に、**データ移行レポート**が表示されます。 すべてのデータが移行されない場合、エラーを含む行をクリックし、順にクリックします**詳細**します。 レポートが完了したら、クリックして**閉じる**します。 データ移行レポートの詳細については、次を参照してください[データ移行レポート (SSMA 一般的)。](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> SQL Express エディションは、対象データベースとして使用される、クライアント側のデータの移行のみが許可されているし、サーバー側のデータ移行はサポートされていません。  
  
## <a name="see-also"></a>参照  
[SQL Server - Azure SQL DB への Sybase ASE データベース移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
