---
title: マージ アーティクル競合回避モジュールの指定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
- merge replication conflict resolution [SQL Server replication], merge article resolvers
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 388d400160e3fa7b3240c7a9c014bcf36ae25f3a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68212092"
---
# <a name="specify-a-merge-article-resolver"></a>マージ アーティクル競合回避モジュールの指定
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、マージ アーティクル競合回避モジュールを指定する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
-   **マージ アーティクル競合回避モジュールを指定するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   マージ レプリケーションでは、以下の競合回避モジュールが使用できます。  
  
    -   既定の競合回避モジュール。 既定の競合回避モジュールの動作は、サブスクリプションがクライアント サブスクリプションまたはサーバー サブスクリプションのどちらであるかによって異なります。 サブスクリプションの種類の指定について詳しくは、「[マージ サブスクリプションの種類と競合解決の優先度の指定 &#40;SQL Server Management Studio&#41;](../specify-a-merge-subscription-type-and-conflict-resolution-priority.md)」をご覧ください。  
  
    -   ユーザーの作成したカスタム競合回避モジュール。ビジネス ロジック ハンドラー (マネージド コードで作成) または COM ベースのカスタム競合回避モジュールです。 詳しくは、「 [Advanced Merge Replication Conflict Detection and Resolution](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)を使用して、マージ アーティクル競合回避モジュールを指定する方法について説明します。 競合する行だけでなく、レプリケートされた各行に対して実行するカスタム ロジックを実装する必要がある場合は、「 [マージ アーティクルのビジネス ロジック ハンドラーの実装](../implement-a-business-logic-handler-for-a-merge-article.md)を使用して、マージ アーティクル競合回避モジュールを指定する方法について説明します。  
  
    -   標準の COM ベース競合回避モジュール。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に含まれています。  
  
-   既定以外の競合回避モジュールを使用する場合は、マージ エージェントが動作しているコンピューターにそのモジュールをコピーして登録する必要があります (ビジネス ロジック ハンドラーを使用している場合は、そのビジネス ロジック ハンドラーもパブリッシャー側で登録する必要があります)。 マージ エージェントは、以下の場所で実行されます。  
  
    -   プッシュ サブスクリプションの場合はディストリビューター  
  
    -   プル サブスクリプションの場合はサブスクライバー  
  
    -   Web 同期を使用するプル サブスクリプションの場合は [!INCLUDE[msCoName](../../../includes/msconame-md.md)] インターネット インフォメーション サービス (IIS) サーバー  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 競合回避モジュールを登録した後、 **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[競合回避モジュール]** タブでアーティクルが競合回避モジュールを使用するように指定します。このダイアログ ボックスは、パブリケーションの新規作成ウィザードおよび **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスから使用できます。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](create-a-publication.md)」および「[View and Modify Publication Properties](view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
#### <a name="to-specify-a-resolver"></a>競合回避モジュールを指定するには  
  
1.  パブリケーションの新規作成ウィザードの **[アーティクル]** ページまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで、テーブルを選択します。  
  
2.  **[アーティクルのプロパティ]** をクリックしてから、 **[反転表示されたテーブル アーティクルのプロパティを設定]** をクリックします。  
  
3.  **[アーティクルのプロパティ - \<Article>]** ページで、 **[競合回避モジュール]** タブをクリックします。  
  
4.  **[ディストリビューターに登録されたカスタム競合回避モジュールを使用する]** を選択し、一覧から競合回避モジュールをクリックします。  
  
5.  競合回避モジュールが入力 (列名など) を必要とする場合は **[競合回避モジュールが必要とする情報の入力]** ボックスで指定します。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  競合回避モジュールを必要とする各アーティクルについて、この処理を繰り返します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-register-a-custom-conflict-resolver"></a>カスタム競合回避モジュールを登録するには  
  
1.  固有のカスタム競合回避モジュールを登録する場合は、次のいずれかの種類を作成します。  
  
    -   ビジネス ロジック ハンドラーとしてのマネージド コード ベースの競合回避モジュール。 詳細については、「 [マージ アーティクルのビジネス ロジック ハンドラーの実装](../implement-a-business-logic-handler-for-a-merge-article.md)」を参照してください。  
  
    -   ストアド プロシージャ ベースの競合回避モジュールと COM-ベースの競合回避モジュール。 詳しくは、「 [マージ アーティクルのカスタム競合回避モジュールの実装](../implement-a-custom-conflict-resolver-for-a-merge-article.md)」をご覧ください。  
  
2.  目的の競合回避モジュールが既に登録されているかを判断するには、パブリッシャーの任意のデータベースに対して [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) を実行します。 これにより、カスタム競合回避モジュールの説明、およびディストリビューターに登録された各 COM ベースの競合回避モジュールのクラス識別子 (LSID)、またはディストリビューターに登録された各ビジネス ロジック ハンドラーのマネージド アセンブリの情報が表示されます。  
  
3.  目的のカスタム競合回避モジュールがまだ登録されていない場合は、ディストリビューターで [sp_registercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql) を実行します。 **@article_resolver** に競合回避モジュールの名前を指定します。ビジネス ロジックの場合はアセンブリの表示名です。 COM ベース競合回避モジュールの DLL の CLSID を指定 **@resolver_clsid** 、ビジネス ロジック ハンドラーでは、指定の値と`true`の **@is_dotnet_assembly** アセンブリの名前 **@dotnet_assembly_name** 、オーバーライドするクラスの完全修飾名と<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>の **@dotnet_class_name** します。  
  
    > [!NOTE]  
    >  マージ エージェント実行可能ファイルがあるディレクトリ、マージ エージェントを同期的に起動するアプリケーションがあるディレクトリ、およびグローバル アセンブリ キャッシュ (GAC) の、いずれとも異なる場所にビジネス ロジック ハンドラー アセンブリが配置されている場合は、 **@dotnet_assembly_name** を使用して、マージ アーティクル競合回避モジュールを指定する方法について説明します。  
  
4.  競合回避モジュールが COM ベースの場合  
  
    -   カスタム競合回避モジュール DLL をプッシュ サブスクリプションのディストリビューター、またはプル サブスクリプションのサブスクライバーにコピーします。  
  
        > [!NOTE]  
        >  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] カスタム競合回避モジュールは、 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM ディレクトリにあります。  
  
    -   regsvr32.exe を使用して、カスタム競合回避モジュール DLL をオペレーティング システムに登録します。 たとえば、次のコマンドをコマンド プロンプトから実行すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Additive Conflict Resolver が登録されます。  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  競合回避モジュールがビジネス ロジック ハンドラーである場合は、マージ エージェント実行可能ファイル (replmerg.exe) と同じフォルダー、マージ エージェントを起動するアプリケーションと同じフォルダー、または手順 3. で **@dotnet_assembly_name** パラメーターに指定したフォルダーのいずれかにアセンブリを配置します。  
  
    > [!NOTE]  
    >  マージ エージェント実行可能ファイルの既定のインストール場所は、 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM です。  
  
#### <a name="to-specify-a-custom-resolver-when-defining-a-merge-article"></a>マージ アーティクルを定義するときにカスタム競合回避モジュールを指定するには  
  
1.  カスタム競合回避モジュールを使用する場合は、上記の手順に従って競合回避モジュールを作成および登録します。  
  
2.  パブリッシャーで、[sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) を実行し、結果セットの **value** フィールドに示された目的のカスタム競合回避モジュールの名前を確認します。  
  
3.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) を実行します。 **@article_resolver** に手順 2. の競合回避モジュールの名前を指定し、 **@resolver_info** パラメーターを使ってカスタム競合回避モジュールの必須入力をすべて指定します。 ストアド プロシージャ ベースのカスタム競合回避モジュールの場合、 **@resolver_info** はストアド プロシージャの名前です。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] によって提供される競合回避モジュールの必須入力の詳細については、「[Microsoft COM ベースの競合回避モジュール](../merge/advanced-merge-replication-conflict-com-based-resolvers.md)」を参照してください。  
  
#### <a name="to-specify-or-change-a-custom-resolver-for-an-existing-merge-article"></a>既存のマージ アーティクルに対するカスタム競合回避モジュールを指定または変更するには  
  
1.  アーティクルに対してカスタム競合回避モジュールが定義されているかどうかを判断するには、[sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) を実行します。 アーティクルに対してカスタム競合回避モジュールが定義されている場合は、 **article_resolver** フィールドに名前が表示されます。 競合回避モジュールに対するすべての入力が結果セットの **resolver_info** フィールドに表示されます。  
  
2.  パブリッシャーで、[sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) を実行し、結果セットの **value** フィールドに示された目的のカスタム競合回避モジュールの名前を確認します。  
  
3.  パブリッシャー側のパブリケーション データベースに対して、[sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) を実行します。 **@property** にビジネス ロジック ハンドラーの完全パスを含む **article_resolver** の値を、 **@value** に手順 2 の目的のカスタム競合回避モジュールの名前を指定します。  
  
4.  カスタム競合回避モジュールの必須入力を変更するには、[sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) を再度実行します。 **@property** に **resolver_info** の値を、 **@value** にカスタム競合回避モジュールの必須入力を指定します。 ストアド プロシージャ ベースのカスタム競合回避モジュールの場合、 **@resolver_info** はストアド プロシージャの名前です。 必須入力の詳細については、「[Microsoft COM ベースの競合回避モジュール](../merge/advanced-merge-replication-conflict-com-based-resolvers.md)」を参照してください。  
  
#### <a name="to-unregister-a-custom-conflict-resolver"></a>カスタム競合回避モジュールの登録を解除するには  
  
1.  パブリッシャーで [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) を実行し、結果セットの **value** フィールドに示された、削除するカスタム競合回避モジュールの名前を確認します。  
  
2.  ディストリビューターで、[sp_unregistercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql) を実行します。 **@article_resolver** に、手順 1 のカスタム競合回避モジュールの完全な名前を指定します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、新しいアーティクルを作成し、競合が発生したときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] UnitPrice **列の平均の計算に** Averaging Conflict Resolver が使用されるように指定します。  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../snippets/tsql/SQL15/replication/howto/tsql/mergearticleresolvers.sql#sp_addmerge_resolver)]  
  
 次の例では、アーティクルを変更して、競合が発生したときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] UnitsOnOrder **列の合計の計算に** Additive Conflict Resolver が使用されるように指定します。  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../snippets/tsql/SQL15/replication/howto/tsql/mergearticleresolvers.sql#sp_changemerge_resolver)]  
  
## <a name="see-also"></a>参照  
 [Advanced Merge Replication Conflict Detection and Resolution](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [マージ アーティクルのビジネス ロジック ハンドラーの実装](../implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
