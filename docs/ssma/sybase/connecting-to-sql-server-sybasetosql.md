---
title: SQL Server (SybaseToSQL) への接続 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 4f40fd6fa88b001eaa222789d6be35b83f9bf90a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948544"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>SQL Server への接続 (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) のデータベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のターゲット インスタンスのいずれかに接続する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 SSMA がのインスタンスのすべてのデータベースに関するメタデータを取得して接続すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でデータベースのメタデータを表示し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラー。 SSMA のインスタンスに関する情報を格納する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続しているが、パスワードは保存されません。  
  
接続を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロジェクトを終了するまでアクティブに保ちます。 プロジェクトを開くときにに再接続する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]する場合は、サーバーにアクティブに接続します。 データベース オブジェクトが読み込まれるまでオフラインで作業できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]しデータを移行します。  
  
インスタンスに関するメタデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が自動的に同期されていません。 代わりに、内のメタデータを更新する場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーである必要があります手動で更新する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」の説明に従って、メタデータ、"Synchronizing[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ"このトピックで後述します。  
  
## <a name="required-sql-server-permissions"></a>必要な SQL Server のアクセス許可  
接続に使用されるアカウント[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]そのアカウントで実行されるアクションに応じて、さまざまなアクセス許可が必要です。  
  
-   ASE のオブジェクトに変換する[!INCLUDE[tsql](../../includes/tsql-md.md)]からメタデータを更新する構文、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、か、アカウントをスクリプトに変換された構文を保存するのインスタンスにログインする権限を持って必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
-   データベース オブジェクトに読み込むために[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、アクセス許可の最小要件は、メンバーシップ、 **db_owner**ターゲット データベースのデータベース ロール。  
  
-   データを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、アカウントのメンバーである必要があります、 **sysadmin**サーバーの役割。 これは実行に必要、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント データの移行のパッケージ。  
  
-   SSMA によって生成されるコードを実行するアカウントが必要**Execute**のすべてのユーザー定義関数のアクセス許可、 **ssma_syb**のスキーマ、 **sysdb**データベース。 これらの関数は、ASE システムの機能と同等の機能を提供し、変換されたオブジェクトが使用されます。  
  
場合に接続するために使用するアカウント[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]すべての移行を実行するタスク、アカウントのメンバーである必要がありますが、 **sysadmin**サーバーの役割。  
  
## <a name="establishing-a-sql-server-connection"></a>SQL Server の接続を確立します。  
ASE データベース オブジェクトを変換する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文のインスタンスへの接続を確立する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ASE データベースやデータベースを移行します。  
  
接続のプロパティを定義するときに、オブジェクトとデータを移行するデータベースを指定します。 接続した後、ASE スキーマ レベルでは、このマッピングをカスタマイズできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。 [SQL Server スキーマへの Sybase ASE スキーマのマッピング&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)します。  
  
> [!IMPORTANT]  
> 接続する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、ことを確認のインスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が実行されていると、接続を受け入れることができます。  
  
**SQL Server に接続するには**  
  
1.  **ファイル**メニューの  **SQL サーバーへの接続**します。  
  
    以前に接続されている場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、コマンドの名前になります**SQL Server に再接続**します。  
  
2.  接続ダイアログ ボックスで入力するかのインスタンスの名前を選択[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
    -   ローカル コンピューターの既定のインスタンスに接続する場合は、入力**localhost**またはドット ( **.** )。  
  
    -   別のコンピューターで既定のインスタンスに接続する場合は、コンピューターの名前を入力します。  
  
    -   別のコンピューター上の名前付きインスタンスに接続する場合は、コンピューター名の後に、円記号とし、\myinstance など、インスタンス名を入力します。  
  
3.  場合、インスタンスの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]既定以外のポートで接続を受け入れる、使用されるポート番号を入力するように構成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内の接続、**サーバー ポート**ボックス。 既定のインスタンスの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]既定のポート番号は 1433 です。 名前付きインスタンスは、SSMA は、ポート番号の取得を試みます、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービス。  
  
4.  **データベース**ボックスに、ターゲット データベースの名前を入力します。  
  
    このオプションに再接続する場合は使用できません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
5.  **認証**ボックスで、接続に使用する認証の種類を選択します。 現在の Windows アカウントを使用する**Windows 認証**します。 使用する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインで、 **SQL Server 認証**とログイン名とパスワードを入力します。  
  
6.  セキュリティで保護された接続は、2 つのコントロールを追加、**暗号化接続**と**TrustServerCertificate**チェック ボックス。 場合にのみ**暗号化接続**がオンになって、 **TrustServerCertificate**チェック ボックスを表示します。 ときに**暗号化接続**がチェックされます (true) と**TrustServerCertificate**チェック ボックスがオフ (false)、これは SQL Server の SSL 証明書を検証します。 サーバー証明書の検証は、SSL ハンドシェイクの一部であり、接続先のサーバーが適切なサーバーであることを保証します。 これを確実にクライアント側およびサーバー側で、証明書をインストールする必要があります。  
  
7.  **[接続]** をクリックします。  
  
**高いバージョンの互換性について**  
  
-   接続できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 の場合、移行プロジェクトの作成は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005。  
  
-   接続できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 の場合、移行プロジェクトの作成は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 つまり下位バージョンに接続することはできませんが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   のみに接続できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 が作成されたプロジェクトが SQL Server 2012 の場合。  
  
-   SQL Azure の高いバージョンの互換性が正しくありません。  
  
||||||||
|-|-|-|-|-|-|-|
|**プロジェクトの種類とターゲット サーバーのバージョン**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (バージョン。9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (バージョン。10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Version:13.x)|SQL Azure|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|はい|[はい]|[はい]|[はい]|はい||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||はい|[はい]|[はい]|はい||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||はい|[はい]|はい||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||||はい|はい|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||はい||  
|SQL Azure||||||はい|  
  
> [!IMPORTANT]
> データベース オブジェクトの変換が実施しているのバージョンに従っていませんが、プロジェクトの種類に従って、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続しています。 場合に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年プロジェクトでは、変換は実行に従って[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 の新しいバージョンに接続している場合でも[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016)  
  
## <a name="reconnecting-to-sql-server"></a>SQL Server に再接続  
接続を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロジェクトを終了するまでアクティブに保ちます。 プロジェクトを開くときにに再接続する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]する場合は、サーバーにアクティブに接続します。 負荷のデータベース オブジェクトに、メタデータを更新するまでオフラインで作業できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データを移行します。  
  
再接続プロシージャ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]接続を確立するための手順と同じです。  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL サーバーのメタデータの同期  
に関するメタデータ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースが自動的に更新されません。 内のメタデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に最初に接続するときに、メタデータ エクスプ ローラーは、メタデータのスナップショット[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、または最後の時刻を手動で更新されたメタデータ。 すべてのデータベースまたは任意の 1 つのデータベースまたはデータベース オブジェクトのメタデータを手動で更新することができます。  
  
**メタデータを同期するには**  
  
1.  接続されていることを確認[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーで、データベースの横にあるチェック ボックスを選択するかデータベースのスキーマを更新します。  
  
    たとえば、すべてのデータベースのメタデータを更新するボックスをオンに、横に**データベース**します。  
  
3.  データベースまたは個々 のデータベースまたはデータベースのスキーマを右クリックし、**データベースと同期する**します。  
  
## <a name="next-step"></a>次の手順  
移行の次の手順は、プロジェクトのニーズによって異なります。  
  
-   ASE のデータベースとスキーマ間のマッピングをカスタマイズするかどうかと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースとスキーマを参照してください。 [SQL Server スキーマへの Sybase ASE スキーマのマッピング&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)します。  
  
-   プロジェクトの構成オプションをカスタマイズする場合を参照してください。[プロジェクト オプションの設定&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)します。  
  
-   カスタム ソースとターゲットのデータ型のマッピングを参照してください[マッピング Sybase ASE と SQL Server データ型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)します。  
  
-   Sybase ASE データベース オブジェクトの定義を変換できる場合、これらのいずれかを実行する必要はありません、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクト定義します。 詳細については、次を参照してください。 [Sybase ASE データベース オブジェクトの変換&#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server - Azure SQL DB への Sybase ASE データベース移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
