---
title: Integration Services での読み込み
description: SQL Server Integration Services (SSIS) パッケージを使用して並列データウェアハウス (PDW) にデータを読み込む方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b0bcb5cfe1ec4111aaea7153f35bca084df62b76
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401011"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>Integration Services を使用して並列データウェアハウスにデータを読み込む
SQL Server Integration Services (SSIS) パッケージを使用して SQL Server 並列データウェアハウスにデータを読み込む方法について説明します。  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>方  
Integration Services は、データの高パフォーマンスの抽出、変換、読み込み (ETL) を行うための SQL Server のコンポーネントであり、一般的にデータウェアハウスの設定と更新に使用されます。  
  
PDW 変換先アダプターは Integration Services コンポーネントで、Integration Services .dtsx パッケージを使用して PDW にデータを読み込むことができます。 SQL ServerPDW のパッケージワークフローでは、複数のソースからデータを読み込んでマージし、複数の変換先にデータを読み込むことができます。 データの読み込みは、1 つのパッケージと、同時に実行されている複数のパッケージ内の両方で並行して行われます。同じアプライアンス上で最大 10 の読み込みを並行して実行できます。  
  
このトピックで説明するタスクに加えて、Integration Services の他の機能を使用して、データをデータウェアハウスに読み込む前に、フィルター処理、変換、分析、およびクレンジングを行うことができます。 SQL ステートメントの実行、子パッケージの実行、またはメールの送信によって、パッケージのワークフローを拡張することもできます。  
  
Integration Services の詳細なドキュメントについては、「 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)」を参照してください。  
  
## <a name="HowToDeployPackage"></a>Integration Services パッケージを実行する方法  
これらの方法のいずれかを使用して、Integration Services パッケージを実行します。  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>SQL Server 2008 R2 Business Intelligence Development Studio (入札) からの実行  
[入札] 内からパッケージを実行するには、パッケージを右クリックして [**パッケージの実行**] を選択します。  
  
既定では、入札は64ビットのバイナリを使用してパッケージを実行します。 これは、 **Run64BitRuntime** package プロパティによって決定されます。 このプロパティを設定するには、[**ソリューションエクスプローラー**にアクセスし、プロジェクトを右クリックして、[**プロパティ**] を選択します。 **Integration Services プロパティページ**で、[**構成プロパティ**] にアクセスし、[**デバッグ**] を選択します。 **デバッグオプション**の下に**Run64BitRuntime**プロパティが表示されます。 32ビットランタイムを使用するには、これを**False**に設定します。 64ビットランタイムを使用するには、これを**True**に設定します。  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>SQL Server 2012 から実行 SQL Server Data Tools  
SQL Server Data Tools 内からパッケージを実行するには、パッケージを右クリックして [**パッケージの実行**] を選択します。  
  
### <a name="run-from-powershell"></a>PowerShell から実行する  
**Dtexec**ユーティリティを使用して Windows PowerShell からパッケージを実行するには、次のようにします。`dtexec /FILE <packagePath>`  
  
たとえば、`dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"` のように指定します。  
  
### <a name="run-from-a-windows-command-prompt"></a>Windows コマンドプロンプトから実行する 
Windows コマンドプロンプトから、 **dtexec**ユーティリティを使用してパッケージを実行するには、次のようにします。`dtexec /FILE <packagePath>`  
  
たとえば次のようになります。`dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>データの種類  
Integration Services を使用してデータソースから SQL Server PDW データベースにデータを読み込む場合、最初にデータがソースデータから Integration Services データ型にマップされます。 これにより、複数のデータ ソースのデータをデータ型の共通のセットにマップできます。  
  
その後、データは Integration Services から SQL Server PDW データ型にマップされます。 次の表に、SQL Server PDW データ型ごとに、SQL Server PDW データ型に変換できるデータ型 Integration Services を示します。  
  
|PDW データ型|PDW データ型にマップされるデータ型の Integration Services|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|BIGINT|DT_I1、DT_I2、DT_I4、DT_I8、DT_UI1、DT_UI2、DT_UI4|  
|CHAR|DT_STR|  
|DATE|DT_DBDATE|  
|DATETIME|DT_DATE、DT_DBDATE、DT_DBTIMESTAMP、DT_DBTIMESTAMP2|  
|DATETIME2|DT_DATE、DT_DBDATE、DT_DBTIMESTAMP、DT_DBTIMESTAMP2|  
|DATETIMEOFFSET|DT_WSTR|  
|DECIMAL|DT_DECIMAL、DT_I1、DT_I2、DT_I4、DT_I4、DT_I8、DT_NUMERIC、DT_UI1、DT_UI2、DT_UI4、DT_UI8|  
|FLOAT|DT_R4、DT_R8|  
|INT|DT_I1、DTI2、DT_I4、DT_UI1、DT_UI2|  
|MONEY|DT_CY|  
|NCHAR|DT_WSTR|  
|NUMERIC|DT_DECIMAL、DT_I1、DT_I2、DT_I4、DT_I8、DT_NUMERIC、DT_UI1、DT_UI2、DT_UI4、DT_UI8|  
|NVARCHAR|DT_WSTR、DT_STR|  
|REAL|DT_R4|  
|SMALLDATETIME|DT_DBTIMESTAMP2|  
|SMALLINT|DT_I1、DT_I2、DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**データ型の有効桁数の制限付きサポート**  
  
PDW では、有効桁数が28を超える値を含む DT_NUMERIC または DT_DECIMAL の入力列をマップすると、検証エラーが生成されます。  
  
**サポートされていないデータ型**  
  
SQL Server PDW は、次の Integration Services データ型をサポートしていません。  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
これらの型のデータを含む列を SQL Server PDW に読み込むには、データ変換の変換をデータフローの上流に追加して、データを互換性のあるデータ型に変換する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
Integration Services の読み込みパッケージを実行するには、次のものが必要です。  
  
-   データベースに対する読み込み権限。  
  
-   対象のテーブルに対する適用可能な INSERT、UPDATE、DELETE 権限。  
  
-   ステージングデータベースが使用されている場合、ステージングデータベースに対する CREATE 権限。 これは、一時テーブルを作成するためのものです。  
  
-   ステージングデータベースが使用されていない場合は、コピー先データベースに対する権限を作成します。 これは、一時テーブルを作成するためのものです。  
  
## <a name="GenRemarks"></a>一般的な注釈  
Integration Services パッケージで複数の SQL Server PDW 変換先が実行されていて、いずれかの接続が終了した場合、Integration Services は SQL Server PDW のすべての送信先へのデータのプッシュを停止します。  
  
## <a name="Limits"></a>規則や制限  
Integration Services パッケージの場合、同じデータソースの SQL Server PDW の宛先の数は、アクティブな読み込みの最大数によって制限されます。 最大数は事前に構成されており、ユーザーは構成できません。 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
同じデータソースの各 Integration Services パッケージの変換先は、パッケージの実行時に1つの負荷としてカウントされます。 たとえば、アクティブな読み込みの最大数が 10 であるとします。 同じデータ ソースの 11 以上の変換先を開こうとすると、パッケージは実行されません。  
  
各パッケージが使用するアクティブな読み込みが最大数を超えない限り、複数のパッケージを同時に実行できます。 たとえば、アクティブな読み込みの最大数が 10 の場合、それぞれが 10 の変換先を使用する 2 つのパッケージを同時に実行できます。 一方のパッケージが読み込みキューで待機しているときに、もう一方のパッケージが実行されます。  
  
読み込みキューの読み込みの数が、キューに登録された読み込みの最大数を超えると、パッケージは実行されません。 たとえば、負荷の最大数がアプライアンスごとに10個で、キューに置かれた負荷の最大数がアプライアンスあたり40である場合、それぞれが10の宛先を開く5つの Integration Services パッケージを同時に実行できます。 6 番目のパッケージを実行しようとしても、実行されません。  

> [!IMPORTANT]
> ソーステーブルに SQL 照合順序が指定された char および varchar 列が含まれている場合、データソースを PDW のマップ先アダプターと共に SSIS で OLE DB 使用すると、データが破損する可能性があります。 ソーステーブルに SQL 照合順序を持つ char または varchar 列が含まれている場合は、ADO.NET ソースを使用することをお勧めします。 

  
## <a name="Locks"></a>ロック動作  
Integration Services を使用してデータを読み込む場合、SQL ServerPDW は行レベルのロックを使用して、変換先テーブルのデータを更新します。 つまり、各行は更新時に読み取り/書き込み用にロックされます。 変換先テーブル内の行は、データがステージング テーブルに読み込まれる間はロックされません。  
  
## <a name="Examples"></a>例  
  
### <a name="Walkthrough"></a>ある. フラットファイルからの単純な読み込み  
次のチュートリアルでは、Integration Services を使用して SQL Server PDW アプライアンスにフラットファイルデータを読み込む簡単なデータ読み込みについて説明します。  この例では、前に説明したように、Integration Services がクライアントコンピューターに既にインストールされており、SQL Server PDW の宛先がインストールされていることを前提としています。  
  
この例では、次の DDL `Orders`を含むテーブルに読み込みます。 `Orders`テーブルは、 `LoadExampleDB`データベースの一部です。  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
読み込みデータを次に示します。  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
読み込みの準備として、読み込みデータを`exampleLoad.txt`含むフラットファイルを作成します。  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
まず、次の手順を実行して Integration Services パッケージを作成します。  
  
1.  \(SQL Server Data Tools SSDT\)で、[**ファイル**]、[**新規作成**]、[**プロジェクト**] の順に選択します。 一覧表示されたオプションから [ **Integration Services プロジェクト**] を選択します。 このプロジェクト`ExampleLoad`に名前を指定し、[ **OK]** をクリックします。  
  
2.  [**制御フロー** ] タブをクリックし、[**ツールボックス**] から [**データフロータスク**] を [**制御フロー** ] ペインにドラッグします。  
  
3.  [**データフロー** ] タブをクリックし、[**フラットファイルソース**] を**ツールボックス**から [**データフロー** ] ペインにドラッグします。 先ほど作成したボックスをダブルクリックして、[**フラットファイルソースエディター**] を開きます。  
  
4.  [**接続マネージャー** ] をクリックし、[**新規作成**] をクリックします。  
  
5.  [**接続マネージャー名**] ボックスに、接続のフレンドリ名を入力します。 この例では`Example Load Flat File CM`、を使用します。  
  
6.  [**参照**] をクリック`ExampleLoad.txt`し、ローカルコンピューターからファイルを選択します。  
  
7.  フラットファイルには列名を持つ行が含まれているため、[**最初のデータ行] ボックスで列名**をクリックします。  
  
8.  左側の列**の列をクリックし**、読み込まれるデータをプレビューして、列の名前とデータが正しく解釈されていることを確認します。  
  
9. 左側の列で [**詳細設定**] をクリックします。 各列名をクリックして、データに関連付けられているデータ型を確認します。 読み込まれたデータのデータ型が変換先の列の型と互換性を持つように、ボックスに変更を入力します。  
  
10. [ **OK** ] をクリックして、接続マネージャーを保存します。  
  
11. [ **OK]** をクリックして、**フラットファイルソースエディター**を終了します。  
  
データフローの変換先を指定します。  
  
1.  **SQL Server PDW 変換先**を**ツールボックス**から [**データフロー** ] ペインにドラッグします。  
  
2.  先ほど作成したボックスをダブルクリックして、 **SQL Server PDW 変換先エディター**を読み込みます。  
  
3.  [**接続マネージャー**] の横にある下矢印をクリックします。  
  
4.  [**新しい接続の作成**] を選択します。  
  
5.  サーバー、ユーザー、パスワード、および宛先データベースの情報を、アプライアンス固有の情報に入力します。 (例を次に示します)。 
  **[OK]** をクリックします。  
  
    [InfiniBand connections] \ (**サーバー名**\) には、「<appliance-name>-name」と入力します。  
  
    イーサネット接続の場合、[**サーバー名**]: 制御ノードクラスター、コンマ、ポート17001の IP アドレスを入力します。 たとえば、10.192.63.134、17001のようになります。  
  
    **ユーザーズ**`user1`  
  
    **入力**`password1`  
  
    **転送先データベース:**`LoadExampleDB`  
  
6.  変換先テーブル`Orders`を選択します。  
  
7.  読み込みモードとして [**追加**] を選択し、[ **OK**] をクリックします。  
  
転送元から転送先へのデータフローを指定します。  
  
1.  [**データフロー** ] ペインで、緑色の矢印を [**フラットファイルソース**] ボックスから [ **SQL Server PDW 変換先**] ボックスにドラッグします。  
  
2.  [ **SQL Server PDW 先**] ボックスをダブルクリックして、 **SQL Server PDW 変換先エディター**が再度表示されるようにします。 左側の [マップされていない**入力列**] の下に、フラットファイルの列名が表示されます。 右側の [マップされていない**変換先列**] の下に、コピー先テーブルの列名が表示されます。 [マップされていない**入力列**] と [マップされていない**変換先列**] の列名をドラッグまたはダブルクリックし**て、列**をマップします。 [ **OK]** をクリックして設定を保存します。  
  
3.  [**ファイル**] メニューの [**保存**] をクリックして、パッケージを保存します。  
  
コンピューター Integration Services でパッケージを実行します。  
  
1.  Integration Services**ソリューションエクスプローラー** (右の列) で、右クリック`Package.dtsx`して [**実行**] を選択します。  
  
2.  パッケージが実行され、進行状況とエラーが [**進行状況**] ウィンドウに表示されます。 SQL クライアントを使用して負荷を確認するか、SQL Server PDW 管理コンソールを使用して負荷を監視します。  
  
## <a name="see-also"></a>参照  
[SSIS PDW 変換先アダプターを使用するスクリプトタスクを作成する](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[パッケージの設計と実装 (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[チュートリアル : ウィザードを使用した基本パッケージの作成](https://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[はじめに (Integration Services)](https://go.microsoft.com/fwlink/?LinkId=202412)  
[動的パッケージ生成のサンプル](https://go.microsoft.com/fwlink/?LinkId=202413)  
[並列処理用の SSIS パッケージのデザイン (SQL Server ビデオ)](https://msdn.microsoft.com/library/dd795221.aspx)  
[Microsoft SQL Server コミュニティの例: Integration Services](https://go.microsoft.com/fwlink/?LinkId=202415)  
[変更データ キャプチャによる増分読み込みの向上](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[緩やかに変化するディメンション変換](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[一括挿入タスク](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
