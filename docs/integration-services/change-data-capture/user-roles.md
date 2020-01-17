---
title: ユーザー ロール | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: be0ec384-e03b-4483-96ca-02b289804d6a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 194eb7232aaf0ffd1f323d6291c0efb06f88a397
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298591"
---
# <a name="user-roles"></a>ユーザー ロール

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ここでは、Change Data Capture Service for Oracle by Attunity のユーザー ロールについて説明します。 ここで説明するロールは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ロール、Windows ロール、または Oracle データベース ロールです。  
  
## <a name="windows-user-roles"></a>Windows ユーザー ロール  
 ここでは、Oracle CDC Service によって使用される Windows ユーザー ロールについて説明します。  
  
### <a name="computer-administrator-oracle-cdc-service"></a>コンピューター管理者:Oracle CDC Service  
 コンピューターの管理者は、コンピューターでの CDC Service の作成とメンテナンスを担当する Windows ユーザーです。 このユーザーは、ローカル コンピューターの Administrators グループに属している必要があります。  
  
 Oracle CDC Service のコンピューターの管理者が実行するタスクには次のものがあります。  
  
-   CDC Service for Oracle ソフトウェアのインストール  
  
-   Oracle CDC Windows サービスの作成  
  
-   CDC Service から対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの接続の設定 (接続文字列と資格情報)  
  
-   CDC Service のマスター パスワードによる Oracle ログ マイニングの資格情報の保護  
  
-   CDC Service Windows サービスの削除  
  
-   CDC Service for Oracle ソフトウェアのアンインストール  
  
-   CDC Service for Oracle ソフトウェアのメンテナンス (更新プログラムのインストールなど)  
  
-   CDC Service Windows サービスの開始と停止  
  
 Microsoft フェールオーバー クラスターなどの高可用性構成を使用している場合、コンピューターの管理者は、次のような追加の役割と権限を持つ必要があります。  
  
-   すべてのクラスター ノード上の CDC Service for Oracle ソフトウェアのインストールとメンテナンス。  
  
-   さまざまなクラスター ノードでの CDC Service Windows サービスに対する汎用クラスター サービス リソースの定義。  
  
-   CDC Service for Oracle がインストールされているコンピューターで管理者として承認されたコンピューターの管理者の業務遂行。 この人物は、CDC Service for Oracle をインストールし、CDC Service 構成コンソールを使用して CDC Service for Oracle をローカル コンピューターで構成します。  
  
### <a name="service-account-oracle-cdc-service"></a>サービス アカウント:Oracle CDC Service  
 これは Oracle CDC Service Windows サービス アカウントで、Oracle CDC Service を実行するために使用する Windows アカウント (サービス アカウント) です。  
  
 サービス アカウントに必要な特権は、Oracle クライアントと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC プロバイダーを使用するための特権だけです。 このアカウントは、特定のプロバイダーで必要な場合を除いて、ファイルにアクセスする必要はありません (たとえば、 **tnsnames.ora** ファイルで Oracle クライアントの接続文字列が Oracle データベース インスタンスを参照している場合、サービス アカウントにはそのファイルへの読み取りアクセス権が必要です)。  
  
 Windows Vista または Windows Server 2008 で Oracle CDC Service を作成する場合、既定のサービス アカウントは NETWORK SERVICE アカウントです。  
  
 Windows 7 および Windows Server 2008 R2 以降では、既定のサービス アカウントは NT Service\\<service-name> です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が、別のコンピューターで実行されているか、クラスター化された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスであって、サービスが Windows 認証を使用して対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続する必要がある場合、サービス アカウントはドメイン アカウントにする必要があります。  
  
## <a name="sql-server-user-roles"></a>SQL Server ユーザー ロール  
 ここでは、Oracle CDC Service によって使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー ロールについて説明します。  
  
### <a name="oracle-cdc-service-administrator"></a>Oracle CDC Service の管理者  
 CDC Service の管理者は、対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの Oracle CDC Service アーティファクトを完全に制御できる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーです。 CDC Service の管理者は、Oracle CDC デザイナー コンソールを使用して Oracle CDC インスタンスを設計します。  
  
 CDC Service の管理者には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定サーバー ロールの **public** と **dbcreator**が付与されている必要があります。  
  
 CDC Service の管理者が実行するタスクには次のものがあります。  
  
-   Oracle CDC インスタンス ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース) をホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの準備。 このタスクでは、MSXDBCDC と呼ばれる特別なデータベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに作成します。  
  
-   Oracle CDC インスタンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの作成。 このタスクには、新しく作成した CDC 用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの有効化が含まれます。これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者 (**sysadmin**) が行う必要があります。  
  
-   Oracle CDC インスタンスの設計。 このタスクには、ソース Oracle データベースとキャプチャ対象テーブルについての情報の提供が含まれます。これは、Oracle データベース管理者が行う必要があります。  
  
-   長期にわたる Oracle CDC インスタンスのメンテナンス。キャプチャ インスタンスの追加と削除や構成の更新などが含まれます。  
  
-   Oracle CDC インスタンスの有効化または無効化。  
  
-   Oracle CDC インスタンスの状態の監視。  
  
-   Oracle CDC インスタンスに影響する問題のトラブルシューティング。  
  
 CDC Service の管理者は、少なくとも最初は、Oracle CDC インスタンスに関連付けられた **CDC データベース用の** db_owner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定データベース ロールに属しています。 そのため、CDC Service の管理者は、CDC データベースに格納されている変更データにアクセスできます。 CDC データベースの **db_owner** ロールを作成したら別のユーザーに割り当てることができ、このユーザーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの準備と別の Oracle CDC インスタンスの作成を除く上記のすべてのタスクを実行できるようになります。  
  
 CDC Service の管理者は、Oracle CDC Windows サービスの作成時に指定されたマスター パスワードを把握しておく必要はありません。  
  
### <a name="system-administrator"></a>システム管理者  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーで、Oracle CDC Service に関連付けられた **インスタンスの** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定サーバー ロールが付与されている必要があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者が行う Oracle CDC に固有のタスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 用の Oracle CDC インスタンスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの有効化だけです。 このタスクは、新しい Oracle CDC インスタンスを作成するときに、Oracle CDC デザイナー コンソールを使用して実行します。  
  
### <a name="oracle-cdc-service-user"></a>Oracle CDC Service ユーザー  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC Service ユーザーは、このサービスで処理される MSXDBCDC およびすべての Oracle CDC インスタンス (CDC データベース) に対する作業を実行するために Oracle CDC Service によって使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインです。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC Service ユーザーには、以下が付与されている必要があります。  
  
-   サーバーで処理されるすべての CDC データベースの固定データベース ロール **db_dlladmin**、 **db_datareader**、および **db_datawriter** のメンバー。  
  
-   MSXDBCDC データベースの固定データベース ロール **db_datareader** および **db_datawriter** のメンバー。  
  
 Oracle CDC Service は、単一の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを使用してすべての CDC データベースおよび MSXDBCDC データベースを処理するので、このログインをこれらすべてのデータベースでマップする必要があります。  
  
### <a name="oracle-cdc-change-consumer"></a>Oracle CDC 変更コンシューマー  
 Oracle CDC 変更コンシューマーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC インスタンス データベースの CDC テーブルに格納されている変更を使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーです。  
  
 このユーザーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC インフラストラクチャによって生成される CDC 関数を使用して各 CDC テーブルにアクセスするために必要なユーザー ロールを決定します。 キャプチャ インスタンスの指定時にユーザー ロールを指定しない場合は、変更へのアクセスが CDC データベースの **db_owner** 固定データベース ロールのメンバーに制限されます。  
  
## <a name="oracle-user-roles"></a>Oracle ユーザー ロール  
 ここでは、Oracle CDC Service によって使用される Oracle ユーザー ロールについて説明します。  
  
### <a name="database-administrator-dba"></a>データベース管理者 (DBA)  
 Oracle データベース管理者 (DBA) は、Oracle データベース ユーザーです。 Oracle DBA が実行するタスクには次のものがあります。  
  
-   ソース Oracle データベースを ARCHIVELOG モードで動作させるための設定。  
  
-   必要な権限を持つログ マイニング ユーザーの設定。  
  
-   キャプチャ対象テーブルの補足ログの設定。  
  
-   使用できなくなったアーカイブ済みのトランザクション ログ ファイルを処理できるように復元するための支援。  
  
 Oracle データベース管理者は、実行する必要がある Oracle SQL スクリプトを取得して、その実行前に評価することができます。 また、Oracle SQL スクリプトを Oracle CDC デザイナー コンソールから直接実行することもできます。  
  
 Oracle データベース管理者が Oracle CDC Designer コンソールの使用を選択した場合、管理者の資格情報は保持されません。ただし、資格情報が使用されたコンテキスト (ダイアログ) は除きます。  
  
 Oracle データベース管理者は、Oracle CDC Service の管理者と連携して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC インスタンスを構成します。  
  
### <a name="log-mining-user"></a>ログ マイニング ユーザー  
 Oracle Log Miner ユーザーは、Oracle トランザクション ログにアクセスして処理するために必要な特権が付与された特殊な Oracle データベース ユーザーです。  
  
 このユーザーの資格情報は、非対称キー暗号化を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC インスタンス データベースに格納されます。 その資格情報には Oracle CDC Service のみがアクセスでき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC インスタンス データベースの所有者はアクセスできません。  
  
 ログ マイニング ユーザーに付与されている必要がある特権を以下に示します。  
  
-   \<any-captured-table> に対する SELECT  
  
-   SELECT ANY TRANSACTION  
  
-   DBMS_LOGMNR に対する EXECUTE  
  
-   V$LOGMNR_CONTENTS に対する SELECT  
  
-   V$ARCHIVED_LOG に対する SELECT  
  
-   V$LOG に対する SELECT  
  
-   V$LOGFILE に対する SELECT  
  
-   V$DATABASE に対する SELECT  
  
-   V$THREAD に対する SELECT  
  
-   ALL_INDEXES に対する SELECT  
  
-   ALL_OBJECTS に対する SELECT  
  
-   DBA_OBJECTS に対する SELECT  
  
-   ALL_TABLES に対する SELECT  
  
 これらの特権を V$xxx に付与できないときは、V $xxx に付与してください。  
  
### <a name="schema-user"></a>スキーマ ユーザー  
 Oracle スキーマ ユーザーは、キャプチャする Oracle テーブルのスキーマへの読み取りアクセスが可能な Oracle ユーザーです。 このユーザーは、Oracle CDC デザイナー コンソールを操作して Oracle スキーマ、キャプチャするテーブル、その列、インデックス、およびキーの一覧を取得するときに必要です。  
  
 このユーザーの資格情報は格納されません。 必要になるたびに CDC デザイナー コンソールによって要求され、残りの UI セッションの間保持されます。  
  
  
