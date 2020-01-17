---
title: Integration Services サービスへのアクセス許可 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0c2caa68-7834-4ea0-bd77-4f3a7c86d634
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 989db1ed792d960b7a0dca22bd82ec8b2f5aa7df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058230"
---
# <a name="grant-permissions-to-integration-services-service"></a>Integration Services サービスへの権限を付与する
  以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] をインストールすると、既定で Users グループの全ユーザーが [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスにアクセスできました。 現在のリリースの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]をインストールした場合、ユーザーは [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスにアクセスできません。 このサービスは既定で保護されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストール後に、管理者はサービスに対するアクセスを許可する必要があります。  
  
### <a name="to-grant-access-to-the-integration-services-service"></a>Integration Services サービスへのアクセスを許可するには  
  
1.  Dcomcnfg.exe を実行します。 Dcomcnfg.exe には、レジストリ内の特定の設定を変更するためのユーザー インターフェイスが用意されています。  
  
2.  **[コンポーネント サービス]** ダイアログで、[コンポーネント サービス] > [コンピューター] > [マイ コンピューター] > [DCOM の構成] ノードの順に展開します。  
  
3.  右クリックして**Microsoft SQL Server Integration Services 12.0**、 をクリックし、**プロパティ**します。  
  
4.  **[セキュリティ]** タブで、 **[起動とアクティブ化のアクセス許可]** 領域の **[編集]** をクリックします。  
  
5.  ユーザーを追加し、適切なアクセス許可を割り当てて、[OK] をクリックします。  
  
6.  アクセス許可で手順 4. と 5. を繰り返します。  
  
7.  SQL Server Management Studio を再起動します。  
  
8.  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスを再開します。  
  
  
