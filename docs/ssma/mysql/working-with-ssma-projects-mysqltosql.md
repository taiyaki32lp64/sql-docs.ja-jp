---
title: SSMA プロジェクト (MySQLToSQL) での作業 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 37a763c0acca891d8bbbc1a310edcb6f8b987436
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904901"
---
# <a name="working-with-ssma-projects-mysqltosql"></a>SSMA プロジェクトでの作業 (MySQLToSQL)
SQL Server または SQL Azure に MySQL データベースを移行するには、最初に SSMA プロジェクトを作成する必要があります。 プロジェクトは、次の情報を含むファイルです。  
  
-   SQL Server または SQL Azure に移行するための MySQL データベースに関するメタデータ。  
  
-   SQL Server または SQL Azure 移行済みのオブジェクトとデータを受信するは、ターゲット インスタンスに関するメタデータ。  
  
-   SQL Server または SQL Azure 接続情報です。  
  
-   プロジェクトの設定。  
  
プロジェクトを開くときに、MySQL と SQL Server または SQL Azure から切断されます。 オフラインで作業できます。 SQL Server に再接続する詳細については、次を参照してください[SQL Server に接続する&#40;MySQLToSQL。&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>既定のプロジェクト設定を確認します。  
SSMA には、変換、データベースの読み込みとデータの移行、および MySQL と SQL Server または SQL Azure での SSMA の同期のいくつかの設定が含まれています。 既定の設定は、多くのユーザーに適しています。 ただし、新しい SSMA プロジェクトを作成する前に、設定を確認する必要があります。 必要な場合は、すべての新しいプロジェクトに使用される既定の設定を変更できます。  
  
##### <a name="to-review-default-project-settings"></a>既定のプロジェクト設定を確認するには  
  
1.  選択**プロジェクト設定の既定の**から、**ツール**メニュー。  
  
2.  プロジェクトの種類を選択します。**移行ターゲット バージョン**設定が表示/変更するには、クリックのドロップダウン**全般**タブ。  
  
3.  左側のウィンドウで次のようにクリックします。**変換**します。  
  
4.  右側のウィンドウで確認し、必要に応じて設定を変更します。 これらの設定の詳細については、次を参照してください。[プロジェクト設定&#40;変換&#41; &#40;MySQLToSQL&#41; ](../../ssma/mysql/project-settings-conversion-mysqltosql.md)します。  
  
5.  移行、同期、SQL Azure、GUI、およびマッピングの種類のページの手順 1. ~ 3. を繰り返します。  
  
-   移行の設定については、次を参照してください。[プロジェクト設定&#40;移行&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)します。  
  
-   SQL Server への同期設定の詳細については、次を参照してください。[プロジェクト設定&#40;同期&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)します。  
  
-   GUI の設定については、次を参照してください。[プロジェクトの設定 (GUI) (SSMA 一般的)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)します。  
  
-   データ型マッピングの設定については、次を参照してください。[プロジェクト設定&#40;型マッピング&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)します。  
  
-   SQL Azure の設定については、次を参照してください。[プロジェクト設定&#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)します。  
  
> [!NOTE]  
> SQL Azure の設定が選択した場合にのみ表示されます**SQL Azure への移行**してプロジェクトを作成します。  
  
## <a name="creating-new-projects"></a>新しいプロジェクトの作成  
SQL Server または SQL Azure に MySQL データベースからデータを移行するには、プロジェクトを作成する必要があります。  
  
##### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには  
  
1.  選択**新しいプロジェクト**から、**ファイル**メニュー。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。 **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  **名前**ボックスに、プロジェクトの名前を入力します。  
  
3.  **場所**ボックスで、入力するか、プロジェクトのフォルダーを選択します。  
  
4.  **移行に**ドロップダウンで、ターゲットのバージョンを選択します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移行に使用します。 使用可能なオプションがあります。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   Azure SQL DB  
  
クリックして**OK**  
  
SSMA は、プロジェクト ファイルを作成します。  
  
## <a name="customizing-project-settings"></a>プロジェクト設定のカスタマイズ  
既定値を定義するだけでなくすべての新しい SSMA プロジェクトに適用されるプロジェクトの設定は各プロジェクトの設定をカスタマイズもできます。 詳細については、次を参照してください。[プロジェクト オプションの設定&#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)します。  
  
ソースとターゲット データベース間のデータ型マッピングをカスタマイズするときに、プロジェクト、データベース、またはオブジェクト レベルでは、マッピングを定義できます。 詳細については、次を参照してください。[マッピング MySQL および SQL Server データ型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)します。  
  
## <a name="saving-projects"></a>プロジェクトの保存  
プロジェクトの保存機能は、基本的に、プロジェクトの設定と、オプションでは、データベースのメタデータを SSMA プロジェクト ファイルに保存するユーザーを使用できます。  
  
##### <a name="to-save-a-project"></a>プロジェクトを保存するには  
  
-   **ファイル**メニューの **保存**プロジェクト。  
  
場合は、プロジェクト内のデータベースが変更されたか、変換されていない、SSMA は読み込みおよびメタデータを保存することを求められます。 読み込みとメタデータの保存をオフラインで作業できます。 テクニカル サポート担当者などの他のユーザーに完全なプロジェクト ファイルを送信することもできます。 メタデータを保存する場合は、次の操作を行います。  
  
1.  状態を表示する各データベースに対して**メタデータが不足している**データベース名の横にあるチェック ボックスをオンにします。 メタデータの保存には数分かかる場合があります。 この時点でのメタデータを保存したくない場合は、チェック ボックスをオンされません。  
  
2.  **[保存]** をクリックします。  
  
SSMA は MySQL スキーマを解析し、プロジェクト ファイルにメタデータを保存します。  
  
## <a name="opening-projects"></a>プロジェクトを開く  
プロジェクトを開くときに、MySQL および SQL Server または SQL Azure からに切断されています。 これにより、オフラインで作業できます。 メタデータを更新するには、SQL Server または SQL Azure にデータベース オブジェクトを読み込みます。 データを移行するには、SQL Server または SQL Azure に再接続する必要があります。  
  
##### <a name="to-open-a-project"></a>プロジェクトを開くには  
  
1.  次の手順のいずれかを使用します。  
  
    1.  **ファイル**メニューで、**最近使ったプロジェクト**します。  
  
    2.  開きたいプロジェクトを選択します。  
  
    3.  **ファイル**メニューの **プロジェクトを開く**、.m2ssproj のプロジェクト ファイルの検索、ファイルを選択およびクリックして**オープン**します。  
  
2.  MySQL に再接続するには、**ファイル**メニューの  **MySQL への再接続**します。  
  
3.  上の SQL Server に再接続するには、**ファイル**メニューの  **SQL Server に再接続**します。  
  
4.  上の SQL Azure に再接続する、**ファイル**メニューの  **SQL Azure に再接続します。**  
  
## <a name="next-step"></a>次の手順  
移行プロセスでは、次の手順は[MySQL に接続する&#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>参照  
[MySQL に接続する&#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[SQL Server - Azure SQL DB への移行 MySQL データベース&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[SQL Server に接続する&#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[Azure SQL DB に接続する&#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
