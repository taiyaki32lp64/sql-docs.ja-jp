---
title: 変換先の選択 (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 746aed7f49b0db51f46a32fdf040eb5b9e968dd2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768027"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>[変換先の選択] (SQL Server インポートおよびエクスポート ウィザード)
  使用して、**変換先の選択**ページをコピーするデータの送信先を指定します。  
  
 このウィザードの詳細については、次を参照してください。 [SQL Server インポートおよびエクスポート ウィザード](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)します。 ウィザードを正常に実行するために必要なアクセス許可と同様に、ウィザードを開始するためのオプションについては、次を参照してください。 [、SQL Server インポートおよびエクスポート ウィザードを実行](start-the-sql-server-import-and-export-wizard.md)します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードの目的は、変換元から変換先にデータをコピーすることです。 また、このウィザードでは、変換先データベースと変換先テーブルも作成できます。 ただし、複数のデータベースやテーブルまたは他の種類のデータベース オブジェクトをコピーする必要がある場合は、データベース コピー ウィザードを使用してください。 詳細については、「 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)」を参照してください。  
  
## <a name="static-options"></a>静的オプション  
 **変換先**  
 変換先の保存形式に対応したデータ プロバイダーを選択します。 データ ソースに使用できるプロバイダーが複数存在する可能性があります。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用することができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client、.NET Framework Data Provider for SQL Server、または、Microsoft OLE DB Provider for SQL Server。  
  
> [!NOTE]  
>  データを ODBC 変換先に保存するには、.NET Framework Data Provider for ODBC を選択します。  
  
 **データソース**プロパティは、さまざまなオプションは、コンピューターにインストールされているプロバイダーによって異なります。 次の表に、一般的に使用される変換先に対応するオプションを示します。 他のプロバイダーについては、プロバイダー固有のマニュアルを参照してください。  
  
## <a name="dynamic-options"></a>動的オプション  
 以下では、いくつかのデータ ソースで利用可能なオプションを示します。 [変換先] ドロップダウン リストに表示される変換先をすべて示しているわけではありません。  
  
### <a name="destination--sql-server-native-client-or-microsoft-ole-db-provider-for-sql-server"></a>[変換先] = [SQL Server Native Client] または [Microsoft OLE DB Provider for SQL Server]  
 **サーバー名**  
 データを受け取るサーバーの名前を入力するか、一覧からサーバーを選択します。  
  
 **[Windows 認証を使用する]**  
 パッケージで Microsoft Windows 認証を使用してデータベースにログインするかどうかを指定します。 より高いセキュリティのためには Windows 認証をお勧めします。  
  
 **[SQL Server 認証を使用する]**  
 データベースへのログインに、パッケージが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用するかどうかを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、ユーザー名とパスワードを入力する必要があります。  
  
 **ユーザー名**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合に、データベース接続用のユーザー名を指定します。  
  
 **Password**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合に、データベース接続用のパスワードを指定します。  
  
 **[データベース]**  
 指定されたインスタンス上のデータベースの一覧から選択[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、クリックして新しいデータベースを作成または**新規**します。  
  
 **[更新]**  
 **[更新]** をクリックして、利用可能なデータベースの一覧を復元します。  
  
 **[新規作成]**  
 使用して新しい変換先データベースを作成、 **Create Database**  ダイアログ ボックス。  
  
### <a name="destination--flat-file-destination"></a>[変換先] = [フラット ファイル変換先]  
 **[ファイル名]**  
 データを格納するファイルのパスとファイル名を指定します。 または、 **[参照]** をクリックしてファイルを探します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、ファイルを検索します。  
  
 **ロケール**  
 文字の並べ替え順と日時の形式を定義するロケールの ID (LCID) を指定します。  
  
 **Unicode**  
 Unicode を使用するかどうかを示します。 Unicode を使用する場合、コード ページを指定する必要はありません。  
  
 **コード ページ**  
 使用する言語のコード ページを指定します。  
  
 **形式**  
 区切り形式、固定幅形式、または幅合わせしない形式を使用するかどうかを示します。  
  
|値|説明|  
|-----------|-----------------|  
|[区切り記号]|列は、 **[列]** ページで指定した区切り記号で区切られます。|  
|[固定幅]|列は固定幅を持ちます。|  
|[幅合わせしない]|幅合わせしないファイルとは、最後の列以外のすべての列が固定幅を持つファイルです。最後の列は、行区切り記号で区切られます。|  
  
 **テキスト修飾子**  
 使用するテキスト修飾子を入力します。 たとえば、各テキスト列を引用符で囲むように指定できます。  
  
 **先頭データ行を列名として使用する**  
 先頭のデータ行に列名を表示するかどうかを指定します。  
  
### <a name="destination--microsoft-excel"></a>[変換先] = [Microsoft Excel]  
  
> [!NOTE]  
>  選択**Excel** Excel 2003 を使用するデータ ソースに接続する場合にのみ、またはそれ以前。 Excel 2007 を使用するデータ ソースに接続するには、選択**Microsoft Office 12.0 Access Database Engine OLE DB Provider**、 をクリックして**プロパティ**、し、**すべて**のタブ、**データ リンク プロパティ** ダイアログ ボックスの**拡張プロパティ**、入力`Excel 12.0`します。  
  
 **[Excel ファイル パス]**  
 データを格納するブックのパスとファイル名を指定 (たとえば、C:\MyData.xls、 \\\Sales\Database\Northwind.xls)。 または、 **[参照]** をクリックしてブックを探します。  
  
 **[参照]**  
 使用して、Excel ブックを検索、**オープン** ダイアログ ボックス。  
  
 **[Excel バージョン]**  
 変換先のブックで使用される Excel のバージョンを選択します。  
  
> [!NOTE]  
>  データを変換先の [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] にエクスポートする場合、ウィザードでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Excel 変換先コンポーネントを使用します。 いくつかの使用に関する考慮事項と既知の問題については、次を参照してください。 [Excel 変換先](../data-flow/excel-destination.md)します。  
  
### <a name="destination--microsoft-access"></a>[変換先] = [Microsoft Access]  
  
> [!NOTE]  
>  選択**Access** Access 2003 を使用するデータベースに接続する場合にのみ、またはそれ以前。 Access 2007 を使用するデータベースに接続するには、選択**Microsoft Office 12.0 Access Database Engine OLE DB Provider**します。  
  
 **[ファイル名]**  
 データを格納するデータベース ファイルのパスとファイル名を指定する (たとえば、C:\MyData.mdb、 \\\Sales\Database\Northwind.mdb)。 または、 **[参照]** をクリックしてデータベース ファイルを探します。  
  
 **[参照]**  
 データベース ファイルを使用して参照、**オープン** ダイアログ ボックス。  
  
 **ユーザー名**  
 ワークグループの情報ファイルがデータベースに関連付けられている場合は、データベース接続のために有効なユーザー名を指定します。  
  
 **Password**  
 ワークグループの情報ファイルがデータベースに関連付けられている場合は、データベース接続のためにユーザーのパスワードを指定します。 ただし、データベースがすべてのユーザーに対して 1 つのパスワードで保護されている場合、 **[データ リンク プロパティ]** ダイアログ ボックスでもこの値を入力する必要があります。このダイアログ ボックスを表示するには **[詳細設定]** ボタンをクリックします。  
  
 **詳細設定**  
 **[データ リンク プロパティ]** ダイアログ ボックスで、データベースのパスワードや既定以外のワークグループ情報ファイルなどの詳細なオプションを指定します。 OLE DB プロバイダーのプロパティの詳細については、 [MSDN ライブラリ](https://go.microsoft.com/fwlink/?linkid=62553)の「データ アクセス」を検索してください。  
  
  
