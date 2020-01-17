---
title: アクセスのための SQL Server Migration Assistant のインストール (アクセス可能な SQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- installing SSMA
- instructions, installation
- instructions, upgrade
- licensing SSMA
- prerequisites for installing SSMA
- procedure, installation
- procedure, licensing
- procedure, upgrading
- removing SSMA
- Setup
- uninstalling SSMA
- upgrading SSMA
ms.assetid: dd50eebd-75df-4e0d-8c4d-88b511aae4c7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 80fc19b17ac1c01f0c57d828a3bc4821050f761d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257892"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>アクセスのための SQL Server Migration Assistant のインストール (アクセス可能な SQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Access の Migration Assistant (ssma) は、Windows インストーラーベースのウィザードを使用してインストールされます。 このトピックでは、インストールの前提条件、SSMA の最新バージョンへのリンク、SSMA のインストール、ライセンス、アンインストール、およびアップグレードの手順について説明します。  
  
## <a name="prerequisites"></a>前提条件  
SSMA をインストールする前に、システムが次の要件を満たしていることを確認してください。  
  
-   Windows 7 以降のバージョン、または Windows Server 2008 以降のバージョン。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows インストーラー3.1 以降のバージョン。  
  
-   .NET Framework [!INCLUDE[msCoName](../../includes/msconame_md.md)]バージョン4.0 以降のバージョン。 .NET Framework バージョン4.0 は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]製品ディスクと、 [Microsoft .NET ガイド](https://docs.microsoft.com/dotnet/framework/)の情報を使用して入手できます。
  
-   にアクセスし、データベースオブジェクトとデータの移行先となる、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure DB のターゲットインスタンスをホストするコンピューターに対する十分なアクセス許可を付与します。  
  
-   Microsoft Data Access Object (DAO) プロバイダーバージョン12.0 または14.0。 Microsoft Office 2010/2007 製品から DAO プロバイダーをインストールするか、Microsoft web サイトからダウンロードすることができます。  
  
-   SQL Azure への移行については、SQL Server ネイティブアクセスクライアント (SNAC) バージョン10.5 以降。 最新バージョンの SNAC は、 [Microsoft® SQL Server® 2008 R2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=16978)から入手できます。  
  
-   4 GB の RAM (推奨)。  
  
## <a name="installing-ssma"></a>SSMA のインストール  
SSMA は Web からダウンロードできます。 最新バージョンをダウンロードするには、 [SQL Server Migration Assistant のダウンロードページ](https://aka.ms/ssmaforaccess)を参照してください。  
  
最新バージョンをダウンロードした後は、SSMA をインストールする前にからインストールファイルを抽出する必要があります。

> [!IMPORTANT]  
> -   新しいバージョンをインストールする前に、アクセスするために SSMA の以前のバージョンをすべてアンインストールしてください。  
  
**SSMA をインストールするには**  
  
1.  SSMA for Access *n*をダブルクリックします。 *n*はビルド番号です。  
  
2.  [ようこそ] ページで **[次へ]** をクリックします。  
  
    前提条件がインストールされていない場合は、最初に必要なコンポーネントをインストールする必要があることを示すメッセージが表示されます。 すべての前提条件がインストールされていることを確認してから、インストールプログラムを再実行してください。  
  
3.  使用許諾契約書をお読みください。同意する場合は、 **[同意する] を選択し**、[**次へ**] をクリックします。  
  
4.  [セットアップの種類の選択] ページで、[**標準**] をクリックします。  
  
5.  
  **[インストール]** をクリックします。  
  
既定のインストール場所は、Access の場合は C:\Program の SQL Server Migration Assistant です。  
  
## <a name="uninstalling-ssma-for-access"></a>SSMA をアンインストールしてアクセスできるようにする  
コントロールパネルの [**プログラムの追加と削除**] を使用して ssma をアンインストールします。 プログラムをアンインストールしても、SSMA プロジェクトファイルまたはログファイルは削除されないことに注意してください。  
  
**SSMA をアンインストールするには**  
  
1.  [**スタート**]、[**コントロール パネル**]、[**プログラムの追加と削除**] の順にクリックします。  
  
2.  [**アクセス] に Microsoft SQL Server Migration Assistant**を選択し、[**削除**] をクリックします。  
  
## <a name="upgrading-to-a-later-version"></a>新しいバージョンへのアップグレード  
Access 用に新しいバージョンの SSMA にアップグレードする場合は、まず SSMA をアンインストールしてから新しいバージョンをインストールする必要があります。 SSMA for Access のアンインストールに関するセクションの手順に従って、このプロセスを完了します。  
  
SSMA の以前のバージョンで作成したプロジェクトを開くと、プロジェクトを新しいバージョンに変換するかどうかを確認するメッセージが表示されます。 新しいバージョンの SSMA でプロジェクトを使用する場合は、[**はい**] をクリックします。  
  
## <a name="see-also"></a>参照  
[Access データベースの移行の準備](preparing-access-databases-for-migration-accesstosql.md)  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Access アプリケーションの SQL Server へのリンク](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
