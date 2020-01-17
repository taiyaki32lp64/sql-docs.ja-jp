---
title: SQL Server (MySQLToSql) での SSMA コンポーネントのインストール |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 64040f4a0caf8253e6d6e8a3b00ff21e0cebe6d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075348"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>SQL Server での SSMA コンポーネントのインストール (MySQLToSql)
SSMA のインストール、に加えて必要がありますもコンポーネントをインストールする実行しているコンピューターで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 これらのコンポーネントには、データの移行、およびサーバー間の接続を有効に MySQL プロバイダーをサポートする SSMA 拡張パックが含まれます。  
  
## <a name="ssma-for-mysql-extension-pack"></a>SSMA for MySQL の拡張機能パック  
SSMA の拡張機能パックでは、データベースを追加します。 **sysdb**、のインスタンスを指定する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 このデータベースには、テーブルとデータを移行するために必要なストアド プロシージャが含まれています。  
  
データを移行する場合にも、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA 作成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント ジョブ、データを移行するサーバー側のデータ移行のエンジンを使用する場合。  
  
### <a name="prerequisites"></a>必須コンポーネント  
SSMA for MySQL サーバーのコンポーネントをインストールする前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]コンピューターが、次の要件を満たしていることを確認します。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows インストーラー 3.1 またはそれ以降のバージョン。  
  
-   MySQL クライアント プロバイダーとを移行する MySQL データベースに接続します。 MySQL 製品メディアまたは MySQL の Web サイトからプロバイダーをインストールすることができます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスをインストール中に実行する必要があります。 インスタンスの一覧を設定するために使用がこの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]セットアップ ウィザードでします。 無効にすることができます、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスのインストール後にします。  
  
    > [!NOTE]  
    > 場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスが実行されているが、まだ、セットアップでインスタンスの一覧表示されない、UDP ポート 1434 のブロックを解除する必要があります。 Windows ファイアウォールを使用するには、ポートに一時的にブロックを解除するか、Windows ファイアウォールを一時的に無効にすることができます。 ウイルス対策ソフトウェアを一時的に無効にすることもあります。 インストール後にファイアウォールやウイルス対策ソフトウェアを有効にしてください。  
  
### <a name="installing-the-extension-pack"></a>拡張機能パックをインストールします。  
拡張機能パックをインストールするとデータを移行する前にいつ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
> [!IMPORTANT]  
> 拡張機能パックをインストールするには、メンバーである、 **sysadmin**サーバー ロールのインスタンスを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
**拡張機能パックをインストールするには**  
  
1.  MySQL の拡張機能パックには、SSMA をコピーします。*n*します。Install.exe、場所*n*を実行しているコンピューターに、ビルド番号は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
2.  MySQL の拡張機能パックには、SSMA をダブルクリックします。*n*します。Install.exe します。  
  
3.  [ようこそ] ダイアログ ボックスで、次のようにクリックします。**次**します。  
  
4.  [使用許諾契約書] ダイアログ ボックスで、ライセンス契約を読みます。 同意する場合は、選択、 **、使用許諾契約書に同意**チェック ボックスをオンにし**次**。  
  
5.  [セットアップの種類の選択] ダイアログ ボックスで、次のようにクリックします。**標準**します。  
  
6.  インストール ダイアログ ボックスの準備完了、 をクリックして**インストール**します。  
  
7.  完了、最初のステップのインストール ダイアログ ボックスで、をクリックして**次**します。  
  
    インスタンスを選択する、新しいダイアログ ボックスが表示されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の拡張機能パックのインストール。  
  
8.  インスタンスを選択[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]する MySQL のスキーマを移行してする順にクリックします**次**します。  
  
    既定のインスタンスには、コンピューターと同じ名前があります。 名前付きインスタンスの後に、円記号とインスタンス名が指定されます。  
  
9. [接続] ダイアログ ボックスで、認証方法を選択し、**次**します。  
  
    Windows 認証は、Windows 資格情報を使用してのインスタンスにログオンしようとする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 選択した場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を入力する必要があります、認証、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログイン名とパスワード。  
  
10. 次のダイアログ ボックスで次のように選択します。**インストール ユーティリティ データベース** *n*ここで、 *n* 、バージョン番号は、順にクリックします **[次へ]** します。  
  
    **Sysdb**テーブルとデータベースが作成され、そのデータベースに (サーバー側のデータ移行のエンジンを使用して) データの移行に必要なストアド プロシージャが作成されます。  
  
11. 別のインスタンスにユーティリティをインストールする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を選択します**はい**、順にクリックします**次**します。 または、をクリックしてウィザードを終了するには、**いいえ**します。  
  
## <a name="see-also"></a>関連項目  
[SSMA for MySQL クライアントのインストール&#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[SQL Server - Azure SQL DB への移行 MySQL データベース&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
