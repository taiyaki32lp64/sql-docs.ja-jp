---
title: Sybase ASE (SybaseToSQL) への接続 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: e1debb31cd70c73e3fecd569a58534377742a9a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948524"
---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>Sybase ASE への接続 (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) のデータベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure では、移行するデータベースを含むアダプティブ サーバーに接続する必要があります。 接続するときに、SSMA はアダプティブ サーバー上のすべてのデータベースに関するメタデータを取得し、Sybase メタデータ エクスプ ローラー ウィンドウでデータベースのメタデータを表示します。 SSMA は、データベース サーバーに関する情報を格納しますが、パスワードは保存されません。  
  
プロジェクトを閉じるまで ASE への接続をアクティブに保ちます。 プロジェクトを再度開くと、アクティブなサーバーに接続する場合 ASE に再接続する必要があります。  
  
アダプティブ サーバーに関するメタデータは、自動的に更新されません。 代わりに、Sybase メタデータ エクスプ ローラーでメタデータを更新する場合は、する必要があります手動で更新するメタデータは、このトピックの後半の「Sybase ASE メタデータの更新」セクションで説明しました。  
  
## <a name="required-ase-permissions"></a>ASE が必要なアクセス許可  
ASE への接続に使用されるアカウントが少なくとも必要**パブリック**に移行するすべてのソース データベースおよび master データベースにアクセスできる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 さらに、移行対象のテーブルに対するアクセス許可を選択するユーザー SELECT 権限が必要で、次のシステム テーブル。  
  
-   [source_db].dbo.sysobjects  
  
-   [source_db].dbo.syscolumns  
  
-   [source_db].dbo.sysusers  
  
-   [source_db].dbo.systypes  
  
-   [source_db].dbo.sysconstraints  
  
-   [source_db].dbo.syscomments  
  
-   [source_db].dbo.sysindexes  
  
-   [source_db].dbo.sysreferences  
  
-   master.dbo.sysdatabases  
  
## <a name="establishing-a-connection-to-ase"></a>ASE への接続を確立します。  
アダプティブのサーバーに接続するときに、SSMA はデータベース サーバーでデータベース メタデータを読み取り、プロジェクト ファイルにこのメタデータを追加します。 オブジェクトを変換するときに、このメタデータを SSMA によって使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure の構文にデータを移行するときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 Sybase メタデータ エクスプ ローラー ウィンドウでこのメタデータを参照して、個々 のデータベース オブジェクトのプロパティを確認できます。  
  
> [!IMPORTANT]  
> データベース サーバーに接続することを確認する前に、データベース サーバーが実行されていると、接続を受け入れることができます。  
  
**Sybase ASE に接続するには**  
  
1.  **ファイル**メニューの  **Sybase への接続**します。  
  
    Sybase へ接続されていた場合、コマンド名になります**Sybase への再接続**します。  
  
2.  **プロバイダー**ボックスに、Sybase サーバーに接続するコンピューターにインストールされているプロバイダーのいずれかを選択します。  
  
3.  **モード**ボックスで、いずれかを選択**標準モード**または**高度なモード**します。  
  
    標準モードを使用すると、サーバー名、ポート、ユーザー名、およびパスワードを指定します。 接続文字列を指定するのにには、高度なモードを使用します。 このモードは通常、トラブルシューティングや技術的なサポートの使用にのみ使用します。  
  
4.  選択した場合**標準モード**、次の値を指定します。  
  
    1.  **サーバー名**ボックスで、入力するか、またはデータベース サーバーの IP アドレスを選択します。  
  
    2.  既定値が (5000) のポートでの Sybase 接続に使用されるポート番号を入力の接続を受け入れるように、データベース サーバーが構成されていない場合、**サーバー ポート**ボックス。  
  
    3.  **ユーザー名**ボックスに、必要なアクセス許可のある Sybase アカウントを入力します。  
  
    4.  **パスワード**ボックスに、指定されたユーザー名のパスワードを入力します。  
  
5.  選択した場合**高度なモード**での接続文字列を指定、**接続文字列**ボックス。  
  
    別の接続文字列の例は次のとおりです。  
  
    1.  **Sybase OLE DB プロバイダーの接続文字列:**  
  
        Sybase ASE OLE DB 12.5 の接続文字列の例のとおりです。  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Sybase ASE OLE DB、15 の接続文字列の例のとおりです。  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Sybase ODBC プロバイダーの接続文字列:**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Sybase ADO.NET プロバイダーの接続文字列:**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    詳細については、次を参照してください。 [Sybase への接続&#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)します。  
  
## <a name="reconnecting-to-sybase-ase"></a>Sybase ASE への再接続  
プロジェクトを閉じるまで、データベース サーバーへの接続をアクティブに保ちます。 プロジェクトを再度開くと、アダプティブ サーバーにアクティブに接続する場合を再接続する必要があります。 メタデータを更新するには、データベース オブジェクトに読み込む必要になるまでオフラインで作業できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のデータを移行します。  
  
## <a name="refreshing-sybase-ase-metadata"></a>Sybase ASE メタデータの更新  
ASE のデータベースについてのメタデータは、自動的に更新されません。 Sybase メタデータ エクスプ ローラー内のメタデータは、アダプティブ サーバー、または前回のメタデータを手動で更新することに初めて接続されたときのメタデータのスナップショットです。 1 つのデータベース、1 つのデータベース スキーマ、またはすべてのデータベースのメタデータを手動で更新することができます。  
  
**メタデータを更新するには**  
  
1.  適応型のサーバーに接続していることを確認します。  
  
2.  Sybase メタデータ エクスプ ローラーでは、データベースまたはデータベースのスキーマを更新する横のチェック ボックスを選択します。  
  
3.  データベースまたは個々 のデータベースまたはデータベースのスキーマを右クリックし、**データベースからの更新**します。  
  
4.  現在のオブジェクトを確認するメッセージが表示されたら、クリックして**はい**します。  
  
## <a name="next-step"></a>次の手順  
  
-   移行プロセスの次の手順が、 [SQL Server のインスタンスへの接続](connecting-to-sql-server-sybasetosql.md) / [SQL Azure のインスタンスに接続します。](connecting-to-azure-sql-db-sybasetosql.md)  
  
## <a name="see-also"></a>参照  
[SQL Server - Azure SQL DB への Sybase ASE データベース移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
