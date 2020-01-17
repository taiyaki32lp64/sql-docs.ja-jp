---
title: マージ アーティクルのビジネス ロジック ハンドラーの設定
description: レプリケーション プログラミングまたはレプリケーション管理オブジェクトを使用し、マージ レプリケーション同期のビジネス ロジック ハンドラーを構成します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], business logic handlers
- merge replication business logic handlers [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
- business logic handlers [SQL Server replication]
- BusinessLogicModule class
ms.assetid: ed477595-6d46-4fa2-b0d3-a5358903ec05
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8ba12a2dc53b845d52d2a3dcac574bed08865c12
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322149"
---
# <a name="implement-a-business-logic-handler-for-a-merge-article"></a>マージ アーティクルのビジネス ロジック ハンドラーの実装
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] でレプリケーション プログラミングまたはレプリケーション管理オブジェクト (RMO) を使用して、マージ アーティクルにビジネス ロジック ハンドラーを実装する方法について説明します。  
  
 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 名前空間は、マージ レプリケーションの同期処理中に発生するイベントを処理する、複雑なビジネス ロジックを記述するためのインターフェイスを実装します。 ビジネス ロジック ハンドラーのメソッドは、同期中にレプリケートされる変更行ごとに、レプリケーション処理から呼び出すことができます。  
  
 ビジネス ロジック ハンドラーを実装するための一般的な手順を次に示します。  
  
1.  ビジネス ロジック ハンドラーのアセンブリを作成します。  
  
2.  ディストリビューターにアセンブリを登録します。  
  
3.  マージ エージェントが実行されるサーバーにアセンブリを配置します。 プル サブスクリプションの場合、エージェントはサブスクライバー上で実行されます。プッシュ サブスクリプションの場合、エージェントはディストリビューター上で実行されます。 Web 同期を使用した場合、エージェントは Web サーバー上で実行されます。  
  
4.  ビジネス ロジック ハンドラーを使用するアーティクルを作成するか、またはビジネス ロジック ハンドラーを使用する既存のアーティクルを変更します。  
  
 指定するビジネス ロジック ハンドラーは、同期されるすべての行に対して実行されます。 その他のアプリケーションまたはネットワーク サービスに対する複雑なロジックおよび呼び出しは、パフォーマンスに影響を与える可能性があります。 ビジネス ロジック ハンドラーについて詳しくは、「[Execute Business Logic During Merge Synchronization](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)」(マージ同期中のビジネス ロジックの実行) をご覧ください。  
  
 **このトピックの内容**  
  
-   **マージ アーティクルにビジネス ロジック ハンドラーを実装するために使用するもの:**  
  
     [レプリケーション プログラミング](#ReplProg)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="ReplProg"></a> レプリケーション プログラミングの使用  
  
#### <a name="to-create-and-deploy-a-business-logic-handler"></a>ビジネス ロジック ハンドラーを作成および配置するには  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio で、.NET アセンブリの新しいプロジェクトを作成し、ビジネス ロジック ハンドラーの実装コードを記述します。  
  
2.  次の名前空間の参照をプロジェクトに追加します。  
  
    |アセンブリ参照|Location|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM (既定インストール)|  
    |<xref:System.Data>|GAC (.NET Framework のコンポーネント)|  
    |<xref:System.Data.Common>|GAC (.NET Framework のコンポーネント)|  
  
3.  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> クラスをオーバーライドするクラスを追加します。  
  
4.  処理対象の変更の種類を指定する <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> プロパティを実装します。  
  
5.  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> クラスのメソッドのうち、次のいずれかまたは複数のメソッドをオーバーライドします。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> - 同期中、データ変更がコミットされたときに呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> - DELETE ステートメントをアップロードまたはダウンロードするときにエラーが発生すると呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> - DELETE ステートメントをアップロードまたはダウンロードするときに呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> - INSERT ステートメントをアップロードまたはダウンロードするときにエラーが発生すると呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> - INSERT ステートメントをアップロードまたはダウンロードするときに呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> - パブリッシャーおよびサブスクライバーで、UPDATE ステートメントの競合が発生した場合に呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> - パブリッシャーおよびサブスクライバーで、UPDATE ステートメントと DELETE ステートメントが競合した場合に呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> - UPDATE ステートメントをアップロードまたはダウンロードするときにエラーが発生すると呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> - UPDATE ステートメントをアップロードまたはダウンロードするときに呼び出されます。  
  
6.  プロジェクトをビルドして、ビジネス ロジック ハンドラー アセンブリを作成します。  
  
7.  アセンブリを、マージ エージェント実行可能ファイル (replmerg.exe) を含むディレクトリ (既定のインストールの場合は [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM) に配置するか、.NET グローバル アセンブリ キャッシュ (GAC) にインストールします。 マージ エージェント以外のアプリケーションがアセンブリへのアクセスを必要とする場合は、アセンブリを GAC にのみインストールしてください。 アセンブリを GAC にインストールするには、.NET Framework SDK のグローバル アセンブリ キャッシュ ツール (**Gacutil.exe** ) を使用します。  
  
    > [!NOTE]  
    >  ビジネス ロジック ハンドラーは、Web 同期を使用するときに replisapi.dll をホストする IIS サーバーなど、マージ エージェントを実行する各サーバーに配置する必要があります。  
  
#### <a name="to-register-a-business-logic-handler"></a>ビジネス ロジック ハンドラーを登録するには  
  
1.  パブリッシャーで、[sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) を実行して、アセンブリがまだビジネス ロジック ハンドラーとして登録されていないことを確認します。  
  
2.  ディストリビューターで、[sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) を実行します。 **\@article_resolver** にビジネス ロジック ハンドラーの表示名を、 **\@is_dotnet_assembly** に **true** を、 **\@dotnet_assembly_name** にアセンブリの名前を、 **\@dotnet_class_name** に <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> をオーバーライドするクラスの完全修飾名を指定します。  
  
    > [!NOTE]  
    >  マージ エージェント実行可能ファイルがあるディレクトリ、マージ エージェントを同期的に起動するアプリケーションがあるディレクトリ、およびグローバル アセンブリ キャッシュ (GAC) の、いずれとも異なる場所にアセンブリが配置されている場合は、 **\@dotnet_assembly_name** にアセンブリ名を含む完全なパスを指定する必要があります。 Web 同期を使用する場合は、Web サーバーでアセンブリの位置を指定する必要があります。  
  
#### <a name="to-use-a-business-logic-handler-with-a-new-table-article"></a>新しいテーブル アーティクルでビジネス ロジック ハンドラーを使用するには  
  
1.  [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を実行してアーティクルを定義し、 **\@article_resolver** にビジネス ロジック ハンドラーの表示名を指定します。 詳しくは、「 [アーティクルを定義](../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
#### <a name="to-use-a-business-logic-handler-with-an-existing-table-article"></a>既存のテーブル アーティクルでビジネス ロジック ハンドラーを使用するには  
  
1.  [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行し、 **\@publication**、 **\@article** を指定し、 **\@property** に **article_resolver** 値、 **\@value** にビジネス ロジック ハンドラーの表示名を指定します。  
  
###  <a name="TsqlExample"></a> 例 (レプリケーション プログラミング)  
 次の例に、監査ログを作成するビジネス ロジック ハンドラーを示します。  
  
 [!code-cs[HowTo#rmo_BusinessLogicCode](../../relational-databases/replication/codesnippet/csharp/rmohowto/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 次の例では、ビジネス ロジック ハンドラー アセンブリをディストリビューターに登録し、カスタム ビジネス ロジックを使用するように既存のマージ アーティクルを変更します。  
  
 [!code-sql[HowTo#sp_RegisterBLH_10](../../relational-databases/replication/codesnippet/tsql/implement-a-business-log_3.sql)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
  
#### <a name="to-create-a-business-logic-handler"></a>ビジネス ロジック ハンドラーを作成するには  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio で、.NET アセンブリの新しいプロジェクトを作成し、ビジネス ロジック ハンドラーの実装コードを記述します。  
  
2.  次の名前空間の参照をプロジェクトに追加します。  
  
    |アセンブリ参照|Location|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM (既定インストール)|  
    |<xref:System.Data>|GAC (.NET Framework のコンポーネント)|  
    |<xref:System.Data.Common>|GAC (.NET Framework のコンポーネント)|  
  
3.  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> クラスをオーバーライドするクラスを追加します。  
  
4.  処理対象の変更の種類を指定する <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> プロパティを実装します。  
  
5.  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> クラスのメソッドのうち、次のいずれかまたは複数のメソッドをオーバーライドします。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> - 同期中、データ変更がコミットされたときに呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> - DELETE ステートメントのアップロードまたはダウンロード時、エラーが発生した場合に呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> - DELETE ステートメントをアップロードまたはダウンロードするときに呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> - INSERT ステートメントのアップロードまたはダウンロード時、エラーが発生した場合に呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> - INSERT ステートメントをアップロードまたはダウンロードするときに呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> - パブリッシャーおよびサブスクライバーで、UPDATE ステートメントの競合が発生した場合に呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> - パブリッシャーおよびサブスクライバーで、UPDATE ステートメントと DELETE ステートメントが競合した場合に呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> - UPDATE ステートメントのアップロードまたはダウンロード時、エラーが発生した場合に呼び出されます。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> - UPDATE ステートメントをアップロードまたはダウンロードするときに呼び出されます。  
  
    > [!NOTE]  
    >  アーティクル競合時の処理がカスタム ビジネス ロジックによって明示的に定義されていない場合は、アーティクルの既定の競合回避モジュールによって処理されます。  
  
6.  プロジェクトをビルドして、ビジネス ロジック ハンドラー アセンブリを作成します。  
  
#### <a name="to-register-a-business-logic-handler"></a>ビジネス ロジック ハンドラーを登録するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、ディストリビューターへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> クラスのインスタンスを作成します。 手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を渡します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumBusinessLogicHandlers%2A> を呼び出し、返された <xref:System.Collections.ArrayList> オブジェクトをチェックして、そのアセンブリがビジネス ロジック ハンドラーとしてまだ登録されていないことを確認します。  
  
4.  <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler> クラスのインスタンスを作成します。 次のプロパティを指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetAssemblyName%2A> - .NET アセンブリの名前です。 マージ エージェントの実行可能ファイルがあるディレクトリ、マージ エージェントを同期的に起動するアプリケーションがあるディレクトリ、および GAC の、いずれとも異なる場所にアセンブリが配置されている場合は、アセンブリ名に完全パスを含める必要があります。 ビジネス ロジック ハンドラーを Web 同期で使用する場合は、アセンブリ名に完全パスを含める必要があります。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetClassName%2A> - <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> をオーバーライドし、ビジネス ロジック ハンドラーを実装するクラスの完全修飾名です。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> - ビジネス ロジック ハンドラーへのアクセス時に使用する表示名です。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.IsDotNetAssembly%2A> - **\@is_dotnet_assembly**」を参照してください。  
  
#### <a name="to-deploy-a-business-logic-handler"></a>ビジネス ロジック ハンドラーを配置するには  
  
1.  マージ エージェントが実行されるサーバーにアセンブリを配置します。格納場所は、ディストリビューターにビジネス ロジック ハンドラーを登録したときに指定した場所になります。 プル サブスクリプションの場合、エージェントはサブスクライバー上で実行されます。プッシュ サブスクリプションの場合、エージェントはディストリビューター上で実行されます。 Web 同期を使用した場合、エージェントは Web サーバー上で実行されます。 ビジネス ロジック ハンドラーの登録時、アセンブリ名に完全パスを含めなかった場合は、マージ エージェントの実行可能ファイルがあるディレクトリ (マージ エージェントを同期的に起動するアプリケーションがあるディレクトリ) にアセンブリを配置してください。 同じアセンブリを使用するアプリケーションが複数存在する場合は、アセンブリを GAC にインストールする必要があります。  
  
#### <a name="to-use-a-business-logic-handler-with-a-new-table-article"></a>新しいテーブル アーティクルでビジネス ロジック ハンドラーを使用するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeArticle> クラスのインスタンスを作成します。 次のプロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Article.Name%2A>にアーティクル名を指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>にパブリケーション名を指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A>にパブリケーション データベース名を指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A>にビジネス ロジック ハンドラーの表示名 ( <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>) を指定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.Article.Create%2A> メソッドを呼び出します。 詳しくは、「 [アーティクルを定義](../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
#### <a name="to-use-a-business-logic-handler-with-an-existing-table-article"></a>既存のテーブル アーティクルでビジネス ロジック ハンドラーを使用するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeArticle> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.Article.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> の各プロパティを設定します。  
  
4.  手順 1. で作成した接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから **false**が返された場合、手順 3. で指定したアーティクルのプロパティが正しく定義されていないか、アーティクルが存在していません。 詳しくは、「 [View and Modify Article Properties](../../relational-databases/replication/publish/view-and-modify-article-properties.md)」をご覧ください。  
  
6.  <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>にビジネス ロジック ハンドラーの表示名を設定します。 これは、ビジネス ロジック ハンドラーの登録時に指定した <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> プロパティの値になります。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次のビジネス ロジック ハンドラーの例では、サブスクライバーでの挿入、更新、および削除に関する情報をログに記録します。  
  
 [!code-cs[HowTo#rmo_BusinessLogicCode](../../relational-databases/replication/codesnippet/csharp/rmohowto/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 次の例では、ディストリビューターにビジネス ロジック ハンドラーを登録します。  
  
 [!code-cs[HowTo#rmo_RegisterBLH_10](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_registerblh_10)]  
  
 [!code-vb[HowTo#rmo_vb_RegisterBLH_10](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_registerblh_10)]  
  
 次の例では、既存のアーティクルを変更してビジネス ロジック ハンドラーを使用します。  
  
 [!code-cs[HowTo#rmo_ChangeMergeArticle_BLH](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## <a name="see-also"></a>参照  
 [マージ アーティクルのカスタム競合回避モジュールの実装](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [ビジネス ロジック ハンドラーのデバッグ&#40;レプリケーション プログラミング&#41;](../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [レプリケーション管理オブジェクトの概念](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
  
  
