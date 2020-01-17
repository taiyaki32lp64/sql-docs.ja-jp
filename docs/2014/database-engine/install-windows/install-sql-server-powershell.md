---
title: SQL Server PowerShell のインストール | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a90a30a0ae7fe09d49b1d42b577b13370c48c0de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775442"
---
# <a name="install-sql-server-powershell"></a>SQL Server PowerShell のインストール
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップは、Windows PowerShell 2.0 をインストールしていないのに、PowerShell コンポーネントを含む [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能を選択したことが検出された場合に停止します。 Windows 管理フレームワークを使用して PowerShell をインストールしてから、セットアップを再実行する必要があります。  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-powershell-support"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell サポートのインストール  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを使用して、Windows PowerShell に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サポートを提供するソフトウェアをインストールします。 PowerShell サポートを必要とする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能を選択すると、Windows PowerShell 2.0 がインストールされているかどうかが確認されます。 PowerShell 2.0 が存在する場合は、セットアップにより次の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell コンポーネントがインストールされます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell スナップイン。スナップインは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用の以下の 2 種類の Windows PowerShell サポートを実装する dll ファイルです。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コマンドレットのセット。 コマンドレットは特定の操作を実装するコマンドです。 たとえば、 **Invoke-Sqlcmd** では、 [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd **ユーティリティを使用して実行することもできる** スクリプトまたは XQuery スクリプトが実行され、 **Invoke-PolicyEvaluation** では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトがポリシー ベースの管理ポリシーに準拠しているかどうかが報告されます。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロバイダー。 プロバイダーでは、ファイル システム パスと同様のパスを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの階層内を移動できます。 各オブジェクトは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト モデルのクラスに関連付けられています。 クラスのメソッドやプロパティを使用して、オブジェクトの操作を実行できます。 たとえば、パスでデータベース オブジェクトに移動した場合、Microsoft.SqlServer.Managment.SMO.Database クラスのメソッドとプロパティを使用してデータベースを管理できます。  
  
-   **Sqlps**モジュールを読み込む Windows PowerShell 2.0 セッションにインポートされる、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スナップイン。  
  
-   非推奨とされる**sqlps**ユーティリティを Windows PowerShell 2.0 セッションを開始し、インポート、 **sqlps**モジュール。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、オブジェクト エクスプローラー ツリーからの Windows PowerShell セッションの起動をサポートします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、Windows PowerShell ジョブ ステップをサポートします。  
  
 インストールされていない、またはがアンインストールされている場合は、Windows PowerShell 2.0 次の手順でインストールする必要があります、 [Windows Management Framework](https://go.microsoft.com/fwlink/?LinkId=186214)ページ。  
  
 セットアップの終了後に Windows PowerShell がアンインストールされると、Windows PowerShell 用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能は機能しなくなります。 Windows PowerShell をアンインストールできるのは Windows ユーザーです。また、Windows PowerShell のアンインストールは、Windows オペレーティング システムのアップグレードで必要になる場合があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 機能を使用するには、Windows Management Framework を使用して PowerShell 2.0 を再インストールする必要があります。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  
  
  
