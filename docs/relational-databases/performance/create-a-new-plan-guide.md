---
title: 新しいプラン ガイドの作成 | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.designer.newplanguide.f1
helpviewer_keywords:
- creating plan guides
- plan guides [SQL Server]. creating
ms.assetid: e1ad78bb-4857-40ea-a0c6-dcf5c28aef2f
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 5f37f0189df126054626fdd4820368911b1fa5cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946965"
---
# <a name="create-a-new-plan-guide"></a>新しいプラン ガイドの作成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
プラン ガイドは、クエリ ヒントまたは固定クエリ プランをクエリにアタッチすることにより、クエリの最適化を促します。 プラン ガイドでは、最適化するステートメントと、使用するクエリ ヒントを含む OPTION 句 またはクエリの最適化に使用する特定のクエリ プランのいずれかを指定します。 クエリが実行されると、クエリ オプティマイザーにより [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがプラン ガイドと照合され、実行時にクエリに OPTION 句がアタッチされるか、指定されたクエリ プランが使用されます。  

プラン ガイドは固定クエリ プランまたはクエリ ヒントをクエリに適用します。
  
##  <a name="Restrictions"></a> 制限事項と制約事項  
-   sp_create_plan_guide の引数は、表示される順序で指定する必要があります。 **sp_create_plan_guide**のパラメーターに値を指定する場合、パラメーター名はすべて明示的に指定するか、すべて指定しないかのいずれかにする必要があります。 たとえば、 **@name =** を指定する場合は、 **@stmt =** 、 **@type =** なども指定する必要があります。 同様に、 **@name =** を省略してパラメーター値だけを指定する場合は、その他のパラメーター名も省略し、値だけを指定する必要があります。 引数の名前は、構文を理解しやすくするための説明目的のものです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、指定したパラメーター名と、その名前が使用されている位置にあるパラメーターの名前が一致しているかどうかは確認されません。  
  
-   同一のクエリとバッチまたはモジュールに対し、複数の OBJECT または SQL プラン ガイドを作成できます。 ただし、有効にできるプラン ガイドは常に 1 つだけです。  
  
-   @module_or_batch 値で参照するストアド プロシージャ、関数、または DML トリガーが、WITH ENCRYPTION 句を指定するものであるか一時的なものである場合、この値に対して OBJECT 型のプラン ガイドは作成できません。  
  
-   有効、無効にする場合のどちらでも、そのプラン ガイドで参照されている関数、ストアド プロシージャ、または DML トリガーを削除または変更しようとすると、エラーが発生します。 プラン ガイドで参照され、トリガーが定義されているテーブルを削除しようとする場合もエラーが発生します。  

##  <a name="Permissions"></a> Permissions  
 OBJECT 型のプラン ガイドを作成するには、参照先オブジェクトに対する ALTER 権限が必要です。 SQL または TEMPLATE タイプのプラン ガイドを作成するには、現在のデータベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SSMS を使用してプラン ガイドを作成する  
1.  プラス記号をクリックして、作成するプラン ガイドのあるデータベースを展開し、プラス記号をクリックして **[プログラミング]** フォルダーを展開します。  
  
2.  **[プラン ガイド]** フォルダーを右クリックし、 **[新しいプラン ガイド...]** をクリックします。 ![select_plan_guide](../../relational-databases/performance/media/select-plan-guide.png)
  
3.  **[新しいプラン ガイド]** ダイアログ ボックスの **[名前]** ボックスに、プラン ガイドの名前を入力します。  
  
4.  **[ステートメント]** ボックスに、プラン ガイドの適用対象の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを入力します。  
  
5.  **[スコープの種類]** ボックスの一覧で、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが存在するエンティティの種類を選択します。 これは [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントとプラン ガイドを照合するコンテキストを示します。 選択できる値は、 **OBJECT**、 **SQL**、および **TEMPLATE**です。  
  
6.  **[スコープのバッチ]** ボックスに、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを含むバッチ テキストを入力します。 バッチ テキストには、`USE`*database* ステートメントを含めることはできません。 **[スコープのバッチ]** ボックスは、スコープの種類として **[SQL]** を選択した場合にのみ利用できます。 スコープの種類が SQL であるとき、[スコープのバッチ] ボックスに何も入力しなかった場合、バッチ テキストの値は、 **[ステートメント]** ボックスと同じ値に設定されます。  
  
7.  **[スコープのスキーマ名]** ボックスに、対象のオブジェクトを含んでいるスキーマの名前を入力します。 **[スコープのスキーマ名]** ボックスは、スコープの種類として **[オブジェクト]** を選択した場合にのみ利用できます。  
  
8.  **[スコープのオブジェクト名]** ボックスに、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを含む [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャ、ユーザー定義スカラー関数、複数ステートメントのテーブル値関数、または DML トリガーの名前を入力します。 **[スコープのオブジェクト名]** ボックスは、スコープの種類として **[オブジェクト]** を選択した場合にのみ利用できます。  
  
9. **ステートメントに埋め込まれているすべてのパラメーターの名前とデータ型を** [パラメーター] [!INCLUDE[tsql](../../includes/tsql-md.md)] ボックスに入力します。  
  
   パラメーターは、次の条件のいずれかを満たす場合にのみ適用されます。  
  
   -   スコープの種類が **SQL** または **TEMPLATE**の場合。 **TEMPLATE**の場合、パラメーターを NULL にすることはできません。  
  
   -   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが sp_executesql を使用して送信され、パラメーターの値が指定されている場合、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が内部でステートメントをパラメーター化した後に送信する場合。  
  
10. **ステートメントに適用されるクエリ ヒントまたはクエリ プランを** [ヒント] [!INCLUDE[tsql](../../includes/tsql-md.md)] ボックスに入力します。 1 つまたは複数のクエリ ヒントを指定するには、有効な OPTION 句を入力します。  
  
11. **[OK]** をクリックします。  

![plan_guide](../../relational-databases/performance/media/plan-guide.png)  

##  <a name="TsqlProcedure"></a> T-SQL を使用してプラン ガイドを作成する  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```sql  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
  
    ```  

詳細については、「[sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)」を参照してください。  

  
