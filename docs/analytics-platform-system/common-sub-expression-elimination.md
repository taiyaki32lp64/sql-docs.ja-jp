---
title: 共通部分式
description: Analytics Platform System CU 7.3 で導入されたクエリの改善の例を示します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 12/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: d05314f4d100e469c621d42a10ed89671b2bdd9c
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401334"
---
# <a name="common-subexpression-elimination-explained"></a>共通部分式の削除について説明します。

APS CU 7.3 では、SQL クエリオプティマイザーにおける共通部分式の削除によって、クエリのパフォーマンスが向上します。 改善により、2つの方法でクエリが向上します。 1つ目の利点は、このような式を特定して削除することで、SQL のコンパイル時間を短縮できることです。 2つ目の重要な利点は、これらの冗長な部分式に対するデータ移動操作が不要になるため、クエリの実行時間が短縮されます。

```sql
select top 100 asceding.rnk, i1.i_product_name best_performing, i2.i_product_name worst_performing
  from(select *
       from (select item_sk,rank() over (order by rank_col asc) rnk
             from (select ss_item_sk item_sk,avg(ss_net_profit) rank_col
                   from store_sales ss1
                   where ss_store_sk = 8
                   group by ss_item_sk
                   having avg(ss_net_profit) > 0.9*(select avg(ss_net_profit) rank_col
                                                    from store_sales
                                                    where ss_store_sk = 8
                                                      and ss_hdemo_sk is null
                                                    group by ss_store_sk))V1)V11
       where rnk  < 11) asceding,
      (select *
       from (select item_sk,rank() over (order by rank_col desc) rnk
             from (select ss_item_sk item_sk,avg(ss_net_profit) rank_col
                   from store_sales ss1
                   where ss_store_sk = 8
                   group by ss_item_sk
                   having avg(ss_net_profit) > 0.9*(select avg(ss_net_profit) rank_col
                                                    from store_sales
                                                    where ss_store_sk = 8
                                                      and ss_hdemo_sk is null
                                                    group by ss_store_sk))V2)V21
       where rnk  < 11) descending,
  item i1,
  item i2
  where asceding.rnk = descending.rnk
    and i1.i_item_sk=asceding.item_sk
    and i2.i_item_sk=descending.item_sk
  order by asceding.rnk
  ;
```
前述の TPC-DS ベンチマークツールからのクエリを考えてみましょう。  上記のクエリでは、サブクエリは同じですが、rank () over 関数を使用した order by 句は、2つの異なる方法で並べ替えられています。 CU 7.3 以前では、このサブクエリは2回評価されて実行されます。1回は昇順で、1回は降順で、2つのデータ移動操作を行います。 APS CU 7.3 をインストールすると、サブクエリの部分が1回評価されるため、データの移動が減少し、クエリの処理が速くなります。

APS CU 7.3 にアップグレードした後でも機能をテストできるようにする "OptimizeCommonSubExpressions" という[機能スイッチ](appliance-feature-switch.md)が導入されました。 この機能は既定でオンになっていますが、無効にすることができます。 

> [!NOTE] 
> 機能スイッチの値を変更するには、サービスを再起動する必要があります。

サンプルクエリを試すには、テスト環境で次のテーブルを作成し、前述のクエリのプランの説明を評価します。 

```sql
CREATE TABLE [dbo].[store_sales] (
    [ss_sold_date_sk] int NULL, 
    [ss_sold_time_sk] int NULL, 
    [ss_item_sk] int NOT NULL, 
    [ss_customer_sk] int NULL, 
    [ss_cdemo_sk] int NULL, 
    [ss_hdemo_sk] int NULL, 
    [ss_addr_sk] int NULL, 
    [ss_store_sk] int NULL, 
    [ss_promo_sk] int NULL, 
    [ss_ticket_number] int NOT NULL, 
    [ss_quantity] int NULL, 
    [ss_wholesale_cost] decimal(7, 2) NULL, 
    [ss_list_price] decimal(7, 2) NULL, 
    [ss_sales_price] decimal(7, 2) NULL, 
    [ss_ext_discount_amt] decimal(7, 2) NULL, 
    [ss_ext_sales_price] decimal(7, 2) NULL, 
    [ss_ext_wholesale_cost] decimal(7, 2) NULL, 
    [ss_ext_list_price] decimal(7, 2) NULL, 
    [ss_ext_tax] decimal(7, 2) NULL, 
    [ss_coupon_amt] decimal(7, 2) NULL, 
    [ss_net_paid] decimal(7, 2) NULL, 
    [ss_net_paid_inc_tax] decimal(7, 2) NULL, 
    [ss_net_profit] decimal(7, 2) NULL
)
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([ss_item_sk]),  PARTITION ([ss_sold_date_sk] RANGE RIGHT FOR VALUES (2450815, 2451180, 2451545, 2451911, 2452276, 2452641, 2453006)));

CREATE TABLE [dbo].[item] (
    [i_item_sk] int NOT NULL, 
    [i_item_id] char(16) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, 
    [i_rec_start_date] date NULL, 
    [i_rec_end_date] date NULL, 
    [i_item_desc] varchar(200) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_current_price] decimal(7, 2) NULL, 
    [i_wholesale_cost] decimal(7, 2) NULL, 
    [i_brand_id] int NULL, 
    [i_brand] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_class_id] int NULL, 
    [i_class] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_category_id] int NULL, 
    [i_category] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_manufact_id] int NULL, 
    [i_manufact] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_size] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_formulation] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_color] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_units] char(10) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_container] char(10) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_manager_id] int NULL, 
    [i_product_name] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL
)
WITH (CLUSTERED INDEX ( [i_item_sk] ASC ), DISTRIBUTION = REPLICATE);
```
クエリの [プランの説明] を見ると、CU 7.3 より前 (または機能スイッチがオフになっている場合) に、クエリの合計操作数が17に達した後 (または機能スイッチがオンになっている場合)、同じクエリによって合計で9個の操作が表示されていることがわかります。 データ移動操作をカウントするだけの場合は、前のプランの移動操作が4回、新しいプランに2つの移動操作があることがわかります。 新しいクエリオプティマイザーでは、新しいプランで既に作成した一時テーブルを再利用することで、2つのデータ移動操作を減らすことができました。これにより、クエリの実行時間が短縮されました。 


