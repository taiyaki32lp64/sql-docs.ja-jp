---
title: マージ アーティクルのパラメーター化された行フィルターの定義および変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- parameterized filters [SQL Server replication], defining
- parameterized filters [SQL Server replication], modifying
- merge replication [SQL Server replication], dynamic filters
- merge replication parameterized filters [SQL Server replication]
- filters [SQL Server replication], parameterized
- modifying filters, parameterized row
- dynamic filters [SQL Server replication]
ms.assetid: de0482a2-3cc8-4030-8a4a-14364549ac9f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86a96f938a036edf39b3602278f9b6b6d2d46719
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68212116"
---
# <a name="define-and-modify-a-parameterized-row-filter-for-a-merge-article"></a>マージ アーティクルのパラメーター化された行フィルターの定義および変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、パラメーター化された行フィルターを定義および変更する方法について説明します。  
  
 テーブル アーティクルを作成する際には、パラメーター化された行フィルターを使用できます。 このフィルターでは [WHERE](/sql/t-sql/queries/where-transact-sql) 句を使用して、パブリッシュする適切なデータを選択します。 静的行フィルターのようにこの句でリテラル値を指定するのではなく、システム関数[SUSER_SNAME](/sql/t-sql/functions/suser-sname-transact-sql) および [HOST_NAME](/sql/t-sql/functions/host-name-transact-sql) のいずれかまたは両方を指定します。 詳しくは、「 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。  
  
 
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   パブリケーションに対するサブスクリプションが初期化された後に、パラメーター化された行フィルターを追加、変更、または削除した場合は、変更を行った後で、新しいスナップショットを生成し、すべてのサブスクリプションを再初期化する必要があります。 プロパティ変更の要件の詳細については、「[Change Publication and Article Properties](change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) をご覧ください。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   パラメーター化された行フィルター句では列名に関数を適用しないことをお勧めします。これは、 `LEFT([MyColumn]) = SUSER_SNAME()`のように指定すると、パフォーマンスに問題が生じるためです。 フィルター句で HOST_NAME を使用していて、HOST_NAME 値をオーバーライドする場合は、CONVERT を使用するデータ型の変換が必要になる可能性があります。 このようなケースの推奨事項の詳細については、「[Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)」の「HOST_NAME() 値のオーバーライド」をご覧ください。  
  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで、パラメーター化された行フィルターを定義、変更、または削除します。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](create-a-publication.md)」および「[View and Modify Publication Properties](view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
#### <a name="to-define-a-parameterized-row-filter"></a>パラメーター化された行フィルターを定義するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで、 **[追加]** をクリックし、次に **[フィルターの追加]** をクリックします。  
  
2.  **[フィルターの追加]** ダイアログ ボックスで、ドロップダウン リスト ボックスからフィルター選択するテーブルを選択します。  
  
3.  **[フィルター ステートメント]** テキスト ボックスで、フィルター ステートメントを作成します。 テキスト領域に直接入力することも、 **[列]** ボックスから列をドラッグ アンド ドロップすることもできます。  
  
    -   **[フィルター ステートメント]** テキスト領域には、次の形式の既定のテキストが表示されます。  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
    -   既定のテキストは変更できません。標準の SQL 構文を使用して WHERE キーワードの後にフィルター句を入力してください。 パラメーター化されたフィルターには、システム関数 `HOST_NAME()` および `SUSER_SNAME()` の呼び出し、あるいは、これらの関数のいずれかまたは両方を参照するユーザー定義関数の呼び出しが含まれています。 パラメーター化された行フィルターの完全なフィルター句の例を次に示します。  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         WHERE 句には、2 つの部分で構成されている名前を使用する必要があります。3 つまたは 4 つの部分で構成されている名前の使用はサポートされていません。  
  
4.  複数のサブスクライバー間でのデータの共有方法に一致するオプションを選択します。  
  
    -   **[このテーブルの 1 行を複数のサブスクリプションに移動する]**  
  
    -   **[このテーブルの 1 行を 1 つのサブスクリプションのみに移動する]**  
  
     **[このテーブルの 1 行を 1 つのサブスクリプションのみに移動する]** を選択すると、マージ レプリケーションは、格納および処理するメタデータを減らすことにより、パフォーマンスを最適化できます。 ただし、データのパーティション分割によって、1 つの行が複数のサブスクライバーにレプリケートされないことを確認する必要があります。 詳細については、「 [パラメーター化された行フィルター](../merge/parameterized-filters-parameterized-row-filters.md)」トピックの「[パーティションのオプション] の設定」をご覧ください。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  
  
#### <a name="to-modify-a-parameterized-row-filter"></a>パラメーター化された行フィルターを変更するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** の **[行のフィルター選択]** ページで、 **[フィルター選択されたテーブル]** ペイン内のフィルターを選択し、 **[編集]** をクリックします。  
  
2.  **[フィルターの編集]** ダイアログ ボックスで、フィルターを変更します。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-parameterized-row-filter"></a>パラメーター化された行フィルターを削除するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** の **[行のフィルター選択]** ページで、 **[フィルター選択されたテーブル]** ペイン内のフィルターを選択し、 **[削除]** をクリックします。  
  

  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 パラメーター化された行フィルターは、レプリケーション ストアド プロシージャを使用してプログラムから作成し、変更できます。  
  
#### <a name="to-define-a-parameterized-row-filter-for-an-article-in-a-merge-publication"></a>マージ パブリケーション内のアーティクルにパラメーター化された行フィルターを定義するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) を実行します。 **@publication** を指定し、アーティクルの名前を **@article** に、パブリッシュするテーブルを **@source_object** に、パラメーター化されたフィルターを定義する WHERE 句 (`WHERE` は含めません) を **@subset_filterclause** に指定します。 **@partition_options** に次のいずれかの値を指定します。これにより、パラメーター化された行フィルターによって行われるパーティション分割の種類が指定されます。  
  
    -   **0** - アーティクルのフィルター選択が静的であるか、各パーティションに対して一意なデータのサブセットは生成されません ("重複する" パーティション)。  
  
    -   **1** - 生成されるパーティションは重複しており、サブスクライバーでの更新によって行が属しているパーティションを変更することはできません。  
  
    -   **2** - アーティクルのフィルター選択によって重複しないパーティションが生成されますが、複数のサブスクライバーが同じパーティションを受け取ることができます。  
  
    -   **3** - アーティクルのフィルター選択によって、各サブスクリプションで一意な重複しないパーティションが生成されます。  
  
#### <a name="to-change-a-parameterized-row-filter-for-an-article-in-a-merge-publication"></a>マージ パブリケーション内のアーティクルに適用するパラメーター化された行フィルターを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)を実行します。 指定 **@publication** 、 **@article** 、@property`subset_filterclause`の **@property** 式のパラメーター化されたフィルターを定義します。 **@value** (は含まれません`WHERE`)、および値の**1**両方の **@force_invalidate_snapshot** と **@force_reinit_subscription** .  
  
2.  この変更によって別のパーティション分割が発生した場合、 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) を再び実行します。 指定 **@publication** 、 **@article** 、@property`partition_options`の **@property** 、およびの最も適切なパーティション分割オプション **@value** 次のいずれかを指定することができます。  
  
    -   **0** - アーティクルのフィルター選択が静的であるか、各パーティションに対して一意なデータのサブセットは生成されません ("重複する" パーティション)。  
  
    -   **1** - 生成されるパーティションは重複しており、サブスクライバーでの更新によって行が属しているパーティションを変更することはできません。  
  
    -   **2** - アーティクルのフィルター選択によって重複しないパーティションが生成されますが、複数のサブスクライバーが同じパーティションを受け取ることができます。  
  
    -   **3** - アーティクルのフィルター選択によって、各サブスクリプションで一意な重複しないパーティションが生成されます。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、 `Employee` テーブルに対して一連の結合フィルターを使用してアーティクルがフィルター選択されるマージ パブリケーションで、アーティクルのグループを定義します。このテーブル自体はパラメーター化された行フィルターを **LoginID** 列に使用してフィルター選択されています。 同期の間、[HOST_NAME](/sql/t-sql/functions/host-name-transact-sql) 関数により返される値はオーバーライドされます。 詳細については、「 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)」の「HOST_NAME() 値のオーバーライド」をご覧ください。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubdynamic1.sql#sp_mergedynamicpub1)]  
  
  
## <a name="see-also"></a>関連項目  
 [マージ アーティクル間の結合フィルターの定義および変更](define-and-modify-a-join-filter-between-merge-articles.md)   
 [パブリケーションとアーティクルのプロパティの変更](change-publication-and-article-properties.md)   
 [Join Filters](../merge/join-filters.md)   
 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)  
  
  
