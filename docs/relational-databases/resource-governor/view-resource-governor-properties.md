---
title: リソース ガバナーのプロパティの表示 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.rg.properties.f1
helpviewer_keywords:
- Resource Governor, properties
ms.assetid: de3510df-f792-4a9d-80fa-f198fd36cdc8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 2250030405a0c6bb2512e3b8446cb76e11a7080e
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72903910"
---
# <a name="view-resource-governor-properties"></a>View Resource Governor Properties
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の [リソース ガバナーのプロパティ] ページを使用して、リソース プールやワークロード グループなどのリソース ガバナー エンティティを作成または構成できます。  
  
 ##  <a name="BeforeYouBegin"></a> 関連トピック 
 **[リソース ガバナーのプロパティ]** ページでは、リソース ガバナー エンティティのプロパティを表示する以外に、さまざまな構成タスクを実行できます。 詳細については、次のトピックをご覧ください。  
  
-   [リソース ガバナーの有効化](../../relational-databases/resource-governor/enable-resource-governor.md)  
  
-   [リソース ガバナーを無効にしたとき](../../relational-databases/resource-governor/disable-resource-governor.md)  
  
-   [リソース プールの作成](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
-   [ワークロード グループの作成](../../relational-databases/resource-governor/create-a-workload-group.md)  
  
-   [リソース プールの設定の変更](../../relational-databases/resource-governor/change-resource-pool-settings.md)  
  
-   [ワークロード グループの設定の変更](../../relational-databases/resource-governor/change-workload-group-settings.md)  
  
-   [ワークロード グループの移動](../../relational-databases/resource-governor/move-a-workload-group.md)  
  
 ワークロード グループまたはリソース プールを追加、削除、または移動してから **[OK]** をクリックすると、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントが実行されます。  
  
 リソース プールまたはワークロード グループの作成操作または再構成操作が失敗した場合は、プロパティ ページのタイトルの下に簡単なエラー メッセージが表示されます。 詳細なエラー メッセージを表示するには、エラー メッセージの下矢印をクリックします。  
  
 [sys.dm_resource_governor_configuration](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md) 動的管理ビューにクエリを実行して is_configuration_pending の現在の状態を取得することにより、構成が保留中かどうかを確認できます。  
  
##  <a name="Permissions"></a> Permissions  
 リソース ガバナーのプロパティを表示するには、VIEW SERVER STATER 権限が必要です。 リソース ガバナーの構成タスクを行うには、CONTROL SERVER 権限が必要です。  
  
##  <a name="ViewRGProp"></a> [リソース ガバナーのプロパティ] ページ  
 **で、次の [リソース ガバナーのプロパティ] ページでリソース ガバナーのプロパティを表示するには [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でオブジェクト エクスプローラーを開き、 **[管理]** ノードを **[リソース ガバナー]** ノードまで再帰的に展開します。  
  
2.  **[リソース ガバナー]** を右クリックし、 **[プロパティ]** をクリックすると、 **[リソース ガバナーのプロパティ]** ページが開きます。  
  
3.  このページのフィールドの詳細については、「 [リソース ガバナー プロパティ](#RGProp)」を参照してください。  
  
4.  変更を保存するには、 **[OK]** をクリックします。  

##  <a name="RGProp"></a> Resource Governor properties  
 **[分類子関数の名前]**  
 分類子関数を一覧から選択して指定します。  
  
 **リソース ガバナーの有効化**  
 チェック ボックスをオンまたはオフにしてリソース ガバナーを有効または無効にします。  
  
 **[リソース プール]**  
 提供されるグリッドを使用して、リソース プールおよび外部リソース プールの構成を作成または変更します。 このグリッドには、あらかじめ定義されている内部プールおよび既定プールの情報が設定されています。 プールの行の最初の列をクリックして、使用するプールを選択します。 新しいリソース プールを作成するには、先頭にアスタリスク ( **&#42;** ) が付いている行をクリックします。  
  
 **[名前]**  
 リソース プールの名前を指定します。  
  
 **[最小 CPU %]**  
 CPU の競合がある場合に、リソース プールのすべての要求に保証される平均 CPU 帯域幅を指定します。 範囲は 0 から 100 です。  
  
 **[最大 CPU %]**  
 CPU の競合がある場合に、このリソース プールのすべての要求に割り当てられる最大平均 CPU 帯域幅を指定します。 範囲は 0 から 100 です。 既定の設定は 100 です。  
  
 **[最小メモリ %]**  
 このリソース プール用に確保され、他のリソース プールとは共有できないメモリ量の最小値を指定します。 範囲は 0 から 100 です。  
  
 **[最大メモリ %]**  
 このリソース プールの要求で使用できる合計サーバー メモリを指定します。 範囲は 0 から 100 です。 既定の設定は 100 です。  
  
 詳細については、「[CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)」および「[CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)」を参照してください。  
  
 **[リソース プールのワークロード グループ]**  
 提供されるグリッドを使用して、ワークロード グループ構成を作成または変更します。 このグリッドには、あらかじめ定義されている内部グループおよび既定グループの情報が設定されています。 グループの行の最初の列をクリックして、使用するグループを選択します。 新しいワークロード グループを作成するには、先頭にアスタリスク ( **&#42;** ) が付いている行をクリックします。  
  
 **[名前]**  
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
  
 詳細については、「[CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)」を参照してください。  
  
## <a name="view-resource-governor-properties-using-transact-sql"></a>Transact-SQL を使用してリソース ガバナーのプロパティを表示する  
 **Transact-SQL を使用してリソース ガバナーのプロパティを表示する**  
  
1.  リソース ガバナー エンティティの定義を表示するには、「[リソース ガバナーのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)」を使用します。  
  
2.  リソース ガバナー エンティティの現在の構成を表示するには、「[リソース ガバナー関連の動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)」を使用します。  
  
## <a name="more-information"></a>詳細情報
 [[リソース ガバナー]](../../relational-databases/resource-governor/resource-governor.md)   
 [リソース ガバナーの有効化](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [リソース ガバナー リソース プール](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [リソース ガバナー ワークロード グループ](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [リソース ガバナーの分類子関数](../../relational-databases/resource-governor/resource-governor-classifier-function.md)  
  
  
