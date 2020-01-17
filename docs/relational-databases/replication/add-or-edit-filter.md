---
title: フィルターの追加または編集 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.addeditfilter.f1
ms.assetid: bdd7c71d-1c59-4044-bfe8-c85f908345bb
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 21d23387b3d17f54cbd6cfed3398cf5a0e8cffe6
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770798"
---
# <a name="add-or-edit-filter"></a>フィルターの追加または編集
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[フィルターの追加]** ダイアログ ボックスと **[フィルターの編集]** ダイアログ ボックスを使用すると、静的行フィルターおよびパラメーター化された行フィルターを追加したり編集したりできます。  
  
> [!NOTE]  
>  既存のパブリケーション内のフィルターを編集するには、パブリケーション用の新しいスナップショットが必要です。 パブリケーションにサブスクリプションがある場合は、サブスクリプションを再度初期化する必要があります。 プロパティ変更の詳細については、「[パブリケーションおよびアーティクルのプロパティの変更](../../relational-databases/replication/publish/change-publication-and-article-properties.md)」を参照してください。  
  
 すべての種類のパブリケーションに静的フィルターを含めることができ、マージ パブリケーションにはパラメーター化されたフィルターも含めることができます。 静的フィルターは、パブリケーションが作成されたときに評価されます。パブリケーションに対するすべてのサブスクライバーは、同じデータを受け取ります。 パラメーター化されたフィルターは、レプリケーションの同期中に評価されます。サブスクライバーごとのログインまたはコンピューター名に基づいて、異なるサブスクライバーが異なるデータのパーティションを受け取ることができます。 ダイアログ ボックスの **[サンプル ステートメント]** リンクをクリックして、フィルターの種類ごとのサンプルを参照します。 フィルター オプションの詳細については、「[パブリッシュされたデータのフィルター処理](../../relational-databases/replication/publish/filter-published-data.md)」を参照してください。  
  
 行フィルターを使用すれば、テーブルからパブリッシュの対象となる行のサブセットを指定できます。 行フィルターを使用して、ユーザーにとって必要のない行 (機密性の高い情報など) を削除したり、さまざまなサブスクライバーに送られるさまざまなデータのパーティションを作成したりできます。 さまざまなデータのパーティションをさまざまなサブスクライバーにパブリッシュすると、複数のサブスクライバーが同じデータを更新することによって発生する可能性のある競合を回避するためにも役立ちます。  
  
## <a name="options"></a>オプション  
 このダイアログ ボックスには、トランザクション パブリケーションとスナップショット アプリケーション用の 2 段階のプロセスと、マージ パブリケーション用の 3 段階のプロセスがあります。 すべての種類のパブリケーションで、フィルター対象のテーブルと、フィルターに含む 1 つまたは複数の列を選択する必要があります。フィルターは、標準の WHERE 句として定義されます。  
  
1.  **[フィルターを適用するテーブルを選択します。]**  
  
     既存のフィルターを編集している場合は、テーブルの選択は変更できません。 新しいフィルターを追加している場合は、ドロップダウン リスト ボックスから、テーブルを選択します。 テーブルは、 **[アーティクル]** ページでテーブルが選択されていて、まだ行フィルターを持たない場合にのみ、リスト ボックスに表示されます。 テーブルに行フィルターがあり、新しいフィルターを定義する場合は、次の手順に従います。  
  
    1.  **[フィルターの追加]** ダイアログ ボックスで **[キャンセル]** をクリックします。  
  
    2.  **[テーブル行のフィルター選択]** ページのフィルター ペインでテーブルを選択し、 **[編集]** をクリックします。  
  
    3.  **[フィルターの編集]** ダイアログ ボックスの既存のフィルターを編集します。  
  
2.  **[フィルター ステートメントを完成させ、サブスクライバーが受け取るテーブル行を指定します。]**  
  
     新しいフィルター ステートメントを定義するか、既存のステートメントを編集します。 **[列]** リスト ボックスには、 **[フィルターを適用するテーブルを選択します。]** で選択したテーブルからパブリッシュするすべての列が一覧表示されます。 **[フィルター ステートメント]** テキスト領域には、次の形式の既定のテキストが表示されます。  
  
     `SELECT <published_columns> FROM [schema].[tablename] WHERE`  
  
     このテキストは変更できません。標準の [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文を使用して、WHERE キーワードの後にフィルター句を入力します。 パブリッシャーが Oracle パブリッシャーの場合は、WHERE 句は Oracle クエリ構文に準拠する必要があります。 可能であれば、複雑なフィルターの使用は避けます。 静的フィルターとパラメーター化されたフィルターは、両方ともパブリケーションの処理時間を増加させます。したがって、フィルター ステートメントは可能な限り簡潔にしてください。  
  
    > [!IMPORTANT]  
    >  パフォーマンスの理由により、マージ パブリケーションの場合は、パラメーター化された行フィルター句の列名に、 `LEFT([MyColumn]) = SUSER_SNAME()`などの関数を適用しないことをお勧めします。 フィルター句で HOST_NAME を使用していて、HOST_NAME 値をオーバーライドする場合は、CONVERT を使用するデータ型の変換が必要になる可能性があります。 このようなケースの推奨事項の詳細については、「[Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」の「HOST_NAME() 値のオーバーライド」をご覧ください。  
  
3.  **[このテーブルからデータを取得するサブスクリプションの数を指定します。]**  
  
     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみで、マージ レプリケーションのみです。 マージ レプリケーションを使用して、お使いのデータとアプリケーションに最適なパーティションの種類を指定できます。 **[このテーブルの 1 行を 1 つのサブスクリプションのみに移動する]** を選択すると、マージ レプリケーションでは、重複しないパーティションのオプションが設定されます。 重複しないパーティションを事前計算済みパーティションと共に使用することで、パフォーマンスが向上します。事前計算済みパーティションに関連するアップロードの負担が、重複しないパーティションによって最小限に抑えられるためです。 重複しないパーティションのパフォーマンス上の利点は、使用するパラメーター化されたフィルターと結合フィルターが複雑になるほど明確になります。 このオプションを選択する場合は、データのパーティション分割によって、1 つの行が複数のサブスクライバーにレプリケートされないことを確認する必要があります。 詳細については、「 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」トピックの「[パーティションのオプション] の設定」をご覧ください。  
  
 フィルターを追加または編集した後に、 **[OK]** をクリックして変更を保存し、ダイアログ ボックスを閉じます。 指定したフィルターは、SELECT 句のテーブルに対して解析され、実行されます。 フィルター ステートメントに構文エラーが含まれるか、他の問題がある場合は、通知されるため、フィルター ステートメントを編集することができます。  
  
## <a name="see-also"></a>参照  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [パブリッシュされたデータのフィルター選択](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
