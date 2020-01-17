---
title: Oracle パブリッシャーの構成 | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], configuring
ms.assetid: 240c8416-c8e5-4346-8433-07e0f779099f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d6c0aa05f095907b39cacf39f65dfc3b09d9786e
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907188"
---
# <a name="configure-an-oracle-publisher"></a>Oracle パブリッシャーの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Oracle パブリッシャーからパブリケーションを作成する方法は、通常のスナップショットおよびトランザクション パブリケーションを作成する方法と同じですが、Oracle パブリッシャーからパブリケーションを作成する前に、次の手順を実行する必要があります (手順 1、3、および 4 については、このトピックで詳しく説明します)。  
  
1.  提供されているスクリプトを使用して Oracle データベース内にレプリケーション管理ユーザーを作成します。  
  
2.  パブリッシュするテーブルに、各テーブルの SELECT アクセス許可を、手順 1. で作成した Oracle 管理ユーザーに対して直接 (ロールを通じてではなく) 許可します。  
  
3.  Oracle クライアント ソフトウェアと OLE DB プロバイダーを [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターにインストールしてから、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを停止して再起動します。 ディストリビューターを 64 ビットのプラットフォームで実行している場合は、64 ビット バージョンの Oracle OLE DB プロバイダーを使用する必要があります。  
  
4.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターで Oracle データベースをパブリッシャーとして構成します。  

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、トランザクション レプリケーションとスナップショット レプリケーションに対する次の異種シナリオをサポートします。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーへのデータのパブリッシュ  

-   Oracle に対するデータのパブリッシュには次の制限があります。  

  | |2016 以前 |2017 以降 |
  |-------|-------|--------|
  |Oracle からのレプリケーション |Oracle 10g 以前のみをサポート |Oracle 10g 以前のみをサポート |
  |Oracle へのレプリケーション |Oracle 12c まで |サポートされていません |

 SQL Server 以外のサブスクライバーへの異種レプリケーションは非推奨とされます。 Oracle パブリッシングは非推奨とされます。 データを移動するには、変更データ キャプチャと [!INCLUDE[ssIS](../../../includes/ssis-md.md)]を使用してソリューションを作成します。  


 Oracle データベースからレプリケートできるオブジェクトの一覧については、「[Design Considerations and Limitations for Oracle Publishers (Oracle パブリッシャーの設計上の注意点と制限)](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)」を参照してください。  
  
> [!NOTE]  
>  パブリッシャーまたはディストリビューターを有効にし、Oracle パブリケーションまたは Oracle パブリケーションのサブスクリプションを作成するには、 **sysadmin** 固定サーバー ロールのメンバーであることが必要です。  
  
## <a name="creating-the-replication-administrative-user-schema-within-the-oracle-database"></a>Oracle データベース内でのレプリケーション管理ユーザー スキーマの作成  
 レプリケーション エージェントは、Oracle データベースに接続して、ユーザー スキーマのコンテキストで操作を実行します。このユーザー スキーマは作成する必要があります。 このスキーマには多くの権限を許可する必要があります。この権限については、次のセクションに示します。 このスキーマは、Oracle パブリッシャーでの [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション プロセスで作成されたすべてのオブジェクト (パブリック シノニム **MSSQLSERVERDISTRIBUTOR**は除く) を所有します。 Oracle データベースで作成したオブジェクトの詳細については、「 [Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)」を参照してください。  
  
> [!NOTE]  
>  **MSSQLSERVERDISTRIBUTOR** パブリック シノニムと、 **CASCADE** オプションで構成した Oracle レプリケーション ユーザーを削除すると、Oracle パブリッシャーからすべてのレプリケーション オブジェクトが削除されます。  
  
 Oracle レプリケーション ユーザー スキーマのセットアップに役立つサンプル スクリプトが提供されています。 このスクリプトは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール後、 *\<drive>* :\\\Program Files\Microsoft SQL Server\\ *\<InstanceName>* \MSSQL\Install\oracleadmin.sql ディレクトリで使用できます。 このスクリプトについては、「 [Script to Grant Oracle Permissions](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)」でも説明します。  
  
 DBA 特権を持つアカウントを使用して Oracle データベースに接続し、スクリプトを実行します。 このスクリプトでは、レプリケーション管理ユーザー スキーマのユーザーとパスワード、およびオブジェクトを作成するときに使用する既定のテーブルスペースの入力が要求されます (このテーブルスペースは Oracle データベース内に存在していることが必要です)。 オブジェクトに他のテーブルスペースを指定する方法の詳細については、「[Manage Oracle Tablespaces (Oracle テーブルスペースの管理)](../../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md)」を参照してください。 ユーザー名と複雑なパスワードを選択しますが、後で Oracle データベースをパブリッシャーとして構成するときにこの情報を提供する必要があるため、どちらもメモしておいてください。 スキーマはレプリケーションに必要なオブジェクトでのみ使用し、このスキーマではパブリッシュするテーブルを作成しないでください。  
  
### <a name="creating-the-user-schema-manually"></a>手動によるユーザー スキーマの作成  
 レプリケーション管理ユーザー スキーマを手動で作成する場合は、スキーマに次の権限を直接またはデータベース ロールを通じて許可する必要があります。  
  
-   CREATE PUBLIC SYNONYM および DROP PUBLIC SYNONYM  
  
-   CREATE PROCEDURE  
  
-   CREATE SEQUENCE  
  
-   CREATE SESSION  
  
 また、次の権限を、(ロールを通じてではなく) 直接ユーザーに許可する必要もあります。  
  
-   CREATE ANY TRIGGER。 これは、スナップショット レプリケーションとトランザクション レプリケーションの両方の場合にのみ必要です。  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
## <a name="installing-and-configuring-oracle-client-networking-software-on-the-sql-server-distributor"></a>SQL Server ディストリビューターへの Oracle クライアント ネットワーク ソフトウェアのインストールと構成  
 Oracle クライアント ネットワーク ソフトウェアおよび Oracle OLE DB プロバイダーを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターにインストールして構成し、ディストリビューターが Oracle パブリッシャーと接続できるようにします。 ソフトウェアをインストールしたら、ソフトウェアがインストールされているフォルダーに適切な権限を設定し、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを停止して再起動してからすべての設定が更新されているかどうかを確認します (権限については、この後の「ディレクトリ権限の設定」を参照してください)。  
  
> [!NOTE]  
>  Oracle クライアント ネットワーク ソフトウェアは、最新バージョンであることが必要です。 Oracle では、最新バージョンのクライアント ソフトウェアをインストールすることを推奨しています。 このため、データベース ソフトウェアよりもクライアント ソフトウェアの方が新しいバージョンであることがよくあります。  
  
 クライアント ネットワーク ソフトウェアを最も簡単にインストールおよび構成するには、Oracle クライアント ディスクの Oracle Universal Installer と Net Configuration Assistant を使用します。  
  
 Oracle Universal Installer で、次の情報を指定する必要があります。  
  
|[情報]|[説明]|  
|-----------------|-----------------|  
|Oracle ホーム|Oracle ソフトウェアのインストール ディレクトリのパスです。 既定値 (C:\oracle\ora90 など) をそのまま使用するか、別のパスを入力します。 Oracle ホームの詳細については、このトピックの「Oracle ホームに関する注意点」を参照してください。|  
|Oracle ホーム名|Oracle ホーム パスの別名|  
|インストールの種類|Oracle 10g では、インストール オプションとして **[Administrator]** を選択してください。|  
  
 Oracle Universal Installer が完了したら、Net Configuration Assistant を使用してネットワーク接続を構成します。 ネットワーク接続を構成するには、4 つの情報を指定する必要があります。 Oracle データベース管理者は、データベースとリスナーをセットアップするときにネットワークを構成しています。この情報が不明な場合は、管理者に問い合わせてください。 以下の操作を行う必要があります。  
  
|操作|[説明]|  
|------------|-----------------|  
|データベースを識別する|データベースは 2 とおりの方法で識別できます。 1 つ目は、SID (Oracle System Identifier) を使用する方法で、すべての Oracle リリースで使用できます。 2 つ目は、サービス名を使用する方法で、Oracle リリース 8.0 以降で使用できます。 どちらの方法も、データベースの作成時に構成される値を使用します。データベースのリスナーの構成時に管理者が使用したものと同じ命名方法を、クライアント ネットワーク構成でも使用することが重要です。|  
|データベースのネットワークの別名を識別する|Oracle データベースへのアクセスに使用するネットワークの別名を指定する必要があります。 Oracle データベースを、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターでパブリッシャーとして識別するときに、この別名を指定します。 ネットワークの別名とは、基本的にはデータベースの作成時に構成されたリモート SID またはサービス名へのポインターです。ネットワークの別名は、各種の Oracle リリースや製品では、ネット サービス名や TNS 別名など、複数の名前で呼ばれています。 SQL*Plus では、ログイン時に "ホスト文字列" パラメーターとしてこの別名の入力画面が表示されます。|  
|ネットワーク プロトコルを選択する|サポート対象とする適切なプロトコルを選択します。 ほとんどのアプリケーションでは TCP を使用します。|  
|データベース リスナーを識別するホスト情報を指定する|ホストは、Oracle リスナーを実行中のコンピューターの名前または DNS 別名で、通常はデータベースが存在しているコンピューターです。 プロトコルによっては、追加情報を指定する必要があります。 たとえば、TCP を選択した場合は、リスナーが対象データベースへの接続要求を受信待ちしているポートを指定する必要があります。 既定の TCP 構成ではポート 1521 を使用します。|  
  
### <a name="setting-directory-permissions"></a>ディレクトリ権限の設定  
 ディストリビューター上の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスが実行されるアカウントには、Oracle クライアント ネットワーク ソフトウェアがインストールされているディレクトリ (およびすべてのサブディレクトリ) に対する読み取り権限と実行権限を付与する必要があります。  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>SQL Server ディストリビューターと Oracle パブリッシャー間の接続のテスト  
 Net Configuration Assistant の終了間際に、Oracle パブリッシャーへの接続をテストするオプションを選択できます。 接続をテストする前に、Oracle データベース インスタンスがオンラインで、Oracle リスナーが実行中であることを確認してください。 テストが成功しなかった場合、接続しようとするデータベースを担当する Oracle DBA に連絡してください。  
  
 Oracle パブリッシャーへの接続に成功したら、作成したレプリケーション管理ユーザー スキーマに関連付けられたアカウントとパスワードを使用してデータベースにログインします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスが使用しているアカウントと同じ Windows アカウントで実行している場合は、次の操作を行う必要があります。  
  
1.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。  
  
2.  「 `cmd` 」と入力して **[OK]** をクリックします。  
  
3.  コマンド プロンプトで、次のように入力します。  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     例: `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  ネットワーク構成が正常に行われていれば、ログインは成功し、`SQL` プロンプトが表示されます。  
  
5.  Oracle データベースへの接続中に問題が発生した場合は、「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 」の「 [ssNoVersion](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。  
  
### <a name="considerations-for-oracle-home"></a>Oracle ホームに関する注意点  
 Oracle では、アプリケーション バイナリをサイド バイ サイド インストールできますが、ある時点でレプリケーションが使用できるバイナリ セットは 1 つだけです。 各バイナリ セットは Oracle ホームに関連付けられ、バイナリはディレクトリ %ORACLE_HOME%\bin に格納されます。 レプリケーションが Oracle パブリッシャーに接続するときに、正しいバイナリ セット (具体的には最新バージョンのクライアント ネットワーク ソフトウェア) が使用されるようにしてください。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスおよび [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント サービスで使用されるアカウントを使ってディストリビューターにログインし、適切な環境変数を設定します。 %ORACLE_HOME% 変数は、クライアント ネットワーク ソフトウェアをインストールしたときに指定したインストール ポイントを参照するように設定する必要があります。 %PATH% には、最初に検出される Oracle エントリとして %ORACLE_HOME% \bin ディレクトリを含める必要があります。 環境変数の設定の詳細については、Windows のマニュアルを参照してください。  
  
## <a name="configuring-the-oracle-database-as-a-publisher-at-the-sql-server-distributor"></a>SQL Server ディストリビューターでの Oracle データベースのパブリッシャーとしての構成  
 Oracle パブリッシャーは常にリモート ディストリビューターを使用するため、Oracle パブリッシャーのディストリビューターとして機能するように [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスを構成する必要があります。1 つの Oracle パブリッシャーは 1 つのディストリビューターのみ使用しますが、1 つのディストリビューターは複数の Oracle パブリッシャーに対応できます。 ディストリビューターを構成したら、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターで、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、Transact-SQL、レプリケーション管理オブジェクト (RMO) を通じて Oracle データベース インスタンスをパブリッシャーとして識別します。 ディストリビューターの構成の詳細については、「[Configure Distribution (ディストリビューションの構成)](../../../relational-databases/replication/configure-distribution.md)」を参照してください。  
  
> [!NOTE]  
>  Oracle パブリッシャーの名前を、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターと同じ名前、または同じディストリビューターを使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パブリッシャーと同じ名前にすることはできません。  
  
 Oracle データベースをパブリッシャーとして識別する場合は、次の Oracle パブリッシング オプションを選択する必要があります: [Complete] または [Oracle (ゲートウェイ)] パブリッシャーを識別した後は、パブリッシャーをいったん削除して再構成しない限り、このオプションは変更できません。 [Complete] オプションでは、スナップショット パブリケーションとトランザクション パブリケーションに、Oracle パブリッシングでサポートされるすべての機能セットが提供されます。 [Oracle (ゲートウェイ)] オプションでは、システム間のゲートウェイとしてレプリケーションが機能する場合にパフォーマンスを向上させるための最適化が行われます。  
  
 Oracle パブリッシャーを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターで識別した後、レプリケーションによって Oracle データベースの TNS サービス名と同じ名前のリンク サーバーが作成されます。 このリンク サーバーはレプリケーションでのみ使用できます。 リンク サーバー接続で Oracle パブリッシャーに接続する必要がある場合は、別の TNS サービス名を作成してから、[sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) を呼び出すときにこの名前を使用します。  
  
 Oracle パブリッシャーを構成してパブリケーションを作成するには、「 [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Administrative Considerations for Oracle Publishers (Oracle パブリッシャーの管理上の注意点)](../../../relational-databases/replication/non-sql/administrative-considerations-for-oracle-publishers.md)   
 [Data Type Mapping for Oracle Publishers (Oracle パブリッシャーのデータ型マッピング)](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Glossary of Terms for Oracle Publishing (Oracle パブリッシングの用語)](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Oracle パブリッシングの概要](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
