---
title: スクリプトの生成とパブリッシュ ウィザード | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql9.swb.generatescriptswizard.chooseviews.f1
- sql13.swb.generatescriptswizard.manageproviders.f1
- sql9.swb.generatescriptswizard.scriptwizarddescription.f1
- sql9.swb.generatescriptswizard.choosedefaults.f1
- sql13.swb.generatescriptswizard.summarypage.f1
- sql13.swb.generatescriptswizard.providerconfiguration.f1
- sql9.swb.generatescriptswizard.chooseuddt.f1
- sql9.swb.generatescriptswizard.chooserules.f1
- sql13.swb.generatescriptswizard.introduction.f1
- sql13.swb.generatescriptswizard.setscriptingoptions.f1
- sql13.swb.generatescriptswizard.saveorpublishscripts.f1
- sql9.swb.generatescriptswizard.progress.f1
- sql9.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.welcome.f1
- sql9.swb.generatescriptswizard.scriptfileoption.f1
- sql13.swb.generatescriptswizard.chooseobjects.f1
- sql13.swb.generatescriptswizard.advancedpublishingoptions.f1
- sql9.swb.generatescriptswizard.selectdatabase.f1
- sql9.swb.generatescriptswizard.choosetables.f1
- sql9.swb.generatescriptswizard.choosestoredprocedures.f1
- sql9.swb.generatescriptswizard.chooseobjecttypes.f1
- sql13.swb.generatescriptswizard.advancedscriptingoptions.f1
- sql9.swb.generatescriptswizard.choosescriptoptions.f1
- sql9.swb.generatescriptswizard.chooseudf.f1
helpviewer_keywords:
- databases [SQL Server], publishing
- publishing databases
- scripts [SQL Server], generating
- scripts [SQL Server], publishing
- databases [SQL Server], generating scripts
- Publish Database Wizard
ms.assetid: 5ee520ba-ec7e-4199-a441-189e9e264b37
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0671a283261a6c0867e4349f8cd0f2baadf0cbd7
ms.sourcegitcommit: a1ddeabe94cd9555f3afdc210aec5728f0315b14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70123000"
---
# <a name="generate-and-publish-scripts-wizard"></a>スクリプトの生成とパブリッシュ ウィザード
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  **スクリプトの生成とパブリッシュ ウィザード** を使用すると、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] または [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]のインスタンス間でデータベースを転送するスクリプトを作成できます。 データベース用のスクリプトは、ローカル ネットワーク上のデータベース エンジンのインスタンスまたは [!INCLUDE[ssSDS](../../includes/sssds-md.md)]から生成できます。 生成したスクリプトは、データベース エンジンの別のインスタンスまたは [!INCLUDE[ssSDS](../../includes/sssds-md.md)]で実行できます。 また、ウィザードを使用して、Database Publishing Services を使用して作成された Web サービスに、データベースの内容を直接パブリッシュすることもできます。 スクリプトの作成は、データベース全体または特定のオブジェクトに限定して行うことができます。  

スクリプトの生成とパブリッシュ ウィザードの使用に関する詳細なチュートリアルについては、[チュートリアル:スクリプト生成ウィザード](https://docs.microsoft.com/sql/ssms/tutorials/scripting-ssms#script-databases)に関するページをご覧ください。


  
## <a name="before-you-begin"></a>はじめに  
 転送元と転送先のデータベースは、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]、または [!INCLUDE[ssDE](../../includes/ssde-md.md)] 以降を実行している [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のインスタンス上に配置できます。  
  
###  <a name="PubHostSvc"></a> ホストされたサービスへのパブリッシュ  
 **スクリプトの生成とパブリッシュ ウィザード** を使用すると、スクリプトの作成に加えて、ホストされた特定の種類の SQL Server Web サービスにデータベースをパブリッシュできます。 SQL Server Hosting Toolkit には、CodePlex 上で共有されているソース プロジェクトとして Database Publishing Services が提供されています。 Database Publishing Services プロジェクトを使用すると、Web ホスティング プロバイダーの顧客がデータベースを簡単に Web サービスに配置できる一連の Web サービスを構築することができます。 SQL Server Hosting Toolkit のダウンロードの詳細については、「 [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025)」をご覧ください。  
  
 データベースを Web ホスティング サービスにパブリッシュするには、ウィザードの **[スクリプト作成オプションの設定]** ページで **[Web サービスにパブリッシュ]** オプションを選択します。  
  
###  <a name="Permissions"></a> Permissions  
 データベースをパブリッシュするには、少なくとも元のデータベースで db_ddladmin 固定データベース ロールのメンバーシップが必要です。 ホスティング プロバイダーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにデータベース スクリプトをパブリッシュするには、少なくともターゲット データベースで db_ddladmin 固定データベース ロールのメンバーシップが必要です。  
  
 また、ホスティング プロバイダーのアカウントにアクセスしてデータベースをウィザードでパブリッシュするには、ユーザー名とパスワードを入力する必要があります。 ソース データベースをパブリッシュする前に、ホスティング プロバイダーにターゲット データベースを作成しておく必要もあります。 パブリッシュを実行すると、その既存のデータベースのオブジェクトは上書きされます。  
  
##  <a name="GenPubScriptWiz"></a> スクリプトの生成とパブリッシュ ウィザードの使用  
 **スクリプトを生成してパブリッシュするには**  
  
1.  **オブジェクト エクスプローラー**で、スクリプト化するデータベースを含んだインスタンスのノードを展開します。  
  
2.  **[タスク]** をポイントし、 **[スクリプトの生成]** をクリックします。  

    ![スクリプト生成ウィザード](media/generate-and-publish-scripts-wizard/generatescripts.png)
  
3.  ウィザードの各ダイアログの手順を実行します。  
  
    -   [[説明] ページ](#Introduction)  
    -   [[オブジェクトの選択] ページ](#ChooseObjects)   
    -   [[スクリプト作成オプションの設定] ページ](#SetScriptOpt)  
    -   [[スクリプト作成の詳細オプション] ページ](#AdvScriptOpt)  
    -   [[プロバイダーの管理] ページ](#MgProviders)   
    -   [[パブリッシングの詳細オプション] ページ](#AdvPubOpts)  
    -   [[プロバイダーの構成] ページ](#ProvConfig)  
    -   [[概要] ページ](#Summary)   
    -   [[スクリプトの保存またはパブリッシュ] ページ](#SavePubScripts)  
  
###  <a name="Introduction"></a> [説明] ページ  
 このページには、スクリプトを生成またはパブリッシュする手順が説明されています。  
  
 **[次回からこのページを表示しない]** : **スクリプトの生成とパブリッシュ ウィザード**を次回起動したときにこのページをスキップします。  
  
  ![[説明] ページ](media/generate-and-publish-scripts-wizard/intro.png)
  
###  <a name="ChooseObjects"></a> [オブジェクトの選択] ページ  
 このページでは、このウィザードで生成されたスクリプトに含めるオブジェクトを選択できます。 次のウィザード ページでは、これらのスクリプトを指定した場所に保存するか、これらのスクリプトを使用して、 [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025)がインストールされているリモートの Web ホスティング プロバイダーにデータベース オブジェクトをパブリッシュするかを選択できます。  
  
 **データベース全体のスクリプトを作成するオプション** : データベース内のすべてのオブジェクトのスクリプトを生成し、データベース自体のスクリプトを含めます。 

   ![すべての DB のスクリプトを作成](media/generate-and-publish-scripts-wizard/scriptall.png) 
  
 **[特定のデータベース オブジェクトの選択]** : ウィザードを制限して、データベース内の選択した特定のオブジェクトのみのスクリプトを生成します。  
  
-   **[データベース オブジェクト]** : スクリプトに含めるオブジェクトを少なくとも 1 つ選択します。  
  
-   **[すべて選択]** : 利用可能なすべてのチェック ボックスをオンにします。  
  
-   **[すべて選択解除]** : すべてのチェック ボックスをオフにします。 続行するには、1 つ以上のデータベース オブジェクトを選択する必要があります。  

   ![特定のデータベースのスクリプトを作成](media/generate-and-publish-scripts-wizard/scriptspecificobjects.png)
  
###  <a name="SetScriptOpt"></a> [スクリプト作成オプションの設定] ページ  
 このページでは、スクリプトを指定した場所に保存するか、スクリプトを使用してリモートの Web ホスティング プロバイダーにデータベース オブジェクトをパブリッシュするかを指定します。 パブリッシュするには、Database Publishing Services Web サービスを使用してインストールされた Web サービスにアクセスできる必要があります。  
  
 **[オプション]** : スクリプトを指定した場所に保存する場合は、 **[スクリプトを指定した場所に保存]** をクリックします。 その後、データベース エンジンのインスタンスまたは [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に対して、保存したスクリプトを実行できます。 リモートの Web ホスティング プロバイダーにデータベース オブジェクトをパブリッシュする場合は、 **[Web サービスにパブリッシュ]** をクリックします。  
  
 **[スクリプトを指定した場所に保存]** : 1 つまたは複数の Transact-SQL スクリプト ファイルを指定した場所に保存します。  

  ![保存](media/generate-and-publish-scripts-wizard/save.png)   
  
-   **[ファイルに保存]** : スクリプトを 1 つ以上の .sql ファイルに保存します。 参照ボタン ( **…** ) をクリックしてファイルの名前と場所を指定します。 同じ名前のファイルが既に存在する場合にそのファイルを置き換えるには、 **[既存のファイルの上書き]** チェック ボックスをオンにします。 スクリプトを生成する方法を指定するには、 **[単一ファイル]** または **[オブジェクトごとに 1 つのファイル]** をクリックします。 スクリプトに使用するテキストの種類を指定するには、 **[Unicode テキスト]** または **[ANSI テキスト]** をクリックします。  
  
-   **[クリップボードに保存]** : Transact-SQL スクリプトをクリップボードに保存します。  
  
-   **[新しいクエリ ウィンドウに保存]** : データベース エンジン クエリ エディター ウィンドウにスクリプトを生成します。 エディター ウィンドウが開いていない場合、スクリプトのターゲットとして新しいエディター ウィンドウが開きます。  
  
 **[Web サービスにパブリッシュ]** : プロバイダーを構成したリモート Web ホスティング サービスに、選択したオブジェクトをパブリッシュします。  
  
-   **[プロバイダーの管理]** : **[プロバイダーの管理]** ダイアログ ボックスが表示されます。 **[プロバイダーの管理]** ダイアログ ボックスでは、ホスティング プロバイダーを追加、編集、および削除できます。 各プロバイダーでは、Web ホスティング サービスへの接続情報と、そのサービス上の対象になるデータベースを指定します。  
  
-   **[詳細設定]** : スクリプトのパブリッシングに関する拡張オプションを選択できる場合には、 **[パブリッシングの詳細オプション]** ダイアログ ボックスが表示されます。  
  
-   **[プロバイダー]** : 選択したオブジェクトのパブリッシュ先のデータベースをホストしている Web ホスティング サービスの接続情報を指定するプロバイダーを選択します。 プロバイダーを選択するには、 **[プロバイダーの管理]** ダイアログ ボックスにプロバイダーが少なくとも 1 つは表示される必要があります。  
  
-   **[対象になるデータベース]** : 選択したオブジェクトのパブリッシュ先のデータベースを選択します。 対象になるデータベースを選択する前に、プロバイダーを選択する必要があります。  
  
###  <a name="AdvScriptOpt"></a> [スクリプト作成の詳細オプション] ページ  
 このページでは、このウィザードでスクリプトを生成する方法を指定できます。 さまざまなオプションを使用できます。 オプションが [データベース エンジンの種類] **で指定したバージョンの SQL Server または** [!INCLUDE[ssSDS](../../includes/sssds-md.md)] によってサポートされていない場合、グレーで表示されます。  

![[詳細設定オプション]](media/generate-and-publish-scripts-wizard/advanced.png)
  
 **[オプション]** : 詳細オプションを指定するには、各オプションの右にある使用可能な設定の一覧から値を選択します。  
  
 **[全般]** : 次のオプションは、スクリプト全体に適用されます。  
  
-   **[ANSI Padding]** : **ANSI PADDING ON** をスクリプトに含めます。 既定値は **True**です。  
  
-   **[ファイルに追加]** : **True**の場合、 **[スクリプト作成オプションの設定]** ページで指定した既存のスクリプトの末尾に、このスクリプトを追加します。 **False**の場合、以前のスクリプトが新しいスクリプトで上書きされます。 既定値は **False**です。  
  
-   **[エラー発生時にスクリプトを続行]** : **False** の場合、エラーが発生した時点でスクリプトの生成を停止します。 **True** の場合は、スクリプトの生成を続行します。 既定値は **False**です。  
  
-   **[UDDT を基本型に変換]** : **True**の場合、ユーザー定義データ型 (UDDT) を、その UDDT の作成に使用された基本データ型に変換します。 スクリプトを実行するデータベースに UDDT が存在しない場合は、 **True** を使用します。 **False**の場合は、UDDT が使用されます。 既定値は **False**です。  
  
-   **[依存オブジェクトのスクリプトを生成]** : 選択したオブジェクトのスクリプトを実行するにあたり、その他のオブジェクトも必要な場合は、それらのオブジェクトのスクリプトも生成します。 既定値は **True**です。  
  
-   **[説明用ヘッダーを含める]** : **True**の場合はスクリプトに説明用のコメントが追加され、オブジェクトごとに、スクリプトが複数のセクションに分割されます。 既定値は **False**です。  
  
-   **[If NOT EXISTS を含める]** : **True**の場合は、オブジェクトが既にデータベースに存在するかどうかを確認するステートメントが追加されます。オブジェクトが既に存在する場合は、新しいオブジェクトは作成されません。 既定値は **False**です。  
  
-   **[システム制約名を含める]** : **False** の場合、元のデータベースで自動的に名前を付けられた制約の既定値は、対象のデータベースで自動的に名前が変更されます。 **True**の場合、制約は元のデータベースと対象のデータベースで同じ名前になります。  
  
-   **[サポートされていないステートメントを含める]** : **False**の場合は、選択したサーバーのバージョンまたはエンジンの種類でサポートされていないオブジェクトのステートメントをスクリプトに含めません。 **True**の場合は、サポートされていないオブジェクトをスクリプトに含めます。 サポートされていないオブジェクトの各ステートメントには、選択した SQL Server バージョンまたはエンジンの種類に対してスクリプトを実行する前にステートメントを編集する必要があるというコメントが付加されます。 既定値は **False**です。  
  
-   **[オブジェクト名を修飾するスキーマ]** : 作成されるオブジェクトの名前にスキーマ名を含めます。 既定値は **True**です。  
  
-   **[バインドのスクリプトを作成]** : 既定のオブジェクトとルール オブジェクトのバインドのスクリプトを生成します。 既定値は **False**です。 詳細については、「[CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md) 」と「[CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)」を参照してください。  
  
-   **[スクリプトの照合順序]** : 照合順序に関する情報をスクリプトに追加します。 既定値は **False**です。 詳細については、「 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
-   **[既定のスクリプトを作成]** : テーブル列の既定値を設定するために使用される既定のオブジェクトを含めます。 既定値は **True**です。 詳細については、「[CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)」を参照してください。  
  
-   **[DROP および CREATE のスクリプトを作成]** : **[CREATE のスクリプトを作成]** の場合、オブジェクトを作成する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを追加します。 **[DROP のスクリプトを作成]** の場合、オブジェクトを削除する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを追加します。 **[DROP および CREATE のスクリプトを作成]** の場合、スクリプトを作成するオブジェクトごとに [!INCLUDE[tsql](../../includes/tsql-md.md)] の DROP ステートメントとその後に CREATE ステートメントをスクリプトに追加します。 既定値は **[CREATE のスクリプトを作成]** です。  
  
-   **[拡張プロパティのスクリプトを作成]** : オブジェクトに拡張プロパティが含まれている場合、それらの拡張プロパティをスクリプトに追加します。 既定値は **True**です。  
  
-   **[エンジンの種類のスクリプト]** : 選択した [!INCLUDE[ssSDS](../../includes/sssds-md.md)] または SQL Server データベース エンジンのインスタンスのいずれかで実行できるスクリプトを作成します。 指定した種類でサポートされていないオブジェクトはスクリプトに追加されません。 既定値は、元のサーバーの種類です。  
  
-   **[サーバーのバージョン互換のスクリプト]** : 選択したバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で実行できるスクリプトを作成します。 あるバージョンの新機能のスクリプトを、それ以前のバージョン用に生成することはできません。 既定値は、元のサーバーのバージョンです。  
  
-   **[スクリプト ログイン]** : スクリプトを生成するオブジェクトがデータベース ユーザーの場合に、このオプションを使用すると、そのユーザーに必要なログインが作成されます。 既定値は **False**です。  
  
-   **[オブジェクトレベル権限のスクリプトを作成]** : データベース内のオブジェクトに権限を設定するためのスクリプトを追加します。 既定値は **False**です。  
  
-   **[統計のスクリプトを作成]** : **[統計のスクリプトを作成]** に設定すると、オブジェクトの統計を再作成する **CREATE STATISTICS** ステートメントが追加されます。 **[統計とヒストグラムのスクリプトを作成します]** オプションを選択すると、ヒストグラムの情報も作成されます。 既定では、 **[統計のスクリプトを作成しません]** が設定されています。 詳細については、「[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)」を参照してください。  
  
-   **[USE DATABASE のスクリプトを作成]** : スクリプトに **USE DATABASE** ステートメントを追加します。 データベース オブジェクトが適切なデータベースに作成されるようにするには、 **USE DATABASE** ステートメントを含めます。 スクリプトが別のデータベースで使用される可能性がある場合は、 **False** を選択して **USE DATABASE** ステートメントを除外します。 既定値は **True**です。 詳細については、「[USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)」を参照してください。  
  
-   **[スクリプトを作成するデータの種類]** - スクリプトを作成する対象を選択します: **[データのみ]** 、 **[スキーマのみ]** 、またはその両方。 既定値は **[スキーマのみ]** です。  
  
 **[テーブル/ビュー オプション]** : 次のオプションは、テーブルまたはビューのスクリプトのみに適用されます。  
  
-   **[変更の追跡のスクリプトを作成]** : 変更の追跡が元のデータベースまたは元のデータベースのテーブルで有効になっている場合に、変更の追跡のスクリプトを作成します。 既定値は **False**です。 詳細については、「[変更の追跡について &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)」を参照してください。  
  
-   **[CHECK 制約のスクリプトを作成]** : **CHECK** 制約をスクリプトに追加します。 既定値は **True**です。 **CHECK** 制約を追加すると、指定した条件を満たすデータのみがテーブルに入力されます。 詳しくは、「 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)」をご覧ください。  
  
-   **[データ圧縮オプションのスクリプトを作成]** : データ圧縮オプションが元のデータベースまたは元のデータベースのテーブルで構成されている場合に、データ圧縮オプションのスクリプトを作成します。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。 既定値は **False**です。  
  
-   **[外部キーのスクリプトを作成]** : 外部キーをスクリプトに追加します。 既定値は **True**です。 外部キーは、テーブル間のリレーションシップを示し、そのリレーションシップを適用します。  
  
-   **[フルテキスト インデックスのスクリプトを作成]** : フルテキスト インデックスを作成するスクリプトを作成します。 既定値は **False**です。  
  
-   **[インデックスのスクリプトを作成]** : インデックスを作成するスクリプトを作成します。 既定値は **True**です。 インデックスを使用すると、データをすばやく検索できます。  
  
-   **[主キーのスクリプトを作成]** : テーブルに主キーを作成するスクリプトを作成します。 既定値は **True**です。 主キーは、テーブルの各行を一意に識別します。  
  
-   **[トリガーのスクリプトを作成]** : テーブルに DML トリガーを作成するスクリプトを作成します。 既定値は **False**です。 DML トリガーは、データベースで DML (データ操作言語) イベントが発生したときに起動されるようにプログラミングされた操作です。 詳しくは、「 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)」をご覧ください。  
  
-   **[一意キーのスクリプトを作成]** : テーブルに一意キーを作成するスクリプトを作成します。 一意キーにより、重複するデータを入力できなくなります。 既定値は **True**です。 詳細については、「 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)」を参照してください。  
  
###  <a name="MgProviders"></a> [プロバイダーの管理] ページ  
 このダイアログ ボックスを使用すると、ホスティング プロバイダー接続を表示、追加、編集、削除、またはテストできます。 ホスティング プロバイダーによって、CodePlex 上にある SQL Server Hosting Toolkit の Database Publishing Service プロジェクトを使用して作成される Web サービスの接続情報が指定されます。  
  
 **[構成済みのプロバイダー]** : 保存されている各ホスティング プロバイダーの名前と **Web** サービス アドレスが一覧表示されます。  
  
 **[新規作成]** : **[新規プロバイダーのプロバイダー構成]** ダイアログ ボックスが開き、新しいホスティング プロバイダーを追加できます。  
  
 **[編集]** : 対応する **[プロバイダーの構成]** ダイアログ ボックスが開き、既存のホスティング プロバイダーを編集できます。  
  
 **[削除]** : 選択したホスティング プロバイダーを削除します。  
  
 **[テスト]** : 選択したプロバイダーの情報を使用して、ホスティング サービスへの接続をテストします。  
  
 **[OK]** : **[ホスティング プロバイダー]** ダイアログ ボックスで行ったすべての変更を保存します。  
  
 **[キャンセル]** : **[ホスティング プロバイダー]** ダイアログ ボックスで行ったすべての変更を取り消します。  
  
###  <a name="AdvPubOpts"></a> [パブリッシングの詳細オプション] ページ  
 このページでは、このウィザードでデータベースをパブリッシュする方法を指定できます。 さまざまなオプションを使用できます。 オプションが [データベース エンジンの種類] **で指定したバージョンの SQL Server または** [!INCLUDE[ssSDS](../../includes/sssds-md.md)] によってサポートされていない場合、グレーで表示されます。  

  ![パブリッシングの詳細](media/generate-and-publish-scripts-wizard/advancedpublish.png)
  
 **[オプション]** : 詳細オプションを指定するには、各オプションの右にある使用可能な設定の一覧から値を選択します。  
  
 **[全般]** : 次のオプションは、パブリケーション全体に適用されます。  
  
1.  **[UDDT を基本型に変換]** : **True**の場合、ユーザー定義データ型 (UDDT) を、その UDDT の作成に使用された基本データ型に変換します。 スクリプトを実行するデータベースに UDDT が存在しない場合は、 **True** を使用します。 **False**の場合は、UDDT が使用されます。 既定値は **False**です。  
  
2.  **[照合順序のパブリッシュ]** - テーブル列の照合順序に関する情報を追加します。 既定値は **False**です。 詳細については、「 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
3.  **[既定値のパブリッシュ]** - テーブル列の既定値を設定するために使用される既定のオブジェクトを含めます。 既定値は **True**です。 詳細については、「[CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)」を参照してください。  
  
4.  **[依存オブジェクトのパブリッシュ]** - 選択したオブジェクトのスクリプトを実行するにあたり、その他のオブジェクトも必要な場合は、それらのオブジェクトもパブリッシュします。 既定値は **True**です。  
  
5.  **[拡張プロパティのパブリッシュ]** - オブジェクトに拡張プロパティが含まれている場合、パブリッシング用のプロバイダーに送信するスクリプトにそれらの拡張プロパティを追加します。 既定値は **True**です。  
  
6.  **[サーバーのバージョン互換のパブリッシュ]** - 選択したバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で実行できるように、パブリッシング用のリモート プロバイダーに送信されるスクリプトを作成します。 あるバージョンの新機能のスクリプトを、それ以前のバージョン用に生成することはできません。 既定値は、元のサーバーのバージョンです。  
  
7.  **[オブジェクトレベル権限のパブリッシュ]** - データベース内の選択したオブジェクトに対する権限を含めます。 既定値は **False**です。  
  
8.  **[統計のパブリッシュ]** - **[統計のパブリッシュ]** に設定すると、オブジェクトの統計を再作成する **CREATE STATISTICS** ステートメントが追加されます。 **[統計とヒストグラムのパブリッシュ]** オプションを選択すると、ヒストグラムの情報も作成されます。 既定では、 **[統計をパブリッシュしない]** が設定されています。 詳細については、「[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)」を参照してください。  
  
9. **[VarDecimal オプションのパブリッシュ]** - **vardecimal** テーブル形式が元のデータベース テーブルで有効になっている場合に、対象のデータベース テーブルでもそのテーブル形式を有効にします。 既定値は **True**です。  
  
10. **[オブジェクト名を修飾するスキーマ]** : 作成されるオブジェクトの名前にスキーマ名を含めます。 既定値は **True**です。  
  
11. **[バインドのスクリプトを作成]** - 既定のオブジェクトとルール オブジェクトのバインドを、パブリッシング用のプロバイダーに送信するスクリプトに追加します。 既定値は **True**です。 詳細については、「[CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md) 」と「[CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)」を参照してください。  
  
12. **[パブリッシュするデータの型]** - スクリプトを作成する対象を選択します: **[データのみ]** 、 **[スキーマのみ]** 、またはその両方。 既定値は **[スキーマとデータ]** です。  
  
 **[パブリッシング オプション]** : Web ホスト プロバイダーをパブリッシュするときにトランザクションを使用するかどうかを指定します。  
  
1.  **[トランザクションを使用してパブリッシュ]** - 選択したオブジェクトをリモートの Web ホスティング プロバイダーにパブリッシュします。 対象データベースでパブリッシュが完了できない場合、トランザクションはロールバックされます。 既定値は **True**です。  
  
 **[テーブル/ビュー オプション]** - 次のオプションは、テーブルまたはビューのみに適用されます。  
  
1.  **[CHECK 制約のパブリッシュ]** - パブリッシュ処理に **CHECK** 制約の作成を含めます。 既定値は **True**です。 **CHECK** 制約を追加すると、指定した条件を満たすデータのみがテーブルに入力されます。 詳細については、「 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)」を参照してください。  
  
2.  **[外部キーのパブリッシュ]** - パブリッシュ処理に外部キーの作成を含めます。 既定値は **True**です。 外部キーは、テーブル間のリレーションシップを示し、そのリレーションシップを適用します。 詳しくは、「 [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md)」をご覧ください。  
  
3.  **[フルテキスト インデックスのパブリッシュ]** - フルテキスト インデックスを作成するスクリプトを作成します。 既定値は **False**です。  
  
4.  **[インデックスのパブリッシュ]** - パブリッシュ処理にテーブルのインデックスを含めます。 既定値は **True**です。 インデックスを使用すると、データをすばやく検索できます。  
  
5.  **[主キーのパブリッシュ]** - パブリッシュ処理に主キーの作成を含めます。 既定値は **True**です。 主キーは、テーブルの各行を一意に識別します。 詳しくは、「 [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md)」をご覧ください。  
  
6.  **[トリガーのパブリッシュ]** - パブリッシュ処理に DML トリガーの作成を含めます。 既定値は **True**です。 DML トリガーは、データベースで DML (データ操作言語) イベントが発生したときに起動されるようにプログラミングされた操作です。 詳しくは、「 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)」をご覧ください。  
  
7.  **[一意キーのパブリッシュ]** - パブリッシュ処理にテーブルの一意キーの作成を含めます。 一意キーにより、重複するデータを入力できなくなります。 既定値は **True**です。 詳しくは、「 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)」をご覧ください。  
  
8.  **[変更の追跡のパブリッシュ]** - 変更の追跡が元のデータベースまたは元のデータベースのテーブルで有効になっている場合に、パブリッシュ処理に変更の追跡を含めます。 既定値は **False**です。 詳細については、「[変更の追跡について &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)」を参照してください。  
  
9. **[データ圧縮オプションのパブリッシュ]** - データ圧縮オプションが元のデータベースまたは元のデータベースのテーブルで構成されている場合に、パブリッシュ処理にデータ圧縮オプションを含めます。 既定値は **True**です。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。  
  
###  <a name="ProvConfig"></a> [プロバイダーの構成] ページ  
 このダイアログ ボックスを使用すると、ホスティング プロバイダーの設定を表示または変更することができます。 このダイアログ ボックスを使用すると、次の操作を実行できます。  
  
-   ホスティング プロバイダーの接続情報の表示、追加、または編集  
  
-   プロバイダー接続用のデータベースの表示、追加、編集、または削除  
  
-   ホスティング プロバイダーのデータベースの自動構成  
  
 ホスティング プロバイダーによって、CodePlex 上にある SQL Server Hosting Toolkit の Database Publishing Service プロジェクトを使用して作成される Web サービスの接続情報が指定されます。  
  
 **[名前]** - ホスティング プロバイダーの名前です。  
  
 **[Web サービス アドレス]** - ホスティング サービスの HTTPS アドレスです。  
  
 **[Web サービス認証]** - ホスティング サービスにログオンするために必要なユーザー名とパスワードです。  
  
 **[パスワードの保存]** - パスワードを暗号化してローカル コンピューターに保存します。  
  
 **[使用できるデータベース]** - ホスティング プロバイダー用に構成されたデータベースが、 *server_name*.*database_name*という形式で昇順に表示されます。  
  
 **[新規作成]** - **[データベース構成]** ダイアログ ボックスが開き、新しいデータベースを追加できます。  
  
 **[編集]** - 選択したデータベースに対応する **[データベース構成]** ダイアログ ボックスが開きます。  
  
 **[削除]** - 選択したデータベースを削除します。  
  
 **[既定に設定]** - データベースを既定のデータベースに設定します。  
  
 **[OK]** - このダイアログ ボックスで行ったすべての変更を保存して、ウィザードに戻ります。  
  
 **[キャンセル]** - このダイアログ ボックスで行ったすべての変更を取り消して、ウィザードに戻ります。  
  
###  <a name="Summary"></a> [概要] ページ  
 このページには、このウィザードで選択したオプションがまとめて表示されます。 オプションを変更するには、 **[戻る]** をクリックします。 保存またはパブリッシュするスクリプトの生成を開始するには、 **[次へ]** をクリックします。  
  
 **[選択内容の確認]** - ウィザードの各ページで行った選択の内容が表示されます。 ノードを展開すると、対応するページで選択したオプションが表示されます。  
  
###  <a name="SavePubScripts"></a> [スクリプトの保存またはパブリッシュ] ページ  
 このページを使用して、実行中のウィザードの進行状況を監視します。  
  
 **[詳細]** - **[アクション]** 列が表示され、ウィザードの進行状況を確認できます。 スクリプトが生成されると、このウィザードでは、選択内容に基づいて、スクリプトをファイルに保存するか、スクリプトを使用して Web サービスにパブリッシュします。 各手順が完了したときに、 **[結果]** 列の値をクリックすると、対応する手順の結果を確認できます。  
  
 **[レポートの保存]** - クリックすると、ウィザードの進行状況の結果がファイルに保存されます。  
  
 **[キャンセル]** - 処理が完了する前やエラーが発生した場合にクリックしてウィザードを閉じます。  
  
 **[完了]** - 処理が完了した後やエラーが発生した場合にクリックしてウィザードを閉じます。  
 
## <a name="generating-scripts-on-azure-sql-data-warehouse"></a>Azure SQL Data Warehouse のスクリプトの生成  

"Script As..." を使用して生成された構文が [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] のような構文になっていないときや、エラー メッセージが表示されたときは、SQL Server Management Studio でスクリプト作成オプションを [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] に設定することが必要な場合があります。  

### <a name="how-to-set-default-scripting-options-to-sql-data-warehouse"></a>既定のスクリプト作成オプションを SQL Data Warehouse に設定する方法  

[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] の構文を使用してオブジェクトのスクリプトを作成するためには、以下のようにして既定のスクリプト作成オプションを [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] に設定します。  

1. **[ツール]** をクリックし、次に **[オプション]** をクリックします。  
2. **[全般スクリプト作成オプション]** で、次のように設定します。  
    1. データベース エンジンの種類に対応したスクリプト:**Microsoft Azure SQL Database**。  
    2. データベース エンジン エディションのスクリプト:**Microsoft Azure SQL Data Warehouse Edition**。  
3. **[OK]** をクリックします。

### <a name="how-to-generate-scripts-for-sql-data-warehouse-when-it-is-not-the-default-scripting-option"></a>SQL Data Warehouse が既定のスクリプト作成オプションになっていないときに SQL Data Warehouse のスクリプトを生成する方法  

上記のように [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] を既定のスクリプト作成オプションとして設定した場合は、この手順を無視できます。 ただし、異なる既定スクリプト作成オプションを使用することを選択すると、エラーが発生する可能性があります。 エラーを避けるためには、次の手順に従って、 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]のスクリプトを生成してパブリッシュします。  

1. SQL Data Warehouse データベースを右クリックします。  
2. **[スクリプトの生成...]** を選択します。  
3. スクリプトを作成するオブジェクトを選択します。  
4. **[スクリプト作成オプション]** で、 **[詳細設定]** をクリックします。 **[全般]** で、次のように設定します。  
    1. データベース エンジンの種類に対応したスクリプト:**Microsoft Azure SQL Database**。  
    2. データベース エンジン エディションのスクリプト:**Microsoft Azure SQL Data Warehouse Edition**。  
5. **[スクリプトの保存またはパブリッシュ]** をクリックし、次に **[完了]** をクリックします。  

手順 4 で設定したオプションは保存されません。 これらのオプションを保存する場合は、「 **既定のスクリプト作成オプションを SQL Data Warehouse に設定する方法**」の手順に従ってください。  
  
## <a name="see-also"></a>参照  
 [SMO のインストール](../../relational-databases/server-management-objects-smo/installing-smo.md)   
 [他のサーバーへのデータベースのコピー](../../relational-databases/databases/copy-databases-to-other-servers.md)  
  
  
