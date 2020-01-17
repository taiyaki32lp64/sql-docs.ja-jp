---
title: Azure の SSIS カタログ (SSISDB) に接続する | Microsoft Docs
description: Azure SQL Database サーバーでホストされている SSIS カタログ (SSISDB) に接続するために必要な接続情報を確認します。
ms.date: 09/23/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: 436d65965fa0fa114f1891293972141f1373a696
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037170"
---
# <a name="connect-to-the-ssis-catalog-ssisdb-in-azure"></a>Azure の SSIS カタログ (SSISDB) に接続する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Azure SQL Database サーバーでホストされている SSIS カタログ (SSISDB) に接続するために必要な接続情報を確認します。 接続するには、次の項目が必要です。
- 完全修飾サーバー名
- データベース名
- ログイン情報 

> [!IMPORTANT]
> この時点では、Azure Data Factory での Azure SSIS Integration Runtime の作成とは切り離して、Azure SQL Database に SSISDB カタログ データベースを作成することはできません。 Azure SSIS IR は、Azure 上で SSIS パッケージを実行するランタイム環境です。 プロセスのチュートリアルについては、「[Azure で SSIS パッケージをデプロイし、実行する](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)」を参照してください。 

## <a name="prerequisites"></a>Prerequisites
始める前に、バージョン 17.2 以降の SQL Server Management Studio (SSMS) があることを確認します。 SSISDB カタログ データベースが SQL Database Managed Instance でホストされている場合は、SSMS のバージョンが 17.6 以降であることを確認します。 最新バージョンの SSMS をダウンロードするには、「[SQL Server Management Studio (SSMS) のダウンロード](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)」を参照してください。

## <a name="get-the-connection-info-from-the-azure-portal"></a>Azure Portal から接続情報を取得する
1. [Azure ポータル](https://portal.azure.com/)にログインします。
2. Azure Portal で、左側のメニューから **[SQL Databases]** を選択し、 **[SQL データベース]** ページで [`SSISDB` データベース] を選択します。 
3. `SSISDB` データベースの **[概要]** ページで、次の図のように、完全修飾サーバー名を確認します。 **[クリックしてコピー]** オプションを呼び出すには、サーバー名にマウス ポインターを移動します。

    ![サーバー接続情報](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. SQL Database サーバーのログイン情報を忘れてしまった場合は、[SQL Database サーバー] ページに移動します。 ここでは、サーバー管理者名を表示でき、必要に応じて、パスワードをリセットできます。

## <a name="connect-with-ssms"></a>SSMS との接続
1. SQL Server Management Studio を開きます。

2. **サーバーに接続します**。 **[サーバーへの接続]** ダイアログ ボックスに次の情報を入力します。

   | 設定       | 提案される値 | [説明] | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **サーバーの種類** | データベース エンジン | この値は必須です。 |
   | **サーバー名** | 完全修飾サーバー名 | 名前は **mysqldbserver.database.windows.net** の形式である必要があります。 |
   | **[認証]** | SQL Server 認証 (SQL Server Authentication) | |
   | **Login** | サーバー管理者アカウント | これはサーバーを作成したときに指定したアカウントです。 |
   | **パスワード** | サーバー管理者アカウントのパスワード | これはサーバーを作成したときに指定したパスワードです。 |

    ![SSMS を使用してサーバーに接続する](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-1.png)

3. **SSISDB データベースに接続します**。 **[オプション]** を選択して、 **[サーバーへの接続]** ダイアログ ボックスを展開します。 展開した **[サーバーへの接続]** ダイアログ ボックスで、 **[接続プロパティ]** タブを選択します。 **[データベースへの接続]** フィールドで、`SSISDB` を選択または入力します。

    > [!IMPORTANT]
    > 接続時に `SSISDB` を選択しないと、オブジェクト エクスプローラーで SSIS カタログが表示されない場合があります。

    ![接続に SSISDB データベースを選択する](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-2.png)

4. **[接続]** を選択します。

5. オブジェクト エクスプローラーで、 **[Integration Services カタログ]** 、 **[SSISDB]** の順に展開し、SSIS カタログ データベース内のオブジェクトを表示します。

    ![SSMS のオブジェクト エクスプローラーで SSISDB データベースを探す](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-3.png)

## <a name="next-steps"></a>次の手順
- パッケージを配置します。 詳細については、「[SQL Server Management Studio (SSMS) を使用して SSIS プロジェクトを配置する](../ssis-quickstart-deploy-ssms.md)」を参照してください。
- パッケージを実行します。 詳細については、「[SQL Server Management Studio (SSMS) を使用して SSIS プロジェクトを配置する](../ssis-quickstart-run-ssms.md)」を参照してください。
- パッケージのスケジュールを設定します。 詳細については、「[Azure で SSIS パッケージのスケジュールを設定する](ssis-azure-schedule-packages.md)」を参照してください。
