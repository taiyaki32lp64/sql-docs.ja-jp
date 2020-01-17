---
title: SQL Server (SybaseToSQL) での SSMA コンポーネントのインストール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1fbc3a8f74b21bd5a53bdd874b5c41ef522e29f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029008"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>SQL Server での SSMA コンポーネントのインストール (SybaseToSQL)
に加えて、サーバー側のデータ移行を使用するため、SSMA をインストールする必要がありますもコンポーネントをインストールするを実行しているコンピューターで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 これらのコンポーネントには、データの移行、およびサーバー間の接続を有効にする Sybase プロバイダーをサポートする SSMA 拡張パックが含まれます。  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA for Sybase 拡張パック  
SSMA の拡張機能パックでは、データベースを追加します。 **sysdb**と**ssmatesterdb_syb**、のインスタンスを指定する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 **Sysdb**データベースには、テーブルとデータを移行するために必要なストアド プロシージャが含まれています。 **Ssmatester_syb**データベースにはスキーマが含まれています**ssma_sybase_utilities**、SSMA テスター コンポーネントによって使用されるオブジェクト (テーブル、トリガー、ビュー) が作成されました。  
  
データを移行する場合にも、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA 作成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント ジョブのデータを移行するサーバー側のデータ移行のエンジンを使用するとします。  
  
### <a name="installing-the-extension-pack"></a>拡張機能パックをインストールします。  
拡張機能パックをインストールするとデータを移行する前にいつ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
> [!IMPORTANT]  
> 拡張機能パックをインストールするには、インスタンスで sysadmin サーバー ロールのメンバーである[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
**拡張機能パックをインストールするには**  
  
1.  Sybase の拡張機能パックには、SSMA をコピーします。*n*します。Install.exe、場所*n*を実行しているコンピューターに、ビルド番号は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
2.  Sybase の拡張機能パックには、SSMA をダブルクリックします。*n*します。Install.exe します。  
  
3.  [ようこそ] ページで、次のようにクリックします。**次**します。  
  
4.  使用許諾契約書 ページで、ライセンス契約を読みます。 同意する場合は、選択、 **、使用許諾契約書に同意**チェック ボックスをオンにし**次**。  
  
5.  セットアップの種類の選択 ページで、次のようにクリックします。**標準**します。  
  
6.  準備完了 [インストール] ページで、をクリックして**インストール**します。  
  
7.  最初のステップのインストール ページの完了 で、をクリックして**次**します。  
  
    インスタンスを選択する、新しいダイアログ ボックスが表示されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の拡張機能パックのインストール。  
  
8.  インスタンスを選択[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、ASE のデータベースの移行およびする をクリックし、**次**。  
  
    既定のインスタンスには、コンピューターと同じ名前があります。 名前付きインスタンスの後に、円記号とインスタンス名が指定されます。  
  
9. 接続パラメーター] ページで、[認証方法を選択してクリックして**次**します。  
  
    Windows 認証は、Windows 資格情報を使用してのインスタンスにログオンしようとする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 選択した場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を入力する必要があります、認証、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログイン名とパスワード。  
  
10. サーバーの管理 ページで、次のように選択します。**ユーティリティ データベースのインストール** *n*ここで、 *n* 、バージョン番号は、順にクリックします**次**します。  
  
    **Sysdb**データベースが作成され、そのデータベースにストアド プロシージャが作成されます。  
  
    場合**テスター データベースのインストール**オプションがオンになって、テスト担当者**ssmatesterdb_syb**データベースが作成されます。  
  
11. 別のインスタンスにユーティリティをインストールする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を選択します**インスタンスを返す**、順にクリックします**次**します。 または、をクリックしてウィザードを終了するには、**終了**します。  
  
### <a name="sql-server-database-objects"></a>SQL Server データベース オブジェクト  
拡張機能パックをインストールした後を参照してください、 **ssma_syb.bcp_migration_packages**テーブルに、 **sysdb**データベース。 次のストアド プロシージャも表示されます。  
  
-   **bcp_clean_migration_data**  
  
-   **bcp_ensure_message_table**  
  
-   **bcp_insert_new_message**  
  
-   **bcp_post_process**  
  
-   **bcp_read_new_migration_messages**  
  
-   **bcp_save_migration_package**  
  
-   **bcp_smart_truncate**  
  
-   **bcp_start_migration_process**  
  
-   **get_jobstep_info**  
  
-   **stop_agent_process**  
  
データを移行するたびに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA を作成、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント ジョブ。 これらのジョブの名前は**ssma_syb データ移行パッケージ {GUID}** に表示し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のエージェント ノード[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Jobs フォルダーでします。  
  
## <a name="sybase-providers"></a>Sybase プロバイダー  
ASE からのデータを移行する場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ASE の間で直接 SQL Azure、データの移行と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure です。 データの移行が遅くなりますこのため、SSMA を通過にしません。  
  
### <a name="installing-the-sybase-providers"></a>Sybase プロバイダーをインストールします。  
次の手順は、Sybase のプロバイダーをインストールするための基本的なインストール手順を提供します。 正確な手順については、Sybase のセットアップ プログラムのバージョンによって異なります。  
  
> [!IMPORTANT]  
> セットアップ プログラムを実行する前に、ライセンス契約に違反していないことを確認します。  
  
1.  Sybase ASE のセットアップ プログラムを実行します。  
  
2.  カスタム セットアップを選択します。  
  
3.  [機能の選択] ページで、ODBC、OLE DB および ADO.NET データ プロバイダーを選択します。  
  
4.  選択した機能を確認し、をクリックし、**完了**データ プロバイダーをインストールします。  
  
## <a name="see-also"></a>関連項目  
[SSMA for Sybase クライアントのインストール&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[SQL Server - Azure SQL DB への Sybase ASE データベース移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
