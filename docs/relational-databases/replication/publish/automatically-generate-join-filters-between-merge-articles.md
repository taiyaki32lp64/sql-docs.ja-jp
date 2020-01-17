---
title: 結合フィルターの自動生成 (マージ)
description: SQL Server Management Studio (SSMS) でマージ レプリケーションを実行するための [パブリケーションの新規作成ウィザード] の [テーブル行のフィルター選択] ページで一連の結合フィルターを自動的に生成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- automatic join filter generation
- join filters
ms.assetid: 7ef419f4-c17f-42a5-9068-174a3ec08941
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a8bc0ae6764d96b03088cb05eb72dc5ab4f3a0d6
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321285"
---
# <a name="automatically-generate-join-filters-between-merge-articles"></a>マージ アーティクル間の結合フィルターを自動的に生成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで、一連の結合フィルターが自動的に生成されます。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](../../../relational-databases/replication/publish/create-a-publication.md)」および「[View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
> [!NOTE]  
>  パブリケーションに対するサブスクリプションを初期化した後に、 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで一連の結合フィルターを自動的に生成した場合は、変更を行った後で、新しいスナップショットを生成し、すべてのサブスクリプションを再初期化する必要があります。 プロパティ変更の要件の詳細については、「[Change Publication and Article Properties](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) をご覧ください。  
  
 結合フィルターは、一連のテーブルに対して手動で作成できます。また、テーブルに定義された外部キーと主キーのリレーションシップに基づいてレプリケーションによって自動的に生成することもできます。 手動での結合フィルターの作成の詳細については、「[マージ アーティクル間の結合フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)」を参照してください。  
  
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
  
         複数のサブスクライバー間でのデータの共有方法に一致するオプションを選択します。 **[このテーブルの 1 行を複数のサブスクリプションに移動する]** または **[このテーブルの 1 行を 1 つのサブスクリプションのみに移動する]** 。 **[このテーブルの 1 行を 1 つのサブスクリプションのみに移動する]** を選択すると、マージ レプリケーションは、格納および処理するメタデータを減らすことにより、パフォーマンスを最適化できます。 ただし、データのパーティション分割によって、1 つの行が複数のサブスクライバーにレプリケートされないことを確認する必要があります。 詳細については、「 [パラメーター化された行フィルター](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」トピックの「[パーティションのオプション] の設定」をご覧ください。  
  
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
 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)   
 [パラメーター化された行フィルター](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
