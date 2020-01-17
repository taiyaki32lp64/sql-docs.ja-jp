---
title: マージ アーティクルのカスタム競合回避モジュールの実装 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 47d0f7c4eb6c78b9e551fafdc1e018a27604086e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721232"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>マージ アーティクルのカスタム競合回避モジュールの実装
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)] または [COM ベースのカスタム競合回避モジュール](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)を使用して、マージ アーティクルのカスタム競合回避モジュールを実装する方法について説明します。  
  
 **このトピックの内容**  
  
-   **マージ アーティクルのカスタム競合回避モジュールを実装するためにに使用するもの:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [COM ベースの競合回避モジュール](#COM)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 各パブリッシャーで、固有のカスタム競合回避モジュールを [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャとして記述できます。 同期中に、このストアド プロシージャは、競合回避モジュールが登録されているアーティクル内で競合が発生した場合に呼び出されます。競合する行の情報は、マージ エージェントによってプロシージャの必須パラメーターに渡されます。 ストアド プロシージャ ベースのカスタム競合回避モジュールは、常にパブリッシャーで作成されます。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャ競合回避モジュールは、行の変更ベースの競合を処理するためにのみ呼び出されます。 このモジュールは、他の種類の競合 (PRIMARY KEY 違反による挿入の失敗や一意インデックス制約違反) の処理には使用できません。  
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>ストアド プロシージャ ベースのカスタム競合回避モジュールを作成するには  
  
1.  パブリッシャーのパブリケーションまたは **msdb** データベースで、次の必須パラメーターを実装する新しいシステム ストアド プロシージャを作成します。  
  
    |パラメーター|データ型|説明|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|`sysname`|競合を解決する対象のテーブルの所有者名。 これは、パブリケーション データベース内のテーブルの所有者です。|  
    |**@tablename**|`sysname`|競合を解決する対象のテーブル名。|  
    |**@rowguid**|`uniqueidentifier`|競合している行の一意の識別子。|  
    |**@subscriber**|`sysname`|競合する変更の反映元であるサーバーの名前。|  
    |**@subscriber_db**|`sysname`|競合する変更の反映元であるデータベースの名前。|  
    |**@log_conflict OUTPUT**|`int`|競合を後で解決できるように、マージ処理で競合をログに記録するかどうかを指定します。<br /><br /> **0** = 競合をログに記録しない。<br /><br /> **1** = サブスクライバーは競合で優先されない。<br /><br /> **2** = パブリッシャーは競合で優先されない。|  
    |**@conflict_message OUTPUT**|`nvarchar(512)`|競合をログに記録する場合の解決に関するメッセージ。|  
    |**@destowner**|`sysname`|サブスクライバー側でパブリッシュされたテーブルの所有者。|  
  
     このストアド プロシージャは、マージ エージェントからパラメーターに渡された値を使用して、カスタム競合回避ロジックを実装します。このロジックでは、ベース テーブルと同じ構造を持ち、競合で優先されたバージョンの行のデータ値を含んでいる、単一行の結果セットを返す必要があります。  
  
2.  サブスクライバーでパブリッシャーへの接続に使用される任意のログインに対して、ストアド プロシージャの EXECUTE 権限を許可します。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>新しいテーブル アーティクルにカスタム競合回避モジュールを使用するには  
  
1.  **@article_resolver** パラメーターに **MicrosoftSQL** **Server ストアド プロシージャ競合回避モジュール**の値を、 **@resolver_info** パラメーターに競合回避ロジックを実装するストアド プロシージャの名前を指定し、[sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) を実行してアーティクルを定義します。 詳しくは、「 [Define an Article](publish/define-an-article.md)」をご覧ください。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>既存のテーブル アーティクルにカスタム競合回避モジュールを使用するには  
  
1.  **@publication** と **@article** を指定し、 **@property** に **article_resolver** の値を、 **@value** に **MicrosoftSQL** **Server Stored ProcedureResolver** の値を指定して、[sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) を実行します。  
  
2.  **@publication** と **@article** を指定し、 **@property** に **resolver_info** の値を、 **@value** に競合回避ロジックを実装するストアド プロシージャの名前を指定して、[sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) を実行します。  
  
##  <a name="COM"></a> COM ベースのカスタム競合回避モジュールの使用  
 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 名前空間により実装されるインターフェイスを利用して、マージ レプリケーション同期処理で発生するイベントを処理し、競合を回避するための複雑なビジネス ロジックを作成できます。 詳細については、「 [マージ アーティクルのビジネス ロジック ハンドラーの実装](implement-a-business-logic-handler-for-a-merge-article.md)」を参照してください。 また、ネイティブ コード ベースのカスタム ビジネス ロジックを独自に作成して、競合を回避することもできます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++ などの製品を使用して、このロジックを COM コンポーネントとしてビルドし、ダイナミック リンク ライブラリ (DLL) にコンパイルします。 このような COM ベースのカスタム競合回避モジュールには、競合回避のために用意されている専用の **ICustomResolver** インターフェイスを実装する必要があります。  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>COM ベース カスタム競合回避モジュールを作成して登録するには  
  
1.  COM 互換のオーサリング環境で、カスタム競合回避モジュール ライブラリへの参照を追加します。  
  
2.  Visual C++ プロジェクトの場合は、#import ディレクティブを使用してこのライブラリをプロジェクトにインポートします。  
  
3.  **ICustomResolver** インターフェイスを実装するクラスを作成します。  
  
4.  メソッドとプロパティを実装します。  
  
5.  プロジェクトをビルドして、カスタム競合回避モジュール ライブラリ ファイルを作成します。  
  
6.  マージ エージェントの実行可能ファイルが置かれているディレクトリ (通常は \Microsoft SQL Server\100\COM) に、そのライブラリを配置します。  
  
    > [!NOTE]  
    >  カスタム競合回避モジュールは、プル サブスクリプションの場合はサブスクライバーに、プッシュ サブスクリプションの場合はディストリビューターに、Web 同期に使用する場合は Web サーバーに配置する必要があります。  
  
7.  次のように、配置先のディレクトリから regsvr32.exe を使用してカスタム競合回避モジュール ライブラリを登録します。  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  パブリッシャーで [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) を実行し、そのライブラリがカスタム競合回避モジュールとしてまだ登録されていないことを確認します。  
  
9. カスタム競合回避モジュールとしてライブラリを登録するには、ディストリビューターで [sp_registercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql) を実行します。 COM オブジェクトのフレンドリ名を指定 **@article_resolver** のライブラリの ID (CLSID)  **@resolver_clsid** の値と`false`の **@is_dotnet_assembly** .  
  
    > [!NOTE]  
    >  カスタム競合回避モジュールが不要になったら、[sp_unregistercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql) を使用して登録を解除できます。  
  
10. (省略可) クラスターで手順 5. ～ 8. を繰り返して、クラスターの全ノードにカスタム競合回避モジュールを登録します。 この手順は、フェールオーバーの後にカスタム競合回避モジュールに調整エージェントを適切に読み込むために必要です。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>新しいテーブル アーティクルにカスタム競合回避モジュールを使用するには  
  
1.  パブリッシャーで [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) を実行し、目的の競合回避モジュールの表示名をメモします。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) を実行してアーティクルを定義します。 手順 1. で調べたアーティクル競合回避モジュールの表示名を **@article_resolver** を使用して、マージ アーティクルのカスタム競合回避モジュールを実装する方法について説明します。 詳しくは、「 [アーティクルを定義](publish/define-an-article.md)」をご覧ください。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>既存のテーブル アーティクルにカスタム競合回避モジュールを使用するには  
  
1.  パブリッシャーで [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) を実行し、目的の競合回避モジュールの表示名をメモします。  
  
2.  [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) を実行し、 **@publication** 、 **@article** を指定し、 **@property** に **article_resolver** 値、 **@value** に手順 1 のアーティクル競合回避モジュールの表示名を指定します。  
  
#### <a name="viewing-a-sample-custom-resolver"></a>サンプルのカスタム競合回避モジュールの表示  
  
1.  SQL Server 2000 サンプル ファイルにサンプルが提供されています。 ダウンロード、 [ **sql2000samples.zip**](https://github.com/Microsoft/sql-server-samples/blob/master/samples/tutorials/Miscellaneous/sql2000samples.zip)します。 これにより、6.9 MB に 3 つのファイルがダウンロードされます。  
  
2.  ダウンロードされた圧縮済み .cab ファイルからファイルを抽出します。  
  
3.  **setup.exe**を実行します。  
  
    > [!NOTE]  
    >  インストール オプションを選択する場合は、 **レプリケーション** サンプルをインストールするだけで済みます。 (既定のインストール パスは**C:\Program Files (x86) \Microsoft SQL Server 2000 Samples\1033\\** )  
  
4.  インストール フォルダーに移動します。 (既定のフォルダーは **C:\Program Files (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\unzip_sqlreplSP3.exe**)  
  
5.  **unzip_sqlreplSP3.exe** プログラムを実行します。  
  
    > [!NOTE]  
    >  サンプルの com 競合回避モジュールが (既定で) **C:\Program Files (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\resolver\subspres** フォルダーにインストールします。  
  
6.  **subspres** フォルダーで、すべてのソース ファイルで **#include sqlres.h** を検出し、 **#import "replrec.dll" no_namespace, raw_interfaces_only**で置き換えます。  
  
## <a name="see-also"></a>関連項目  
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [COM-Based Custom Resolvers](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [レプリケーション セキュリティの推奨事項](security/replication-security-best-practices.md)  
  
  
