---
title: Ssma for DB2 作業の開始 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0eab4f23e342c95d83baa70dd03aba2f5d4bc8d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989640"
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>Ssma for DB2 作業の開始 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) の DB2 できます簡単に変換する DB2 データベース スキーマ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマへの結果として得られるスキーマのアップロード[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を DB2 からデータを移行および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
このトピックでは、インストール プロセスを紹介し、SSMA ユーザー インターフェイスを理解し、支援します。  
  
## <a name="installing-ssma"></a>SSMA のインストール  
SSMA を使用する最初にインストールする必要 SSMA クライアント プログラム ソース DB2 データベースとのターゲット インスタンスの両方にアクセスできるコンピューター[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 実行しているコンピューター上の DB2 OLEDB プロバイダー[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 これらのコンポーネントは、データの移行と DB2 システム関数のエミュレーションをサポートします。 インストール手順については、次を参照してください。 [SSMA for DB2 をインストールする&#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)します。  
  
SSMA を起動するには、クリックして**開始**、 をポイント**すべてのプログラム**、 をポイント **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for DB2**、順にクリックします **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Migration Assistant for DB2**します。  
  
## <a name="ssma-for-db2-user-interface"></a>SSMA for DB2 のユーザー インターフェイス  
SSMA を使用して、DB2 のデータベースを移行できます SSMA のインストール後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 これは、開始する前に SSMA ユーザー インターフェイスを理解するのに役立ちます。 次の図では、SSMA、メタデータ エクスプ ローラー、メタデータ、ツールバー、出力ウィンドウで、エラー一覧 ウィンドウなどのユーザー インターフェイスを示しています。  
  
![SSMA ユーザー インターフェイス](../../ssma/db2/media/ssma_db2_ui.png "SSMA ユーザー インターフェイス")  
  
移行を開始するには、最初に新しいプロジェクトを作成する必要があります。 次に、DB2 データベースに接続します。 接続に成功した後は、DB2 スキーマが DB2 メタデータ エクスプ ローラーに表示されます。 変換を評価するレポートの作成などのタスクを実行する DB2 メタデータ エクスプ ローラーでオブジェクトを右クリックしを実行できます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 ツールバーとメニューを使用して、これらのタスクを実行することもできます。  
  
インスタンスに接続することも必要があります。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 階層、接続が成功した[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースが表示されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラー。 DB2 スキーマに変換した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマの場合、これらの変換されたスキーマを選択する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーでスキーマの同期をとって[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
変換後のスキーマを同期した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、DB2 メタデータ エクスプ ローラーに戻るしへの DB2 スキーマからデータを移行できます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
これらのタスクとその実行方法の詳細については、次を参照してください。 [SQL Server への DB2 データベースの移行&#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)します。  
  
次のセクションでは、SSMA ユーザー インターフェイスの機能について説明します。  
  
### <a name="metadata-explorers"></a>メタデータ エクスプ ローラー  
SSMA は、参照および DB2 に対して操作を実行する 2 つのメタデータ エクスプ ローラーを含むと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
#### <a name="db2-metadata-explorer"></a>DB2 メタデータ エクスプ ローラー  
DB2 メタデータ エクスプ ローラーでは、DB2 スキーマに関する情報を示します。 DB2 メタデータ エクスプ ローラーを使用すると、次のタスクを実行できます。  
  
-   各スキーマ内のオブジェクトを参照します。  
  
-   変換でオブジェクトを選択し、オブジェクトを変換し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文。 詳細については、次を参照してください。 [DB2 スキーマの変換&#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)します。  
  
-   データ移行のためのテーブルを選択し、これらのテーブルからデータを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。 [SQL Server への DB2 データベースの移行&#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)します。  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server メタデータ エクスプ ローラー  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メタデータ エクスプ ローラーのインスタンスに関する情報を表示する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 インスタンスに接続すると[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SSMA は、そのインスタンスに関するメタデータを取得し、プロジェクト ファイルに格納します。  
  
使用することができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]変換後の DB2 データベース オブジェクトを選択しのインスタンスとそれらのオブジェクトを同期するメタデータ エクスプ ローラー[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
### <a name="metadata"></a>メタデータ  
各メタデータ エクスプ ローラーの右側には、選択したオブジェクトを記述するタブが。 たとえば、DB2 メタデータ エクスプ ローラーでテーブルを選択する場合は、6 つのタブが表示されます。**テーブル**、 **SQL**、**型マッピング、レポート**、**プロパティ**、および**データ**します。 **レポート** タブには、選択したオブジェクトを格納しているレポートを作成した後にのみ情報が含まれます。 内のテーブルを選択した場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーで、3 つのタブが表示されます。**テーブル**、 **SQL**、および**データ**します。  
  
ほとんどのメタデータの設定とは、読み取り専用です。 ただし、次のメタデータを変更できます。  
  
-   DB2 メタデータ エクスプ ローラーでプロシージャを変更し、マッピングを入力できます。 変更後の手順を変換し、マッピングを入力するには、スキーマを変換する前に、変更を加えます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーを変更できますが、[!INCLUDE[tsql](../../includes/tsql-md.md)]ストアド プロシージャ。 これらの変更を表示する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]へのスキーマを読み込む前に、これらの変更を加える[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
メタデータ エクスプ ローラーで行われた変更は、ソースまたはターゲット データベースではなく、プロジェクトのメタデータに反映されます。  
  
### <a name="toolbars"></a>[ツール バー]  
SSMA は 2 つのツールバー: プロジェクト ツールバー、および移行ツールバー。  
  
#### <a name="the-project-toolbar"></a>プロジェクトのツールバー  
プロジェクトのツールバーには、プロジェクトでの作業、DB2 への接続およびへの接続用のボタンが含まれています。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 これらのボタンで、コマンドのように、**ファイル**メニュー。  
  
#### <a name="migration-toolbar"></a>移行のツールバー  
次の表は、ツールバーのコマンドを移行には。  
  
|ボタン|機能|  
|------|--------|  
|**レポートを作成します。**|選択した DB2 オブジェクトに変換します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文、し、どのように成功して、変換を示すレポートを作成します。<br /><br />オブジェクトは DB2 メタデータ エクスプ ローラーで選択されている場合を除き、このコマンドは無効です。|  
|**スキーマを変換します。**|選択した DB2 オブジェクトに変換します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクト。<br /><br />オブジェクトは DB2 メタデータ エクスプ ローラーで選択されている場合を除き、このコマンドは無効です。|  
|**データを移行します。**|DB2 データベースからデータを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 このコマンドを実行する前に DB2 スキーマを変換する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマ、しにオブジェクトを読み込むと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。<br /><br />オブジェクトは DB2 メタデータ エクスプ ローラーで選択されている場合を除き、このコマンドは無効です。|  
|**[停止]**|現在のプロセスを停止します。|  
  
### <a name="menus"></a>メニュー  
次の表では、SSMA メニューを示します。  
  
|メニュー|説明|  
|----|-----------|  
|**[最近使ったファイル]**|プロジェクトでの作業、DB2 への接続およびへの接続用のコマンドを含む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|**[編集]**|検索とテキストのコピーなどの詳細ページを操作するコマンド[!INCLUDE[tsql](../../includes/tsql-md.md)]SQL の詳細ウィンドウ。 含まれています、**ブックマークの管理**オプション、いることができますを既存のブックマークの一覧を参照してください。 ダイアログ ボックスの右側にあるボタンを使用するには、ブックマークを管理します。|  
|**[表示]**|含まれています、**メタデータ エクスプ ローラーの同期**コマンド。 DB2 メタデータ エクスプ ローラーの間でオブジェクトを同期して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラー。 表示し、非表示にするためのコマンドも含まれています、**出力**と**エラー一覧**ペインおよびオプション**レイアウト**レイアウトを管理します。|  
|**ツール**|レポートを作成し、オブジェクトとデータを移行するためのコマンドが含まれています。 アクセスできます、**グローバル設定**と**プロジェクト設定** ダイアログ ボックス。|  
|**ヘルプ**|SSMA のヘルプにアクセスを提供します、**について** ダイアログ ボックス。|  
  
### <a name="output-pane-and-error-list-pane"></a>出力ウィンドウおよびエラー一覧 ウィンドウ  
**ビュー**メニュー コマンドの出力ウィンドウおよびエラー一覧 ウィンドウの表示を切り替えるには。  
  
-   [出力] ペインは、SSMA からオブジェクトへの変換、オブジェクトの同期、およびデータの移行中にステータス メッセージを示します。  
  
-   エラー一覧ウィンドウには、並べ替え可能なリストでのエラー、警告、および情報メッセージが表示されます。  
  
## <a name="see-also"></a>参照  
[DB2 のデータを SQL Server に移行する&#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[ユーザー インターフェイス リファレンス&#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
