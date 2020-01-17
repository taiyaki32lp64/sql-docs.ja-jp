---
title: SQL Server Migration Assistant for Access の概要 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- error list pane
- getting started
- menus
- metadata explorers
- output pane
- toolbars
- user interface
- user interface overview
ms.assetid: 462a731f-08f1-44e1-9eeb-4deac6d2f6c5
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 863e62dc9e2970f7531bba15f7242c73c5b0f9e7
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68259920"
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>SQL Server Migration Assistant for Access (AccessToSQL) の概要
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) のアクセスでは、すぐに Access データベース オブジェクトを変換することができる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB のオブジェクトに結果のオブジェクトをアップロードする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB へのアクセスからデータを移行および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。 かどうか必要に応じて、リンクすることもテーブルにアクセスする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB のテーブルを使用して、既存の Access のフロント エンド アプリケーションを続行できるように[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。  
  
このトピックでは、インストール プロセスについて説明し、SSMA ユーザー インターフェイスを理解するのに役立ちます。  
  
## <a name="installing-ssma"></a>SSMA のインストール  
SSMA を使用するには、最初にする必要があります、プログラムのインストール SSMA クライアントを移行する、両方のデータベースにアクセスできるコンピューターとのターゲット インスタンスに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。 インストール手順については、次を参照してください。[をインストールする SQL Server Migration Assistant for Access &#40;AccessToSQL&#41;](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md)します。  
  
SSMA を起動するには、クリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**SQL Server Migration Assistant for Access**、し、 **SQL Server の移行Assistant for Access**します。  
  
## <a name="using-ssma"></a>SSMA を使用します。  
SSMA のインストール後に Access データベースを移行するツールを使用する前に、SSMA ユーザー インターフェイスに慣れるに役立ちます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。 SSMA ユーザー インターフェイスで、メタデータ エクスプ ローラー、メタデータ、ツールバー、出力ウィンドウ、およびエラー一覧 ウィンドウを含む次の図に示します。  
  
![SSMA for Access のグラフィカル ユーザー インターフェイス](../../ssma/access/media/ssmaforaccessgui.gif "SSMA for Access のグラフィカル ユーザー インターフェイス")  
  
移行を開始するには、新しいプロジェクトを作成し、アクセス メタデータ エクスプ ローラーに Access データベースを追加します。 などのタスクを実行するアクセス メタデータ エクスプ ローラーでオブジェクトを右クリックし、ことができます。
- エクスポートする Access データベース オブジェクトのインベントリ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。
- 変換の評価レポートを作成する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。
- アクセスのスキーマの変換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB のスキーマ。

ツールバーとメニューを使用して、これらのタスクを実行することもできます。  
  
インスタンスに接続することも必要があります。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 階層、接続が成功した[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にデータベースが表示されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラー。 アクセスのスキーマに変換した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマの場合、これらの変換されたスキーマを選択することができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーへのスキーマを読み込むと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
移行から新しいプロジェクト ダイアログ ボックスのドロップダウン リストに Azure SQL DB を選択した場合は、Azure SQL DB に接続する必要があります。 接続が成功した Azure SQL DB データベースの階層は、Azure SQL DB メタデータ エクスプ ローラーに表示されます。 Access スキーマを Azure SQL DB のスキーマに変換した後は、Azure SQL DB メタデータ エクスプ ローラーでこれらの変換されたスキーマを選択しへのスキーマを読み込む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
変換されたスキーマの読み込み後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]か、Azure SQL DB へのアクセスのメタデータ エクスプ ローラーに戻ってに Access データベースからデータを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB データベース。 かどうか必要に応じて、リンクすることもテーブルにアクセスする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB のテーブル。  
  
これらのタスクとその実行方法の詳細については、次のトピックを参照してください。  
  
-   [Access データベースの移行の準備](preparing-access-databases-for-migration-accesstosql.md)  
  
-   [SQL Server へのアクセス データベースの移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
-   [SQL Server への Access アプリケーションのリンク](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
次のセクションでは、SSMA ユーザー インターフェイスの機能について説明します。  
  
### <a name="metadata-explorers"></a>メタデータ エクスプ ローラー  
SSMA は、参照、および操作へのアクセスを実行に使用できる 2 つのメタデータ エクスプ ローラーを含むと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB データベース。  
  
#### <a name="access-metadata-explorer"></a>メタデータ エクスプ ローラーにアクセスします。  
メタデータ エクスプ ローラーのアクセスは、プロジェクトに追加された Access データベースに関する情報を示します。 Access データベースを追加すると、SSMA は、メタデータ アクセス メタデータ エクスプ ローラーで使用できるは、そのデータベースに関するメタデータを取得します。  
  
メタデータ エクスプ ローラーのアクセスを使用して、次のタスクを実行できます。  
  
-   各アクセス データベースのテーブルを参照します。  
  
-   変換のためのオブジェクトを選択し、オブジェクトを変換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文。 詳細については、次を参照してください。 [Access データベース オブジェクトの変換](converting-access-database-objects-accesstosql.md)します。  
  
-   データ移行のオブジェクトを選択し、それらのオブジェクトからデータを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。 [SQL Server への Access データの移行](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)します。  
  
-   リンクし、アクセスのリンクを解除し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]テーブル。  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server または Azure SQL DB メタデータ エクスプ ローラー  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL DB メタデータ エクスプ ローラーのインスタンスに関する情報が表示または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。 インスタンスに接続すると[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB、SSMA そのインスタンスに関するメタデータを取得し、プロジェクト ファイルに格納します。  
  
変換された Access データベース オブジェクトを選択して読み込むことは、SQL Server または Azure SQL DB メタデータ エクスプ ローラーを使用できます (同期) これらのオブジェクトのインスタンスに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。  
  
詳細については、次を参照してください。[を SQL Server に変換されたデータベース オブジェクトの読み込み](loading-converted-database-objects-into-sql-server-accesstosql.md)します。  
  
### <a name="metadata"></a>メタデータ  
各メタデータ エクスプ ローラーの右側には、選択したオブジェクトを記述するタブが。 たとえば、アクセス メタデータ エクスプ ローラーでテーブルを選択する場合、4 つのタブが表示されます。**テーブル**、**の種類のマッピング**、**プロパティ**、および**データ**します。 内のテーブルを選択した場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーで、次の 3 つのタブが表示されます。**テーブル**、 **SQL**、および**データ**します。  
  
ほとんどのメタデータの設定とは、読み取り専用です。 ただし、次のメタデータを変更できます。  
  
-   アクセス メタデータ エクスプ ローラーでは、型のマッピングを変更できます。 レポートを作成したり、スキーマを変換したりする前に、これらの変更を作成してください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーでテーブルとインデックスのプロパティを変更することができます、**テーブル**タブ。スキーマを読み込む前に、これらの変更を加える[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。 [Access データベース オブジェクトの変換](converting-access-database-objects-accesstosql.md)します。  
  
### <a name="toolbars"></a>[ツール バー]  
SSMA は 2 つのツールバー: プロジェクト ツールバー、および移行ツールバー。  
  
#### <a name="the-project-toolbar"></a>プロジェクトのツールバー  
プロジェクトのツールバーには、プロジェクトでの作業、Access データベースのファイルを追加およびへの接続ボタンが含まれています。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。 これらのボタンで、コマンドのように、**ファイル**メニュー。  
  
#### <a name="the-migration-toolbar"></a>移行のツールバー  
移行のツールバーには、次のコマンドが含まれています。  
  
|ボタン|機能|  
|----------|------------|  
|**変換、読み込み、および移行**|Access データベースを変換、変換されたオブジェクトに読み込みます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB へのデータを移行したり[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB では、すべて 1 つの手順でします。|  
|**レポートを作成します。**|選択したアクセスのスキーマを変換します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB の構文、し、どのように成功して、変換を示すレポートを作成します。<br /><br />このコマンドは、オブジェクトがアクセス メタデータ エクスプ ローラーで選択されている場合にのみ使用できます。|  
|**スキーマを変換します。**|選択したアクセスのスキーマを変換します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB のスキーマ。<br /><br />このコマンドは、オブジェクトがアクセス メタデータ エクスプ ローラーで選択されている場合にのみ使用できます。|  
|**データを移行します。**|Access データベースからデータを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。 このコマンドを実行する前にに Access スキーマを変換する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB のスキーマ、しにオブジェクトを読み込むと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB。<br /><br />このコマンドは、オブジェクトがアクセス メタデータ エクスプ ローラーで選択されている場合にのみ使用できます。|  
|**[停止]**|オブジェクトを変換するなど、現在のプロセスを停止する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB の構文。|  
  
### <a name="menus"></a>メニュー  
SSMA には、次のメニューが含まれています。  
  
|メニュー|説明|  
|--------|---------------|  
|**[最近使ったファイル]**|移行ウィザードは、プロジェクトの操作への接続の追加と、Access データベース ファイルの削除コマンドが含まれています[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。|  
|**[編集]**|検索とテキストのコピーなどの詳細ページを操作するコマンド[!INCLUDE[tsql](../../includes/tsql-md.md)]SQL の詳細ウィンドウ。 開くには、**ブックマークの管理**ダイアログ ボックスで、編集 メニューで、ブックマークの管理 をクリックします。 ダイアログ ボックスで、既存のブックマークの一覧が表示されます。 ダイアログ ボックスの右側にあるボタンを使用するには、ブックマークを管理します。|  
|**[表示]**|含まれています、**メタデータ エクスプ ローラーの同期**コマンド。 これにより、同期アクセス メタデータ エクスプ ローラーの間でオブジェクトと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB メタデータ エクスプ ローラー。 表示と非表示のコマンドも格納、**出力**と**エラー一覧**ペインおよびオプション**レイアウト**レイアウトを管理します。|  
|**ツール**|レポートを作成、データをエクスポート、オブジェクトとデータを移行、テーブルをリンクするためのコマンドが含まれていて、グローバルにアクセスし、プロジェクトの設定 ダイアログ ボックスを提供します。|  
|**ヘルプ**|SSMA のヘルプにアクセスを提供します、**について** ダイアログ ボックス。|  
  
### <a name="output-pane-and-error-list-pane"></a>出力ウィンドウおよびエラー一覧 ウィンドウ  
**ビュー**メニュー コマンドの出力ウィンドウおよびエラー一覧 ウィンドウの表示を切り替えるには。  
  
-   [出力] ペインは、SSMA からオブジェクトへの変換、オブジェクトの同期、およびデータの移行中にステータス メッセージを示します。  
  
-   エラー一覧 ウィンドウでは、エラー、警告、および情報メッセージを並べ替えることができますを一覧に表示します。  
  
## <a name="see-also"></a>関連項目  
[SQL Server へのアクセス データベースの移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
