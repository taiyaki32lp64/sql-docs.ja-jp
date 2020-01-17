---
title: SQL Server (DB2eToSQL) への接続 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b59803cb-3cc6-41cc-8553-faf90851410e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7ab4c1f691820fb19dde7a3e3166abc2ff065b18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126641"
---
# <a name="connecting-to-sql-server-db2etosql"></a>SQL Server (DB2eToSQL) への接続
DB2 のデータベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 または Azure SQL DB がこれらのターゲット インスタンスのいずれかに接続する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 SSMA がのインスタンスのすべてのデータベースに関するメタデータを取得して接続すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でデータベースのメタデータを表示し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラー。 SSMA のインスタンスに関する情報を格納する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続しているが、パスワードは保存されません。  
  
接続を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロジェクトを終了するまでアクティブに保ちます。 プロジェクトを開くときにに再接続する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]する場合は、サーバーにアクティブに接続します。 データベース オブジェクトが読み込まれるまでオフラインで作業できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]しデータを移行します。  
  
インスタンスに関するメタデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が自動的に同期されていません。 代わりでメタデータを更新する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーである必要があります手動で更新する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ。 詳細については、次を参照してください。、"Synchronizing[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ"このトピックで後述します。  
  
## <a name="required-sql-server-permissions"></a>必要な SQL Server のアクセス許可  
接続に使用されるアカウント[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]アカウントで実行された操作に応じてさまざまなアクセス許可が必要です。  
  
-   DB2 オブジェクトに変換する[!INCLUDE[tsql](../../includes/tsql-md.md)]からメタデータを更新する構文、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、か、アカウントをスクリプトに変換された構文を保存するのインスタンスにログオンする権限を持って必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
-   データベース オブジェクトに読み込むために[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、アカウントのメンバーである必要があります、 **sysadmin**サーバーの役割。 これは、CLR アセンブリのインストールに必要です。  
  
-   データを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、アカウントのメンバーである必要があります、 **sysadmin**サーバーの役割。 これは実行に必要、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント データの移行のパッケージ。  
  
-   SSMA によって生成されるコードを実行するアカウントが必要**Execute**のすべてのユーザー定義関数のアクセス許可、 **ssma_DB2**ターゲット データベースのスキーマ。 これらの関数は、DB2 システム関数と同等の機能を提供し、変換されたオブジェクトが使用します。  
  
場合に接続するために使用するアカウント[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]すべての移行を実行するタスク、アカウントのメンバーである必要がありますが、 **sysadmin**サーバーの役割。  
  
## <a name="establishing-a-sql-server-connection"></a>SQL Server の接続を確立します。  
DB2 データベース オブジェクトを変換する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文のインスタンスへの接続を確立する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB2 データベースまたはデータベースを移行します。  
  
接続のプロパティを定義するときに、オブジェクトとデータを移行するデータベースを指定します。 接続した後に、DB2 スキーマ レベルでは、このマッピングをカスタマイズできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。 [SQL Server スキーマへの DB2 スキーマのマッピング&#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md)します。  
  
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
  
5.  **認証**ボックスで、接続に使用する認証の種類を選択します。 現在の Windows アカウントを使用する**Windows 認証**します。 使用する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインで、 **SQL Server 認証**、ログイン名とパスワードを指定します。  
  
6.  セキュリティで保護された接続は、2 つのコントロールを追加、**暗号化接続**と**TrustServerCertificate**チェック ボックス。 場合にのみ**暗号化接続**がオンになって、 **TrustServerCertificate**チェック ボックスを表示します。 ときに**暗号化接続**がチェックされます (true) と**TrustServerCertificate**チェック ボックスがオフ (false)、これは SQL Server の SSL 証明書を検証します。 サーバー証明書の検証は、SSL ハンドシェイクの一部であり、接続先のサーバーが適切なサーバーであることを保証します。 これを確実にクライアント側およびサーバー側で、証明書をインストールする必要があります。  
  
7.  **[接続]** をクリックします。  
  
**高いバージョンの互換性について**  
  
-   接続できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 の場合、移行プロジェクトの作成は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005。  
  
-   接続できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 の場合、移行プロジェクトの作成は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 つまり下位バージョンに接続することはできませんが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   接続できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 が作成されたプロジェクトが SQL Server 2012 の場合。  
  
||||||  
|-|-|-|-|-|  
|**プロジェクトの種類とターゲット サーバーのバージョン**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Version:13.x)|Azure SQL DB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|はい|[はい]|はい||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||はい|はい||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014|||はい||  
|Azure SQL DB||||はい|  
  
> [!IMPORTANT]  
> データベース オブジェクトの変換が実施しているのバージョンに従っていませんが、プロジェクトの種類に従って、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続しています。 場合に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 または Azure SQL DB します。  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL サーバーのメタデータの同期  
に関するメタデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースが自動的に更新されません。 内のメタデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に最初に接続するときに、メタデータ エクスプ ローラーは、メタデータのスナップショット[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、または最後の時刻を手動で更新されたメタデータ。 すべてのデータベースまたは任意の 1 つのデータベースまたはデータベース オブジェクトのメタデータを手動で更新することができます。  
  
**メタデータを同期するには**  
  
1.  接続されていることを確認[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーで、データベースの横にあるチェック ボックスを選択するかデータベースのスキーマを更新します。  
  
    たとえば、すべてのデータベースのメタデータを更新するボックスをオンに、横に**データベース**します。  
  
3.  右クリック**データベース**、または個々 のデータベースまたはデータベースのスキーマ、および選択**データベースと同期する**します。  
  
## <a name="next-step"></a>次の手順  
移行の次の手順は、プロジェクトのニーズによって異なります。  
  
-   DB2 スキーマの間のマッピングをカスタマイズして[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースとスキーマを参照してください。 [SQL Server スキーマへの DB2 スキーマのマッピング&#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md)します。  
  
-   プロジェクトの構成オプションをカスタマイズするを参照してください。[プロジェクト設定&#40;変換&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md)および関連するセクション。  
  
-   ソースとターゲットのデータ型のマッピングをカスタマイズするを参照してください。[マッピング DB2 と SQL Server データ型&#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)します。  
  
-   DB2 データベース オブジェクトの定義を変換できる場合は、次のタスクを実行する必要はありません、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクト定義します。 詳細については、次を参照してください。 [DB2 スキーマの変換&#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server にデータベースを移行する DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
