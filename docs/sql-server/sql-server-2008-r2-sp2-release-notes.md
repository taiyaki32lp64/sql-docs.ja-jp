---
title: SQL Server 2008 R2 SP2 リリース ノート | Microsoft Docs
ms.prod: sql
ms.technology: install
ms.custom: ''
ms.date: 10/15/2019
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server 2008 R2 SP2
- Release Notes, SQL Server 2008 R2 SP2
ms.assetid: e2bd3de7-674c-4ea7-8d53-bb40bba86fae
author: craigg-msft
ms.author: craigg
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: 61afc55e04f7cd317e11c7db527dc97fb80fc7be
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72904259"
---
# <a name="sql-server-2008-r2-sp2-release-notes"></a>SQL Server 2008 R2 SP2 リリース ノート
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
このリリース ノートでは、Microsoft SQL Server 2008 R2 Service Pack 2 のインストールやトラブルシューティングを行う前に知っておく必要がある、既知の問題について説明しています。 このリリース ノート ドキュメントは、SQL Server 2008 R2 SP2 のすべてのエディションに適用され、オンラインでのみ利用できます。 このリリース ノート ドキュメントは定期的に更新されます。  
  
## <a name="10-whats-new-in-service-pack-2"></a>1.0 Service Pack 2 の新機能  
**sys.dm_db_stats_properties**動的管理ビュー (DMV) が追加されました。 この DMV を使用して、現在のデータベース内にある指定されたテーブルまたはインデックス付きビューの統計プロパティを返すことができます。 たとえば、この DMV は、サンプルの行数およびヒストグラムのステップ数を返します。  
  
## <a name="20-before-you-install"></a>2.0 インストールの準備  
[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] の更新プログラムのインストール方法については、 [SQL Server 2008 R2 サービスのドキュメント](https://msdn.microsoft.com/library/dd638062(SQL.105).aspx)を参照してください。  
  
SQL Server 2008 R2 のインストール方法の一般的な情報については、SQL Server 2008 R2 の Readme を参照してください。 この Readme ドキュメントは、インストール メディアにあります。 [SQL Server フォーラム](https://social.msdn.microsoft.com/Forums/category/sqlserver/)でも、詳細な情報を参照することができます。
  
### <a name="21-choose-the-correct-file-to-download-and-install"></a>2.1 ダウンロードとインストールに使用する正しいファイルの選択  
ダウンロードとインストールに使用するファイルを確認するには、次の表を参照してください。 サービス パックをインストールする前に、システム要件を正しく満たしていることを確認します。 システム要件は、この表にあるリンクされたダウンロード ページに記載されています。  
  
|現在インストールされているバージョン|目的|ダウンロードとインストール|  
|-------------------------------------------|----------------------|---------------------------|  
|SQL Server 2008 R2 または SQL Server 2008 R2 SP1 のいずれかのエディションの 32 ビット バージョン|SQL Server 2008 R2 SP2 の 32 ビット バージョンへアップグレード|SQLServer2008R2SP2-KB2630458-x86-ENU ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=251790)から)|  
|SQL Server 2008 R2 RTM Express または SQL Server 2008 R2 SP1 Express の 32 ビット バージョン|SQL Server 2008 R2 SP2 の 32 ビット バージョンへアップグレード|SQLServer2008R2SP2-KB2630458-x86-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=251790)から)|  
|SQL Server 2008 R2 または SQL Server 2008 R2 SP1 のクライアントと管理ツールのみの 32 ビット バージョン (SQL Server 2008 R2 Management Studio を含む)|SQL Server 2008 R2 SP2 の 32 ビット バージョンへクライアントと管理ツールをアップグレード|SQLServer2008R2SP2-KB2630458-x86-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=251790)から)|  
|SQL Server 2008 R2 Management Studio Express または SQL Server 2008 R2 SP1 Management Studio Express の 32 ビット バージョン|SQL Server 2008 R2 SP2 Management Studio Express の 32 ビット バージョンへアップグレード|SQLManagementStudio_x86_ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=251791)から)|  
|SQL Server 2008 R2 または SQL Server 2008 R2 SP1 のいずれかのエディションの 32 ビット バージョン **および** クライアントと管理ツールの 32 ビット バージョン (SQL Server 2008 R2 RTM Management Studio 含む)|SQL Server 2008 R2 SP2 の 32 ビット バージョンへすべての製品をアップグレード|SQLServer2008R2SP2-KB2630458-x86-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=251790)から)|  
|[Microsoft SQL Server 2008 R2 用 Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=16978)の 1 つ以上のツールの 32 ビット バージョン|Microsoft SQL Server 2008 R2 SP2 用 Feature Pack の 32 ビット バージョンへツールをアップグレード|[Microsoft SQL Server 2008 R2 SP2 用 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=251792)の 1 つ以上のファイル|  
|SQL Server 2008 R2 の 32 ビット インストールなし|Server 2008 R2 のインストール (SP2 含む)|[SQL Server 2008 R2 SP2 - Express Edition](https://go.microsoft.com/fwlink/?LinkId=251791) に移動して、指示に従ってください。|  
|SQL Server 2008 R2 Management Studio の 32 ビット インストールなし|SQL Server 2008 R2 Management Studio のインストール (SP2 含む)|SQLManagementStudio_x86_ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=251791) から) を使用して無料の SQL Server 2008 R2 SP2 Management Studio Express Edition をインストールしてください。|  
|SQL Server 2008 R2 または SQL Server 2008 R2 SP1 のいずれかのエディションの 64 ビット バージョン|SQL Server 2008 R2 SP2 の 64 ビット バージョンへアップグレード|SQLServer2008R2SP2-KB2630458-x64-ENU または SQLServer2008R2SP2-KB2630455-IA64-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=251790)から)|  
|SQL Server 2008 R2 RTM Express または SQL Server 2008 R2 SP1 Express の 64 ビット バージョン|SQL Server 2008 R2 SP2 の 64 ビット バージョンへアップグレード|SQLServer2008R2SP2-KB2630458-x64-ENU.exe または SQLServer2008R2SP2-KB2630455-IA64-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=251790)から)|  
|SQL Server 2008 R2 または SQL Server 2008 R2 SP1 のクライアントと管理ツールのみの 64 ビット バージョン (SQL Server 2008 R2 Management Studio 含む)|SQL Server 2008 R2 SP2 の 64 ビット バージョンへクライアントと管理ツールをアップグレード|SQLServer2008R2SP2-KB2630458-x64-ENU.exe または SQLServer2008R2SP2-KB2630455-IA64-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=251790)から)|  
|SQL Server 2008 R2 Management Studio Express または SQL Server 2008 R2 SP1 Management Studio Express の 64 ビット バージョン|SQL Server 2008 R2 SP2 Management Studio Express の 64 ビット バージョンへアップグレード|SQLManagementStudio_x64_ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=251791)から)|  
|SQL Server 2008 R2 または SQL Server 2008 R2 SP1 のいずれかのエディションの 64 ビット バージョン **および** クライアントと管理ツールの 64 ビット バージョン (SQL Server 2008 R2 RTM Management Studio 含む)|SQL Server 2008 R2 SP2 の 64 ビット バージョンへすべての製品をアップグレード|SQLServer2008R2SP2-KB2630458-x64-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=251790)から)|  
|[Microsoft SQL Server 2008 R2 用 Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=16978)の 1 つ以上のツールの 64 ビット バージョン|Microsoft SQL Server 2008 R2 SP2 用 Feature Pack の 64 ビット バージョンへツールをアップグレード|[Microsoft SQL Server 2008 R2 SP2 用 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=251792)の 1 つ以上のファイル|  
|SQL Server 2008 R2 の 64 ビット インストールなし|Server 2008 R2 のインストール (SP2 含む)|[SQL Server 2008 R2 SP2 - Express Edition](https://go.microsoft.com/fwlink/?LinkId=251791) に移動して、指示に従ってください。|  
|SQL Server 2008 R2 Management Studio の 64 ビット インストールなし|SQL Server 2008 R2 Management Studio のインストール (SP2 含む)|SQLManagementStudio_x64_ENU.exe ( [ここから](https://go.microsoft.com/fwlink/p/?LinkId=251791) ) を使用して無料の SQL Server 2008 R2 SP2 Management Studio Express Edition をインストールしてください。|  
  
### <a name="22-setup-might-fail-if-sqagtresdll-is-locked-by-another-process"></a>2.2 別のプロセスによって SQAGTRES.dll がロックされている場合のセットアップ失敗  
**問題点**: SQL Server のセットアップ操作が次のエラーにより失敗する場合:`Upgrading of cluster resource C:\Program Files\Microsoft SQL Server\MSSQL10_50.<Instance name>\MSSQL\Binn\SQAGTRES.DLL on machine <Computer name> failed with Win32Exception. Please look at inner exception for details.` 根本的な原因は、C:\Windows\system32\SQAGTRES.DLL が別のプロセスによってロックされていて、セットアップが更新できなかったことです。  
  
**回避策**:C:\Windows\system32\SQAGTRES.DLL を一時的な名前 (C:\Windows\system32\SQAGTRES_old.DLL など) に変更して、セットアップ エラー メッセージの再試行オプションを選択します。 これにより、セットアップを続行できます。 再起動後、一時ファイル C:\Windows\system32\SQAGTRES_old.DLL は削除できます。  
  
## <a name="30-known-issues-fixed-in-this-service-pack"></a>3.0 この Service Pack で修正された既知の問題  
この Service Pack で修正されたすべてのバグと既知の問題については、この [サポート技術情報記事](https://support.microsoft.com/kb/2630455)を参照してください。  
  
## <a name="see-also"></a>参照  
[SQL Server のバージョンとエディションを確認する方法](https://support.microsoft.com/kb/321185)  
  
