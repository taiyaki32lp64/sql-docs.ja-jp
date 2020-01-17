---
title: マージ サブスクライバーのパーティション情報の検証 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication data validation [SQL Server replication], partitions
- parameterized filters [SQL Server replication], validating partition information
- validating partition information
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3bada5fc49dc344510164260330699b60a3288cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63255312"
---
# <a name="validate-partition-information-for-a-merge-subscriber"></a>マージ サブスクライバーのパーティション情報の検証
  マージ パプリケーションに対してパラメーター化された行フィルターを定義している場合は、サブスクライバー情報 (サブスクライバーのログイン名など) を参照する関数を使用します。 既定では、レプリケーションはその関数に基づいて、各同期の前およびサブスクライバーにスナップショットが適用されるたびに、サブスクライバー情報を検証します。 検証プロセスによって、各サブスクライバーのデータが正しくパーティション分割されます。 検証の動作は、**validate_subscriber_info** パブリケーション プロパティで制御されます。このプロパティは、[sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) または **[パブリケーションのプロパティ]** ダイアログ ボックスの **[サブスクリプション オプション]** ページで変更できます。 パブリケーションのプロパティの変更の詳細については、「 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)」を参照してください。  
  
## <a name="how-partition-validation-works"></a>パーティション検証の動作  
 たとえば、 **SUSER_SNAME()** 関数によってパブリケーションをフィルター選択するとき、マージ エージェントは **SUSER_SNAME()** 式で有効なデータに基づいて初期スナップショットを各サブスクライバーに適用します。  
  
 検証が有効な場合、次の同期のためにサブスクライバーがパブリッシャーに再接続すると、マージ エージェントはサブスクライバーの情報を検証し、各サブスクライバーのパーティションが、初期スナップショットで受信したパーティションと同じであるかどうかを確認します。 その後の各マージ アプリケーションまたはスナップショット アプリケーションでは、マージ エージェントは各サブスクライバーのパーティションを検証します。  
  
 フィルター式で使用されている関数が初期スナップショットで返された値と異なる値を返すことをマージ エージェントが検出すると、マージ アプリケーションまたはスナップショット アプリケーションは失敗し、場合によってはそのサブスクライバーのサブスクリプションを再初期化する必要があります。 サブスクライバーのマージ設定が変更された場合に発生する問題を回避するために再初期化が必要な場合がありますが、ログイン名などのサブスクライバーの情報を変更して、元のスナップショット時に使用していた値に戻すだけで十分な場合もあります。  
  
 マージ エージェントがパーティションを検証するときには、フィルター式で使用するすべての関数から返される値に対してパーティションを検証するだけなく、メタデータのクリーンアップ操作やスキーマ変更などの変更が行われる前に、その変更で無効になったスナップショットが生成されていたかどうかもチェックします。 パーティション化されたスナップショットが古すぎる場合、マージ エージェントはエラーを返します。この場合は、現在の標準スナップショットに基づいてそのサブスクライバーのパーティション化されたスナップショットを再生成する必要があります。  
  
## <a name="see-also"></a>参照  
 [レプリケーション管理に関する FAQ](administration/frequently-asked-questions-for-replication-administrators.md)   
 [Best Practices for Replication Administration](administration/best-practices-for-replication-administration.md)   
 [サブスクリプションの再初期化](reinitialize-subscriptions.md)   
 [レプリケートされたデータの検証](validate-data-at-the-subscriber.md)  
  
  
