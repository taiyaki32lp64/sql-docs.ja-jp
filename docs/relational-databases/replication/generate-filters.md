---
title: '[フィルターの生成] | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.generatefilters.f1
ms.assetid: be28515c-5d6d-467b-b933-d7c8d97a45b4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 79ca361c5f330196c4363441f573732e5ff15b6a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72905040"
---
# <a name="generate-filters"></a>[フィルターの生成]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[フィルターの生成]** ダイアログ ボックスでは、マージ パブリケーション内の 1 つのテーブルに対して行フィルターを定義できます。これを行うと、レプリケーションによって、外部キー リレーションシップを介して関連付けられる他のテーブルにそのフィルターが自動的に拡張されます。 たとえば、フランスの顧客データのみを含むように、フィルターを顧客テーブルに定義した場合、レプリケーションによってこのフィルターが拡張され、関連する受注テーブルや受注詳細テーブルには、フランスの顧客に関連する情報のみが含まれることになります。  
  
## <a name="options"></a>オプション  
 このダイアログ ボックスには、テーブルに行フィルターを作成するための 3 段階のプロセスがあります。 主キーと外部キーのリレーションシップを通じて、フィルターされたテーブルと関連するテーブルにフィルターが拡張されます。 たとえば、3 つのテーブル、 **Customer**、 **SalesOrderHeader**、および **SalesOrderDetail**に、 **Customer** と **SalesOrderHeader**のリレーションシップおよび **SalesOrderHeader** と **SalesOrderDetail**のリレーションシップが与えられている場合、 **Customer**に行フィルターを適用すると、レプリケーションによってこのフィルターが **SalesOrderHeader** と **SalesOrderDetail**に拡張されます。  
  
1.  **[フィルターを適用するテーブルを選択します。]**  
  
     ドロップダウン リスト ボックスからテーブルを選択します。 テーブルは、 **[アーティクル]** ページで選択されている場合のみ、このリスト ボックスに表示されます。  
  
2.  **[フィルター ステートメントを完成させ、サブスクライバーが受け取るテーブル行を指定します。]**  
  
     新しいフィルター ステートメントを定義します。 **[列]** リスト ボックスには、 **[フィルターを適用するテーブルを選択します。]** で選択したテーブルからパブリッシュするすべての列が一覧表示されます。 **[フィルター ステートメント]** テキスト領域には、次の形式の既定のテキストが表示されます。  
  
     `SELECT <published_columns> FROM [tableowner].[tablename] WHERE`  
  
     このテキストは変更できません。標準の [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文を使用して、WHERE キーワードの後にフィルター句を入力します。  
  
    > [!IMPORTANT]  
    >  パラメーター化された行フィルター句では列名に関数を適用しないことをお勧めします。これは、 `LEFT([MyColumn]) = SUSER_SNAME()`のように指定すると、パフォーマンスに問題が生じるためです。 フィルター句で HOST_NAME を使用していて、HOST_NAME 値をオーバーライドする場合は、CONVERT を使用するデータ型の変換が必要になる可能性があります。 このようなケースの推奨事項の詳細については、「[Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」の「HOST_NAME() 値のオーバーライド」をご覧ください。  
  
3.  **[このテーブルからデータを取得するサブスクリプションの数を指定します。]**  

     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみ。 マージ レプリケーションを使用して、お使いのデータとアプリケーションに最適なパーティションの種類を指定できます。 **[このテーブルの 1 行を 1 つのサブスクリプションのみに移動する]** を選択すると、マージ レプリケーションでは、重複しないパーティションのオプションが設定されます。 重複しないパーティションを事前計算済みパーティションと共に使用することで、パフォーマンスが向上します。事前計算済みパーティションに関連するアップロードの負担が、重複しないパーティションによって最小限に抑えられるためです。 重複しないパーティションのパフォーマンス上の利点は、使用するパラメーター化されたフィルターと結合フィルターが複雑になるほど明確になります。 このオプションを選択する場合は、データのパーティション分割によって、1 つの行が複数のサブスクライバーにレプリケートされないことを確認する必要があります。 詳細については、「 [パラメーター化された行フィルター](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」トピックの「[パーティションのオプション] の設定」をご覧ください。  
  
 フィルターを追加した後で、 **[OK]** をクリックして終了し、ダイアログ ボックスを閉じます。 指定したフィルターは、SELECT 句のテーブルに対して解析され、実行されます。 フィルター ステートメントに構文エラーなどの問題がある場合には通知され、フィルター ステートメントを編集することができます。  
  
 ステートメントが解析された後で、レプリケーションによって必要な結合フィルターが作成されます。 このウィザードが実行されているパブリッシャーにディストリビューターを構成していない場合、ディストリビューターを構成するように要求されます。  
  
## <a name="see-also"></a>参照  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [パブリッシュされたデータのフィルター選択](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
