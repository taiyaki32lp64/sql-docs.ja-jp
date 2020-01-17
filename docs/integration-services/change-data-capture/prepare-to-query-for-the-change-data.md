---
title: 変更データのクエリを準備する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],preparing query
ms.assetid: 9ea2db7a-3dca-4bbf-9903-cccd2d494b5f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 610f75fa8b706dab60b9691b4f5e5e82c2bdb93f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294623"
---
# <a name="prepare-to-query-for-the-change-data"></a>変更データのクエリを準備する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  変更データの増分読み込みを実行する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの制御フローにおいて、3 番目に行う最後のタスクは、変更データのクエリを準備してデータ フロー タスクを追加することです。  
  
> [!NOTE]  
>  制御フローの 2 番目のタスクは、選択した間隔の変更データが準備できていることを確認することです。 このタスクの詳細については、「[データの変更の準備ができているかどうかを判断する](../../integration-services/change-data-capture/determine-whether-the-change-data-is-ready.md)」を参照してください。 制御フローをデザインするプロセス全体の説明については、「[変更データ キャプチャ &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)」を参照してください。  
  
## <a name="design-considerations"></a>デザインに関する考慮事項  
 変更データを取得するには、間隔のエンドポイントを入力パラメーターとして受け取り、指定した間隔の変更データを返す Transact-SQL テーブル値関数を呼び出します。 この関数は、データ フローの変換元コンポーネントによって呼び出されます。 この変換元コンポーネントに関する詳細については、「 [変更データを取得および理解する](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md)」を参照してください。  
  
 OLE DB ソース、ADO ソース、ADO NET ソースなどの最もよく使用される [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変換元コンポーネントでは、テーブル値関数のパラメーター情報を取得できません。 したがって、ほとんどの変換元では、パラメーター化された関数を直接呼び出すことはできません。  
  
 入力パラメーターを関数に渡すには、次の 2 つのデザイン方法があります。  
  
-   **パラメーター化クエリを文字列として作成します**。 スクリプト タスクまたは SQL 実行タスクを使用して、文字列にハードコーディングされたパラメーター値で動的 SQL 文字列を作成できます。 その後、この文字列をパッケージ変数に格納したものを使用して、変換元コンポーネントの SqlCommand プロパティを設定できます。 変換元コンポーネントでパラメーター情報が不要になるので、この方法は有効です。  
  
    > [!NOTE]  
    >  発生するオーバーヘッドは、SQL 実行タスクよりも事前コンパイルしたスクリプトの方が少なくなります。  
  
-   **パラメーター化されたラッパーを使用します**。 パラメーター化されたテーブル値関数を呼び出すラッパーとして、パラメーター化されたストアド プロシージャを作成できます。 変換元コンポーネントでストアド プロシージャのパラメーター情報を正常に取得できるので、この方法は有効です。  
  
 ここでは最初のデザイン方法を使用し、パラメーター化クエリを文字列として作成します。  
  
## <a name="preparing-the-query"></a>クエリの準備  
 入力パラメーターの値を 1 つのクエリ文字列に連結する前に、クエリで必要なパッケージ変数を設定する必要があります。  
  
#### <a name="to-set-up-package-variables"></a>パッケージ変数を設定するには  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]の **[変数]** ウィンドウで、SQL 実行タスクによって返されるクエリ文字列を格納する文字列データ型の変数を作成します。  
  
     この例では、SqlDataQuery という名前の変数を使用します。  
  
 パッケージ変数を作成したら、スクリプト タスクまたは SQL 実行タスクを使用して入力パラメーターの値を連結できます。 次の 2 つの手順では、このコンポーネントを構成する方法について説明します。  
  
#### <a name="to-use-a-script-task-to-concatenate-the-query-string"></a>スクリプト タスクを使用してクエリ文字列を連結するには  
  
1.  **[制御フロー]** タブで、スクリプト タスクをパッケージの For ループ コンテナーの後に追加し、For ループ コンテナーをこのタスクに連結します。  
  
    > [!NOTE]  
    >  この手順では、パッケージによって 1 つのテーブルから増分読み込みが実行されることを前提としています。 複数のテーブルから読み込みが実行され、パッケージに親パッケージと複数の子パッケージが存在する場合、このタスクは最初のコンポーネントとして各子パッケージに追加されます。 詳細については、「 [複数のテーブルの増分読み込みを実行する](../../integration-services/change-data-capture/perform-an-incremental-load-of-multiple-tables.md)」を参照してください。  
  
2.  **[スクリプト タスク エディター]** の **[スクリプト]** ページで、次のオプションを選択します。  
  
    1.  **[ReadOnlyVariables]** で **[User::DataReady]** 、 **[User::ExtractStartTime]** 、および **[User::ExtractEndTime]** を一覧から選択します。  
  
    2.  **[ReadWriteVariables]** で [User::SqlDataQuery] を一覧から選択します。  
  
3.  **[スクリプト タスク エディター]** の **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックしてスクリプト開発環境を開きます。  
  
4.  Main プロシージャに、次のいずれかのコード セグメントを入力します。  
  
    -   C# でプログラミングしている場合は、次のコード行を入力します。  
  
        ```csharp 
        int dataReady;  
        System.DateTime extractStartTime;  
        System.DateTime extractEndTime;  
        string sqlDataQuery;  
  
        dataReady = (int)Dts.Variables["DataReady"].Value;  
        extractStartTime = (System.DateTime)Dts.Variables["ExtractStartTime"].Value;  
        extractEndTime = (System.DateTime)Dts.Variables["ExtractEndTime"].Value;  
  
        if (dataReady == 2)  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) + "', '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
        else  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" + ", '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
  
        Dts.Variables["SqlDataQuery"].Value = sqlDataQuery;  
        ```  
  
         \- - または -  
  
    -   [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]でプログラミングしている場合は、次のコード行を入力します。  
  
        ```vb  
        Dim dataReady As Integer  
        Dim extractStartTime As Date  
        Dim extractEndTime As Date  
        Dim sqlDataQuery As String  
  
        dataReady = CType(Dts.Variables("DataReady").Value, Integer)  
        extractStartTime = CType(Dts.Variables("ExtractStartTime").Value, Date)  
        extractEndTime = CType(Dts.Variables("ExtractEndTime").Value, Date)  
  
        If dataReady = 2 Then  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) & _  
              "', '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        Else  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" & _  
              ", '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        End If  
  
        Dts.Variables("SqlDataQuery").Value = sqlDataQuery  
  
        ```  
  
5.  スクリプトの実行から **DtsExecResult.Success** を返す既定のコード行はそのまま使用します。  
  
6.  スクリプト開発環境と **[スクリプト タスク エディター]** を閉じます。  
  
#### <a name="to-use-an-execute-sql-task-to-concatenate-the-query-string"></a>SQL 実行タスクを使用してクエリ文字列を連結するには  
  
1.  **[制御フロー]** タブで、SQL 実行タスクをパッケージの For ループ コンテナーの後に追加し、For ループ コンテナーをこのタスクに連結します。  
  
    > [!NOTE]  
    >  この手順では、パッケージによって 1 つのテーブルから増分読み込みが実行されることを前提としています。 複数のテーブルから読み込みが実行され、パッケージに親パッケージと複数の子パッケージが存在する場合、このタスクは最初のコンポーネントとして各子パッケージに追加されます。 詳細については、「 [複数のテーブルの増分読み込みを実行する](../../integration-services/change-data-capture/perform-an-incremental-load-of-multiple-tables.md)」を参照してください。  
  
2.  **[SQL 実行タスク エディター]** の **[全般]** ページで、次のオプションを選択します。  
  
    1.  **[ResultSet]** で **[単一行]** を選択します。  
  
    2.  ソース データベースへの有効な接続を構成します。  
  
    3.  **[SQLSourceType]** で **[直接入力]** を選択します。  
  
    4.  **[SQLStatement]** に、次の SQL ステートメントを入力します。  
  
        ```sql
        declare @ExtractStartTime datetime,  
        @ExtractEndTime datetime,   
        @DataReady int  
  
        select @DataReady = ?,   
        @ExtractStartTime = ?,   
        @ExtractEndTime = ?  
  
        if @DataReady = 2  
        select N'select * from CDCSample.uf_Customer'  
        + N'('''+ convert(nvarchar(30),@ExtractStartTime,120)  
        + ''', '''  
        + convert(nvarchar(30),@ExtractEndTime,120) + ''') '   
        as SqlDataQuery  
        else  
        select N'select * from CDCSample.uf_Customer'  
        + N'(null, '''  
        + convert(nvarchar(30),@ExtractEndTime,120)  
        + ''') '  
        as SqlDataQuery  
  
        ```  
  
        > [!NOTE]  
        >  このサンプルの **else** 句では、開始日時として NULL 値を渡すことによって変更データの最初の読み込みのクエリが生成されます。 このサンプルは、変更データ キャプチャを有効にする前に行われた変更もデータ ウェアハウスにアップロードする必要があるシナリオには対応していません。  
  
3.  **[SQL 実行タスク エディター]** の **[パラメーター マッピング]** ページで、次のマッピングを行います。  
  
    1.  DataReady 変数をパラメーター 0 にマップします。  
  
    2.  ExtractStartTime 変数をパラメーター 1 にマップします。  
  
    3.  ExtractEndTime 変数をパラメーター 2 にマップします。  
  
4.  **[SQL 実行タスク エディター]** の **[結果セット]** ページで、結果名を SqlDataQuery 変数にマップします。  
  
     結果名は、返される単一列の名前 SqlDataQuery になります。  
  
 上記の手順で、ハードコーディングされた入力パラメーターの文字列値を使用してクエリ文字列を準備するタスクを構成しました。 次に、このクエリ文字列のコード例を示します。  
  
 `select * from CDCSample. uf_Customer('2007-06-11 14:21:58', '2007-06-12 14:21:58')`  
  
## <a name="adding-a-data-flow-task"></a>データ フロー タスクの追加  
 パッケージの制御フローをデザインする最後の手順として、データ フロー タスクを追加します。  
  
#### <a name="to-add-a-data-flow-task-and-complete-the-control-flow"></a>データ フロー タスクを追加して制御フローを完成させるには  
  
-   **[制御フロー]** タブで、データ フロー タスクを追加し、クエリ文字列を連結したタスクを連結します。  
  
## <a name="next-step"></a>次の手順  
 クエリ文字列を準備してデータ フロー タスクを構成したら、次にデータベースから変更データを取得するテーブル値関数を作成します。  
  
 **次のトピック:** [変更データを取得する関数を作成する](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)  
  
  
