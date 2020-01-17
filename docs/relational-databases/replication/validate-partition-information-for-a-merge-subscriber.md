---
title: パーティション情報の検証 (マージ)
description: SQL Server でマージ サブスクライバーのパーティション情報を検証する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: da57b7586fb80346dda466004a9cd47a3bb08884
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321551"
---
# <a name="validate-partition-information-for-a-merge-subscriber"></a>マージ サブスクライバーのパーティション情報の検証
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  マージ パプリケーションに対してパラメーター化された行フィルターを定義している場合は、サブスクライバー情報 (サブスクライバーのログイン名など) を参照する関数を使用します。 既定では、レプリケーションはその関数に基づいて、各同期の前およびサブスクライバーにスナップショットが適用されるたびに、サブスクライバー情報を検証します。 検証プロセスによって、各サブスクライバーのデータが正しくパーティション分割されます。 検証の動作は、**validate_subscriber_info** パブリケーション プロパティで制御されます。このプロパティは、[sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) または **[パブリケーションのプロパティ]** ダイアログ ボックスの **[サブスクリプション オプション]** ページで変更できます。 パブリケーションのプロパティの変更の詳細については、「 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」を参照してください。  
  
## <a name="how-partition-validation-works"></a>パーティション検証の動作  
 たとえば、 **SUSER_SNAME()** 関数によってパブリケーションをフィルター選択するとき、マージ エージェントは **SUSER_SNAME()** 式で有効なデータに基づいて初期スナップショットを各サブスクライバーに適用します。  
  
 検証が有効な場合、次の同期のためにサブスクライバーがパブリッシャーに再接続すると、マージ エージェントはサブスクライバーの情報を検証し、各サブスクライバーのパーティションが、初期スナップショットで受信したパーティションと同じであるかどうかを確認します。 その後の各マージ アプリケーションまたはスナップショット アプリケーションでは、マージ エージェントは各サブスクライバーのパーティションを検証します。  
  
 フィルター式で使用されている関数が初期スナップショットで返された値と異なる値を返すことをマージ エージェントが検出すると、マージ アプリケーションまたはスナップショット アプリケーションは失敗し、場合によってはそのサブスクライバーのサブスクリプションを再初期化する必要があります。 サブスクライバーのマージ設定が変更された場合に発生する問題を回避するために再初期化が必要な場合がありますが、ログイン名などのサブスクライバーの情報を変更して、元のスナップショット時に使用していた値に戻すだけで十分な場合もあります。  
  
 マージ エージェントがパーティションを検証するときには、フィルター式で使用するすべての関数から返される値に対してパーティションを検証するだけなく、メタデータのクリーンアップ操作やスキーマ変更などの変更が行われる前に、その変更で無効になったスナップショットが生成されていたかどうかもチェックします。 パーティション化されたスナップショットが古すぎる場合、マージ エージェントはエラーを返します。この場合は、現在の標準スナップショットに基づいてそのサブスクライバーのパーティション化されたスナップショットを再生成する必要があります。  
  
## <a name="see-also"></a>参照  
 [レプリケーション管理に関する FAQ](../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [Best Practices for Replication Administration](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [レプリケートされたデータの検証](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
