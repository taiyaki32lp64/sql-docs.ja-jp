---
title: '[エージェント プロファイル] | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.profiles.perfprofiles.f1
helpviewer_keywords:
- Agent Profiles dialog box
ms.assetid: 0422e99c-e688-419b-bb4c-c7bebeef1d8d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: bea15bd12af6675bd0567e2f607d865c50453717
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770771"
---
# <a name="agent-profiles"></a>[エージェント プロファイル]
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[エージェント プロファイル]** ダイアログ ボックスを使用すると、エージェント プロファイルを管理できます。 エージェント プロファイルを利用すると、各エージェントの実行時パラメーターを容易に管理できます。 それぞれのエージェントは既定のプロファイルを持ちます。一部のエージェントには、追加の定義済みプロファイルが用意されています。 たとえば、マージ エージェントには、低帯域幅接続の "低速リンク" プロファイルが用意されています。 ほとんどのアプリケーションでは定義済みのプロファイルで十分ですが、ユーザー定義プロファイルを作成して、エージェントの動作をカスタマイズすることもできます。  
  
## <a name="options"></a>オプション  
 **[ページの選択]**  
 左側のペインでエージェントを選択すると、エージェントのプロファイルが右側のペインに表示されます。  
  
 **[新規の既定]**  
 特定の種類のエージェントに対してジョブを作成するときに使用するプロファイルを選択します。 たとえば、マージ パブリケーションに対していくつかのサブスクリプションを作成する場合、選択されたプロファイルが各サブスクリプションのマージ エージェント ジョブで使用されます。 既存のジョブのプロファイルを変更するには、プロファイルを選択し、 **[既存のエージェントの変更]** をクリックします。  
  
 **[名前]**  
 プロファイルの名前。  
  
 **型**  
 プロファイルの種類です。 **[ユーザー]** (ユーザー定義) または **[システム]** (定義済み)。  
  
 **[プロパティ] (...)**  
 クリックすると、エージェント プロファイルの各パラメーターに使用されている値が表示されます。  
  
 **[新規作成]**  
 クリックすると、新しいプロファイルを作成できます。  
  
 **削除**  
 ユーザー定義プロファイルを削除するには、プロファイルを選択し、 **[削除]** をクリックします。 定義済みのプロファイルは削除できません。  
  
 **[既存のエージェントの変更]**  
 特定の種類のエージェントのすべての既存のジョブで、選択したプロファイルを使用する場合は、プロファイルを選択して **[既存のエージェントの変更]** をクリックします。 たとえば、マージ パブリケーションに対して作成したサブスクリプションがいくつかあり、これらの各サブスクリプションのマージ エージェント ジョブで **低速リンク エージェント プロファイル**を使用するようにプロファイルを変更するには、目的のプロファイルを選択し、 **[既存のエージェントの変更]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェント プロファイルの操作](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [レプリケーション エージェント プロファイル](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  
