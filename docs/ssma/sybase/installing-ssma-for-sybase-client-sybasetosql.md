---
title: SSMA for Sybase クライアント (SybaseToSQL) のインストール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8680685640b234e47f6e68d7fb802fc7e2f5d81c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029023"
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>SSMA for Sybase クライアントのインストール (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) のデータベース サーバーとのインスタンスへの接続に使用されるプログラム ファイルから成る SSMA クライアント[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB、ASE データベース オブジェクトを変換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB の構文、読み込み、オブジェクトに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB へのデータを移行および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQLDB します。  
  
このトピックでは、インストールの前提条件との SSMA のインストール手順を説明します。  
  
## <a name="prerequisites"></a>前提条件  
SSMA が ASE 11.9.2 または以降のバージョンとのすべてのエディションを使用するように設計[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
SSMA をインストールする前に、コンピューターが、次の要件を満たしていることを確認します。  
  
-   Windows 7 またはそれ以降のバージョンまたは Windows Server 2008 以降のバージョン。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows インストーラー 3.1 またはそれ以降のバージョン。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework バージョン 4.0 またはそれ以降のバージョン。 .NET Framework バージョン 4.0 で使用できる、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]製品メディア。 取得することも、 [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882)します。  
  
-   Sybase OLEDB/ADO.Net/ODBC プロバイダーと、データベースが含まれている Sybase ASE データベース サーバーへの接続を移行します。 プロバイダーは、Sybase ASE の製品メディアからインストールできます。 接続の詳細については、次を参照してください。 [Sybase ASE への接続&#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)します。  
  
-   アクセスとのターゲット インスタンスをホストするコンピューターに十分なアクセス許可[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB が、移行するデータベース オブジェクトとデータ。 詳細については、次を参照してください。 [SQL Server に接続する&#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)/[Azure SQL DB に接続する&#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)します。  
  
-   4 GB の RAM を推奨します。  
  
## <a name="installing-the-ssma-for-sybase-client"></a>Sybase クライアント用の SSMA のインストール  
SSMA は、Web からダウンロードします。 最新バージョンをダウンロードするを参照してください。、 [SQL Server Migration Assistant のダウンロード ページ](https://aka.ms/ssmaforsybase)します。  
  
最新バージョンをダウンロードした後は、SSMA をインストールする前からインストール ファイルを抽出する必要があります。  
  
**SSMA クライアントをインストールするには**  
  
1.  SSMA for Sybase をダブルクリックします*n*します。Install.exe、場所*n*ビルド番号です。  
  
2.  [ようこそ] ページで、次のようにクリックします。**次**します。  
  
    前提条件がインストールされていない場合に必要なコンポーネントをインストールする必要がありますまずを示すメッセージが表示されます。 すべての前提条件をインストールし、インストール プログラムをもう一度実行してください。  
  
3.  エンド ユーザー ライセンス契約を読みます。 同意する場合は、選択 **、使用許諾契約書に同意**、順にクリックします**次**します。  
  
4.  セットアップの種類の選択 ページで、次のようにクリックします。**標準**します。  
  
5.  **[インストール]** をクリックします。  
  
> [!IMPORTANT]  
> 1.  新しいバージョンをインストールする前に、Sybase の SSMA のすべての旧バージョンをアンインストールしてください。  
  
既定のインストール場所は C:\Program files \microsoft SQL Server Migration Assistant for Sybase します。  
  
SSMA のプログラム ファイルだけでなくもにインストールする必要 SSMA for Sybase の拡張機能の Pack[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。 [SQL Server での SSMA コンポーネントのインストール&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server での SSMA コンポーネントのインストール&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[SQL Server - Azure SQL DB への Sybase ASE データベース移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
