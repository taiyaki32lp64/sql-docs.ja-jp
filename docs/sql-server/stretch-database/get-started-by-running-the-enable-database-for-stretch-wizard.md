---
title: まずはデータベースのストレッチの有効化ウィザードを実行する
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: quickstart
f1_keywords:
- sql13.swb.stretchwizard.f1
- sql13.swb.stretchwizard.createdatabasecredentials.f1
- sql13.swb.stretchwizard.selectdatabasetables.f1
- sql13.swb.stretchwizard.validatesqlserver.f1
- sql13.swb.stretchwizard.selectazuredeployment.f1
- sql13.swb.stretchwizard.configureazuredeployment.f1
- sql13.swb.stretchwizard.Summary.f1
- sql13.swb.stretchwizard.Results.f1
- sql13.swb.stretchwizard.introduction.f1
helpviewer_keywords:
- Stretch Database, wizard
- Enable Database for Stretch Wizard
ms.assetid: 855dd9fc-f80c-4dbc-bf46-55a9736bfe15
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 5d730c8e71044154b9844174ac8d21837c9ea05f
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843798"
---
# <a name="get-started-by-running-the-enable-database-for-stretch-wizard"></a>まずはデータベースのストレッチの有効化ウィザードを実行する
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


 Stretch Database のデータベースを構成するには、データベースのストレッチの有効化ウィザードを実行します。  この記事では、入力する必要がある情報と、ウィザードで必要な選択について説明します。  
  
 Stretch Database の詳細については、「 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)」を参照してください。 
 
 > [!NOTE] 
 > 後で、Stretch Database を無効にする場合は、テーブルまたはデータベースで Stretch Database を無効にしてもリモート オブジェクトは削除されないことに注意してください。 リモート テーブルまたはリモート データベースを削除する場合は、Azure 管理ポータルを使用して削除する必要があります。 リモート オブジェクトを手動で削除するまで、引き続き Azure ストレージのコストが発生します。 
  
## <a name="launch-the-wizard"></a>ウィザードを起動する  
  
1.  SQL Server Management Studio のオブジェクト エクスプローラーで、ストレッチを有効にするデータベースを選択します。  
  
2.  **[タスク]** を右クリックし、 **[Stretch]** (ストレッチ) を選択してから **[有効化]** を選択して、ウィザードを起動します。  
  
##  <a name="Intro"></a> 概要  
 ウィザードの目的と前提条件を確認します。  
 
 次に重要な前提条件を示します。
 -   データベース設定の変更が可能な管理者である必要があります。
 -   Microsoft Azure のサブスクリプションが必要です。
 -   SQL Server がリモートの Azure サーバーと通信できる必要があります。
  
 ![Stretch Database ウィザードの概要ページ](../../sql-server/stretch-database/media/stretch-wizard-1.png "Stretch Database ウィザードの概要ページ")  
  
##  <a name="Tables"></a> [テーブルの選択]  
 ストレッチを有効にするテーブルを選択します。  
 
多数の行があるテーブルが、並べ替え済み一覧の上部に表示されます。 ウィザードでは、テーブルの一覧を表示する前に、Stretch Database で現在サポートされていないデータ型を分析します。 
  
 ![Stretch Database ウィザードの [テーブルの選択] ページ](../../sql-server/stretch-database/media/stretch-wizard-2.png "Stretch Database ウィザードの [テーブルの選択] ページ")  
  
|[列]|[説明]|  
|------------|-----------------|  
|(タイトルなし)|選択したテーブルのストレッチを有効にするには、この列のチェック ボックスを選択します。|  
|**[名前]**|データベースのテーブル名を指します。|  
|(タイトルなし)|この列には、選択したテーブルで Stretch を無効にはしない警告記号が表示される場合があります。 また、たとえば、テーブルでサポートされていないデータ型が使用されているなど、選択したテーブルで Stretch を有効化しないブロックの問題が表示される場合もあります。 ツールヒントの詳細な情報を表示するには、記号の上にマウス ポインターを移動します。 詳細については、「 [Stretch Database の制限事項](../../sql-server/stretch-database/limitations-for-stretch-database.md)」を参照してください。|  
|**ストレッチ済み**|テーブルが既に Stretch 用に有効であるかどうかを示します。|  
|**移行**|テーブル全体を移行 ( **[テーブル全体]** ) することも、表の既存の列にフィルターを指定することもできます。 移行する行を選択するのに、別のフィルター関数を使用する場合、ウィザードを終了した後、ALTER TABLE ステートメントを実行してフィルター関数を指定します。 フィルター関数の詳細については、「[フィルター関数を使用して、移行する行を選択する](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)」を参照してください。 この関数の適用方法の詳細については、「[テーブルに対して Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)」または「[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)」を参照してください。|  
|**行数**|テーブル内の行数を指定します。|  
|**[サイズ (KB)]**|テーブルのサイズを KB で指定します。|  
  
## <a name="optionally-provide-a-row-filter"></a>オプションで行フィルターを指定する  
 移行する行を選択するフィルター機能を指定する場合に、 **[テーブルの選択]** ページで次の処理を行います。  
  
1.  **[拡張するテーブルを選択します。]** リスト内のテーブルの行で、 **[テーブル全体]** をクリックします。 **[拡張する行の選択]** ダイアログ ボックスが開きます。  
  
     ![日付ベースのフィルター述語を定義する](../../sql-server/stretch-database/media/stretch-wizard-2a.png "日付ベースのフィルター述語を定義する")  
  
2.  **[拡張する行の選択]** ダイアログ ボックスで **[行の選択]** を選択します。  
  
3.  **[名前]** フィールドに、フィルター関数の名前を指定します。  
  
4.  **Where** 句には、テーブルから列、演算子を選択し、値を指定します。  
  
5.  **[確認]** をクリックして、関数をテストします。 関数によって、テーブルから結果が返される場合、つまり、条件を満たす移行する行がある場合、テストによって **[成功]** がレポートされます。  

> [!NOTE] 
> フィルター クエリを表示するテキストボックスは読み取り専用です。 テキストボックスのクエリは編集できません。
  
6.  終了 をクリックして  **テーブルの選択** 画面に戻ります。  

フィルター関数は、ウィザードを終了した場合にのみ、SQL Server に作成されます。 それまでは、 **[テーブルの選択]** ページに戻って、フィルター関数を変更したり、名前を変更したりすることができます。

![フィルター述語を定義した後の [テーブルの選択] ページ](../../sql-server/stretch-database/media/stretch-wizard-2b.png "フィルター述語を定義した後の [テーブルの選択] ページ")

移行する行を選択するために別の種類のフィルター関数を使用する場合、次のいずれかの操作を行います。  
  
-   ウィザードを終了し、ALTER TABLE ステートメントを実行してテーブルの Stretch を有効にして、フィルター関数を指定します。 詳細については、「 [テーブルに対して Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)」を参照してください。  
  
-   ウィザードを終了した後、ALTER TABLE ステートメントを実行してフィルター関数を指定します。 必要な手順については、「 [Add a filter function after running the Wizard](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz)」 (ウィザードの実行後、フィルター関数を追加する) を参照してください。  
  
##  <a name="Configure"></a> Azure を構成する  
  
1.  Microsoft アカウントを使用して Microsoft Azure にサインインします。  
  
     ![Azure にサインインする - Stretch Database ウィザード](../../sql-server/stretch-database/media/stretch-wizard-3.png "Azure にサインインする - Stretch Database ウィザード")  
  
2.  Stretch Database で使用する既存の Azure サブスクリプションを選択します。 

> [!NOTE] 
> データベース上で Stretch を有効にするには、使用しているサブスクリプションへの管理者権限が必要です。 Stretch Database ウィザードでは、ユーザーが管理者権限を持っているサブスクリプションのみが表示されます。
  
3.  Stretch Database で使用する Azure リージョンを選択します。
    -   新しいサーバーを作成すると、このリージョンに作成されます。  
    -   選択したリージョンに既にサーバーがある場合、 **[既存のサーバー]** を選択すると、それらがウィザードにリストされます。
  
     待機時間を最小限に抑えるには、SQL Server が配置されている Azure リージョンを選択してください。 リージョンの詳細については、「 [Azure のリージョン](https://azure.microsoft.com/regions/)」を参照してください。  
  
4.  既存のサーバーを使用するか新しい Azure サーバーを作成するかを指定します。  
  
     SQL Server の Active Directory と Azure Active Directory をフェデレーションすると、リモートの Azure サーバーとの通信で、必要に応じて SQL Server のフェデレーション サービス アカウントを使用することができます。 このオプションの要件の詳細については、「[ALTER DATABASE SET オプション&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。  
  
    -   **新しいサーバーを作成する**  
  
        1.  サーバー管理者のログイン名とパスワードを作成します。  
  
        2.  必要に応じて、SQL Server のフェデレーション サービス アカウントを使用して、リモートの Azure サーバーと通信することができます。  
  
         ![新しい Azure サーバーを作成 - Stretch Database ウィザード](../../relational-databases/tables/media/stretch-wizard-4.png "新しい Azure サーバーを作成 - Stretch Database ウィザード")  
  
    -   **既存のサーバー**  
  
        1.  既存の Azure サーバーを選択します。  
  
        2.  認証方法を選択します。  
  
            -   **[SQL Server 認証]** を選択した場合は、管理者のログインとパスワードを入力します。  
  
            -   SQL Server のフェデレーション サービス アカウントを使用してリモートの Azure サーバーと通信するには、 **[Active Directory 統合認証]** を選択します。 選択したサーバーが Azure Active Directory と統合されていない場合、このオプションは表示されません。
  
         ![既存の Azure サーバーを選択 - Stretch Database ウィザード](../../sql-server/stretch-database/media/stretch-wizard-5.png "既存の Azure サーバーを選択 - Stretch Database ウィザード")  
  
##  <a name="Credentials"></a> セキュリティで保護された資格情報  
 Stretch Database がリモート データベースへの接続に使用する資格情報をセキュリティで保護するためのデータベース マスター キーが必要です。  
  
 データベースにマスター キーが既に存在する場合は、そのパスワードを入力します。  
  
 ![Stretch Database ウィザードの [セキュリティで保護された資格情報] ページ](../../sql-server/stretch-database/media/stretch-wizard-6b.PNG "Stretch Database ウィザードの [セキュリティで保護された資格情報] ページ")  
  
 データベースにマスター キーがない場合は、強力なパスワードを入力してデータベース マスター キーを作成します。  
  
 ![Stretch Database ウィザードの [セキュリティで保護された資格情報] ページ](../../relational-databases/tables/media/stretch-wizard-6.png "Stretch Database ウィザードの [セキュリティで保護された資格情報] ページ")  
  
 データベースのマスター キーを作成する方法については、「[CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)」と「[データベース マスター キーの作成](../../relational-databases/security/encryption/create-a-database-master-key.md)」をご覧ください。 ウィザードが作成する資格情報の詳細については、「[データベース スコープ ベースの資格情報を作成する &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)」を参照してください。  
  
##  <a name="Network"></a> IP アドレスを選択する  
 サブネットの IP アドレスの範囲を使用するか (推奨)、SQL Server のパブリック IP アドレスを使用して SQL Server がリモートの Azure サーバーと通信するためのファイアウォール ルールを Azure に作成します。  
  
 このページで指定した IP アドレスは、 SQL Server で開始された受信データ、クエリ、管理操作が Azure ファイアウォールを通過できるように Azure サーバーに伝えます。 このウィザードで SQL Server のファイアウォール設定が変わることはありません。  
  
 ![Stretch Database ウィザードの [IP アドレスの選択] ページ](../../relational-databases/tables/media/stretch-wizard-7.png "Stretch Database ウィザードの [IP アドレスの選択] ページ")  
  
##  <a name="Summary"></a> 概要  
 入力した値、ウィザードで選択したオプション、Azure の推定コストを確認します。 次に、 **[完了]** を選択してストレッチを有効にします。  
  
 ![Stretch Database ウィザードの概要ページ](../../sql-server/stretch-database/media/stretch-wizard-8.png "Stretch Database ウィザードの概要ページ")  
  
##  <a name="Results"></a> [結果]  
 結果を確認します。  
  
 データの移行状況を監視する方法の詳細については、「[データ移行の監視とトラブルシューティング &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)」を参照してください。  
  
 ![Stretch Database ウィザードの [結果] ページ](../../sql-server/stretch-database/media/stretch-wizard-9.PNG "Stretch Database ウィザードの [結果] ページ")  
  
##  <a name="KnownIssues"></a> ウィザードのトラブルシューティング  
 **Stretch Database ウィザードにエラーが発生しました。**  
 Stretch Database がサーバー レベルでまだ有効になっていなく、システム管理者に有効にする権限がないウィザードを実行すると、ウィザードでエラーが発生します。 システム管理者にローカル サーバー インスタンスの Stretch Database を有効にするように依頼し、ウィザードを再度実行します。 詳しくは、「[前提条件:サーバーで Stretch Database を有効にするためのアクセス許可](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md#EnableTSQLServer)」をご覧ください。  
  
## <a name="next-steps"></a>次の手順  
 Stretch Database の追加のテーブルを有効にします。 データの移行を監視し、ストレッチが有効なデータベースとテーブルを管理します。  
  
-   追加のテーブルを有効にする場合:[Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
-   データ移行の状態を表示する場合: [データ移行の監視とトラブルシューティング &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)  
  
-   [データ移行の一時停止と再開 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [Stretch Database の管理とトラブルシューティング](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [Stretch 対応データベースのバックアップ](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [Stretch 対応データベースの復元](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## <a name="see-also"></a>参照  
 [データベースに対して Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [テーブルに対して Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
