---
title: Ssma for Oracle (OracleToSQL) 作業の開始 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA for Oracle, Metadata Explorers
- SSMA for Oracle, Toolbars
ms.assetid: df79664c-972e-4bef-865a-ce609789fee7
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: ef71a9355bc11c4d377f00a44b2b8cd2958f8656
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264455"
---
# <a name="getting-started-with-ssma-for-oracle-oracletosql"></a>SSMA for Oracle 入門 (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) の Oracle を使用する簡単に変換する Oracle データベース スキーマ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマへの結果として得られるスキーマのアップロード[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を Oracle からデータを移行および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
このトピックでは、インストール プロセスを紹介し、SSMA ユーザー インターフェイスを理解し、支援します。  
  
## <a name="installing-ssma"></a>SSMA のインストール  
SSMA を使用する最初にインストールする必要 SSMA クライアント プログラム ソース Oracle データベースとのターゲット インスタンスの両方にアクセスできるコンピューター[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 インストールする必要あります、拡張機能パックと少なくとも 1 つの Oracle プロバイダーでは、(OLE DB または[!INCLUDE[vstecado](../../includes/vstecado_md.md)]) を実行しているコンピューターで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 これらのコンポーネントは、データの移行と Oracle のシステム関数のエミュレーションをサポートします。 インストール手順については、次を参照してください。 [SSMA for Oracle をインストールする&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)します。  
  
SSMA を起動するには、クリックして**開始**、 をポイント**すべてのプログラム**、 をポイント **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Oracle**、順にクリックします **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Migration Assistant for Oracle**します。  
  
## <a name="ssma-for-oracle-user-interface"></a>SSMA for Oracle のユーザー インターフェイス  
SSMA を使用して、Oracle データベースを移行できます SSMA のインストール後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 これは、開始する前に SSMA ユーザー インターフェイスを理解するのに役立ちます。 次の図では、SSMA、メタデータ エクスプ ローラー、メタデータ、ツールバー、出力ウィンドウで、エラー一覧 ウィンドウなどのユーザー インターフェイスを示しています。  
  
![SSMA for Oracle UI](../../ssma/oracle/media/ssma_oracle_ui.jpg "SSMA for Oracle の UI")  
  
移行を開始するには、最初に新しいプロジェクトを作成する必要があります。 次に、Oracle データベースに接続します。 接続が成功した Oracle スキーマは、Oracle メタデータ エクスプ ローラーに表示されます。 変換を評価するレポートの作成などのタスクを実行する Oracle メタデータ エクスプ ローラーでオブジェクトを右クリックしを実行できます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 ツールバーとメニューを使用して、これらのタスクを実行することもできます。  
  
インスタンスに接続することも必要があります。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 階層、接続が成功した[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースが表示されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラー。 Oracle スキーマに変換した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマの場合、これらの変換されたスキーマを選択する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーでスキーマの同期をとって[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
変換後のスキーマを同期した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle メタデータ エクスプ ローラーに戻るしへの Oracle スキーマからデータを移行できます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
これらのタスクとその実行方法の詳細については、次を参照してください。 [SQL Server への Oracle データベースの移行&#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)します。  
  
次のセクションでは、SSMA ユーザー インターフェイスの機能について説明します。  
  
### <a name="metadata-explorers"></a>メタデータ エクスプ ローラー  
SSMA には参照し、Oracle で操作を実行する 2 つのメタデータ エクスプ ローラーが含まれていますと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
#### <a name="oracle-metadata-explorer"></a>Oracle メタデータ エクスプ ローラー  
Oracle メタデータ エクスプ ローラーでは、Oracle スキーマについての情報が表示されます。 Oracle メタデータ エクスプ ローラーを使用すると、次のタスクを実行できます。  
  
-   各スキーマ内のオブジェクトを参照します。  
  
-   変換でオブジェクトを選択し、オブジェクトを変換し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文。 詳細については、次を参照してください。 [Oracle スキーマの変換&#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)します。  
  
-   データ移行のためのテーブルを選択し、これらのテーブルからデータを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。 [SQL Server に Oracle のデータを移行する&#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md)します。  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server メタデータ エクスプ ローラー  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メタデータ エクスプ ローラーのインスタンスに関する情報を表示する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 インスタンスに接続すると[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SSMA は、そのインスタンスに関するメタデータを取得し、プロジェクト ファイルに格納します。  
  
使用することができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を変換後の Oracle データベース オブジェクトを選択しのインスタンスとそれらのオブジェクトを同期し、メタデータ エクスプ ローラー[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
詳細については、次を参照してください。[を SQL Server に変換されたデータベース オブジェクトの読み込み&#40;OracleToSQL&#41;](../../ssma/oracle/loading-converted-database-objects-into-sql-server-oracletosql.md)します。  
  
### <a name="metadata"></a>メタデータ  
各メタデータ エクスプ ローラーの右側には、選択したオブジェクトを記述するタブが。 たとえば、Oracle メタデータ エクスプ ローラーでテーブルを選択する場合は、6 つのタブが表示されます。**テーブル**、 **SQL**、**型マッピング、レポート**、**プロパティ**、および**データ**します。 **レポート** タブには、選択したオブジェクトを格納しているレポートを作成した後にのみ情報が含まれます。 内のテーブルを選択した場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーで、3 つのタブが表示されます。**テーブル**、 **SQL**、および**データ**します。  
  
ほとんどのメタデータの設定とは、読み取り専用です。 ただし、次のメタデータを変更できます。  
  
-   Oracle メタデータ エクスプ ローラーでプロシージャを変更し、マッピングを入力できます。 変更後の手順を変換し、マッピングを入力するには、スキーマを変換する前に、変更を加えます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーを変更できますが、[!INCLUDE[tsql](../../includes/tsql-md.md)]ストアド プロシージャ。 これらの変更を表示する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]へのスキーマを読み込む前に、これらの変更を加える[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
メタデータ エクスプ ローラーで行われた変更は、ソースまたはターゲット データベースではなく、プロジェクトのメタデータに反映されます。  
  
### <a name="toolbars"></a>[ツール バー]  
SSMA は 2 つのツールバー: プロジェクト ツールバー、および移行ツールバー。  
  
#### <a name="the-project-toolbar"></a>プロジェクトのツールバー  
プロジェクトのツールバーには、プロジェクトでの作業や、Oracle への接続への接続用のボタンが含まれています。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 これらのボタンで、コマンドのように、**ファイル**メニュー。  
  
#### <a name="migration-toolbar"></a>移行のツールバー  
次の表は、ツールバーのコマンドを移行には。  
  
|ボタン|機能|  
|------|--------|  
|**レポートを作成します。**|選択した Oracle オブジェクトに変換します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文、し、どのように成功して、変換を示すレポートを作成します。<br /><br />Oracle メタデータ エクスプ ローラーでオブジェクトが選択されていない場合は、このコマンドが無効です。|  
|**スキーマを変換します。**|選択した Oracle オブジェクトに変換します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクト。<br /><br />Oracle メタデータ エクスプ ローラーでオブジェクトが選択されていない場合は、このコマンドが無効です。|  
|**データを移行します。**|Oracle データベースからデータを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 このコマンドを実行する前に Oracle スキーマに変換する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマ、しにオブジェクトを読み込むと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。<br /><br />Oracle メタデータ エクスプ ローラーでオブジェクトが選択されていない場合は、このコマンドが無効です。|  
|**[停止]**|現在のプロセスを停止します。|  
  
### <a name="menus"></a>メニュー  
次の表では、SSMA メニューを示します。  
  
|メニュー|説明|  
|----|-----------|  
|**[最近使ったファイル]**|プロジェクトでの作業や、Oracle への接続への接続用のコマンドを含む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|**[編集]**|検索とテキストのコピーなどの詳細ページを操作するコマンド[!INCLUDE[tsql](../../includes/tsql-md.md)]SQL の詳細ウィンドウ。 含まれています、**ブックマークの管理**オプション、いることができますを既存のブックマークの一覧を参照してください。 ダイアログ ボックスの右側にあるボタンを使用するには、ブックマークを管理します。|  
|**[表示]**|含まれています、**メタデータ エクスプ ローラーの同期**コマンド。 Oracle メタデータ エクスプ ローラーの間でオブジェクトを同期して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラー。 表示し、非表示にするためのコマンドも含まれています、**出力**と**エラー一覧**ペインおよびオプション**レイアウト**レイアウトを管理します。|  
|**ツール**|レポートを作成し、オブジェクトとデータを移行するためのコマンドが含まれています。 アクセスできます、**グローバル設定**と**プロジェクト設定** ダイアログ ボックス。|  
|**テスト担当者**|テストの場合、リポジトリ、およびバックアップの管理システムの作成と操作のためのコマンドが含まれています。|  
|**ヘルプ**|SSMA のヘルプにアクセスを提供します、**について** ダイアログ ボックス。|  
  
### <a name="output-pane-and-error-list-pane"></a>出力ウィンドウおよびエラー一覧 ウィンドウ  
**ビュー**メニュー コマンドの出力ウィンドウおよびエラー一覧 ウィンドウの表示を切り替えるには。  
  
-   [出力] ペインは、SSMA からオブジェクトへの変換、オブジェクトの同期、およびデータの移行中にステータス メッセージを示します。  
  
-   エラー一覧ウィンドウには、並べ替え可能なリストでのエラー、警告、および情報メッセージが表示されます。  
  
## <a name="see-also"></a>参照  
[SQL Server への Oracle データの移行&#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md)  
[ユーザー インターフェイス リファレンス&#40;OracleToSQL&#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
