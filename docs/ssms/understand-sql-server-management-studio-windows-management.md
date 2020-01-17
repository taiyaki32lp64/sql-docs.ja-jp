---
title: SQL Server Management Studio でのウィンドウの管理について | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- autohide [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], tool windows
- push pin [SQL Server Management Studio]
- tool windows [SQL Server Management Studio]
ms.assetid: bebf8383-dcaf-466e-84f5-63b81c9cfe52
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b70475e8dba26c1a5aa660ec8bf59547dc9251c8
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267588"
---
# <a name="understand-sql-server-management-studio-windows-management"></a>SQL Server Management Studio でのウィンドウの管理について
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のツール ウィンドウは、高機能で柔軟性の高い、効率的なシステムです。ツール ウィンドウでは、以下の操作を行えます。  
  
-   開発および管理のためのユーザー ワークスペースを最大化する。  
  
-   使用していないウィンドウを非表示にし、一度に表示されるウィンドウの数を少なくする。  
  
-   ユーザー環境を簡単にカスタマイズする。  
  
ウィンドウの操作は、 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 環境においてとても重要です。 ユーザーは、頻繁に使用するツールおよびウィンドウに簡単にアクセスすることができます。 また、さまざまな情報に対してどれだけのスペースを割り当てるかを制御でき、それに応じてクエリの編集時には、使用できるスペースが環境によって最大化されます。 ウィンドウは画面上の別の場所に移動できます。 多くのウィンドウは、ドッキングを解除して [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] フレームの外へドラッグすることができます。 この機能は、複数のモニターを使用している場合に特に便利です。  
  
機能性を保ちながら編集のためのスペースを広く使用するために、すべてのウィンドウには自動非表示という機能があります。この機能を使用すると、ウィンドウはメイン [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 環境の端にあるバーの中で、タブとして表示されます。 これらのタブのいずれかの上にポインターを置くと、下に隠れているウィンドウが表示されます。 ウィンドウの自動非表示機能は、ウィンドウの右上隅にあるプッシュピンの形をした **[自動的に隠す]** ボタンをクリックしてオンとオフを切り替えることができます。 **[ウィンドウ]** メニューにも、 **[すべて自動的に隠す]** オプションが用意されています。  
  
一部のコンポーネントでは、コンポーネントを同じ場所にドッキングしてタブとして表示するタブ モードを使用するか、各コンポーネントを別個のウィンドウで表示するマルチドキュメント インターフェイス (MDI) モードを使用するかを設定できます。 この機能を設定するには、 **[ツール]** メニューの **[オプション]** をクリックします。次に、 **[環境]** をクリックし、 **[全般]** をクリックします。  
  
> [!IMPORTANT]  
> ログイン (または包含データベース ユーザー) が接続して認証されると、接続にはログインに関する ID 情報が格納されます。 Windows 認証ログインの場合、これには Windows グループのメンバーシップに関する情報も含まれます。 接続が維持されている限り、ログインの ID が認証された状態は継続します。 パスワードのリセットや Windows グループのメンバーシップの変更など、ID に関する変更を適用するには、認証機関 (Windows または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]) からログオフしてもう一度ログインする必要があります。 **sysadmin** 固定サーバー ロールのメンバーまたは **ALTER ANY CONNECTION** 権限を持つすべてのログインは、 **KILL** コマンドを使用して接続を終了し、ログインの再接続を強制することができます。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] でオブジェクト エクスプ ローラーおよびクエリ エディター ウィンドウに複数の接続を開くときに、接続情報を再利用できます。 再接続を強制するには、すべての接続を閉じます。  
  
> [!IMPORTANT]  
> ログイン (または包含データベース ユーザー) が接続して認証されると、接続にはログインに関する ID 情報がキャッシュされます。 Windows 認証ログインの場合、これには Windows グループのメンバーシップに関する情報も含まれます。 接続が維持されている限り、ログインの ID が認証された状態は継続します。 パスワードのリセットや Windows グループのメンバーシップの変更など、ID に関する変更を適用するには、認証機関 (Windows または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]) からログオフしてもう一度ログインする必要があります。 **sysadmin** 固定サーバー ロールのメンバーまたは **ALTER ANY CONNECTION** 権限を持つすべてのログインは、 **KILL** コマンドを使用して接続を終了し、ログインの再接続を強制することができます。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] でオブジェクト エクスプ ローラーおよびクエリ エディター ウィンドウに複数の接続を開くときに、接続情報を再利用できます。 再接続を強制するには、すべての接続を閉じます。  
  
## <a name="see-also"></a>参照  
[SQL Server Management Studio の使用 [SQL Server]](../ssms/use-sql-server-management-studio.md)  
[SQL Server Management Studio 環境](../ssms/the-sql-server-management-studio-environment.md)  
  
