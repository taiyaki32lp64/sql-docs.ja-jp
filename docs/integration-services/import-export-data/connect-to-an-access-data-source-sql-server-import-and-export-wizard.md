---
title: Access データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 67a361446c69425f6b05bef913ded568a7dcfd75
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296292"
---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>Access データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このトピックでは、SQL Server インポートおよびエクスポート ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページから **Microsoft Access** データ ソースに接続する方法を説明します。

Microsoft Access データベースへの接続例を次のスクリーン ショットに示します。 この例では、ターゲット データベースでワークグループ情報ファイルを使用ないため、ユーザー名とパスワードを入力する必要はありません。

![Access への接続](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>指定するオプション

> [!NOTE]
> このデータ プロバイダーの接続オプションは、Access が変換元または変換先の場合でも同じです。 つまり、表示されるオプションは、ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページともに同じです。

**データ ソース**  
データ プロバイダーの一覧に、Microsoft Access の複数のエントリが含まれている場合があります。 インストールされている最新のバージョン、またはデータベース ファイルを作成した Access のバージョンに対応するバージョンを選択します。

|データ ソース|Office のバージョン|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access (Microsoft Access データベース エンジン)|Office 2010 および Office 2007|
|Microsoft Access (Microsoft Jet データベース エンジン)|Office 2007 より前の Office のバージョン|

> [!IMPORTANT]
> Access データベースに接続するために追加のファイルのダウンロードとインストールが必要になる場合もあります。 詳細については、このページの「[Access に接続するために必要なファイルを取得する](#officeDownloads)」を参照してください。

 **[ファイル名]**  
Access ファイルのパスとファイル名を指定します。 たとえば、ローカル コンピューター上のファイルの場合は **C:\\MyData.mdb**、ネットワーク共有上のファイルの場合は **\\\\Sales\\Database\\Northwind.mdb** と指定します。 または、 **[参照]** をクリックします。 

> [!NOTE]
> **[参照]** をクリックして Access ファイルを見つける場合、 **[開く]** ダイアログ ボックスでは古い .MDB 形式とファイル拡張子を持つファイルが既定でフィルター処理されます。 ただし、データ プロバイダーでは、新しい .ACCDB 形式とファイル拡張子を持つファイルを開くこともできます。
  
 **[参照]**  
 **[ファイルを開く]** ダイアログ ボックスを使用して、データベース ファイルを検索します。  
  
 **User name**  
ワークグループの情報ファイルがデータベースに関連付けられている場合は、有効なユーザー名を指定します。  
  
 **パスワード**  
ワークグループの情報ファイルがデータベースに関連付けられている場合は、ここでユーザーのパスワードを指定します。
 
データベースがすべてのユーザーに対して 1 つのパスワードで保護されている場合は、「[データベース ファイルはパスワードで保護されているか](#database_password)」を参照してください。
  
 **詳細設定**  
**[データ リンク プロパティ]** ダイアログ ボックスで、データベースのパスワードや既定以外のワークグループ情報ファイルなどの詳細なオプションを指定します。  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>データ ソースのリストに Access が表示されない
データ ソースのリストに Access が表示されない場合は、64 ビットのウィザードを実行していないか確認してください。 Excel と Access のプロバイダーは、通常 32 ビットで、64 ビットのウィザードでは表示されません。 代わりに 32 ビットのウィザードを実行します。

> [!NOTE]
> 64 ビット バージョンの SQL Server インポートおよびエクスポート ウィザードを使用するには、SQL Server をインストールする必要があります。 SQL Server Data Tools (SSDT) および SQL Server Management Studio (SSMS) は 32 ビット アプリケーションであり、32 ビット バージョンのウィザードを含む、32 ビット ファイルのみがインストールできます。

## <a name="officeDownloads"></a>Access に接続するために必要なファイルを取得する  
Access と Excel を含む Microsoft Office データ ソース用の接続コンポーネントがまだインストールされていない場合は、必要に応じてダウンロードします。 Access と Excel の両方のファイルの最新バージョンの接続コンポーネントを [Microsoft Access データベース エンジン 2016 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=54920)でダウンロードします。
  
以前のバージョンの Access で作成したファイルは、最新バージョンのコンポーネントで開くことができます。

コンピューターに 32 ビット バージョンの Office が存在する場合は、32 ビット バージョンのコンポーネントをインストールする必要があるほか、32 ビット モードでパッケージが実行されるようにする必要があります。

Office 365 サブスクリプションがある場合は、Microsoft Access 2016 ランタイムではなく、必ず Access データベース エンジン 2016 再頒布可能パッケージをダウンロードしてください。 インストーラーを実行するときに、ダウンロードを Office のクイック実行コンポーネントとサイド バイ サイドでインストールできないことを示すエラー メッセージが表示される場合があります。 このエラー メッセージを回避するには、コマンド プロンプト ウィンドウを開き、`/quiet` スイッチを使用してダウンロードした .EXE ファイルを実行して、Quiet モードでインストールを実行します。 例:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a> データベース ファイルはパスワードで保護されているか
Access データベースがパスワードで保護されているものの、ワークグループの情報ファイルを使用していない場合があります。 すべてのユーザーが同じパスワードを指定する必要がありますが、ユーザー名を入力する必要はありません。 データベースのパスワードを提供するには、次の手順を実行します。

1.  **[データ ソースの選択]** または **[変換先の選択]** ページで、 **[詳細設定]** をクリックして、 **[データ リンク プロパティ]** ダイアログ ボックスを開きます。  
2.  **[データ リンク プロパティ]** ダイアログ ボックスで、 **[すべて]** タブを選択します。  
3.  プロパティと値のリストで、 **[Jet OLEDB:データベースのパスワード]** を選択します。   
    
    ![Access パスワードの指定、画面 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  **[値の編集]** をクリックして、 **[プロパティの値を編集]** ダイアログ ボックスを開きます。  
    
    ![Access パスワードの指定、画面 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  **[プロパティの値を編集]** ダイアログ ボックスで、データベースのパスワードを入力します。
6.  各ダイアログ ボックスで **[OK]** をクリックして、ウィザードの **[データ ソースの選択]** または **[変換先の選択]** ページに戻り、続行します。

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>Access からエクスポートするときに、autonumber 値を保持する
変換元データの既存の ID 値を変換先テーブルの ID 列に挿入できるようにするには、 **[列マッピング]** ダイアログボックスで **[ID 挿入を許可する]** オプションを選択します。 既定では、変換先の ID 列に対して既存の値を挿入することは通常許可されません。 **[列マッピング]** ダイアログ ボックスを表示するには、ウィザードの **[コピー元のテーブルおよびビューを選択]** ページに到達したときに、 **[マッピングの編集]** を選択します。 これらのページを見るには、「[コピー元のテーブルおよびビューを選択](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)」と「[列マッピング](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)」を参照してください。

既存のプライマリ キーが id 列、autonumber 列、または同等の列である場合、既存のプライマリ キー値を保持するには、通常、このオプションを選択する必要があります。 その他の場合、変換先の ID 列には通常、新しい値が割り当てられます。

## <a name="see-also"></a>参照
[データ ソースの選択](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[変換先の選択](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

