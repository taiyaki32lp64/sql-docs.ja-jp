---
title: Linux でのデータベースのエクスポートとインポート
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.openlocfilehash: f99ff799ec91ea455cc37bd994c8555330a8ff0f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68105550"
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>Windows 上で SSMS または SqlPackage.exe を使用して Linux 上でデータベースをエクスポートおよびインポートする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、[SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) と [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx) を使用して SQL Server on Linux 上でデータベースをエクスポートおよびインポートする方法について説明します。 SSMS と SqlPackage.exe は Windows アプリケーションなので、Linux 上のリモート SQL Server インスタンスに接続できる Windows マシンがある場合は、この手法を使用します。

[Windows 上の SSMS を使用して SQL Server on Linux に接続する方法](sql-server-linux-manage-ssms.md)に関するページの説明に従い、常に SQL Server Management Studio (SSMS) の最新バージョンをインストールして使用するようにします。

> [!NOTE]
> ある SQL Server インスタンスから別の SQL Server インスタンスにデータベースを移行する場合は、[バックアップと復元](sql-server-linux-migrate-restore-database.md)を使用することをお勧めします。

## <a name="export-a-database-with-ssms"></a>SSMS を使用してデータベースをエクスポートする

1. Windows の検索ボックスに「**Microsoft SQL Server Management Studio**」と入力し、デスクトップ アプリをクリックして SSMS を起動します。

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. オブジェクト エクスプローラーでソース データベースに接続します。 オンプレミスまたはクラウドの Linux、Windows、または Docker で実行されている Microsoft SQL Server、および Azure SQL Database または Azure SQL Data Warehouse のソース データベースを使用できます。

3. オブジェクト エクスプローラーでソース データベースを右クリックし、 **[タスク]** をポイントして、 **[データ層アプリケーションのエクスポート]** をクリックします。

4. エクスポート ウィザードで **[次へ]** をクリックし、 **[設定]** タブで、BACPAC ファイルをローカル ディスクの場所または Azure BLOB に保存するようにエクスポートを構成します。

5. 既定では、データベース内のすべてのオブジェクトがエクスポートされます。 **[詳細設定]** タブをクリックし、エクスポートするデータベース オブジェクトを選択します。

6. **[次へ]** をクリックし、 **[完了]** をクリックします。

選択した場所に *.BACPAC ファイルが正常に作成されると、ターゲット データベースにインポートする準備は完了です。

## <a name="import-a-database-with-ssms"></a>SSMS を使用してデータベースをインポートする

1. Windows の検索ボックスに「**Microsoft SQL Server Management Studio**」と入力し、デスクトップ アプリをクリックして SSMS を起動します。

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. オブジェクト エクスプローラーでターゲット サーバーに接続します。 オンプレミスまたはクラウドの Linux、Windows、または Docker で実行されている Microsoft SQL Server、および Azure SQL Database または Azure SQL Data Warehouse のターゲット サーバーを使用できます。

3. オブジェクト エクスプローラーで **Databases** フォルダーを右クリックし、 **[データ層アプリケーションのインポート]** をクリックします

4. ターゲット サーバーにデータベースを作成するには、ローカル ディスクから BACPAC ファイルを指定するか、BACPAC ファイルをアップロードした Azure ストレージ アカウントとコンテナーを選択します。

5. データベースの新しいデータベース名を指定します。 Azure SQL Database にデータベースをインポートする場合は、[Microsoft Azure SQL Database のエディション] (サービス レベル)、[データベースの最大サイズ]、および [サービスの目標] (パフォーマンス レベル) を設定します。

6. **[次へ]** をクリックし、 **[完了]** をクリックして、ターゲット サーバーの新しいデータベースに BACPAC ファイルをインポートします。

*.BACPAC ファイルがインポートされ、指定したターゲット サーバーに新しいデータベースが作成されます。

## <a id="sqlpackage"></a> SqlPackage のコマンドライン オプション

また、SQL Server Data Tools (SSDT) コマンドライン ツールである [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx) を使用して、BACPAC ファイルをエクスポートおよびインポートすることもできます。

次のコマンド例では、BACPAC ファイルをエクスポートします。

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

.BACPAC ファイルからデータベース スキーマとユーザー データをインポートするには、次のコマンドを使用します。

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>参照
SSMS の使用方法の詳細については、[SQL Server Management Studio の使用](https://msdn.microsoft.com/library/ms174173.aspx)に関するページを参照してください。 SqlPackage.exe の詳細については、[SqlPackage のリファレンス ドキュメント](https://msdn.microsoft.com/library/hh550080.aspx)を参照してください。
