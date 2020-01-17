---
title: Oracle パブリッシャーのトラブルシューティング | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], Oracle publishing
ms.assetid: be94f1c1-816b-4b1d-83f6-2fd6f5807ab7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c84bf2d98440ff9425cd26a4a71667abea2904e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63021907"
---
# <a name="troubleshooting-oracle-publishers"></a>Oracle パブリッシャーのトラブルシューティング
  このトピックでは、Oracle パブリッシャーを構成および使用する際に発生する可能性のあるいくつかの問題を示します。  
  
## <a name="an-error-is-raised-regarding-oracle-client-and-networking-software"></a>Oracle クライアントおよびネットワーキング ソフトウェアに関連するエラーが発生する  
 ディストリビューター上の [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が実行されるアカウントには、Oracle クライアント ネットワーク ソフトウェアがインストールされているディレクトリ (およびすべてのサブディレクトリ) に対する読み取り権限と実行権限を付与する必要があります。 これらの権限が付与されていなかったり、Oracle クライアント コンポーネントが正しくインストールされていない場合は、次のエラー メッセージが表示されます。  
  
 "[Microsoft OLE DB Provider for Oracle] によるサーバーへの接続に失敗しました。 Oracle クライアントおよびネットワーク コンポーネントが見つかりません。 これらのコンポーネントは、Oracle Corporation によって提供され、Oracle バージョン 7.3.3 以降のクライアント ソフトウェエア インストールの一部です。 これらのコンポーネントがインストールされるまで、プロバイダーは機能しません。"  
  
 適切な Oracle クライアントがディストリビューターにインストールされている場合は、そのクライアントのインストールが完了した後に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をいったん停止して再起動したか確認してください。 これは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でクライアント コンポーネントを認識するために必要です。  
  
 権限が付与されていること、およびコンポーネントが正しくインストールされていることを確認したにもかかわらず、このエラーが継続して発生する場合は、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDTC\MTxOCI のレジストリ設定が正しいかどうかを確認してください。  
  
-   Oracle 10g の場合、正しい設定は次のようになります。  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql10.dll  
  
    -   OracleXaLib = oraclient10.dll  
  
-   Oracle 9i の場合、正しい設定は次のようになります。  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql9.dll  
  
    -   OracleXaLib = oraclient9.dll  
  
## <a name="the-sql-server-distributor-cannot-connect-to-the-oracle-database-instance"></a>SQL Server ディストリビューターが Oracle データベース インスタンスに接続できない  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターが Oracle パブリッシャーに接続できない場合は、次の点を確認してください。  
  
-   必要な Oracle ソフトウェアがディストリビューターにインストールされているかどうか。  
  
-   Oracle データベースがオンラインになっており、SQL*Plus などのツールを使用して Oracle データベースに接続できるかどうか。  
  
-   レプリケーションが Oracle パブリッシャーに接続する際に使用するログインに十分な権限があるかどうか。 詳細については、「[Configure an Oracle Publisher](configure-an-oracle-publisher.md)」(Oracle パブリッシャーの構成) をご覧ください。  
  
-   Oracle パブリッシャーの構成中に定義された TNS 名が tnsnames.ora ファイルに記載されているかどうか。  
  
-   正しい Oracle ホームおよびパスが使用されているかどうか。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターに Oracle バイナリのセットが 1 つしかインストールされていない場合でも、Oracle ホーム関連の環境変数が正しく設定されていることを確認してください。 環境変数の値を変更した場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を停止してから再起動して、変更を有効にする必要があります。  
  
 接続の構成とテストの詳細については、「[Configure an Oracle Publisher (Oracle パブリッシャーの構成)](configure-an-oracle-publisher.md)」の「Installing and Configuring Oracle Client Networking Software on the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributor (SQL Server ディストリビューターへの Oracle クライアント ネットワーク ソフトウェアのインストールと構成)」を参照してください。  
  
## <a name="the-oracle-publisher-is-associated-with-another-distributor"></a>Oracle パブリッシャーが別のディストリビューターに関連付けられている  
 Oracle パブリッシャーは、1 つの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターにのみ関連付けることができます。 別のディストリビューターを Oracle パブリッシャーに関連付ける場合は、関連付けられているディストリビューターを削除してから、別のディストリビューターを使用する必要があります。 ディストリビューターを最初に削除しない場合、次のエラー メッセージのいずれかが表示されます。  
  
-   "Oracle サーバー インスタンス '\<*OraclePublisherName*>' は、'\<*SQLServerDistributorName*>' をディストリビューターとして使用するように構成されています。 '\<*NewSQLServerDistributorName*>' をディストリビューターとして使用するためには、Oracle サーバー インスタンスの現在のレプリケーション構成を削除する必要があります。その場合、サーバー インスタンス上のすべてのパブリケーションが削除されます。"  
  
-   "Oracle サーバー '\<*OracleServerName*>' は、既にディストリビューター '\<*SQLServerDistributorName*>. *\<DistributionDatabaseName>* ' のパブリッシャー '\<*OraclePublisherName*>' として定義されています。 パブリッシャーを削除するか、パブリック シノニム ' *\<SynonymName>* ' を削除して、再作成してください。"  
  
 Oracle パブリッシャーが削除されると、Oracle データベース内のレプリケーション オブジェクトが自動的にクリーンアップされます。 ただし、Oracle レプリケーション オブジェクトを手動でクリーンアップすることが必要な場合もあります。 レプリケーションで作成した Oracle レプリケーション オブジェクトを手動でクリーン アップするには、次の手順を実行します。  
  
1.  DBA 権限で Oracle パブリッシャーに接続します。  
  
2.  SQL コマンド `DROP PUBLIC SYNONYM MSSQLSERVERDISTRIBUTOR;`を実行します。  
  
3.  SQL コマンド `DROP USER <replication_administrative_user_schema>``CASCADE;`を実行します。  
  
## <a name="sql-server-error-21663-is-raised-regarding-the-lack-of-a-primary-key"></a>主キーの欠如に関する SQL Server エラー 21663 が発生する  
 トランザクション パブリケーションのアーティクルには、有効な主キーが必要です。 有効な主キーがない場合は、アーティクルを追加しようとすると、次のエラー メッセージが表示されます。  
  
 "ソース テーブル [\<*TableOwner*>].[\<*TableName*>] に有効な主キーが見つかりません。"  
  
 主キーの要件の詳細については、トピック「 [Design Considerations and Limitations for Oracle Publishers](design-considerations-and-limitations-for-oracle-publishers.md)」の「一意のインデックスおよび制約」を参照してください。  
  
## <a name="sql-server-error-21642-is-raised-regarding-a-duplicate-linked-server-login"></a>リンク サーバー ログインの重複に関する SQL Server エラー 21642 が発生する  
 Oracle パブリッシャーを最初に構成するときに、パブリッシャーとディストリビューター間の接続用にリンク サーバー エントリが作成されます。 リンク サーバーには、Oracle TNS サービスと同じ名前が付けられます。 同じ名前でリンク サーバーを作成しようとすると、次のエラー メッセージが表示されます。  
  
 "異種パブリッシャーにはリンク サーバーが必要です。 リンク サーバー ' *\<LinkedServerName>* ' は既に存在します。 リンク サーバーを削除するか、または別のパブリッシャー名を選択してください。"  
  
 このエラーは、リンク サーバーを直接作成しようとしたり、Oracle パブリッシャーと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューター間のリレーションシップを以前に削除し、再構成しようとしている場合に発生する可能性があります。 パブリッシャーを再構成しようとしているときにこのエラーが表示される場合は、[sp_dropserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropserver-transact-sql) を使用してリンク サーバーを削除してください。  
  
 リンク サーバー接続で Oracle パブリッシャーに接続する必要がある場合は、別の TNS サービス名を作成してから、[sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql) を呼び出すときにこの名前を使用します。 TNS サービス名の作成の詳細については、Oracle のマニュアルを参照してください。  
  
## <a name="sql-server-error-21617-is-raised"></a>SQL Server エラー 21617 が発生する  
 Oracle パブリッシングでは、Oracle アプリケーション SQL*PLUS を使用して、パブリッシャー サポートコードのパッケージを Oracle データベースにダウンロードします。 Oracle パブリッシャーを構成する前に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は SQL\*PLUS がディストリビューターのシステム パスを介してアクセス可能であることを確認します。 SQL\*PLUS を読み込めない場合、次のエラー メッセージが表示されます。  
  
 "SQL*PLUS を実行できません。 ディストリビューターに Oracle クライアント コードの現在のバージョンがインストールされていることを確認してください。"  
  
 ディストリビューターで SQL\*PLUS を検索してください。 Oracle 10g クライアント インストールの場合、この実行可能ファイルの名前は sqlplus.exe です。 通常は %ORACLE_HOME%/bin にインストールされています。 SQL\*PLUS のパスがシステム パスに含まれていることを確認するには、システム変数 **Path** の値を調べます。  
  
1.  **[マイ コンピューター]** を右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[詳細設定]** タブをクリックし、 **[環境変数]** をクリックします。  
  
3.  **[環境変数]** ダイアログ ボックスの **[システム環境変数]** ボックスで、 **[Path]** 変数をクリックし、 **[編集]** をクリックします。  
  
4.  **[システム変数の編集]** ダイアログ ボックスで、 **[変数値]** ボックスに sqlplus.exe を含むフォルダーへのパスが表示されていない場合は、このパスを含むように文字列を編集します。  
  
5.  開いている各ダイアログ ボックスで **[OK]** をクリックして作業を終了し、変更を保存します。  
  
 ディストリビューターで sqlplus.exe が見つからない場合は、Oracle クライアント ソフトウェアの現在のバージョンをディストリビューターにインストールします。 詳細については、「[Configure an Oracle Publisher](configure-an-oracle-publisher.md)」(Oracle パブリッシャーの構成) をご覧ください。  
  
## <a name="sql-server-error-21620-is-raised"></a>SQL Server エラー 21620 が発生する  
 Oracle データベースのバージョン 8.1 よりも前のバージョンに接続している場合、Oracle パブリッシングでは、ディストリビューターにインストールされている Oracle クライアント ソフトウェアが、バージョン 9 からのものである必要があります。 Oracle データベースのバージョン 8.1 以降に接続している場合は、Oracle クライアント ソフトウェアのバージョン 10 以降を使用することをお勧めします。  
  
 Oracle パブリッシャーを構成する前に、Oracle パブリッシングはディストリビューターのシステム パスを介してアクセスできる SQL*PLUS のバージョンが、バージョン 9 以降であることを確認します。 バージョン 9 以降でない場合、次のエラー メッセージが表示されます。  
  
 "システムの Path 変数からアクセスできる SQL*PLUS のバージョンが古いため、Oracle パブリッシングをサポートできません。 ディストリビューターに Oracle クライアント コードの現在のバージョンがインストールされていることを確認してください。"  
  
 ディストリビューターに Oracle クライアント ソフトウェアの複数のバージョンがインストールされている場合は、最新のバージョンが少なくともバージョン 9 であり、システム パス変数でそのバージョンが最初に参照されていることを確認します (最新のバージョンが最初に参照されていれば、他のバージョンが参照されていてもかまいません)。 システム パス変数の編集に関する詳細については、このトピックで既に説明した「SQL Server エラー 21617 が発生する」を参照してください。  
  
## <a name="sql-server-error-21624-or-error-21629-is-raised"></a>SQL Server エラー 21624 または SQL Server エラー 21629 が発生する  
 64 ビット ディストリビューターの場合、Oracle パブリッシングでは、Oracle OLEDB Provider for Oracle (OraOLEDB.Oracle) が使用されます。 ディストリビューターに Oracle OLEDB プロバイダーがインストールおよび登録されていることを確認してください。 このプロバイダーがインストールおよび登録されていない場合、次のエラー メッセージのいずれかまたは両方が表示されます。  
  
-   "ディストリビューター '%s' に登録済みの Oracle OLEDB プロバイダー OraOLEDB.Oracle が見つかりません。 ディストリビューターに現在のバージョンの Oracle OLEDB プロバイダーがインストールおよび登録されていることを確認してください。"  
  
-   "Oracle 用の Oracle OLEDB プロバイダー OraOLEDB.Oracle が登録されていることを示す CLSID レジストリ キーがディストリビューターに存在しません。 ディストリビューターに Oracle OLEDB プロバイダーがインストールおよび登録されていることを確認してください。"  
  
 Oracle クライアント ソフトウェア バージョン 10g を使用している場合、プロバイダーは OraOLEDB10.dll です。バージョン 9i の場合、プロバイダーは OraOLEDB.dll です。 プロバイダーは %ORACLE_HOME%\BIN (たとえば、C:\oracle\product\10.1.0\Client_1\bin) にインストールされます。 ディストリビューターに Oracle OLEDB プロバイダーがインストールされていない場合は、Oracle が提供する Oracle クライアント ソフトウェア インストール ディスクからインストールしてください。 詳細については、「[Configure an Oracle Publisher](configure-an-oracle-publisher.md)」(Oracle パブリッシャーの構成) をご覧ください。  
  
 Oracle OLEDB プロバイダーがインストールされている場合は、そのプロバイダーが登録されていることを確認してください。 プロバイダーの DLL を登録するには、DLL がインストールされているディレクトリから次のコマンドを実行し、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを停止して再起動します。  
  
1.  `regsvr32 OraOLEDB10.dll` または `regsvr32 OraOLEDB.dll`。  
  
## <a name="sql-server-error-21626-or-error-21627-is-raised"></a>SQL Server エラー 21626 または SQL Server エラー 21627 が発生する  
 Oracle パブリッシング環境が正しく構成されていることを確認するために、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] により、構成時に指定したログイン資格情報を使用して、Oracle パブリッシャーへの接続が試行されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターが Oracle パブリッシャーに接続できない場合、次のエラー メッセージが表示されます。  
  
-   "Oracle OLEDB プロバイダー OraOLEDB.Oracle を使用して Oracle データベース サーバー '%s' に接続できません。"  
  
 このエラー メッセージが表示された場合は、Oracle パブリッシャーの構成時に指定したのと同じログインとパスワードを使用して SQL*PLUS を直接実行することにより、Oracle データベースへの接続を確認してください。 詳細については、このトピックで既に説明した「SQL Server ディストリビューターが Oracle データベース インスタンスに接続できない」を参照してください。  
  
## <a name="sql-server-error-21628-is-raised"></a>SQL Server エラー 21628 が発生する  
 64 ビット ディストリビューターの場合、Oracle パブリッシングでは、Oracle OLEDB Provider for Oracle (OraOLEDB.Oracle) が使用されます。 Oracle プロバイダーを[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と同じプロセスで実行可能にするために、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]によってレジストリ エントリが作成されます。 このレジストリ エントリの読み取りまたは書き込みに問題がある場合、次のエラー メッセージが表示されます。  
  
 "ディストリビューター '%s' のレジストリを更新し、Oracle OLEDB プロバイダー OraOLEDB.Oracle を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]と同じプロセスで実行可能にすることができません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が所有しているレジストリ キーの変更が現在のログインに許可されていることを確認してください。"  
  
 Oracle パブリッシングでは、このレジストリ エントリが存在し、64 ビット ディストリビューターの場合は **1** に設定されている必要があります。 このエントリが存在しない場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって作成されます。 このエントリは存在するが、 **0**に設定されている場合は、設定は変更されず、Oracle パブリッシャーの構成は失敗します。  
  
 レジストリ設定を表示および変更するには、次の手順を実行します。  
  
1.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。  
  
2.  **[ファイル名を指定して実行]** ダイアログ ボックスで、「 **regedit**」と入力し、 **[OK]** をクリックします。  
  
3.  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\ *\<InstanceName>* \Providers に移動します。  
  
     [Providers] の下に、[OraOLEDB.Oracle] という名前のフォルダーがあります。 このフォルダーの中に、 **[AllowInProcess]** という名前の DWORD 値があり、値は **1**になっている必要があります。  
  
4.  **[AllowInProcess]** が **0**に設定されている場合は、このレジストリ エントリを **1**に更新します。  
  
    1.  エントリを右クリックし、 **[変更]** をクリックします。  
  
    2.  **[文字列の編集]** ダイアログ ボックスで、 **[値のデータ]** ボックスに「 **1** 」と入力します。  
  
## <a name="sql-server-error-21684-is-raised"></a>SQL Server エラー 21684 が発生する  
 管理ユーザー アカウントに十分な権限がない場合は、次のエラー メッセージが表示されます。  
  
 "Oracle パブリッシャー '%s' の管理者ログインに関連付けられた権限が不十分です。"  
  
 ユーザーに与えられた権限を確認するには、クエリ `SELECT * from session_privs`を実行します。 出力は次のようになります。  
  
 `PRIVILEGE`  
  
 `------------------`  
  
 `CREATE SESSION`  
  
 `CREATE TABLE`  
  
 `CREATE PUBLIC SYNONYM`  
  
 `DROP PUBLIC SYNONYM`  
  
 `CREATE VIEW`  
  
 `CREATE SEQUENCE`  
  
 `CREATE PROCEDURE`  
  
 `CREATE TRIGGER`  
  
## <a name="you-encounter-permissions-issues-for-the-replication-user-schema"></a>レプリケーション ユーザー スキーマの権限に関する問題が発生する  
 レプリケーション ユーザー スキーマには、「[Configure an Oracle Publisher (Oracle パブリッシャーの構成)](configure-an-oracle-publisher.md)」の「Creating the User Schema Manually (手動によるユーザー スキーマの作成)」で説明されている権限が必要です。  
  
## <a name="oracle-error-ora-01000"></a>Oracle エラー ORA-01000  
 パブリケーションへアーティクルを追加処理中に、レプリケーションは Oracle パブリッシャーでカーソルを使用します。 この処理中にパブリッシャーで使用できるカーソルの最大数を超える可能性があります。 最大数を超えると、次のエラーが発生します。  
  
 "ORA-01000: maximum open cursors exceeded"  
  
 この問題を回避するには、Oracle データベースの **max_open_cursors** 設定に、高い値 (1000 以上) を設定します。 この設定の詳細については Oracle のマニュアルを参照してください。  
  
## <a name="oracle-error-ora-01555"></a>Oracle エラー ORA-01555  
 次の Oracle データベース エラーは、スナップショット レプリケーションに関連するものではありません。このエラーは、Oracle でのデータの読み取り一貫性ビューの構築方法に関連します。  
  
 "ORA-01555:スナップショットが古すぎる"  
  
 Oracle では、ロールバック セグメントと呼ばれるオブジェクトを使用して、SQL ステートメントの発行時点のデータの読み取り一貫性ビューを構築します。 "Snapshot too old" エラーは、ロールバック情報が他の同時接続セッションによって上書きされた場合に発生する可能性があります。 Oracle 9i よりも前のバージョンでは、このエラーの発生頻度を減らす方法として、ロールバック セグメントのサイズや数を増やしたり、大きいトランザクションを特定のロールバック セグメントに割り当てる方法が推奨されていました。  
  
 Oracle 9i では、ロールバック セグメントに代わる、UNDO テーブルスペースの概念が導入されました。 Oracle 9i で "Snapshot too old" エラーを回避するには、次の方法をお勧めします。  
  
-   十分な空き領域を持つ UNDO テーブルスペースを作成する。  
  
-   作成したテーブルスペースに保証される保有期間を設定する (Oracle 10G 以上)。  
  
-   Oracle の初期化パラメーター UNDO_MANAGEMENT および UNDO_RETENTION を構成する。  
  
 "Snapshot too old" エラーを回避する方法の詳細については、Oracle のマニュアルを参照してください。  
  
## <a name="oracle-error-ora-22285"></a>Oracle エラー ORA-22285  
 テーブルに BFILE 列が含まれている場合、この列のデータはファイル システムに格納されます。 レプリケーション管理ユーザー アカウントには、次の構文を使用して、このデータが格納されているディレクトリへのアクセスを許可する必要があります。  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 アクセスが許可されていない場合は、ログ リーダー エージェントにより次のエラーが発生します。  
  
 "ORA-22285: non-existent directory or file for FILEOPEN operation"  
  
## <a name="changes-are-made-that-require-reconfiguration-of-the-publisher"></a>パブリッシャーの再構成が必要になる変更  
 レプリケーション メタデータ テーブルまたはプロシージャを変更した場合は、パブリッシャーを削除して再構成する必要があります。 パブリッシャーを再構成するには、パブリッシャーを削除し、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、Transact-SQL、または RMO を使用してパブリッシャーを再構成する必要があります。 パブリッシャーの構成の詳細については、「[Configure an Oracle Publisher (Oracle パブリッシャーの構成)](configure-an-oracle-publisher.md)」を参照してください。  
  
 **Oracle パブリッシャーを削除するには (** SQL Server Management Studio **)**  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] の Oracle パブリッシャーのディストリビューターに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** を右クリックし、 **[ディストリビューターのプロパティ]** をクリックします。  
  
3.  **[ディストリビューターのプロパティ]** ダイアログ ボックスの **[パブリッシャー]** ページで、Oracle パブリッシャーのチェック ボックスをオフにします。  
  
4.  **[OK]** をクリックします。  
  
 **Oracle パブリッシャーを削除するには (Transact-SQL)**  
  
-   **sp_dropdistpublisher**を実行します。 詳細については、「[sp_dropdistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Configure an Oracle Publisher (Oracle パブリッシャーの構成)](configure-an-oracle-publisher.md)   
 [Oracle パブリッシングの概要](oracle-publishing-overview.md)  
  
  
