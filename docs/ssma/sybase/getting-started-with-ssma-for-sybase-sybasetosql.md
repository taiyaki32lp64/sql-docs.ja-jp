---
title: SSMA で SAP ASE (SybaseToSQL) の概要 |Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: f07f230f52fee5707084c01060e92220b35cb75c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029125"
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>SSMA で SAP ASE (SybaseToSQL) の概要
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) の SAP ASE を使用する簡単に変換する SAP Adaptive Server Enterprise (ASE) のデータベース スキーマ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Azure SQL Database スキーマへの結果として得られるスキーマのアップロードまたは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]や Azure SQL Database からデータを移行し、SAP ASE を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。  
  
このトピックでは、インストール プロセスを紹介し、SSMA ユーザー インターフェイスを理解し、支援します。  
  
## <a name="installing-and-licensing-ssma"></a>インストールして、SSMA をライセンス  
SSMA を使用する最初にインストールする必要 SSMA クライアント プログラムのターゲット インスタンスと SAP ASE のソース インスタンスの両方にアクセスできるコンピューター[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。 サーバー側のデータの移行を使用する必要がありますにインストールする拡張機能パックと少なくとも 1 つの SAP ASE プロバイダー (OLE DB または ADO.NET) を実行しているコンピューター[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 これらのコンポーネントは、データの移行と SAP ASE システム関数のエミュレーションをサポートします。 インストール手順については、次を参照してください。 [SAP ASE のインストールの SSMA &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)します。  
  
SSMA を起動するには、クリックして**開始**、 をポイント**すべてのプログラム**、 をポイント **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Sybase**、し、  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Sybase**です。 初めて、SSMA を起動するライセンスのダイアログ ボックスが表示されます。 SSMA を使用する前に、Windows Live ID を使用して、SSMA をライセンスする必要があります。 ライセンスの手順でインストール手順に記載されて、 [for Sybase クライアントのインストールの SSMA &#40;SybaseToSQL&#41; ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)トピック。  
  
## <a name="ssma-for-sap-ase-user-interface"></a>SSMA for SAP ASE のユーザー インターフェイス  
SSMA は、インストールして、ライセンス認証は後に、SAP ASE データベースを移行する SSMA を使用することができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。 これは、開始する前に SSMA ユーザー インターフェイスを理解するのに役立ちます。 次の図では、SSMA、メタデータ エクスプ ローラー、メタデータ、ツールバー、出力ウィンドウで、エラー一覧 ウィンドウなどのユーザー インターフェイスを示しています。  
  
![SSMA for SAP ASE のユーザー インターフェイス](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SSMA for SAP ASE のユーザー インターフェイス")  
  
移行を開始するには、最初に新しいプロジェクトを作成する必要があります。 次に、SAP ASE に接続します。 接続に成功した後は、SAP ASE データベースの階層は、Sybase メタデータ エクスプ ローラーに表示されます。 変換を評価するレポートの作成などのタスクを実行する Sybase メタデータ エクスプ ローラーでオブジェクトを右クリックしを実行できます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。 ツールバーとメニューを通じてこれらのタスクを実行することもできます。  
  
インスタンスに接続する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。 階層、接続が成功した[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で Azure SQL データベースが表示されるか[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラー。 SAP ASE スキーマに変換した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database スキーマでは、これらの変換されたスキーマを選択します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラー、しへのスキーマを読み込む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。  
  
変換されたスキーマの読み込み後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]か Azure SQL Database では、Sybase メタデータ エクスプ ローラーに戻ってに SAP ASE データベースからデータを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL データベース。  
  
これらのタスクとその実行方法の詳細については、次を参照してください。 [SQL Server - Azure SQL Database への SAP ASE データベースの移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)します。  
  
次のセクションでは、SSMA ユーザー インターフェイスの機能について説明します。  
  
### <a name="metadata-explorers"></a>メタデータ エクスプ ローラー  
SSMA には参照し、SAP ASE で操作を実行する 2 つのメタデータ エクスプ ローラーが含まれていますと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL データベース。  
  
#### <a name="sybase-metadata-explorer"></a>Sybase メタデータ エクスプ ローラー  
Sybase メタデータ エクスプ ローラーでは、SAP ASE のソース インスタンスのデータベースに関する情報が表示されます。  
  
Sybase メタデータ エクスプ ローラーを使用すると、次のタスクを実行できます。  
  
-   各データベース内のテーブルを参照します。  
  
-   変換でオブジェクトを選択し、オブジェクトを変換し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database の構文。 詳細については、次を参照してください。 [SAP ASE データベース オブジェクトの変換&#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)します。  
  
-   データ移行のためのオブジェクトを選択し、それらのオブジェクトからデータを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。 詳細については、次を参照してください。 [SAP ASE データの移行 SQL Server - Azure SQL Database の&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md)します。  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server または SQL Azure メタデータ エクスプ ローラー  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure メタデータ エクスプ ローラーのインスタンスに関する情報が表示または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。 インスタンスに接続すると[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database、SSMA そのインスタンスに関するメタデータを取得し、プロジェクト ファイルに格納します。  
  
使用することができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または変換後の SAP ASE データベース オブジェクトを選択し、読み込む SQL Azure メタデータ エクスプ ローラー (同期) これらのオブジェクトのインスタンスに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。  
  
詳細については、次を参照してください。[を SQL Server に変換されたデータベース オブジェクトの読み込み&#40;SybaseToSQL&#41;](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md)します。  
  
### <a name="metadata"></a>メタデータ  
各メタデータ エクスプ ローラーの右側には、選択したオブジェクトを記述するタブが。 たとえば、Sybase メタデータ エクスプ ローラーでテーブルを選択する場合、6 つのタブが表示されます。**テーブル**、 **SQL**、**の種類のマッピング**、**データ**、**プロパティ**、および**レポート**します。 **レポート** タブには、選択したオブジェクトを含むレポートを作成した後にのみ情報が含まれます。 内のテーブルを選択した場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラー、3 つのタブが表示されます。**テーブル**、 **SQL**、および**データ**します。  
  
ほとんどのメタデータの設定とは、読み取り専用です。 ただし、次のメタデータを変更できます。  
  
-   Sybase メタデータ エクスプ ローラーでプロシージャを変更し、マッピングを入力できます。 スキーマを変換する前に、これらの変更を行います。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または変更できる SQL Azure メタデータ エクスプ ローラーで、[!INCLUDE[tsql](../../includes/tsql-md.md)]ストアド プロシージャ。 スキーマを読み込む前に、これらの変更を加える[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
メタデータ エクスプ ローラーで行われた変更は、ソースまたはターゲット データベースではなく、プロジェクトのメタデータに反映されます。  
  
### <a name="toolbars"></a>[ツール バー]  
SSMA は 2 つのツールバー: プロジェクト ツールバー、および移行ツールバー。  
  
#### <a name="the-project-toolbar"></a>プロジェクトのツールバー  
プロジェクトのツールバーには、プロジェクトでの作業、SAP ASE では、接続などに接続するためのボタンが含まれています。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。 これらのボタンで、コマンドのように、**ファイル**メニュー。  
  
#### <a name="the-migration-toolbar"></a>移行のツールバー  
移行のツールバーには、次のコマンドが含まれています。  
  
|ボタン|機能|  
|----------|------------|  
|**レポートを作成します。**|選択した SAP ASE オブジェクトに変換します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文、し、どのように成功して、変換を示すレポートを作成します。<br /><br />このコマンドは、Sybase メタデータ エクスプ ローラーでオブジェクトが選択されている場合にのみ使用できます。|  
|**スキーマを変換します。**|選択した SAP ASE オブジェクトに変換します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database オブジェクト。<br /><br />このコマンドは、Sybase メタデータ エクスプ ローラーでオブジェクトが選択されている場合にのみ使用できます。|  
|**データを移行します。**|SAP ASE データベースからデータを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。 このコマンドを実行する前に SAP ASE スキーマに変換する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database スキーマ、しにオブジェクトを読み込むと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。<br /><br />このコマンドは、Sybase メタデータ エクスプ ローラーでオブジェクトが選択されている場合にのみ使用できます。|  
|**[停止]**|オブジェクトを変換するなど、現在のプロセスを停止する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database の構文。|  
  
### <a name="menus"></a>メニュー  
SSMA には、次のメニューが含まれています。  
  
|メニュー|説明|  
|--------|---------------|  
|**[最近使ったファイル]**|プロジェクトでの作業、SAP ASE では、接続などに接続するためのコマンドを含む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。|  
|**[編集]**|検索とテキストのコピーなどの詳細ページを操作するコマンド[!INCLUDE[tsql](../../includes/tsql-md.md)]SQL の詳細ウィンドウ。 含まれています、**ブックマークの管理**オプション、既存のブックマークの一覧を確認できます。 ダイアログ ボックスの右側にあるボタンを使用するには、ブックマークを管理します。|  
|**[表示]**|含まれています、**メタデータ エクスプ ローラーの同期**コマンド。 これは、Sybase メタデータ エクスプ ローラーの間でオブジェクトを同期し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラー。 表示と非表示のコマンドも格納、**出力**と**エラー一覧**ペインおよびオプション**レイアウト**レイアウトを管理します。|  
|**ツール**|レポートを作成、エクスポート、およびオブジェクトとデータを移行するためのコマンドが含まれています。 アクセスできます、**グローバル設定**と**プロジェクト設定** ダイアログ ボックス。|  
|**テスト担当者**|テスト_ケース、テスト結果を表示、およびデータベースのバックアップの管理用コマンドを作成するコマンドが含まれています。|  
|**ヘルプ**|SSMA のヘルプにアクセスを提供します、**について** ダイアログ ボックス。|  
  
### <a name="output-pane-and-error-list-pane"></a>出力ウィンドウおよびエラー一覧 ウィンドウ  
**ビュー**メニュー コマンドの出力ウィンドウおよびエラー一覧 ウィンドウの表示を切り替えるには。  
  
-   [出力] ペインは、SSMA からオブジェクトへの変換、オブジェクトの同期、およびデータの移行中にステータス メッセージを示します。  
  
-   エラー一覧 ウィンドウでは、エラー、警告、および情報メッセージを並べ替えることができますを一覧に表示します。  
  
## <a name="see-also"></a>関連項目  
[SQL Server - Azure SQL Database への SAP ASE データベースの移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[ユーザー インターフェイス リファレンス&#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
