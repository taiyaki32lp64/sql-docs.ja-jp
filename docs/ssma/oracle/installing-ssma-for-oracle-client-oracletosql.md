---
title: SSMA for Oracle クライアント (OracleToSQL) のインストール |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: fc295e108357040617bf6bdaa1af61fada2c97ee
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68259678"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>SSMA for Oracle クライアントのインストール (OracleToSQL)
SSMA クライアントは、次のタスクを実行するプログラム ファイルで構成されます。  
  
-   Oracle データベースに接続します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続する。  
  
-   Oracle データベースのオブジェクトを変換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文。  
  
-   オブジェクトを読み込む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
-   データを移行して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
このトピックでは、インストールの前提条件との SSMA のインストール手順を説明します。  
  
## <a name="prerequisites"></a>前提条件  
SSMA は、Oracle 9 またはそれ以降のバージョンとのすべてのエディションを使用するように設計[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
SSMA をインストールする前に、コンピューターが、次の要件を満たしていることを確認します。  
  
-   Windows 7 またはそれ以降のバージョンまたは Windows Server 2008 以降のバージョン。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows インストーラー 3.1 またはそれ以降のバージョン。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]バージョン 4.0 またはそれ以降のバージョン。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]バージョン 4.0 は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]製品メディア。 取得することも、 [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882)します。  
  
-   Oracle クライアント 9.0 または以降のバージョンと移行する Oracle データベースへの接続。 Oracle クライアントのバージョンと、同じバージョンまたは Oracle データベースのバージョンより新しいバージョンである必要があります。  
  
    Oracle の製品メディアまたは Oracle の Web サイトから Oracle クライアントをインストールすることができます。 接続の詳細については、次を参照してください。 [Oracle データベースに接続する&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)します。  
  
-   アクセスとのターゲット インスタンスをホストするコンピューターに十分なアクセス許可[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB が、移行するデータベース オブジェクトとデータ。 詳細については、次を参照してください。 [SQL Server に接続する&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)します。  
  
-   4 GB の RAM を推奨します。  
  
## <a name="installing-the-ssma-for-oracle-client"></a>Oracle クライアント用の SSMA のインストール  
SSMA は、Web からダウンロードします。 最新バージョンをダウンロードするを参照してください。、 [SQL Server Migration Assistant のダウンロード ページ](https://aka.ms/ssmafororacle)します。  
  
最新バージョンをダウンロードした後は、SSMA をインストールする前からインストール ファイルを抽出する必要があります。  
  
**SSMA クライアントをインストールするには**  
  
1.  SSMA for Oracle をダブルクリックします*n*します。Install.exe、場所*n*ビルド番号です。  
  
2.  [ようこそ] ページで、次のようにクリックします。**次**します。  
  
    前提条件がインストールされていない場合に必要なコンポーネントをインストールする必要がありますまずを示すメッセージが表示されます。 すべての前提条件をインストールし、インストール プログラムをもう一度実行してください。  
  
3.  エンド ユーザー ライセンス契約を読みます。 同意する場合は、選択 **、使用許諾契約書に同意**、順にクリックします**次**します。  
  
4.  セットアップの種類の選択 ページで、次のようにクリックします。**標準**します。  
  
5.  **[インストール]** をクリックします。  
  
> [!IMPORTANT]  
> 1.  SSMA for Oracle のすべての旧バージョンを新しいバージョンをインストールする前にアンインストールしてください。  
  
既定のインストール場所は C:\Program files \microsoft SQL Server Migration Assistant for Oracle です。  
  
SSMA のプログラム ファイルだけでなく必要がありますにもインストール SSMA for Oracle の拡張機能パック[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。 [SQL Server での SSMA コンポーネントのインストール&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server での SSMA コンポーネントのインストール&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[SQL Server にデータベースを移行する Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
