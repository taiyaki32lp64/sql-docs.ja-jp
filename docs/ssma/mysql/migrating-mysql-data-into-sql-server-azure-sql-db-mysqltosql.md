---
title: SQL Server - Azure SQL DB (MySQLToSQL) への MySQL データの移行 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 83a4a2d1bea5074cc268590d4074bde631f28694
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908832"
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>MySQL のデータの移行には、SQL Server - Azure SQL DB (MySQLToSQL)
変換後のオブジェクトが正常に同期[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のデータを移行する MySQL から[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。  
  
> [!IMPORTANT]  
> 場合、エンジンが使用されているサーバー側のデータの移行のエンジン、その後、移行する前に、データの MySQL の拡張機能パックおよび SSMA を実行しているコンピューターに MySQL プロバイダー、SSMA をインストールする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント サービスが実行されてもする必要があります。 拡張機能パックをインストールする方法の詳細については、次を参照してください[SQL Server (MySQL to SQL) での SSMA コンポーネントのインストール。](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
## <a name="setting-migration-options"></a>移行オプションの設定  
移行する前にデータを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure、プロジェクトの移行オプションの確認、**プロジェクト設定** ダイアログ ボックス。  
  
-   このダイアログ ボックスを使用して、移行のバッチ サイズ、テーブルのロック、制約チェック、null 値の処理、および id 値の処理などのオプションを設定できます。 プロジェクトの移行設定の詳細については、次を参照してください。[プロジェクトの設定 (移行)](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9)します。  
  
    詳細については**データ移行の設定の拡張**を参照してください[データ移行の設定](data-migration-settings-mysqltosql.md)  
  
-   **移行エンジン**で、**プロジェクト設定**ダイアログ ボックスで、2 つの種類のデータ移行のエンジンを使用して、移行プロセスを実行できます。  
  
    1.  クライアント側のデータ移行のエンジン  
  
    2.  サーバー側のデータ移行のエンジン  
  
**クライアント側のデータの移行:**  
  
-   クライアント側でデータ移行を開始するには、選択、**クライアント側のデータ移行のエンジン**オプション、**プロジェクト設定** ダイアログ ボックス。  
  
-   **プロジェクト設定**、**クライアント側のデータ移行のエンジン**オプションを設定します。  
  
    > [!NOTE]  
    > **クライアント側のデータ移行のエンジン**SSMA アプリケーション内に存在し、拡張機能パックの可用性に依存しません。  
  
**サーバー側のデータの移行:**  
  
-   サーバー側のデータ移行中には、エンジンは、ターゲット データベースに存在します。 拡張機能パックによってインストールされます。 拡張機能パックをインストールする方法の詳細については、次を参照してください[SQL Server (MySQL to SQL) での SSMA コンポーネントのインストール。](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
-   サーバー側での移行を開始するには、選択、**サーバー側のデータ移行のエンジン**オプション、**プロジェクト設定** ダイアログ ボックス。  
  
> [!IMPORTANT]  
> **クライアント側のデータ移行**オプションはのみ SQL Azure で使用できます。  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>SQL Server または SQL Azure にデータの移行  
移行データは、MySQL のテーブルから行のデータを移動する一括読み込み操作[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のテーブルのトランザクション。 読み込まれた行の数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各トランザクションでは、プロジェクトの設定で構成されます。  
  
移行のメッセージを表示するには、出力ウィンドウが表示されているを確認します。 それから、**ビュー**メニューの **出力**します。  
  
**データを移行するには**  
  
1.  次のことを検証します。  
  
    -   MySQL プロバイダーは、SSMA を実行しているコンピューターにインストールされます。  
  
    -   ターゲット データベースに変換されたオブジェクトを同期する (SQL Server または SQL Azure)。  
  
2.  MySQL メタデータ エクスプ ローラーでは、移行するデータを含むオブジェクトを選択します。  
  
    -   すべてのスキーマのデータを移行する場合は、横にチェック ボックスを選択します**スキーマ**します。  
  
    -   データを移行または個々 のテーブルの省略は、まずスキーマを展開し、**テーブル**、選択するか、テーブルの横にあるチェック ボックスをオフにします。  
  
3.  データを移行するには、2 つのケースが生じます。  
  
    **クライアント側のデータの移行:**  
  
    -   実行するため**クライアント側のデータ移行**を選択、**クライアント側のデータ移行のエンジン**オプション、**プロジェクト設定** ダイアログ ボックス。  
  
    **サーバー側のデータの移行:**  
  
    -   サーバー側でのデータの移行を行う前に確認します。  
  
        1.  SSMA for MySQL の拡張機能パックは、SQL Server のインスタンスにインストールされます。  
  
        2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント サービスが SQL Server のインスタンスで実行されています。  
  
    -   実行するため**サーバー側のデータ移行**を選択、**サーバー側のデータ移行のエンジン**オプション、**プロジェクト設定** ダイアログ ボックス。  
  
4.  右クリック**スキーマ**MySQL メタデータ エクスプ ローラーでクリック**Migrate Data**します。 個々 のオブジェクトまたはオブジェクトのカテゴリのデータを移行することもできます。オブジェクトまたはその親フォルダーを右クリックします。選択、 **Migrate Data**オプション。  
  
    > [!NOTE]  
    > SSMA for MySQL の拡張機能パックは、SQL Server のインスタンスにインストールされていない場合、**サーバー側のデータ移行のエンジン**が選択されている、ターゲット データベースにデータを移行する際に、次のエラーが発生しました。' SQL Server のデータ移行の SSMA コンポーネントが見つかりません、サーバー側のデータの移行を可能にすることはできません。 拡張機能パックが正しくインストールされているかどうかを確認してください '。 クリックして**キャンセル**データ移行を終了します。  
  
5.  **MySQL への接続**ダイアログ ボックスが接続の資格情報を入力し、クリックして**Connect**します。 MySQL に接続する方法の詳細については、次を参照してください[MySQL への接続&#40;MySQLToSQL。&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
    ターゲット データベースが SQL Server の場合で接続の資格情報を入力し、 **SQL サーバーへの接続** ダイアログ ボックスをクリックします**Connect**します。 SQL Server に接続する方法の詳細については、次を参照してください[SQL サーバーへの接続。](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    ターゲット データベースが SQL Azure の場合は、[接続の資格情報を入力してください。、 **SQL Azure への接続**] ダイアログ ボックスをクリックします**Connect**します。 SQL Azure に接続する方法の詳細については、次を参照してください[Azure SQL DB への接続&#40;MySQLToSQL。&#41;](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md)  
  
    メッセージが表示されます、**出力**ウィンドウ。 移行の完了時に、**データ移行レポート**が表示されます。 すべてのデータが移行されない場合、エラーを含む行をクリックし、順にクリックします**詳細**します。 レポートが完了したら、クリックして**閉じる**します。 データ移行レポートの詳細については、次を参照してください[データ移行レポート (SSMA 一般的)。](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> SQL Express エディションは、対象データベースとして使用される、クライアント側のデータの移行のみが許可されているし、サーバー側のデータ移行はサポートされていません。  
  
## <a name="see-also"></a>参照  
[SQL Server - Azure SQL DB への移行 MySQL データベース&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
