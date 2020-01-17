---
title: SQL Server (AccessToSQL) への接続 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- authentication
- instance of SQL Server
- metadata, refreshing
- ports
- refreshing metadata
- spaces in database names
- special characters
- SQL Server
- SQL Server, connecting
- SQL Server, connecting to
- SQL Server, reconnecting
ms.assetid: f84cf007-ddf1-4396-a07c-3e0729abc769
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 4630ae8d92dbf0e9b1c5bf615dd82d436a5751f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006649"
---
# <a name="connecting-to-sql-server-accesstosql"></a>SQL Server (AccessToSQL) への接続
Access データベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のターゲット インスタンスに接続する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 SSMA がのインスタンス内のデータベースに関するメタデータを取得して接続すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でデータベースのメタデータを表示および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラー。 SSMA のインスタンスに関する情報を格納する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が、接続先は、パスワードを保存しないことです。  
  
SQL Server への接続をプロジェクトを終了するまでアクティブに保ちます。 プロジェクトを再度開くと、サーバーにアクティブに接続する場合に SQL Server に再接続する必要があります。 SQL Server にデータベース オブジェクトを読み込むし、データを移行するまで、オフライン使用できます。  
  
SQL Server のインスタンスに関するメタデータは、自動的に同期されません。 代わりに、SQL Server メタデータ エクスプ ローラー内のメタデータを更新するには、SQL Server のメタデータを手動で更新する必要があります。 詳細については、このトピックの「「SQL Server のメタデータの同期」セクションを参照してください。  
  
## <a name="required-sql-server-permissions"></a>必要な SQL Server のアクセス許可  
接続に使用されるアカウント[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]そのアカウントで実行されるアクションに応じて、さまざまなアクセス許可が必要です。  
  
-   アクセス オブジェクトに変換する[!INCLUDE[tsql](../../includes/tsql-md.md)]からメタデータを更新する構文、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、か、アカウントをスクリプトに変換された構文を保存するのインスタンスにログインする権限を持って必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
-   データベース オブジェクトに読み込むために[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]とデータを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、アクセス許可の最小要件は、メンバーシップ、 **db_owner**ターゲット データベースのデータベース ロール。  
  
## <a name="establishing-a-sql-server-connection"></a>SQL Server の接続を確立します。  
Access データベースのオブジェクトに変換する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文のインスタンスへの接続を確立する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を Access データベースを移行します。  
  
接続のプロパティを定義するときに、オブジェクトとデータを移行するデータベースを指定します。 接続した後、データベース レベルのアクセスには、このマッピングをカスタマイズできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。[マッピング ソースとターゲット データベース](mapping-source-and-target-databases-accesstosql.md)します。  
  
> [!IMPORTANT]  
> 接続する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、ことを確認のインスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が実行されていると、接続を受け入れることができます。 詳細については、次を参照してください。"への接続、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース エンジン"で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
**SQL Server に接続するには**  
  
1.  **ファイル**メニューの  **SQL サーバーへの接続**します。  
  
    以前に接続されている場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、コマンドの名前になります**SQL Server に再接続**します。  
  
2.  **サーバー名**ボックス、入力のインスタンスの名前を選択するか[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
    -   ローカル コンピューターの既定のインスタンスに接続する場合は、入力**localhost**またはドット ( **.** )。  
  
    -   別のコンピューターで既定のインスタンスに接続する場合は、コンピューターの名前を入力します。  
  
    -   名前付きインスタンスに接続する場合は、コンピューター名、バック スラッシュ、およびインスタンス名を入力します。 以下に例を示します。\Myinstance します。  
  
    -   アクティブなユーザー インスタンスに接続する[!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]、名前付きパイプを使用して接続プロトコルと、パイプ名を指定するよう\\ \\.\pipe\sql\query します。 詳細については、[!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] のドキュメントを参照してください。  
  
3.  場合、インスタンスの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]既定以外のポートで接続を受け入れる、使用されるポート番号を入力するように構成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内の接続、**サーバー ポート**ボックス。 既定のインスタンスの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]既定のポート番号は 1433 です。 名前付きインスタンスは、SSMA は、ポート番号の取得を試みます、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービス。  
  
4.  **データベース**ボックスに、オブジェクトとデータの移行のターゲット データベースの名前を入力します。  
  
    このオプションに再接続する場合は使用できません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
    ターゲット データベース名には、スペースや特殊文字を含めることはできません。 Access データベースを移行するなど、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "abc"という名前のデータベース。 Access データベースを移行することはできませんが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "、b、c"という名前のデータベース。  
  
    接続した後は、データベースごとには、このマッピングをカスタマイズできます。 詳細については、次を参照してください[マッピング ソースとターゲット データベース。](mapping-source-and-target-databases-accesstosql.md)  
  
5.  **認証**ドロップダウン メニューで、接続に使用する、認証の種類を選択します。 現在の Windows アカウントを使用する**Windows 認証**します。 使用する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインで、 **SQL Server 認証**、およびユーザー名とパスワードを入力します。  
  
6.  セキュリティで保護された接続は、2 つのコントロールを追加、**暗号化接続**チェック ボックスと**TrustServerCertificate**チェック ボックスをオンします。 場合にのみ**暗号化接続**チェック ボックスをオン**TrustServerCertificate**チェック ボックスが表示されます。 ときに**暗号化接続**checked(true) と**TrustServerCertificate** unchecked(false) は、SQL Server の SSL 証明書を検証します。 サーバー証明書の検証は、SSL ハンドシェイクの一部であり、接続先のサーバーが適切なサーバーであることを保証します。 これを確実にクライアント側およびサーバー側で、証明書をインストールする必要があります。  
  
7.  **[接続]** をクリックします。  
  
**高いバージョンの互換性**  
  
以降のバージョンの SQL Server に接続または再接続することができます。  
  
1.  作成したプロジェクトが SQL Server 2005、SQL Server 2008 または SQL Server 2012 に接続することができます。  
  
2.  作成したプロジェクトは SQL Server 2008 ですが、下位バージョンの SQL Server 2005 つまりへの接続に許可されていない場合は、SQL Server 2012 に接続することができます。  
  
3.  作成したプロジェクトが SQL Server 2012、SQL Server 2012 のみに接続することができます。  
  
4.  SQL Azure の高いバージョンの互換性が正しくありません。  
  
||||||||
|-|-|-|-|-|-|-|
|**プロジェクトの種類とターゲット サーバーのバージョン**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 (バージョン。9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 (バージョン。10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 (Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 (Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 (Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|はい|[はい]|[はい]|[はい]|はい||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||はい|[はい]|[はい]|はい||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||はい|[はい]|はい||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||||はい|はい||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||はい||
|SQL Azure||||||はい|
  
> [!IMPORTANT]  
> データベース オブジェクトの変換は、接続して SQL Server のバージョンに従っていませんが、プロジェクトの種類に従ってに行われます。 SQL Server 2005 のプロジェクトが発生した場合の変換はに従って SQL Server 2005 以上のバージョンの SQL Server (SQL Server 2008/SQL Server 2012 または SQL Server 2014/SQL Server 2016) に接続している場合でも実行されます。  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL サーバーのメタデータの同期  
場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマを変更する接続した後、サーバーと、メタデータを同期することができます。  
  
**SQL Server のメタデータを同期するには**  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーで、右クリック**データベース**、し、**データベースと同期する**です。  
  
## <a name="reconnecting-to-sql-server"></a>SQL Server に再接続  
接続を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロジェクトを終了するまでアクティブに保ちます。 プロジェクトを開くときにに再接続する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]する場合は、サーバーにアクティブに接続します。 データベース オブジェクトが読み込まれるまでオフラインで作業できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]しデータを移行します。  
  
再接続プロシージャ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]接続を確立するための手順と同じです。  
  
## <a name="next-steps"></a>次の手順  
ソースとターゲット データベースの間のマッピングをカスタマイズする場合は、「[マッピング ソースとターゲット データベース](mapping-source-and-target-databases-accesstosql.md)データベース オブジェクトに変換する次手順は、それ以外の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文を使用して[変換データベース オブジェクト](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>参照  
[SQL Server へのアクセス データベースの移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
