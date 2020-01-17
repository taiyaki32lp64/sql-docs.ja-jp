---
title: カスタム競合回避モジュールの実装 (マージ)
description: SQL Server でマージ パブリケーションのカスタム競合回避モジュールを実装する方法について説明します。
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
- merge replication conflict resolution [SQL Server replication], stored procedure-based resolvers
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a71c7c83afe2fcb8b0192f6dfd12c8072ccdc392
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322162"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>マージ アーティクルのカスタム競合回避モジュールを実装する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)] または [COM ベースのカスタム競合回避モジュール](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)を使用して、マージ アーティクルのカスタム競合回避モジュールを実装する方法について説明します。  
  
 **このトピックの内容**  
  
-   **以下を使用して、マージ アーティクルのカスタム競合回避モジュールを実装する**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [COM ベースの競合回避モジュール](#COM)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 各パブリッシャーで、固有のカスタム競合回避モジュールを [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャとして記述できます。 同期中に、競合回避モジュールが登録されたアーティクルで競合が発生すると、このストアド プロシージャが呼び出されます。 マージ エージェントによって、競合している行に関する情報が、プロシージャの必須パラメーターに渡されます。 ストアド プロシージャ ベースのカスタム競合回避モジュールは、常にパブリッシャーで作成されます。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャ競合回避モジュールは、行の変更ベースの競合を処理するためにのみ呼び出されます。 他の種類の競合 (PRIMARY KEY 違反や一意インデックス制約違反によってトリガーされたエラーなど) を処理するためにそれらを使用することはできません。
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>ストアド プロシージャ ベースのカスタム競合回避モジュールを作成するには  
  
1.  パブリッシャーのパブリケーションまたは **msdb** データベースで、次の必須パラメーターを実装する新しいシステム ストアド プロシージャを作成します。  
  
    |パラメーター|データ型|[説明]|  
    |---------------|---------------|-----------------|  
    |**\@tableowner**|**sysname**|競合を解決する対象のテーブルの所有者名。 これは、パブリケーション データベース内のテーブルの所有者です。|  
    |**\@tablename**|**sysname**|競合を解決する対象のテーブル名。|  
    |**\@rowguid**|**uniqueidentifier**|競合がある行の一意の識別子。|  
    |**\@subscriber**|**sysname**|競合する変更の反映元であるサーバーの名前。|  
    |**\@subscriber_db**|**sysname**|競合する変更の反映元であるデータベースの名前。|  
    |**\@log_conflict OUTPUT**|**int**|後で解決できるように、マージ処理で競合をログに記録するかどうかを設定します。<br /><br /> **0** = 競合をログに記録しない。<br /><br /> **1** = サブスクライバーは競合で優先されない。<br /><br /> **2** = パブリッシャーは競合で優先されない。|  
    |**\@conflict_message OUTPUT**|**nvarchar(512)**|競合をログに記録する場合の解決に関するメッセージ。|  
    |**\@destowner**|**sysname**|サブスクライバー側でパブリッシュされたテーブルの所有者。|  
  
     このストアド プロシージャでは、マージ エージェントによってこれらのパラメーターに渡された値を使用して、カスタム競合解決ロジックが実装されます。 ベース テーブルと構造が同じであり、行の競合するバージョンのデータ値が格納されている単一行の結果セットが返される必要があります。  
  
2.  サブスクライバーでパブリッシャーへの接続に使用される任意のログインに対して、ストアド プロシージャの EXECUTE 権限を許可します。  

#### <a name="use-a-custom-conflict-resolver-with-a-new-table-article"></a>新しいテーブル アーティクルでカスタム競合回避モジュールを使用する  
  
1. [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を実行してアーティクルを定義します。 
1. **\@article_resolver** パラメーターに対して、**MicrosoftSQL** **サーバー ストアド プロシージャ競合回避モジュール**の値を指定します。 
1. **\@resolver_info** パラメーターに対して、競合回避ロジックを実装するストアド プロシージャの名前を指定します。 

   詳しくは、「[アーティクルの定義](../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>既存のテーブル アーティクルにカスタム競合回避モジュールを使用するには  
  
1.  **\@publication** と **\@article** を指定し、 **\@property** に **article_resolver** の値を、 **\@value** に **MicrosoftSQL** **Server Stored ProcedureResolver** の値を指定して、[sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行します。  
  
2.  **\@publication** と **\@article** を指定し、 **\@property** に **resolver_info** の値を、 **\@value** に競合回避ロジックを実装するストアド プロシージャの名前を指定して、[sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行します。  
  
##  <a name="COM"></a> COM ベースのカスタム競合回避モジュールの使用  
 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 名前空間で実装されるインターフェイスを利用して、イベントを処理し、マージ レプリケーション同期処理で発生する競合を回避するための複雑なビジネス ロジックを作成できます。 詳細については、「[マージ アーティクルのビジネス ロジック ハンドラーの実装](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)」を参照してください。 また、ネイティブ コード ベースのカスタム ビジネス ロジックを独自に作成して、競合を回避することもできます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++ などの製品を使用して、このロジックを COM コンポーネントとしてビルドし、ダイナミック リンク ライブラリ (DLL) にコンパイルします。 この種の COM ベースのカスタム競合回避モジュールには、競合回避専用に設計されている **ICustomResolver** インターフェイスを実装する必要があります。  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>COM ベース カスタム競合回避モジュールを作成して登録するには  
  
1.  COM 互換のオーサリング環境で、カスタム競合回避モジュール ライブラリへの参照を追加します。  
  
2.  Visual C++ プロジェクトの場合は、#import ディレクティブを使用してこのライブラリをプロジェクトにインポートします。  
  
3.  **ICustomResolver** インターフェイスを実装するクラスを作成します。  
  
4.  メソッドとプロパティを実装します。  
  
5.  プロジェクトをビルドして、カスタム競合回避モジュール ライブラリ ファイルを作成します。  
  
6.  マージ エージェントの実行可能ファイルが置かれているディレクトリ (通常は \Microsoft SQL Server\100\COM) に、そのライブラリを配置します。  
  
    > [!NOTE]  
    >  カスタム競合回避モジュールは、プル サブスクリプションの場合はサブスクライバーに、プッシュ サブスクリプションの場合はディストリビューターに、Web 同期に使用する場合は Web サーバーに配置する必要があります。  
  
7.  次のように、配置先のディレクトリから regsvr32.exe を実行して、カスタム競合回避モジュール ライブラリを登録します。  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  パブリッシャーで [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) を実行して、そのライブラリがカスタム競合回避モジュールとしてまだ登録されていないことを確認します。  
  
9. カスタム競合回避モジュールとしてライブラリを登録するには、ディストリビューターで [sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) を実行します。 COM オブジェクトの表示名を **\@article_resolver** に指定し、ライブラリの ID (CLSID) を **\@resolver_clsid** に指定し、**false** を **\@is_dotnet_assembly** に指定します。  
  
    > [!NOTE]  
    >  カスタム競合回避モジュールが不要になったら、[sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) を使用して登録を解除できます。  
  
10. (省略可) クラスターで手順 6 から 9 を繰り返して、クラスターの全ノードにカスタム競合回避モジュールを登録します。 これらの手順は、フェールオーバーの後にカスタム競合回避モジュールで調整エージェントを適切に読み込むために必要です。
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>新しいテーブル アーティクルにカスタム競合回避モジュールを使用するには  
  
1.  パブリッシャーで [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) を実行し、目的の競合回避モジュールの表示名をメモします。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を実行してアーティクルを定義します。 手順 1. で調べたアーティクル競合回避モジュールの表示名を **\@article_resolver** に指定します。 詳しくは、「[アーティクルの定義](../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>既存のテーブル アーティクルにカスタム競合回避モジュールを使用するには  
  
1.  パブリッシャーで [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) を実行し、目的の競合回避モジュールの表示名をメモします。  
  
2.  [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行し、 **\@publication**、 **\@article** を指定し、 **\@property** に **article_resolver** 値、 **\@value** に手順 1 のアーティクル競合回避モジュールの表示名を指定します。  
  

## <a name="see-also"></a>参照  
 [マージ レプリケーションの競合検出および解決の詳細](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [COM ベースのカスタム競合回避モジュール](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [レプリケーション セキュリティの推奨事項](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
