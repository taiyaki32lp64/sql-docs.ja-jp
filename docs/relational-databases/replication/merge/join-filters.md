---
title: 結合フィルター | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], join
- publications [SQL Server replication], join filters
- merge replication join filters [SQL Server replication]
- join filters
ms.assetid: dd78fd8f-56e3-4582-9abd-6bc25c91e075
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 712665d24946c2826e4ab6c5e53bb853b07642b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033245"
---
# <a name="join-filters"></a>結合フィルター
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  結合フィルターを使用すると、パブリケーションにおける関連するテーブルのフィルター方法に基づいて、テーブルにフィルターを適用できます。 通常、親テーブルにはパラメーター化されたフィルターが使用されます。そのため、テーブル間の結合を定義する場合とほぼ同じ方法で 1 つ以上の結合フィルターを定義できます。 結合フィルターは、結合フィルター句に一致した場合のみ関連テーブルのデータがレプリケートされるように、パラメーター化されたフィルターを拡張します。  
  
 通常、結合フィルターは適用先のテーブルに定義されている主キー/外部キーのリレーションシップに従いますが、これに厳密に限定されてはいません。 結合フィルターには、2 つのテーブルの関連データを比較するためのあらゆるロジックを使用できます。  
  
 [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] サンプル データベースの次のテーブルを検討してみましょう。これらのテーブルは主キーと外部キーのリレーションシップによって関連付けられています。  
  
-   **HumanResources.Employee**  
  
-   **Sales.SalesOrderHeader**  
  
-   **Sales.SalesOrderDetail**  
  
 これらのテーブルは、移動営業部門を支援するアプリケーションで利用できます。ただし、 **HumanResources.Employee** テーブルの各営業担当者が担当顧客の注文に関連するデータのみを受け取れるように、これらのテーブルをフィルター選択する必要があります。  
  
 最初に、親テーブルに対してパラメーター化されたフィルターを定義します。この例では、 **HumanResources.Employee** が親テーブルになります。 このテーブルには **LoginID**列が含まれており、この列には各従業員のログインが *domain\login*形式で格納されています。 このテーブルにフィルターを適用して各従業員が関連データのみを受け取れるようにするには、パラメーター化されたフィルター句を次のように指定します。  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 このフィルターを指定すると、各従業員のサブスクリプションには、当該従業員に関連する **HumanResources.Employee** テーブルのデータのみ (この例では単一の行) が格納されます。 詳細については、「 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」を参照してください。  
  
 次の手順で、このフィルターを各関連テーブルに拡張します。フィルターの拡張に使用する構文は、2 つのテーブルの結合の指定に使用する構文とほぼ同じです。 最初の結合フィルター句を次のように指定します。  
  
```  
Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
```  
  
 この指定により、各営業担当者に関連する注文データのみがサブスクリプションに格納されます。 2 つ目の結合フィルター句を次のように指定します。  
  
```  
SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
```  
  
 この指定により、各営業担当者の注文データに関連する詳細データのみがサブスクリプションに格納されます。 この例では、各ポイントで単一のテーブルが結合されていますが、複数のテーブルを結合することもできます。  
  
 結合フィルターはパブリケーションの新規作成ウィザードと **[パブリケーションのプロパティ]** ダイアログ ボックスで 1 つずつ追加したり、プログラムを使用して追加することができます。 パブリケーションの新規作成ウィザードを使用して結合フィルターを自動的に生成することもできます。このウィザードでテーブルの行フィルターを指定すると、すべての関連テーブルに対して結合フィルターが適用されます。 詳細については、「[マージ アーティクル間の結合フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)」、「[Automatically Generate a Set of Join Filters Between Merge Articles &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/automatically-generate-join-filters-between-merge-articles.md)」 (マージ アーティクル間の一連の結合フィルターを自動的に生成する &#40;SQL Server Management Studio&#41;)、および「[Define an Article](../../../relational-databases/replication/publish/define-an-article.md)」 (アーティクルの定義) を参照してください。  
  
## <a name="optimizing-join-filter-performance"></a>結合フィルターのパフォーマンスの最適化  
 次のガイドラインに従うことにより、結合フィルターのパフォーマンスを最適化できます。  
  
-   結合フィルター階層のテーブル数を制限します。  
  
     結合フィルターを適用できるテーブル数に制限はありませんが、多数のテーブルにフィルターを適用すると、マージ処理中のパフォーマンスに大きく影響します。 テーブルが 5 つ以上の結合フィルターを生成する場合は、小さなテーブル、変更されないテーブル、プライマリ参照テーブルはフィルター選択しないという別の解決策を検討してください。 結合フィルターは、サブスクリプション間でパーティション分割する必要のあるテーブル間でのみ使用します。  
  
-   必要に応じて **join unique key** オプションを **True** に設定します。  
  
     親テーブルの結合列が一意の場合、特別なパフォーマンスの最適化機能をマージ処理で利用できます。 一意な列に基づいて結合条件が指定されている場合、結合フィルターの **join unique key** オプションを設定します。 このオプション設定の詳細については、前のセクションに示されている操作方法のトピックを参照してください。  
  
-   結合フィルターで参照される列にインデックスが作成されていることを確認します。  
  
     結合フィルターで参照される列にインデックスを作成すると、レプリケーションのフィルター処理がより効率的に実行されます。  
  
-   結合フィルターと同様の処理をする行フィルターは作成しないでください。  
  
     WHERE 句にサブクエリを使用すると、結合フィルターと同様の処理の行フィルターを次のように作成できます。  
  
    ```  
    WHERE Customer.SalesPersonID IN (SELECT EmployeeID FROM Employee WHERE LoginID = SUSER_SNAME())   
    ```  
  
     上記のようなロジックを使用する場合、サブクエリではなく結合フィルターを使用することを強くお勧めします。 アプリケーションでサブクエリを使用する行フィルターが必要な場合は、サブクエリが参照するデータが変更されない読み取り専用データであることを確認してください。  
  
## <a name="see-also"></a>参照  
 [マージ レプリケーション用にパブリッシュされたデータのフィルター選択](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [パラメーター化された行フィルター](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
