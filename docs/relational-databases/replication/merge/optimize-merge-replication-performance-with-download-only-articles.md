---
title: ダウンロード専用アーティクルのパフォーマンスの最適化 (マージ)
description: マージ レプリケーションで使用されるダウンロード専用アーティクルのパフォーマンスを最適化する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 8851faa6-e6df-4ea5-a6ea-2a3471680fa3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b2e5ba71eab133751b9ae58d912b933b6821178d
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321457"
---
# <a name="optimize-merge-replication-performance-with-download-only-articles"></a>ダウンロード専用アーティクルを使用したマージ レプリケーションのパフォーマンス最適化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  マージ レプリケーションには、異なるアプリケーション ニーズに対応する 2 種類のアーティクルが用意されています。 アプリケーションでの必要に応じて、パブリケーションにはこれら 2 種類のアーティクルを 1 つ以上格納できます。  
  
-   標準アーティクル  
  
-   ダウンロード専用アーティクル  
  
 ダウンロード専用アーティクルは、パフォーマンス面で標準アーティクルよりも優れています。必要に応じて、ダウンロード専用アーティクルを使用するようにしてください。  
  
> [!NOTE]  
>  ダウンロード専用アーティクルを使用するためには、90RTM 以上の互換性レベルが必要になります。  
  
## <a name="standard-articles"></a>標準アーティクル  
 標準アーティクルは既定のアーティクルであり、強力な競合検出および競合解決機能など、マージ レプリケーションに必要なすべての機能を備えています。 標準アーティクルは、複数のサブスクライバーによって更新されるテーブルに適しています。また、ストアド プロシージャやビューなどのテーブル以外のオブジェクトは、常に標準アーティクルとしてパブリッシュされます。  
  
## <a name="download-only-articles"></a>ダウンロード専用アーティクル  
 ダウンロード専用アーティクルは、製品カタログに格納される一連のアーティクルなど、サブスクライバーで更新されないデータを処理するアプリケーション向けに設計されています。 通常の場合、製品カタログはサブスクライバーではなくパブリッシャーで更新されます。 ダウンロード専用アーティクルはサブスクライバーで更新されないため、追跡メタデータがサブスクライバーに送信されることはありません。 これによってサブスクライバーの記憶域が節約されると共に、特に低速なネットワーク接続ではパフォーマンスの向上にもつながります。  
  
 ダウンロード専用アーティクルはクライアント サブスクリプションと併用されます。アーティクルがダウンロード専用に作成されている場合、クライアント サブスクリプションを使用するサブスクライバーでは、このアーティクルに対して行の挿入、更新、および削除を行うことができません。 サーバー サブスクリプションを使用するパブリッシャーおよびサブスクライバー (通常は、他のサブスクライバーにデータを再パブリッシュするサブスクライバー) では、行の挿入、更新、および削除を行うことができます。 クライアント サブスクリプションの詳細については、「[パブリケーションのサブスクライブ](../../../relational-databases/replication/subscribe-to-publications.md)」を参照してください。  
  
 アーティクルがダウンロード専用になるように指定するには、「[Specify Merge Replication properties](../../../relational-databases/replication/merge/specify-merge-replication-properties.md)」(マージ レプリケーションのプロパティを指定する) を参照してください。  
  
## <a name="using-different-article-types-in-your-applications"></a>アプリケーションに応じた各種アーティクルの使い分け  
 アプリケーションの要件を理解することにより、柔軟性の最大化とパフォーマンスの最適化の間でアプリケーションを調整できます。 たとえば、パブリッシャーとサブスクライバーの両方で多数の競合と変更が発生するアプリケーションでは、標準アーティクルから構成されるパブリケーションを使用します。 セールス フォース オートメーションなど一部のアプリケーションでは、競合の可能性のあるアーティクルと、それ以外にダウンロード専用に指定できる参照テーブル用のアーティクルが使用されることがあります。 POS システムやフィールド フォース オートメーションなどのデータ入力アプリケーションでは、競合を排除するように厳密にデータがパーティション分割されている場合が多く、あるサブスクライバーから他のサブスクライバーにデータが送信されることは決してありません。 このような状況では、重複しないパーティション、ダウンロード専用アーティクル、および事前計算済みパーティションを組み合わせて使用することで、パフォーマンスとスケーラビリティを最大化することができます。 重複しないパーティションおよび事前計算済みパーティションの詳細については、「 [パラメータ化された行フィルタ](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マージ レプリケーションのアーティクル オプション](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [条件付き削除の追跡によるマージ レプリケーション パフォーマンスの最適化](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
