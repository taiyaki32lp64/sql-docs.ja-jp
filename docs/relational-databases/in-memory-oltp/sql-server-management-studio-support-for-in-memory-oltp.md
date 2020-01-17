---
title: SSMS によるインメモリ OLTP のサポート
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ee847b5f-6a1a-448e-a746-d61a023881ff
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e9bd4cb0c2fff4259814f6e33a65777023a801fd
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412530"
---
# <a name="sql-server-management-studio-support-for-in-memory-oltp"></a>SQL Server Management Studio によるインメモリ OLTP のサポート
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インフラストラクチャを管理するための統合環境です。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを構成、監視、および管理するためのツールが備わっています。 詳細については、「 [SQL Server Management Studio](https://msdn.microsoft.com/library/66a6b7b1-de6a-4161-82bd-98ded486947b)」を参照してください。  
  
 このトピックのタスクでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してメモリ最適化テーブル、メモリ最適化テーブルのインデックス、ネイティブ コンパイル ストアド プロシージャ、およびユーザー定義のメモリ最適化テーブル型を管理する方法について説明します。  
  
 プログラムによってメモリ最適化テーブルを作成する方法については、「 [メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャの作成](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)」を参照してください。  
  
### <a name="to-create-a-database-with-a-memory-optimized-data-filegroup"></a>メモリ最適化データ ファイル グループが含まれるデータベースを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンのインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を右クリックし、 **[新しいデータベース]** をクリックします。  
  
3.  新しいメモリ最適化データ ファイル グループを追加するには、 **[ファイル グループ]** ページをクリックします。 **[メモリ最適化データ]** で **[ファイル グループの追加]** をクリックし、メモリ最適化データ ファイル グループの名前を入力します。  **[FILESTREAM ファイル]** という列は、ファイル グループ内のコンテナー数を表します。 コンテナーは、 **[全般]** ページで追加します。  
  
4.  ファイル グループにファイル (コンテナー) を追加するには、 **[全般]** ページをクリックします。 **[データベース ファイル]** の **[追加]** をクリックします。 **[ファイルの種類]** として **[FILESTREAM データ]** を選択し、コンテナーの論理名を指定して、メモリ最適化ファイル グループを選択します。次に **[自動拡張 / 最大サイズ]** が **[無制限]** に設定されていることを確認します。  

     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して新しいデータベースを作成する方法の詳細については、「 [データベースの作成](../../relational-databases/databases/create-a-database.md)」を参照してください。  
  
### <a name="to-create-a-memory-optimized-table"></a>メモリ最適化テーブルを作成するには  
  
1.  **オブジェクト エクスプローラー**で、データベースの **[テーブル]** ノードを右クリックし、 **[新規]** 、 **[メモリ最適化テーブル]** の順にクリックします。  
  
     メモリ最適化テーブルを作成するためのテンプレートが表示されます。  
  
2.  テンプレートのパラメーターを置き換えるには、 **[クエリ]** メニューの **[テンプレート パラメーターの値の指定]** をクリックします。  
  
     テンプレートの使用方法の詳細については、「 [テンプレート エクスプローラー](../../ssms/template/template-explorer.md)」を参照してください。  
  
3.  **オブジェクト エクスプローラー**では、テーブルはまずディスク ベース テーブル、次にメモリ最適化テーブルの順に並べ替えられます。 すべてのテーブルを名前順で確認するには、「 **オブジェクト エクスプローラーの詳細** 」を使用します。  
  
### <a name="to-create-a-natively-compiled-stored-procedure"></a>ネイティブ コンパイル ストアド プロシージャを作成するには  
  
1.  **オブジェクト エクスプローラー**で、データベースの **[ストアド プロシージャ]** ノードを右クリックし、 **[新規]** 、 **[ネイティブ コンパイル ストアド プロシージャ]** の順にクリックします。  
  
     ネイティブ コンパイル ストアド プロシージャを作成するためのテンプレートが表示されます。  
  
2.  テンプレートのパラメーターを置き換えるには、 **[クエリ]** メニューの **[テンプレート パラメーターの値の指定]** をクリックします。  
  
     新しいストアド プロシージャを作成する方法の詳細については、「 [ストアド プロシージャの作成](../../relational-databases/stored-procedures/create-a-stored-procedure.md)」を参照してください。  
  
### <a name="to-create-a-user-defined-memory-optimized-table-type"></a>ユーザー定義のメモリ最適化テーブル型を作成するには  
  
1.  **[オブジェクト エクスプローラー]** でデータベースの **[種類]** ノードを展開し、 **[ユーザー定義テーブル型]** ノードを右クリックします。次に **[新規作成]** をクリックし、 **[ユーザー定義のメモリ最適化テーブル型]** をクリックします。  
  
     ユーザー定義のメモリ最適化テーブル型を作成するためのテンプレートが表示されます。  
  
2.  テンプレートのパラメーターを置き換えるには、 **[クエリ]** メニューの **[テンプレート パラメーターの値の指定]** をクリックします。  
  
     新しいストアド プロシージャを作成する方法の詳細については、「[CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)」を参照してください。  
  
## <a name="memory-monitoring"></a>メモリの監視  
  
#### <a name="view-memory-usage-by-memory-optimized-objects-report"></a>メモリ最適化オブジェクトによるメモリ使用量レポートの表示  
  
-   **オブジェクト エクスプローラー**でデータベースを右クリックし、 **[レポート]** 、 **[標準レポート]** 、 **[メモリ最適化オブジェクトによるメモリ使用量]** の順にクリックします。  
  
     このレポートでは、データベース内のメモリ最適化オブジェクトによるメモリ領域の使用に関して詳細なデータが提供されます。  
  
#### <a name="view-properties-for-allocated-and-used-memory-for-a-table-database"></a>テーブルまたはデータベースに対する割り当てメモリおよび使用メモリのプロパティの表示  
  
1.  インメモリ使用量に関する情報を取得します。  
  
    -   **[オブジェクト エクスプローラー]** でメモリ最適化テーブルを右クリックし、 **[プロパティ]** 、 **[ストレージ]** ページの順にクリックします。 **[データ領域]** プロパティの値は、テーブル内のデータによって使用されるメモリを示します。 **[インデックス領域]** プロパティの値は、テーブルのインデックスによって使用されるメモリを示します。  
  
    -   **[オブジェクト エクスプローラー]** で、データベースを右クリックし、 **[プロパティ]** 、 **[全般]** ページの順にクリックします。 **[メモリ最適化オブジェクトに割り当てられたメモリ]** プロパティの値は、データベースのメモリ最適化オブジェクトに割り当てられたメモリを示します。 **[メモリ最適化オブジェクトに使用されるメモリ]** プロパティの値は、データベースのメモリ最適化オブジェクトに使用されるメモリを示します。  
  
## <a name="supported-features-in-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>でサポートされる機能 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、メモリ最適化データ ファイル グループ、メモリ最適化テーブル、インデックス、およびネイティブ コンパイル ストアド プロシージャを含むデータベースのデータベース エンジンによってサポートされる操作と機能をサポートしています。  
  
 データベース、テーブル、ストアド プロシージャ、ユーザー定義テーブル型、またはインデックス オブジェクトについては、インメモリ OLTP をサポートするために [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の次の機能が更新または拡張されています。  
  
-   オブジェクト エクスプローラー  
  
    -   コンテキスト メニュー  
  
    -   フィルターの設定  
  
    -   スクリプト化  
  
    -   処理手順  
  
    -   Reports  
  
    -   Properties  
  
    -   データベース タスク:  
  
        -   メモリ最適化テーブルを含むデータベースをアタッチおよびデタッチします。  
  
             **[データベースのアタッチ]** のユーザー インターフェイスには、メモリ最適化データ ファイル グループは表示されません。 ただし、データベースのアタッチを続行することはでき、データベースは正しくアタッチされます。  
  
            > [!NOTE]  
            >  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してメモリ最適化データ ファイル グループ コンテナーを持つデータベースをアタッチする場合、データベースのメモリ最適化データ ファイル グループ コンテナーが別のコンピューター上に作成されているときには、両方のコンピューターでメモリ最適化データ ファイル グループ コンテナーの場所が同じである必要があります。 新しいコンピューターでデータベースのメモリ最適化データ ファイル グループ コンテナーを別の場所に配置する場合は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用してデータベースをアタッチできます。 次の例では、新しいコンピューターのメモリ最適化データ ファイル グループ コンテナーの場所は C:\Folder2 です。 ただし、最初のコンピューターでは、メモリ最適化データ ファイル グループ コンテナーは C:\Folder1 に作成されています。  
            >   
            >  `CREATE DATABASE[imoltp] ON`  
            >   
            >  `(NAME =N'imoltp',FILENAME=N'C:\Folder2\imoltp.mdf'),`  
            >   
            >  `(NAME =N'imoltp_mod1',FILENAME=N'C:\Folder2\imoltp_mod1'),`  
            >   
            >  `(NAME =N'imoltp_log',FILENAME=N'C:\Folder2\imoltp_log.ldf')`  
            >   
            >  `FOR ATTACH`  
            >   
            >  `GO`  
  
        -   スクリプトの生成。  
  
             **スクリプトの生成とパブリッシュ ウィザード**で、 **[オブジェクトの有無を確認する]** スクリプト作成オプションの既定値は FALSE です。 ウィザードの **[スクリプト作成オプションの設定]** 画面で、 **[オブジェクトの有無を確認する]** スクリプト作成オプションの値を TRUE に設定すると、生成されるスクリプトに "CREATE PROCEDURE <プロシージャ名> AS" および "ALTER PROCEDURE <プロシージャ名> <プロシージャ定義>" が含められます。 生成されたスクリプトを実行すると、ネイティブ コンパイル ストアド プロシージャが ALTER PROCEDURE をサポートしていないことが原因で、エラーが返されます。  
  
             ネイティブ コンパイル ストアド プロシージャごとに生成されるスクリプトを変更するには  
  
            1.  In "CREATE PROCEDURE <プロシージャ名> AS" で、"AS" を "<プロシージャ定義>" に置き換えます。  
  
            2.  "ALTER PROCEDURE <プロシージャ名> <プロシージャ定義>" を削除します。  
  
        -   データベースのコピー。 メモリ最適化オブジェクトを含むデータベースの場合、コピー先サーバー上にデータベースを作成する動作とデータを転送する動作が 1 回のトランザクション内で実行されることはありません。  
  
        -   データのインポートとエクスポート。 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードの [1 つ以上のテーブルまたはビューからデータをコピーする]** オプションを使用します。 対象のテーブルが転送先データベースに存在しないメモリ最適化テーブルの場合には、以下の手順を実行します。  
  
            1.  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザード**の **[テーブルのコピーまたはクエリの指定]** 画面で、 **[1 つ以上のテーブルまたはビューのデータをコピーする]** を選択します。 続けて、 **[次へ]** をクリックします。  
  
            2.  **[マッピングの編集]** をクリックします。 **[変換先テーブルを作成する]** 、 **[SQL の編集]** の順にクリックします。 CREATE TABLE 構文を入力して、転送先データベースにメモリ最適化テーブルを作成します。 **[OK]** をクリックし、ウィザードの残りの手順を実行します。  
  
        -   メンテナンス プラン。 インデックスを再構成し、再構築するメンテナンス タスクは、メモリ最適化テーブルとそのインデックスではサポートされません。 このため、インデックスを再構築および再構成するメンテナンス プランを実行しても、選択したデータベース内のメモリ最適化テーブルおよびそのインデックスは省略されます。  
  
             メンテナンス タスクの統計の更新は、メモリ最適化テーブルおよびそのインデックスのサンプル スキャンではサポートされていません。 したがって、統計の更新のメンテナンス プランを実行すると、メモリ最適化テーブルおよびそのインデックスの統計は、常に **WITH FULLSCAN, NORECOMPUTE**に更新されます。  
  
-   [オブジェクト エクスプローラーの詳細] ペイン  
  
-   テンプレート エクスプローラー  
  
## <a name="unsupported-features-in-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>でサポートされない機能 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 インメモリ OLTP オブジェクトに対して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、データベース エンジンでもサポートされない機能と操作はサポートしていません。  
  
 サポートされていない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能の詳細については、「 [インメモリ OLTP に対してサポートされていない SQL Server の機能](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)」を参照してください 。  
  
## <a name="see-also"></a>参照  
 [SQL Server によるインメモリ OLTP のサポート](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)  
  
  
