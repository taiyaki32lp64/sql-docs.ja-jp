---
title: SQL Server (MySQLToSQL) への接続 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0ec33e462f1b68d70a86a0fbf4f7cf0214d25770
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103128"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>SQL Server への接続 (MySQLToSQL)
MySQL データベースを SQL Server に移行するには、SQL Server のターゲット インスタンスに接続する必要があります。 接続すると、SSMA は SQL Server のインスタンスのすべてのデータベースに関するメタデータを取得し、SQL Server メタデータ エクスプ ローラーでデータベースのメタデータを表示します。 SSMA は、パスワードは保存されませんに接続している SQL Server のインスタンスの情報を格納します。  
  
SQL Server への接続をプロジェクトを終了するまでアクティブに保ちます。 プロジェクトを再度開くと、サーバーにアクティブに接続する場合に SQL Server に再接続する必要があります。 SQL Server にデータベース オブジェクトを読み込むし、データを移行するまで、オフライン使用できます。  
  
SQL Server のインスタンスに関するメタデータは、自動的に同期されません。 代わりに、SQL Server メタデータ エクスプ ローラー内のメタデータを更新するには、SQL Server のメタデータを手動で更新する必要があります。 詳細については、このトピックの「「SQL Server のメタデータの同期」セクションを参照してください。  
  
## <a name="required-sql-server-permissions"></a>必要な SQL Server のアクセス許可  
SQL Server への接続に使用されるアカウントには、アカウントで実行された操作に応じてさまざまなアクセス許可が必要です。  
  
-   MySQL のオブジェクトに変換する[!INCLUDE[tsql](../../includes/tsql-md.md)]スクリプトの構文は、SQL Server からのメタデータを更新するかに変換された構文を保存する、アカウントは SQL Server のインスタンスにログオンする権限が必要です。  
  
-   最小権限の要件がメンバーシップを SQL Server にデータベース オブジェクトを読み込む、 **db_owner**ターゲット データベースのデータベース ロール。  
  
## <a name="establishing-a-sql-server-connection"></a>SQL Server の接続を確立します。  
MySQL データベースのオブジェクトを SQL Server の構文に変換する前に、または複数の MySQL データベースを移行する SQL Server のインスタンスへの接続を確立する必要があります。  
  
接続のプロパティを定義するときに、オブジェクトとデータを移行するデータベースを指定します。 SQL Server に接続した後は、MySQL スキーマ レベルでは、このマッピングをカスタマイズできます。 詳細については、次を参照してください[MySQL データベースを SQL Server スキーマへのマッピング&#40;MySQLToSQL。&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> SQL Server に接続する前に、SQL Server のインスタンスが実行されていて、接続を受け入れることを確認します。  
  
**SQL Server に接続するには**  
  
1.  **ファイル**メニューの  **SQL サーバーへの接続**(このオプションは、プロジェクトの作成後に有効です)。  
  
    SQL Server に接続した場合、コマンド名になります**SQL Server に再接続**します。  
  
2.  接続ダイアログ ボックスで入力するか、SQL Server のインスタンスの名前を選択します。  
  
    -   ローカル コンピューターの既定のインスタンスに接続する場合は、入力**localhost**またはドット ( **.** )。  
  
    -   別のコンピューターで既定のインスタンスに接続する場合は、コンピューターの名前を入力します。  
  
    -   別のコンピューター上の名前付きインスタンスに接続する場合は、コンピューター名の後に、円記号とし、\myinstance など、インスタンス名を入力します。  
  
3.  SQL Server のインスタンスは、既定以外のポートで接続を受け入れるように構成が場合の SQL Server 接続で使用されるポート番号を入力、**サーバー ポート**ボックス。 SQL Server の既定のインスタンスは既定のポート番号は 1433 です。 名前付きインスタンスの場合は、SSMA を SQL Server Browser サービスからのポート番号の取得を試みます。  
  
4.  **認証**ボックスで、接続に使用する認証の種類を選択します。 現在の Windows アカウントを使用する**Windows 認証**します。 SQL Server ログインを使用するには、SQL Server 認証を選択し、ログイン名とパスワードを入力します。  
  
5.  セキュリティで保護された接続は、2 つのコントロールを追加、**暗号化接続**と**TrustServerCertificate**チェック ボックス。 場合にのみ**暗号化接続**がオンになって、 **TrustServerCertificate**チェック ボックスを表示します。 ときに**暗号化接続**がチェックされます (true) と**TrustServerCertificate**チェック ボックスがオフ (false)、これは SQL Server の SSL 証明書を検証します。 サーバー証明書の検証は、SSL ハンドシェイクの一部であり、接続先のサーバーが適切なサーバーであることを保証します。 これを確実にクライアント側およびサーバー側で、証明書をインストールする必要があります。  
  
6.  [接続] をクリックします。  
  
**高いバージョンの互換性**  
  
以降のバージョンの SQL Server に接続または再接続することができます。  
  
1.  接続できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ときに作成されたプロジェクトは、2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005。  
  
2.  接続できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ときに作成されたプロジェクトは、2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 つまり下位バージョンに接続することはできませんが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
3.  接続できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ときに作成されたプロジェクトは、2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012。  
  
4.  のみに接続できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ときに作成されたプロジェクトは、2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 です。  
  
5.  "SQL Azure"のバージョンの互換性が高いが正しくありません。  
  
||||||||  
|-|-|-|-|-|-|-|  
|**プロジェクトの種類とターゲット サーバーのバージョン**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (バージョン。9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (バージョン。10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012<br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014<br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016<br />(Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|はい|[はい]|[はい]|[はい]|はい||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||はい|[はい]|[はい]|はい||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||はい|[はい]|はい||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||はい|はい||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016|||||はい||  
|SQL Azure||||||はい|  
  
> [!IMPORTANT]  
> データベース オブジェクトの変換が実施しているのバージョンに従っていませんが、プロジェクトの種類に従って、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続します。 場合に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年プロジェクトでは、変換は実行に従って[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 の新しいバージョンに接続している場合でも[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](SQL Server 2008/SQL Server 2012 または SQL Server 2014/SQL Server 2016)。  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL サーバーのメタデータの同期  
SQL Server データベースに関するメタデータは、自動的に更新されません。 SQL Server メタデータ エクスプ ローラー内のメタデータは、最初に、SQL Server に接続されているし、最後を手動でメタデータのスナップショットには、メタデータが更新されました。 すべてのデータベースまたは任意の 1 つのデータベースまたはデータベース オブジェクトのメタデータを手動で更新することができます。  
  
**メタデータを同期するには**  
  
1.  SQL Server に接続していることを確認します。  
  
2.  SQL Server メタデータ エクスプ ローラーで、データベースまたはデータベースのスキーマを更新する横のチェック ボックスを選択します。  
  
    たとえば、すべてのデータベースのメタデータを更新するには、データベースの横にあるボックスを選択します。  
  
3.  データベース、または個々 のデータベースまたはデータベースのスキーマを右クリックし、**データベースと同期する**します。  
  
## <a name="next-step"></a>次の手順  
移行の次の手順は、プロジェクトのニーズによって異なります。  
  
-   MySQL スキーマと SQL Server データベースとスキーマ間のマッピングをカスタマイズするを参照してください[SQL Server スキーマへのマッピングの MySQL データベース&#40;MySQLToSQL。&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   プロジェクトの構成オプションをカスタマイズするを参照してください[プロジェクト オプションの設定&#40;MySQLToSQL。&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   ソースとターゲットのデータ型のマッピングをカスタマイズするを参照してください[マッピング MySQL および SQL Server データ型&#40;MySQLToSQL。&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   これらのタスクを実行する必要はありません場合、MySQL データベースのオブジェクトの定義を SQL Server オブジェクトの定義に変換できます。 詳細については、次を参照してください[MySQL データベースを変換する&#40;MySQLToSQL。&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>関連項目  
[SQL Server - Azure SQL DB への移行 MySQL データベース&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
