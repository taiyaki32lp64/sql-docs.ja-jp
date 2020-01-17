---
title: 方法:CLR データベース オブジェクトを使用する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.allowsqlclrdebugging
ms.assetid: 4a28d43d-eb5e-444d-aace-5df691f38709
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a8ea668f0672a40e8af6fbb81bbce469652eeb54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119887"
---
# <a name="how-to-work-with-clr-database-objects"></a>方法:CLR データベース オブジェクトを使用する
Transact\-SQL プログラミング言語の他にも、.NET Framework 言語を使用して、データの取得と更新を行うデータベース オブジェクトを作成できます。 マネージド コードで記述したデータベース オブジェクトは、SQL Server 共通言語ランタイム (CLR: Common Language Run) データベース オブジェクトと呼ばれます。 SQL Server でホストされる CLR データベース オブジェクトを使用する利点と、Transact\-SQL と CLR の間での選択方法については、「[CLR 統合の利点](../relational-databases/clr-integration/clr-integration-overview.md)」および「[マネージド コードを使用したデータベース オブジェクトの作成の利点](https://msdn.microsoft.com/library/k2e1fb36.aspx)」をご覧ください。  
  
SQL Server Data Tools で CLR データベース オブジェクトを作成するには、データベース プロジェクトを作成し、これに CLR データベース オブジェクトを追加します。 以前のバージョンの Visual Studio とは異なり、CLR プロジェクトを別に作成したうえで、データベース プロジェクトからこのプロジェクトへの参照を追加する必要がありません。 データベース プロジェクトをビルドして公開すると、自動的にプロジェクト内の CLR オブジェクトも同時に公開されます。 このように公開された CLR オブジェクトは、他のデータベース オブジェクトと同じように呼び出して実行できます。  
  
CLR および CLR ビルドのプロパティ ページには、CLR オブジェクトをプロジェクトで使用するための設定が多数含まれています。 具体的には、CLR プロパティ ページには CLR アセンブリに対するアクセス許可を設定するためのアクセス許可レベル設定が含まれています。 また、プロジェクトに追加された CLR データベース オブジェクトの DDL を生成するかどうかを制御する "DDL を生成する" 設定も含まれています。 CLR ビルドのプロパティ ページには、プロジェクト内の CLR コードのコンパイルを構成するために設定できるコンパイラ オプションがすべて含まれています。 これらのプロパティ ページにアクセスするには、**ソリューション エクスプローラー**でプロジェクトを右クリックして、 **[プロパティ]** をクリックします。  
  
CLR データベース オブジェクトのデバッグを有効にするには、**SQL Server オブジェクト エクスプローラー**を開きます。 デバッグする CLR データベースの成果物を含むサーバーを右クリックし、 **[SQL または CLR のデバッグの許可]** をクリックします。 メッセージ ボックスに、警告が表示されます。"デバッグ中は、サーバー上のすべてのマネージ スレッドが停止されます。 このサーバーで SQL/CLR デバッグを有効にしますか?" という警告がメッセージ ボックスに表示されます。 CLR データベース オブジェクトをデバッグすると、実行の中断によりサーバー上のすべてのスレッドが停止され、他のユーザーに影響します。 このため、CLR データベース オブジェクト用アプリケーションのデバッグは運用サーバーでは行わないようにしてください。 また、デバッグを開始すると、**SQL Server オブジェクト エクスプローラー**の設定を変更できないことにも注意してください。 **SQL Server オブジェクト エクスプローラー**で行われた変更が反映されるのは、次回デバッグ セッションを開始するときです。  
  
CLR データベース オブジェクトをビルドするための要件について詳しくは、「[共通言語ランタイム (CLR) 統合によるデータベース オブジェクトの構築](https://msdn.microsoft.com/library/ms131046.aspx)」の関連トピックをご覧ください。  
  
> [!WARNING]  
> 以下に示す手順では、「[接続されているデータベース開発](../ssdt/connected-database-development.md)」および「[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)」に示されているこれまでの手順で作成したエンティティを使用します。  
  
### <a name="to-add-a-clr-database-object-to-your-project"></a>プロジェクトに CLR データベース オブジェクトを追加するには  
  
1.  **ソリューション エクスプローラー**で **TradeDev** データベース プロジェクトを右クリックし、 **[追加]** をポイントして、 **[新しい項目]** をクリックします。  
  
2.  **[C# SQL CLR]** テンプレートをクリックし、 **[SQL CLR ユーザー定義関数]** をクリックします。 既定の名前をそのままにして、 **[追加]** をクリックします。  
  
3.  クラス本体に次のコードを追加します。 この関数では、米国の電話番号を検証します。 有効な番号は、順に 3 桁の数字 (かっこで囲まれていてもよい)、3 桁の数字、および 4 桁の数字で構成されている必要があります。 サポートされる形式は、(425) 555-0123、425-555-0123、425 555 0123、1-425-555-0123 などです。  
  
    ```  
  
    [SqlFunction(IsDeterministic = true, IsPrecise = true)]  
    public static SqlBoolean validatePhone(SqlString phone)  
    {  
        string aNorthAmericanPhoneNumberPattern = @"^[01]?[- .]?(\([2-9]\d{2}\)|[2-9]\d{2})[- .]?\d{3}[- .]?\d{4}$";  
        if (!phone.IsNull)  
        {  
           Regex regex = new Regex(aNorthAmericanPhoneNumberPattern);  
           return regex.IsMatch(phone.Value);  
        }  
        return true;  
     }  
    ```  
  
4.  `Regex` は赤色の下線付きになっています。 `Regex` を右クリックし、 **[解決]** をクリックして、**using System.Text.RegularExpressions** をクリックします。  
  
5.  Microsoft SQL Server 2012 のサーバー インスタンスに対して開発を行っている場合は、この手順をスキップできます。 それ以外の場合、SQL Server 2005 および SQL Server 2008 では .NET Framework の Version 2.0、3.0、または 3.5 でビルドされたデータベース プロジェクトのみがサポートされます。 .NET ターゲット プラットフォームが正しく設定されているか確認するには、**ソリューション エクスプローラー**で **TradeDev** データベース プロジェクトを右クリックし、 **[プロパティ]** をクリックします。 **SQLCLR** プロパティ ページで、 **[ターゲット プラットフォーム]** を **.NET Framework 3.5** 以下に変更します。 最終画面で **[はい]** をクリックしてプロジェクトを閉じ、再度開きます。  
  
6.  **TradeDev** プロジェクトを右クリックし、 **[ビルド]** をクリックしてプロジェクトをビルドします。  
  
7.  Suppliers.sql をダブルクリックして **[デザイナーの表示]** をクリックすることにより、テーブル デザイナーで Suppliers テーブルを開きます。  
  
8.  列グリッドで空の行をクリックし、テーブルに新しい列を追加します。 **[名前]** に「**phone**」、 **[データ型]** に「**nvarchar (128)** 」と入力し、 **[Null を許容]** チェック ボックスはオンのままにします。  
  
9. コンテキスト ペインの **[CHECK 制約]** ノードを右クリックし、 **[新しい CHECK 制約の追加]** をクリックします。  
  
10. スクリプト ペインで、制約の既定の定義を次のように変更します。  
  
    ```  
    CONSTRAINT [CK_Suppliers_CheckPhone] CHECK (dbo.validatePhone(phone)=1),  
    ```  
  
    これにより、新しい phone フィールドへの入力はすべて、前に追加した CLR UDF でチェックされるようになります。  
  
11. F5 キーを押してプロジェクトをビルドし、ローカル データベースに配置します。  
  
### <a name="to-use-clr-database-objects"></a>CLR データベース オブジェクトを使用するには  
  
1.  **SQL Server オブジェクト エクスプローラー**で、プロジェクトを配置する先のローカル データベースに移動します。  
  
2.  既定では、SQL Server の CLR 統合機能はオフになっています。 CLR データベース オブジェクトを使用するには、CLR 統合機能を有効にする必要があります。 CLR 統合を有効にするには、sp_configure ストアド プロシージャの "clr enabled" オプションを使用します。 詳しくは、[clr enabled オプションに関するトピック](../relational-databases/clr-integration/clr-integration-enabling.md)をご覧ください。  
  
    データベースを右クリックし、 **[新しいクエリ]** をクリックします。 クエリ ペインに次のコードを貼り付け、 **[クエリの実行]** をクリックします。  
  
    ```  
  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO  
    ```  
  
3.  Suppliers テーブルを右クリックして、 **[データの表示]** をクリックします。  
  
4.  **id** に「**5**」、**name** に「**Contoso**」と入力し、**Address** フィールドを空のままにして、**phone** に「**425 3122 1222**」と入力します。 **phone** フィールドから Tab キーで移動すると、メッセージが表示され、定義済みの電話番号形式を使用して **phone** フィールドの入力をチェックする既存の CHECK 制約と、`INSERT` ステートメントとが競合していることを示します。  
  
5.  入力を「**425 312 1222**」に変更して Tab キーで移動します。 今回は入力が受け入れられます。  
  
## <a name="see-also"></a>参照  
[CLR 統合機能の利点](../relational-databases/clr-integration/clr-integration-overview.md)  
[マネージド コードを使用してデータベース オブジェクトを作成する利点](https://msdn.microsoft.com/library/k2e1fb36.aspx)  
[共通言語ランタイム (CLR) 統合を使用したデータベース オブジェクトの構築](https://msdn.microsoft.com/library/ms131046.aspx)  
  
