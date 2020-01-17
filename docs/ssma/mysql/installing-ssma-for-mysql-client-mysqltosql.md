---
title: SSMA for MySQL クライアント (MySQLToSQL) のインストール |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9dcdeaff1c4782453a9fd57cc709e17ad3200d28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086823"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>SSMA for MySQL クライアントのインストール (MySQLToSQL)
SSMA for MySQL クライアントは、次のタスクを実行するプログラム ファイルで構成されます。  
  
-   MySQL データベースに接続します。  
  
-   インスタンスに接続する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。  
  
-   MySQL データベースのオブジェクトを変換、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のオブジェクト。  
  
-   オブジェクトを読み込む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。  
  
-   データを移行して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。  
  
このトピックでは、インストールの前提条件と SSMA for MySQL クライアントのインストールの手順を提供します。  
  
## <a name="prerequisites"></a>前提条件  
SSMA for MySQL は MySQL 4.1 またはそれ以降のバージョンと SQL Server 2005、SQL Server 2008、SQL Server 2012、SQL Server 2014、SQL Server 2016、SQL Server 2017 および Azure SQL DB のすべてのエディションを使用するために設計されています。  
  
SSMA をインストールする前に、コンピューターが、次の要件を満たしていることを確認します。  
  
-   Windows 7 またはそれ以降のバージョンまたは Windows Server 2008 以降のバージョン。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows インストーラー 3.1 またはそれ以降のバージョン。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]バージョン 4.0 またはそれ以降のバージョン。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]バージョン 4.0 は、SQL Server の製品メディアに収録されています。 取得することも、 [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882)します。  
  
-   MySQL ODBC ドライバーの 5.1 および移行する MySQL データベースへの接続。 MySQL の Web サイトから、MySQL をインストールすることができます。 接続の詳細については、次を参照してください[MySQL に接続する&#40;MySQLToSQL。&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   アクセスと、移行するデータベース オブジェクトとデータの SQL Server のターゲット インスタンスをホストするコンピューターに十分なアクセス許可。 詳細については、次を参照してください[SQL Server に接続する&#40;MySQLToSQL。&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   SQL Azure のプロジェクトが発生した場合へのアクセスと、移行する Azure SQL DB のインスタンスに十分なアクセス許可はデータベース オブジェクトとデータになります。 詳細については、次を参照してください。 [Azure SQL DB に接続する&#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)します。  
  
-   4 GB の RAM を推奨します。  
  
## <a name="installing-ssma-for-mysql-client"></a>SSMA for MySQL クライアントのインストール  
SSMA は、Web からダウンロードします。 最新バージョンをダウンロードするを参照してください。、 [SQL Server Migration Assistant のダウンロード ページ](https://aka.ms/ssmaformysql)します。  
  
最新バージョンをダウンロードした後は、SSMA をインストールする前に、インストール ファイルを抽出する必要があります。  
  
**SSMA クライアントをインストールするには**  
  
1.  SSMA for MySQL をダブルクリックします*n*します。Install.exe、場所*n*ビルド番号です。  
  
2.  [ようこそ] ページで、次のようにクリックします。**次**します。  
  
    前提条件がインストールされていない場合は、必要なコンポーネントをインストールする必要がありますまずを示すメッセージが表示されます。 インストール プログラムをもう一度実行する前にすべての前提条件をインストールしたことを確認します。  
  
3.  エンド ユーザー ライセンス契約を読みます。 同意する場合は、選択 **、使用許諾契約書に同意**、順にクリックします**次**します。  
  
4.  セットアップの種類の選択 ページで、次のようにクリックします。**標準**します。  
  
5.  **[インストール]** をクリックします。  
  
> [!IMPORTANT]  
> 1.  新しいバージョンをインストールする前に、MySQL の SSMA のすべての旧バージョンをアンインストールしてください。  
  
既定のインストール場所は C:\Program files \microsoft SQL Server Migration Assistant for MySQL です。  
  
64 ビットの Windows マシン for MySQL C:\Microsoft SQL Server Migration Assistant で、製品のインストールします。  
  
## <a name="see-also"></a>参照  
[SQL Server - Azure SQL DB への移行 MySQL データベース&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
