---
title: Oracle サブスクライバー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- data types [SQL Server replication], non-SQL Server Subscribers
- Oracle Subscribers [SQL Server replication]
- non-SQL Server Subscribers, Oracle
- heterogeneous Subscribers, Oracle
- mapping data types [SQL Server replication]
ms.assetid: 591c0313-82ce-4689-9fc1-73752ff122cf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a97acba6af3cb960cf4d98d26d3f8da4805822da
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907985"
---
# <a name="oracle-subscribers"></a>Oracle サブスクライバー
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]以降の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、Oracle の提供する OLE DB プロバイダーによる、Oracle へのプッシュ サブスクリプションがサポートされています。  
  
## <a name="configuring-an-oracle-subscriber"></a>Oracle サブスクライバーの構成  
 Oracle サブスクライバーを構成するには、次の手順を実行してください。  
  
1.  ディストリビューターが Oracle サブスクライバーに接続できるように、Oracle クライアント ネットワーク ソフトウェアおよび Oracle OLE DB プロバイダーを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターにインストールし、これらを構成します。 Oracle クライアント ネットワーク ソフトウェアは、最新バージョンであることが必要です。 Oracle では、最新バージョンのクライアント ソフトウェアをインストールすることを推奨しています。 このため、データベース ソフトウェアよりもクライアント ソフトウェアの方が新しいバージョンであることがよくあります。 最も簡単にソフトウェアをインストールする方法は、Oracle クライアント ディスクで Oracle Universal Installer を使用することです。 Oracle Universal Installer で、次の情報を指定します。  
  
    |[情報]|[説明]|  
    |-----------------|-----------------|  
    |Oracle ホーム|Oracle ソフトウェアのインストール ディレクトリのパスです。 既定値 (C:\oracle\ora90 など) をそのまま使用するか、別のパスを入力します。 Oracle ホームの詳細については、このトピックの「Oracle ホームに関する注意点」を参照してください。|  
    |Oracle ホーム名|Oracle ホーム パスの別名|  
    |インストールの種類|Oracle 10g では、インストール オプションとして **[Runtime]** または **[Administrator]** を選択してください。|  
  
2.  サブスクライバーの TNS 名を作成します。 TNS (Transparent Network Substrate) とは、Oracle データベースが使用する通信層です。 TNS サービス名は、ネットワーク上での Oracle データベース インスタンスの名前です。 TNS サービス名は、Oracle データベースへの接続を構成するときに割り当てます。 レプリケーションでは TNS サービス名を使用してサブスクライバーを識別し、接続を確立します。  
  
     Oracle Universal Installer が完了したら、Net Configuration Assistant を使用してネットワーク接続を構成します。 ネットワーク接続を構成するには、4 つの情報を指定する必要があります。 Oracle データベース管理者は、データベースとリスナーをセットアップするときにネットワークを構成しています。この情報が不明な場合は、管理者に問い合わせてください。 以下の操作を行う必要があります。  
  
    |操作|[説明]|  
    |------------|-----------------|  
    |データベースを識別する|データベースは 2 とおりの方法で識別できます。 1 つ目は、SID (Oracle System Identifier) を使用する方法で、すべての Oracle リリースで使用できます。 2 つ目は、サービス名を使用する方法で、Oracle リリース 8.0 以降で使用できます。 どちらの方法も、データベースの作成時に構成される値を使用します。データベースのリスナーの構成時に管理者が使用したものと同じ命名方法を、クライアント ネットワーク構成でも使用することが重要です。|  
    |データベースのネットワークの別名を識別する|Oracle データベースへのアクセスに使用するネットワークの別名を指定する必要があります。 ネットワークの別名とは、基本的にはデータベースの作成時に構成されたリモート SID またはサービス名へのポインターです。ネットワークの別名は、各種の Oracle リリースや製品では、ネット サービス名や TNS 別名など、複数の名前で呼ばれています。 SQL*Plus では、ログイン時に "ホスト文字列" パラメーターとしてこの別名の入力画面が表示されます。|  
    |ネットワーク プロトコルを選択する|サポート対象とする適切なプロトコルを選択します。 ほとんどのアプリケーションでは TCP を使用します。|  
    |データベース リスナーを識別するホスト情報を指定する|ホストは、Oracle リスナーを実行中のコンピューターの名前または DNS 別名で、通常はデータベースが存在しているコンピューターです。 プロトコルによっては、追加情報を指定する必要があります。 たとえば、TCP を選択した場合は、リスナーが対象データベースへの接続要求を受信待ちしているポートを指定する必要があります。 既定の TCP 構成ではポート 1521 を使用します。|  
  
3.  スナップショット パブリケーションまたはトランザクション パブリケーションを作成して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーに対して有効にしてから、サブスクライバーに対してプッシュ サブスクリプションを作成します。 詳細については、「 [SQL Server 以外のサブスクライバーのサブスクリプションの作成](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)」を参照してください。  

### <a name="setting-directory-permissions"></a>ディレクトリ権限の設定  
 ディストリビューター上の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスが実行されるアカウントには、Oracle クライアント ネットワーク ソフトウェアがインストールされているディレクトリ (およびすべてのサブディレクトリ) に対する読み取り権限と実行権限を付与する必要があります。  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>SQL Server ディストリビューターと Oracle パブリッシャー間の接続のテスト  
 Net Configuration Assistant の終了間際に、Oracle サブスクライバーへの接続をテストするオプションを選択できます。 接続をテストする前に、Oracle データベース インスタンスがオンラインで、Oracle リスナーが実行中であることを確認してください。 テストが成功しなかった場合、接続しようとするデータベースを担当する Oracle DBA に連絡してください。  
  
 Oracle サブスクライバーに正常に接続できたら、サブスクリプションのディストリビューション エージェントに対して構成したのと同じアカウントとパスワードを使用してデータベースにログインを試みます。  
  
1.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。  
  
2.  「 `cmd` 」と入力して **[OK]** をクリックします。  
  
3.  コマンド プロンプトで、次のように入力します。  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     例 : `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  ネットワーク構成が正常に行われていれば、ログインは成功し、 `SQL` プロンプトが表示されます。  
  
### <a name="considerations-for-oracle-home"></a>Oracle ホームに関する注意点  
 Oracle では、アプリケーション バイナリをサイド バイ サイド インストールできますが、ある時点でレプリケーションが使用できるバイナリ セットは 1 つだけです。 各バイナリ セットは Oracle ホームに関連付けられ、バイナリはディレクトリ %ORACLE_HOME%\bin に格納されます。 レプリケーションが Oracle サブスクライバーに接続するときに、正しいバイナリ セット (具体的には最新バージョンのクライアント ネットワーク ソフトウェア) が使用されるようにしてください。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスおよび [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント サービスで使用されるアカウントを使ってディストリビューターにログインし、適切な環境変数を設定します。 %ORACLE_HOME% 変数は、クライアント ネットワーク ソフトウェアをインストールしたときに指定したインストール ポイントを参照するように設定する必要があります。 %PATH% には、最初に検出される Oracle エントリとして %ORACLE_HOME% \bin ディレクトリを含める必要があります。 環境変数の設定の詳細については、Windows のマニュアルを参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューター上に複数の Oracle ホームがある場合は、ディストリビューション エージェントが最新の Oracle OLE DB プロバイダーを使用していることを確認してください。 場合によっては、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターでクライアント コンポーネントを更新しても既定では OLE DB プロバイダーが更新されないことがあります。 古い OLE DB プロバイダーをアンインストールして、最新の OLE DB プロバイダーをインストールしてください。 プロバイダーのインストールおよびアンインストールの詳細については、Oracle のマニュアルを参照してください。  
  
## <a name="considerations-for-oracle-subscribers"></a>Oracle サブスクライバーに関する注意点  
 トピック「 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)」で説明した注意点の他に、Oracle サブスクライバーにレプリケートする場合は以下の問題に注意してください。  
  
-   Oracle では、空の文字列と NULL 値のどちらも NULL として扱われます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の列を NOT NULL として定義し、それらの列を Oracle サブスクライバーにレプリケートしている場合、この問題は重要です。 変更を Oracle サブスクライバーに適用したときの失敗を回避するには、以下のいずれかを実行する必要があります。  
  
    -   パブリッシュされたテーブルに空の文字列が列値として挿入されないようにする。  
  
    -   ディストリビューション エージェント履歴ログで失敗の通知および処理の続行が可能な場合は、ディストリビューション エージェントに対して **-SkipErrors** パラメーターを使用する。 Oracle エラー コード 1400 ( **-SkipErrors1400**) を指定します。  
  
    -   生成されたテーブルの作成スクリプトを変更して、空の文字列が関連付けられている文字型の列から NOT NULL 属性を削除する。さらに、 @creation_script sp_addarticle [の](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)パラメーターを使用して、アーティクルのカスタム作成スクリプトとして変更済みスクリプトを指定する。  
  
-   Oracle サブスクライバーは 0x4071 のスキーマ オプションをサポートしています。 スキーマ オプションの詳細については、「[sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)」を参照してください。  
  
## <a name="mapping-data-types-from-sql-server-to-oracle"></a>SQL Server から Oracle へのデータ型のマッピング  
 次の表は、Oracle を実行しているサブスクライバーへのデータのレプリケーションで使用される、データ型のマッピングを示しています。  
  
|SQL Server データ型|Oracle データ型|  
|--------------------------|----------------------|  
|**bigint**|NUMBER(19,0)|  
|**binary(1-2000)**|RAW(1-2000)|  
|**binary(2001-8000)**|BLOB|  
|**bit**|NUMBER(1)|  
|**char(1-2000)**|CHAR(1-2000)|  
|**char(2001-4000)**|VARCHAR2(2001-4000)|  
|**char(4001-8000)**|CLOB|  
|**date**|[DATE]|  
|**datetime**|DATE|  
|**datetime2(0-7)**|Oracle 9 および Oracle 10 の場合は TIMESTAMP(7)、Oracle 8 の場合は VARCHAR(27)|  
|**datetimeoffset(0-7)**|Oracle 9 および Oracle 10 の場合は TIMESTAMP(7) WITH TIME ZONE、Oracle 8 の場合は VARCHAR(34)|  
|**decimal(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**float(53)**|FLOAT|  
|**float**|FLOAT|  
|**geography**|BLOB|  
|**geometry**|BLOB|  
|**hierarchyid**|BLOB|  
|**image**|BLOB|  
|**int**|NUMBER(10,0)|  
|**money**|NUMBER(19,4)|  
|**nchar(1-1000)**|CHAR(1-1000)|  
|**nchar(1001-4000)**|NCLOB|  
|**ntext**|NCLOB|  
|**numeric(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**nvarchar(1-1000)**|VARCHAR2(1-2000)|  
|**nvarchar(1001-4000)**|NCLOB|  
|**nvarchar(max)**|NCLOB|  
|**real**|real|  
|**smalldatetime**|DATE|  
|**smallint**|NUMBER(5,0)|  
|**smallmoney**|NUMBER(10,4)|  
|**sql_variant**|なし|  
|**sysname**|VARCHAR2(128)|  
|**text**|CLOB|  
|**time(0-7)**|VARCHAR(16)|  
|**timestamp**|RAW(8)|  
|**tinyint**|NUMBER(3,0)|  
|**uniqueidentifier**|CHAR(38)|  
|**varbinary(1-2000)**|RAW(1-2000)|  
|**varbinary(2001-8000)**|BLOB|  
|**varchar(1-4000)**|VARCHAR2(1-4000)|  
|**varchar(4001-8000)**|CLOB|  
|**varbinary(max)**|BLOB|  
|**varchar(max)**|CLOB|  
|**xml**|NCLOB|  
  
## <a name="see-also"></a>参照  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [パブリケーションのサブスクライブ](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
