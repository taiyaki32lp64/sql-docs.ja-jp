---
title: 競合回避モジュールの選択 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- default conflict resolver
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: b7dec3fa-d9d9-409d-b946-f9b9a3202829
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3b93c9b438a22cba125bb7487b393371b4ffd8c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033441"
---
# <a name="advanced-merge-replication-conflict---choose-a-resolver"></a>マージ レプリケーションの競合の詳細 - 競合回避モジュールの選択
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  競合回避モジュールを選択するときには、アプリケーションでの競合解決の重要性、および既定の優先度ベースの競合回避モジュールを使用できるかどうか、アーティクル競合回避モジュールを使用する必要があるかどうかを考慮します。  
  
 データをパーティション分割するときに、複数のユーザーが同じパーティションに書き込まず、レプリケーション トポロジが基本構成 (1 つのパブリッシャーといくつかのサブスクライバー) に比較的従っている場合、競合は非常にまれであるか、またはまったく発生しません。 このような環境では、複雑な競合解決方法が不要な場合もあります。 競合の解決に既定の設定を使用する方法、クライアント サブスクリプションを使用する方法、または最初の変更を優先する方法をお勧めします。 トポロジがより複雑な場合 (再パブリッシュ サブスクライバーを使用するなど) は、サーバー サブスクリプションに特定の優先度を指定する方が適切です。  
  
 アーティクル競合回避モジュールは、ビジネス上のニーズにより既定の競合回避モジュールより細かく調整されたソリューションが必要な場合にお勧めします。 アーティクル競合回避モジュールを使用する場合は、ビジネス ロジック ハンドラーを使用することをお勧めします。 詳細については、「[Execute Business Logic During Merge Synchronization](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)」(マージ同期中のビジネス ロジックの実行) をご覧ください。  
  
 最終的に、既定の競合回避モジュールとアーティクル競合回避モジュールのどちらを使用するかは、アプリケーションのデータおよびビジネス ロジックのニーズによって異なります。 たとえば、異なるサブスクライバーでパーティション分割されていないテーブルに顧客の順位データを入力する従業員がさまざまなジョブ カテゴリ (支社長、工程管理者、販売スタッフ) にまたがっており、ジョブ カテゴリによってデータの優先度が決まるとします。 この場合、アーティクル競合回避モジュールを構築できます。このモジュールは、競合発生時に優先されるデータの判別に、アーティクルから得られたジョブ カテゴリ データを使用します。  
  
 競合がある程度の頻度で発生する場合、以下のように、競合解決方法の実装時に考慮しなければならないことがあります。  
  
|競合解決に際して考慮すべき問題|推奨|  
|-------------------------------|--------------------|  
|異なるジョブ カテゴリのユーザーに対して異なる優先度が必要な場合|既定の競合回避モジュールを使用して、異なる優先度値を持つサーバー サブスクリプションを作成する。<br /><br /> または<br /><br /> アーティクル内の権限値の列を認識するアーティクル競合回避モジュールを使用して、競合を解決する。|  
|最初に変更されたデータが優先される競合解決方法が必要な場合|既定の競合回避モジュールを使用して、クライアント サブスクリプションを作成する。|  
|同じ行に対する変更の競合がない限り、複数のユーザーが同じデータ行を変更することを認める場合|既定の競合回避モジュール、または列レベルの追跡を有効にしたアーティクル競合回避モジュールを使用する。|  
|行の値に対して複数の変更が発生したときに競合のフラグを付ける場合|既定の競合回避モジュール、または行レベルの追跡を有効にしたアーティクル競合回避モジュールを使用する。|  
|論理レコードの値に対して複数の変更が発生したときに競合のフラグを付ける場合|論理レコード レベルの追跡を有効にした既定の競合回避モジュールを使用する (論理レコード機能では、カスタム競合回避モジュールまたはビジネス ロジック ハンドラーはサポートされていません)。|  
|競合の結果データが元の競合データと異なっている必要がある場合|新しい値を計算するアーティクル競合回避モジュールを使用する。|  
  
## <a name="see-also"></a>参照  
 [論理レコードの競合の検出および解決](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [マージ レプリケーションの競合検出および解決の詳細](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [データの再パブリッシュ](../../../relational-databases/replication/republish-data.md)  
  
  
