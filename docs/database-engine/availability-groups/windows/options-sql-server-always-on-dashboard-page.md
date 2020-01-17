---
title: SSMS での可用性グループ ダッシュ ボード
description: SQL Server Management Studio での SQL Server Always On ダッシュ ボードに表示される [オプション] ページの説明。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Alwayson.Dashboard
ms.assetid: 4369b588-e982-4b57-80a1-beb2e879ce0b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ae4c5aae76c41b642d445e92844efa2ddf36fdcc
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822545"
---
# <a name="options-sql-server-always-on-dashboard-page"></a>オプション (SQL Server AlwaysOn、[ダッシュボード] ページ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)][ **のオプション]** ダイアログ ボックスの **[SQL Server AlwaysOn ダッシュボード]** ページを使用して、AlwaysOn ダッシュボードを構成します。  
  
 **このページにアクセスするには:**  
  
 **[ツール]** メニューの **[オプション]** をクリックし、 **[SQL Server AlwaysOn]** フォルダーを展開して、 **[ダッシュボード]** をクリックします。  
  
## <a name="on-this-page"></a>このページの内容  
 **[自動更新を有効にする]**  
 クリックすると、自動更新が有効になります。 オプションは次のとおりです。  
  
-   **[更新間隔 (秒単位)]** フィールドには、ダッシュボードが更新される秒数が表示されます。 既定値は 30 です。 自動更新を有効にすると、このフィールドを編集して更新間隔を変更できます。  
  
-   **[接続の再試行回数]** には、ダッシュボードが監視している可用性グループの可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスにダッシュボードが接続を試行する回数が表示されます。 既定値は、65535 です。 自動更新を有効にすると、このフィールドを編集して接続試行回数を変更できます。  
  
 **[ユーザー定義の AlwaysOn ポリシーを有効にする]。**  
 AlwaysOn ポリシーを定義している場合は、このオプションをクリックしてポリシーを有効にします。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
