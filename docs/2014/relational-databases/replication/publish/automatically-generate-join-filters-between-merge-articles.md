---
title: (SQL Server Management Studio) のマージ アーティクル間の結合フィルターのセットを自動的に生成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- automatic join filter generation
- join filters
ms.assetid: 7ef419f4-c17f-42a5-9068-174a3ec08941
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66c32615b3fd9f417eab27f156b2645c2c89593b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63020973"
---
# <a name="automatically-generate-a-set-of-join-filters-between-merge-articles-sql-server-management-studio"></a>マージ アーティクル間の一連の結合フィルターを自動的に生成する (SQL Server Management Studio)
  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで、一連の結合フィルターが自動的に生成されます。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](create-a-publication.md)」および「[View and Modify Publication Properties](view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
> [!NOTE]  
>  パブリケーションに対するサブスクリプションを初期化した後に、 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで一連の結合フィルターを自動的に生成した場合は、変更を行った後で、新しいスナップショットを生成し、すべてのサブスクリプションを再初期化する必要があります。 プロパティ変更の要件の詳細については、「[パブリケーションおよびアーティクルのプロパティの変更](change-publication-and-article-properties.md)」を参照してください。  
  
 結合フィルターは、一連のテーブルに対して手動で作成できます。また、テーブルに定義された外部キーと主キーのリレーションシップに基づいてレプリケーションによって自動的に生成することもできます。 手動での結合フィルターの作成の詳細については、「[マージ アーティクル間の結合フィルターの定義および変更](define-and-modify-a-join-filter-between-merge-articles.md)」を参照してください。  
  
### <a name="to-automatically-generate-a-set-of-join-filters-between-merge-articles"></a>マージ アーティクル間の一連の結合フィルターを自動的に生成するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで、 **[追加]** をクリックし、次に **[フィルターを自動的に生成]** をクリックします。  
  
    > [!NOTE]  
    >  フィルターを自動的に生成すると、現在パブリケーション内にある行フィルターまたは結合フィルターがすべて削除されます。 一連のフィルターを自動的に生成した後でフィルターを追加できます。  
  
2.  **[フィルターの生成]** ダイアログ ボックスの処理に従って行フィルターを作成します。 次に、主キーと外部キーのリレーションシップによって、フィルター選択されるテーブルに関係する各テーブルに行フィルターが拡張されます。  
  
    1.  ドロップダウン リスト ボックスからフィルター選択するテーブルを選択します。  
  
    2.  **[フィルター ステートメント]** テキスト ボックスで、フィルター ステートメントを作成します。 テキスト領域に直接入力することも、 **[列]** ボックスから列をドラッグ アンド ドロップすることもできます。  
  
         **[フィルター ステートメント]** テキスト領域には、次の形式の既定のテキストが表示されます。  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
         既定のテキストは変更できません。静的行フィルターのフィルター句を入力するか、標準の SQL 構文を使用して WHERE キーワードの後にパラメーター化された行フィルターを入力してください。 パラメーター化された行フィルターの完全なフィルター句は次のようになります。  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         WHERE 句には、2 つの部分で構成されている名前を使用する必要があります。3 つまたは 4 つの部分で構成されている名前の使用はサポートされていません。  
  
    3.  フィルター オプションを指定します。  
  
         複数のサブスクライバー間でのデータの共有方法に一致するオプションを選択します。**このテーブルから行を複数のサブスクリプションに移動する**または**このテーブルから行を 1 つのサブスクリプションに移動する**します。 **[このテーブルの 1 行を 1 つのサブスクリプションのみに移動する]** を選択すると、マージ レプリケーションは、格納および処理するメタデータを減らすことにより、パフォーマンスを最適化できます。 ただし、データのパーティション分割によって、1 つの行が複数のサブスクライバーにレプリケートされないことを確認する必要があります。 詳細については、「 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)」トピックの「[パーティションのオプション] の設定」をご覧ください。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     指定したフィルターは、SELECT 句のテーブルに対して解析され、実行されます。 フィルター ステートメントに構文エラーなどの問題がある場合には通知され、フィルター ステートメントを編集することができます。  
  
     ステートメントの解析が終了すると、レプリケーションによって必要な結合フィルターが作成され、 **[テーブル行のフィルター選択]** ページ、または **[行のフィルター選択]** ページの **[フィルター選択されたテーブル]** ペインに表示されます。 パブリケーションの新規作成ウィザードでフィルターを生成し、このウィザードの実行対象であるパブリッシャーのディストリビューターをまだ構成していない場合は、構成するように要求されます。  
  
4.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  
  
### <a name="to-modify-a-filter-that-was-automatically-generated"></a>自動的に生成されたフィルターを変更するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** の **[行のフィルター選択]** ページで、 **[フィルター選択されたテーブル]** ペイン内のフィルターを選択し、 **[編集]** をクリックします。  
  
2.  **[フィルターの編集]** または **[結合の編集]** ダイアログ ボックスでフィルターを変更します。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-filter-that-was-automatically-generated"></a>自動的に生成されたフィルターを削除するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** の **[行のフィルター選択]** ページで、 **[フィルター選択されたテーブル]** ペイン内のフィルターを選択し、 **[削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Join Filters](../merge/join-filters.md)   
 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)  
  
  
