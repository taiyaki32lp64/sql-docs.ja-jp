---
title: SQL Server のインストールの検証 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34e4c29cb28f76c930f1f04152528ca1a8a89dfc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775235"
---
# <a name="validate-a-sql-server-installation"></a>SQL Server のインストールの検証
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の検出レポートは、コンピューターにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能を確認するために使用できます。 **インストール済み[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]機能の検出レポート**すべてのレポートを表示します[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、および[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]製品や機能を。ローカル サーバーにインストールされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能の検出レポートは、 **インストール センターの** [ツール] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ページで利用できます。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能の検出レポートを実行するには**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール センターを起動します。そのためには、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<バージョン名>]** 、 **[構成ツール]** の順にポイントし、 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール センター]** をクリックします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能の検出レポートを実行するには、 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール センター]** の左側のナビゲーション領域にある **[ツール]** をクリックし、 **[インストール済み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能の検出レポート]** をクリックします。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]検出レポートは %programfiles% に保存\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< 最後のセットアップ セッション\>します。  
  
 また、コマンド ラインから検出レポートを生成することができます。 実行"Setup.exe/Action = RunDiscovery"を追加する場合は、コマンド プロンプトから"/q"上記のコマンドラインに UI は表示されませんが、レポートは %programfiles% に作成されます\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< 最後のセットアップ セッション\>します。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server セットアップ ログ ファイルの表示と読み取り](view-and-read-sql-server-setup-log-files.md)  
  
  
