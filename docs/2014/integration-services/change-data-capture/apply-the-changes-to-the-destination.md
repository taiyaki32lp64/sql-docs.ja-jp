---
title: 変換先に変更を適用する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],applying changes
ms.assetid: 338a56db-cb14-4784-a692-468eabd30f41
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fe555d94eb8e00cddd147c2424d0cf60e1d47b34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771618"
---
# <a name="apply-the-changes-to-the-destination"></a>変換先に変更を適用する
  変更データの増分読み込みを実行する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのデータ フローにおいて、3 番目に行う最後のタスクは、変更を変換先に適用することです。 挿入を適用するコンポーネント、更新を適用するコンポーネント、および削除を適用するコンポーネントが必要です。  
  
> [!NOTE]  
>  変更データの増分読み込みを実行するパッケージのデータ フローをデザインするための 2 番目のタスクは、挿入、更新、および削除を分割することです。 このコンポーネントの詳細については、「[挿入、更新、および削除を処理する](process-inserts-updates-and-deletes.md)」を参照してください。 変更データの増分読み込みを実行するパッケージを作成するプロセス全体の説明については、「[変更データ キャプチャ (SSIS)](change-data-capture-ssis.md)」を参照してください。  
  
## <a name="applying-inserts"></a>挿入の適用  
 挿入を適用するには、新しい行で特別な処理は必要ないので、OLE DB 変換先を使用します。  
  
#### <a name="to-process-inserts-by-using-an-ole-db-destination"></a>OLE DB 変換先を使用して挿入を処理するには  
  
1.  **[データ フロー]** タブで、OLE DB 変換先を追加します。  
  
2.  条件分割変換から挿入を受け取った出力を OLE DB 変換先に接続します。  
  
3.  **[OLE DB 変換先エディター]** の **[接続マネージャー]** ページで、次のオプションを選択します。  
  
    1.  変換先データベースの OLE DB 接続マネージャーを選択または作成します。  
  
    2.  **[データ アクセス モード]** オプションを選択して、変換先テーブルを選択するか、変換先列を含む SQL ステートメントを入力します。  
  
4.  エディターの **[マッピング]** ページで、変更データの適切な列を変換先テーブルにマップします。  
  
## <a name="applying-updates"></a>更新の適用  
 更新を適用するには、OLE DB コマンド変換を使用します。 一度に 1 行を新しい列の値で更新する、パラメーター化された UPDATE ステートメントを使用する必要があるので、この変換を使用します。  
  
> [!NOTE]  
>  変換先コンポーネントを使用して更新を適用することもできます。 この方法を使用する場合は、変換先コンポーネントを使用して、このために作成した一時テーブルに行を保存します。 次に、SQL 実行タスクを使用して、一時テーブルから変換先に対して一括更新および一括削除操作を実行します。  
  
#### <a name="to-process-updates-by-using-an-ole-db-command-transformation"></a>OLE DB コマンド変換を使用して更新を処理するには  
  
1.  **[データ フロー]** タブで、OLE DB コマンド変換を追加します。  
  
2.  条件分割変換から更新を受け取った出力を OLE DB コマンド変換に接続します。  
  
3.  **[OLE DB コマンドの詳細エディター]** の **[接続マネージャー]** タブで、変換先データベースの OLE DB 接続マネージャーを選択または作成します。  
  
4.  **[OLE DB コマンドの詳細エディター]** の **[コンポーネントのプロパティ]** タブの **[SqlCommand]** に、パラメーター化された UPDATE ステートメントを入力します。  
  
     たとえば、Customer テーブルの UPDATE ステートメントの構文は次のようになります。  
  
    ```  
    update CDCSample.Customer  
    set TerritoryID  = ?,  
        CustomerType  = ?,  
        rowguid  = ?,  
        ModifiedDate  = ?  
    where CustomerID = ?  
  
    ```  
  
5.  エディターの **[列マッピング]** タブで、変更データの適切な列を UPDATE ステートメントのパラメーターにマップします。  
  
## <a name="applying-deletes"></a>削除の適用  
 削除を適用するには、OLE DB コマンド変換を使用します。 行を一意に識別する列の値に基づいて一度に 1 行を削除する、パラメーター化された DELETE ステートメントを使用する必要があるので、この変換を使用します。  
  
> [!NOTE]  
>  変換先コンポーネントを使用して削除を適用することもできます。 この方法を使用する場合は、変換先コンポーネントを使用して、このために作成した一時テーブルに行を保存します。 次に、SQL 実行タスクを使用して、一時テーブルから変換先に対して一括更新および一括削除操作を実行します。  
  
#### <a name="to-process-deletes-by-using-an-ole-db-command-transformation"></a>OLE DB コマンド変換を使用して削除を処理するには  
  
1.  **[データ フロー]** タブで、OLE DB コマンド変換をデータ フローに追加します。  
  
2.  条件分割変換から削除を受け取った出力を OLE DB コマンド変換に接続します。  
  
3.  詳細エディターを開いて変換を構成します。  
  
4.  **[OLE DB コマンドの詳細エディター]** の **[接続マネージャー]** タブで、変換先データベースの OLE DB 接続マネージャーを選択または作成します。  
  
5.  **[OLE DB コマンドの詳細エディター]** の **[コンポーネントのプロパティ]** タブの **[SqlCommand]** に、パラメーター化された DELETE ステートメントを入力します。  
  
     たとえば、Customer テーブルの DELETE ステートメントの構文は次のようになります。  
  
    ```  
    delete from Customer where CustomerID = ?  
  
    ```  
  
6.  エディターの **[列マッピング]** タブで、変更データの適切な列を DELETE ステートメントのパラメーターにマップします。  
  
## <a name="optimizing-inserts-and-updates-by-using-merge-functionality"></a>MERGE 機能を使用した挿入と更新の最適化  
 特定の変更データ キャプチャ オプションと Transact-SQL の MERGE キーワードを組み合わせて使用することによって、挿入と更新の処理を最適化できます。 MERGE キーワードの詳細については、「[MERGE (Transact-SQL)](/sql/t-sql/statements/merge-transact-sql)」を参照してください。  
  
 変更データを取得する Transact-SQL ステートメントで、**cdc.fn_cdc_get_net_changes_<capture_instance>** 関数を呼び出すときに、*row_filter_option* パラメーターの値として *all with merge* を指定できます。 この変更データ キャプチャの関数は、挿入と更新を区別するために必要な追加の処理を実行する必要がない場合、効率が向上します。 *all with merge* パラメーター値を指定すると、変更データの **__$operation** 値は、削除の場合は 1、挿入または更新によって生じた変更の場合は 5 になります。 変更データの取得に使用する Transact-SQL 関数の詳細については、「 [変更データを取得および理解する](retrieve-and-understand-the-change-data.md)」を参照してください。 *all with merge* パラメーター値を使用して変更を取得したら、削除を適用して、残りの行を一時テーブルまたはステージング テーブルに出力することができます。 その後、下流の SQL 実行タスクで単一の MERGE ステートメントを使用して、すべての挿入または更新をステージング テーブルから変換先に適用できます。  
  
  
