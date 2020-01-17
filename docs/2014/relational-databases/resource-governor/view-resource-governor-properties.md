---
title: リソース ガバナーのプロパティの表示 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.rg.properties.f1
helpviewer_keywords:
- Resource Governor, properties
ms.assetid: de3510df-f792-4a9d-80fa-f198fd36cdc8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 35d4720a8fe8b8c1b404a97e27b36896f36dd5f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209682"
---
# <a name="view-resource-governor-properties"></a>View Resource Governor Properties
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の [リソース ガバナーのプロパティ] ページを使用して、リソース プールやワークロード グループなどのリソース ガバナー エンティティを作成または構成できます。  
  
1.  **作業を開始する準備:** [アクセス許可](#Permissions)  
  
2.  **使用して、リソース ガバナーのプロパティを表示するには。** [リソース ガバナーのプロパティ ページ](#ViewRGProp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 **[リソース ガバナーのプロパティ]** ページでは、リソース ガバナー エンティティのプロパティを表示する以外に、さまざまな構成タスクを実行できます。 詳細については、次のトピックをご覧ください。  
  
-   [リソース ガバナーの有効化](enable-resource-governor.md)  
  
-   [リソース ガバナーを無効にしたとき](disable-resource-governor.md)  
  
-   [リソース プールの作成](create-a-resource-pool.md)  
  
-   [ワークロード グループの作成](create-a-workload-group.md)  
  
-   [リソース プールの設定の変更](change-resource-pool-settings.md)  
  
-   [ワークロード グループの設定の変更](change-workload-group-settings.md)  
  
-   [ワークロード グループの移動](move-a-workload-group.md)  
  
 ワークロード グループまたはリソース プールを追加、削除、または移動してから **[OK]** をクリックすると、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントが実行されます。  
  
 リソース プールまたはワークロード グループの作成操作または再構成操作が失敗した場合は、プロパティ ページのタイトルの下に簡単なエラー メッセージが表示されます。 詳細なエラー メッセージを表示するには、エラー メッセージの下矢印をクリックします。  
  
 [sys.dm_resource_governor_configuration](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql) 動的管理ビューにクエリを実行して is_configuration_pending の現在の状態を取得することにより、構成が保留中かどうかを確認できます。  
  
###  <a name="Permissions"></a> Permissions  
 リソース ガバナーのプロパティを表示するには、VIEW SERVER STATER 権限が必要です。 リソース ガバナーの構成タスクを行うには、CONTROL SERVER 権限が必要です。  
  
##  <a name="ViewRGProp"></a> リソース ガバナーのプロパティ ページを表示します。  
 **で、次の [リソース ガバナーのプロパティ] ページでリソース ガバナーのプロパティを表示するには [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でオブジェクト エクスプローラーを開き、 **[管理]** ノードを **[リソース ガバナー]** ノードまで再帰的に展開します。  
  
2.  **[リソース ガバナー]** を右クリックし、 **[プロパティ]** をクリックすると、 **[リソース ガバナーのプロパティ]** ページが開きます。  
  
3.  このページのフィールドの詳細については、「 [リソース ガバナー プロパティ](#RGProp)」を参照してください。  
  
4.  変更を保存するには、 **[OK]** をクリックします。  
  
##  <a name="RGProp"></a> リソース ガバナーのプロパティ  
 **[分類子関数の名前]**  
 分類子関数を一覧から選択して指定します。  
  
 **リソース ガバナーの有効化**  
 チェック ボックスをオンまたはオフにしてリソース ガバナーを有効または無効にします。  
  
 **[リソース プール]**  
 提供されるグリッドを使用して、リソース プール構成を作成または変更します。 このグリッドには、あらかじめ定義されている内部プールおよび既定プールの情報が設定されています。 プールの行の最初の列をクリックして、使用するプールを選択します。 新しいリソース プールを作成するには、先頭にアスタリスク ( **&#42;** ) が付いている行をクリックします。  
  
 **名前**  
 リソース プールの名前を指定します。  
  
 **[最小 CPU %]**  
 CPU の競合がある場合に、リソース プールのすべての要求に保証される平均 CPU 帯域幅を指定します。 範囲は 0 から 100 です。  
  
 **[最大 CPU %]**  
 CPU の競合がある場合に、このリソース プールのすべての要求に割り当てられる最大平均 CPU 帯域幅を指定します。 範囲は 0 から 100 です。 既定の設定は 100 です。  
  
 **[最小メモリ %]**  
 このリソース プール用に確保され、他のリソース プールとは共有できないメモリ量の最小値を指定します。 範囲は 0 から 100 です。  
  
 **[最大メモリ %]**  
 このリソース プールの要求で使用できる合計サーバー メモリを指定します。 範囲は 0 から 100 です。 既定の設定は 100 です。  
  
 詳細については、次を参照してください。 [CREATE RESOURCE POOL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)します。  
  
 **[リソース プールのワークロード グループ]**  
 提供されるグリッドを使用して、ワークロード グループ構成を作成または変更します。 このグリッドには、あらかじめ定義されている内部グループおよび既定グループの情報が設定されています。 グループの行の最初の列をクリックして、使用するグループを選択します。 新しいワークロード グループを作成するには、先頭にアスタリスク ( **&#42;** ) が付いている行をクリックします。  
  
 **名前**  
 ワークロード グループの名前を指定します。  
  
 **重要度**  
 ワークロード グループでの要求の相対的な重要度を指定します。 使用可能な設定は [低]、[中]、および [高] です。  
  
 **[最大要求数]**  
 ワークロード グループで実行を許可する同時要求の最大数を指定します。 0 または正の整数を指定する必要があります。  
  
 **[CPU 時間 (秒)]**  
 要求が使用できる最大 CPU 時間を指定します。 0 または正の整数を指定する必要があります。 0 を指定すると、時間は無制限になります。  
  
 **[メモリ許可 (%)]**  
 1 つの要求にプールから割り当てられる最大メモリ容量を指定します。 範囲は 0 から 100 です。  
  
 **[許可のタイムアウト (秒)]**  
 クエリが失敗する前に、リソースが使用可能になるのをそのクエリが待機できる最大時間を指定します。 0 または正の整数を指定する必要があります。  
  
 **並列処理の次数**  
 並列要求の最大 DOP (並列処理の次数) を指定します。 範囲は 0 ～ 64 です。  
  
 詳細については、「[CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql)」を参照してください。  
  
## <a name="view-resource-governor-properties-by-using-transact-sql"></a>TRANSACT-SQL を使用してビューのリソース ガバナーのプロパティ  
 **Transact-SQL を使用してリソース ガバナーのプロパティを表示する**  
  
1.  リソース ガバナー エンティティの定義を表示するには、「[リソース ガバナーのカタログ ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql)」を使用します。  
  
2.  リソース ガバナー エンティティの現在の構成を表示するには、「[リソース ガバナー関連の動的管理ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql)」を使用します。  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](resource-governor.md)   
 [リソース ガバナーの有効化](enable-resource-governor.md)   
 [リソース ガバナー リソース プール](resource-governor-resource-pool.md)   
 [リソース ガバナー ワークロード グループ](resource-governor-workload-group.md)   
 [リソース ガバナーの分類子関数](resource-governor-classifier-function.md)  
  
  
