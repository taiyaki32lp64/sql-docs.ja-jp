---
title: レコードセット変換先を使用する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Recordset destination
ms.assetid: a7b143dc-8008-404f-83b0-b45ffbca6029
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b87d71f8299c55e033adc21e25e29e8fb3d5e9d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900001"
---
# <a name="use-a-recordset-destination"></a>レコードセット変換先を使用する
  レコードセット変換先では、データは外部データ ソースに保存されません。 代わりに、レコードセット変換先では、`Object` データ型の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ変数に格納されるレコードセットのメモリにデータが保存されます。 レコードセット変換先でデータが保存されたら、通常、Foreach ループ コンテナーと Foreach ADO 列挙子を使用して、一度に 1 つのレコードセット行を処理します。 Foreach ADO 列挙子によって、現在の行の各列の値が個別のパッケージ変数に保存されます。 その後、Foreach ループ コンテナー内で構成したタスクによって変数から値が読み取られ、その値を使用してアクションが実行されます。  
  
 レコードセット変換先は、さまざまなシナリオで使用できます。 次にいくつかの例を示します。  
  
-   メール送信タスクと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 式言語を使用して、レコードセットの行ごとにカスタマイズされた電子メール メッセージを送信できます。  
  
-   データ フロー タスク内で変換元として構成されたスクリプト コンポーネントを使用して、列値をデータ フローの列に読み取ることができます。 その後、変換や変換先を使用して、行を変換および保存できます。 この例では、データ フロー タスクが行ごとに 1 回実行されます。  
  
 ここでは、まずレコードセット変換先を使用する一般的な手順について説明し、次に変換先の使用方法の具体的な例を示します。  
  
## <a name="general-steps-to-using-a-recordset-destination"></a>レコードセット変換先を使用する一般的な手順  
 次の手順は、レコードセット変換先にデータを保存し、Foreach ループ コンテナーを使用して各行を処理するために必要な手順をまとめたものです。  
  
#### <a name="to-save-data-to-a-recordset-destination-and-process-each-row-by-using-the-foreach-loop-container"></a>レコードセット変換先にデータを保存し、Foreach ループ コンテナーを使用して各行を処理するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを作成または開きます。  
  
2.  レコードセット変換先でメモリに保存されたレコードセットを格納する変数を作成し、変数の型を `Object` に設定します。  
  
3.  使用するレコードセットの各列の値を格納するために、適切な型の追加の変数を作成します。  
  
4.  データ フローで使用するデータ ソースに必要な接続マネージャーを追加して構成します。  
  
5.  データ フロー タスクをパッケージに追加し、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの [データ フロー] タブで、データの読み込みおよび変換を行うための変換元および変換を構成します。  
  
6.  レコードセット変換先をデータ フローに追加し、変換に接続します。 レコードセット変換先の `VariableName` プロパティに、レコードセットを格納するために作成した変数の名前を入力します。  
  
7.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの [制御フロー] タブで、Foreach ループ コンテナーを追加し、このコンテナーをデータ フロー タスクの後に連結します。 **[Foreach ループ エディター]** を開いて、次の設定を使用してコンテナーを構成します。  
  
    1.  **[コレクション]** ページで、[Foreach ADO 列挙子] をクリックします。 次に、 **[ADO オブジェクト ソース変数]** で、レコードセットが含まれる変数を選択します。  
  
    2.  **[変数のマッピング]** ページで、使用する各列の 0 から始まるインデックスを適切な変数にマップします。  
  
         ループの各反復処理で、列挙子によってこれらの変数に現在の行の列値が設定されます。  
  
8.  Foreach ループ コンテナー内にタスクを追加し、変数から値を読み取って一度に 1 つのレコードセット行を処理するように構成します。  
  
## <a name="example-of-using-the-recordset-destination"></a>レコードセット変換先の使用例  
 次の例では、データ フロー タスクが [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] の従業員に関する情報を Sales.SalesPerson テーブルからレコードセット変換先に読み込みます。 次に、Foreach ループ コンテナーが一度に 1 つのデータ行を読み取って、メール送信タスクを呼び出します。 メール送信タスクは、式を使用して、ボーナス額に関するカスタマイズされた電子メール メッセージを各販売員に送信します。  
  
#### <a name="to-create-the-project-and-configure-the-variables"></a>プロジェクトを作成して変数を構成するには  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、新しい [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを作成します。  
  
2.  **[SSIS]** メニューの **[変数]** をクリックします。  
  
3.  **[変数]** ウィンドウで、レコードセットと現在の行の列値を格納する変数を作成します。  
  
    1.  `BonusRecordset` という名前の変数を作成し、その型を `Object` に設定します。  
  
         `BonusRecordset` 変数にはレコードセットが格納されます。  
  
    2.  `EmailAddress` という名前の変数を作成し、その型を `String` に設定します。  
  
         `EmailAddress` 変数には販売員の電子メール アドレスが格納されます。  
  
    3.  `FirstName` という名前の変数を作成し、その型を `String` に設定します。  
  
         `FirstName` 変数には販売員の名が格納されます。  
  
    4.  `Bonus` という名前の変数を作成し、その型を `Double` に設定します。  
  
         `Bonus` 変数には販売員のボーナス額が格納されます。  
  
#### <a name="to-configure-the-connection-managers"></a>接続マネージャーを構成するには  
  
1.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの [接続マネージャー] 領域で、 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] サンプル データベースに接続する新しい OLE DB 接続マネージャーを追加して構成します。  
  
     この接続マネージャーは、データ フロー タスクの OLE DB ソースがデータを取得するために使用されます。  
  
2.  [接続マネージャー] 領域で、使用可能な SMTP サーバーに接続する新しい SMTP 接続マネージャーを追加して構成します。  
  
     この接続マネージャーは、Foreach ループ コンテナー内のメール送信タスクが電子メールを送信するために使用されます。  
  
#### <a name="to-configure-the-data-flow-and-the-recordset-destination"></a>データ フローとレコードセット変換先を構成するには  
  
1.  **デザイナーの** [制御フロー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブで、データ フロー タスクをデザイン画面に追加します。  
  
2.  **[データ フロー]** tab, add an OLE DB source to the [データ フロー] task, and then open the **[OLE DB ソース エディター]** を開きます。  
  
3.  エディターの **[接続マネージャー]** ページで、次の設定を使用してソースを構成します。  
  
    1.  **[OLE DB 接続マネージャー]** で、前もって作成した OLE DB 接続マネージャーを選択します。  
  
    2.  **[データ アクセス モード]** で、 **[SQL コマンド]** を選択します。  
  
    3.  **[SQL コマンド テキスト]** で、次のクエリを入力します。  
  
        ```  
        SELECT     Person.Contact.EmailAddress, Person.Contact.FirstName, CONVERT(float, Sales.SalesPerson.Bonus) AS Bonus  
        FROM         Sales.SalesPerson INNER JOIN  
                              Person.Contact ON Sales.SalesPerson.SalesPersonID = Person.Contact.ContactID  
        ```  
  
        > [!NOTE]  
        >  Bonus 列の `currency` 値を `float` 型のパッケージ変数に読み込む前に、その値を `Double` に変換する必要があります。  
  
4.  **[データ フロー]** タブで、レコードセット変換先を追加し、この変換先を OLE DB ソースの後に連結します。  
  
5.  **[レコードセット変換先エディター]** を開いて、次の設定を使用して変換先を構成します。  
  
    1.  **コンポーネントのプロパティ** タブの`VariableName`プロパティで、`User::BonusRecordset`します。  
  
    2.  **[入力列]** タブで、使用可能な 3 つすべての列を選択します。  
  
#### <a name="to-configure-the-foreach-loop-container-and-run-the-package"></a>Foreach ループ コンテナーを構成してパッケージを実行するには  
  
1.  **デザイナーの** [制御フロー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブで、Foreach ループ コンテナーを追加し、このコンテナーをデータ フロー タスクの後に連結します。  
  
2.  **[Foreach ループ エディター]** を開いて、次の設定を使用してコンテナーを構成します。  
  
    1.  **コレクション** ページの**列挙子**を選択します**Foreach ADO 列挙子**、および**ADO オブジェクト ソース変数**を選択します。`User::BonusRecordset`.  
  
    2.  **変数のマッピング**ページで、マップ`User::EmailAddress`をインデックス 0、`User::FirstName`をインデックス 1、および`User::Bonus`インデックス 2 にします。  
  
3.  **[制御フロー]** タブで、Foreach ループ コンテナー内にメール送信タスクを追加します。  
  
4.  **[メール送信タスク エディター]** を開いて、 **[メール]** ページで次の設定を使用してタスクを構成します。  
  
    1.  **[SmtpConnection]** で、前もって構成した SMTP 接続マネージャーを選択します。  
  
    2.  **[差出人]** に、適切な電子メール アドレスを入力します。  
  
         自分の電子メール アドレスを使用すると、パッケージが正常に実行されているかどうかを確認できます。 メール送信タスクによって [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]に存在しない販売員にメッセージが送信されると、配信できなかったことが通知されます。  
  
    3.  **[宛先]** に、既定の電子メール アドレスを入力します。  
  
         この値は使用されませんが、実行時に各販売員の電子メール アドレスに置き換えられます。  
  
    4.  **[件名]** に、「Your annual bonus」と入力します。  
  
    5.  **[MessageSourceType]** に対して **[直接入力]** を選択します。  
  
5.  **[メール送信タスク エディター]** の **[式]** ページで、参照ボタン ( **[...]** ) をクリックして **[プロパティ式エディター]** を開きます。  
  
6.  **[プロパティ式エディター]** で、次の情報を入力します。  
  
    1.  **[ToLine]** に、次の式を追加します。  
  
        ```  
        @[User::EmailAddress]  
        ```  
  
    2.  **MessageSource** プロパティに、次の式を追加します。  
  
        ```  
        "Dear " +  @[User::FirstName] + ": The amount of your bonus for this year is $" +  (DT_WSTR, 12) @[User::Bonus] + ". Thank you!"  
        ```  
  
7.  パッケージを実行します。  
  
     有効な SMTP サーバーと自分の電子メール アドレスを指定すると、メール送信タスクによって [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]に存在しない販売員にメッセージが送信され、配信できなかったことが通知されます。  
  
  
