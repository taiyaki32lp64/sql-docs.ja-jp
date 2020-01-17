---
title: その他の Reporting Services のアップグレードに関する問題 \|Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- command line setup [Reporting Services]
- Setup commands [Reporting Services]
- multivalued parameters [Reporting Services]
- WMI provider [Reporting Services]
- compile errors [Reporting Services]
- single-valued parameters [Reporting Services]
- data processing extensions [Reporting Services]
- report compilation errors [Reporting Services]
- authentication [Reporting Services]
ms.assetid: 42dd2f06-1de9-449e-ab9d-f4ef25f8b728
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 07d18dd9c99902f53b5bb1855b79c350bbfbdbe8
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952477"
---
# <a name="other-reporting-services-upgrade-issues"></a>Reporting Services のアップグレードに関するその他の問題
  このトピックでは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 機能のアップグレード中に発生する可能性のある既知の問題について説明します。 **これらの問題は、アップグレードアドバイザーでは検出されません。** 詳細については、「 [SQL Server 2014 リリースノート](https://go.microsoft.com/fwlink/?LinkID=296445)」を参照してください。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード。|  
  
|問題点|[説明]|適用対象|  
|-----------|-----------------|----------------|  
|SharePoint ファームのアップグレード|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共有サービスをアップグレードするには、その前にファーム内の他のすべての [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントが [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] にアップグレードされている必要があります。<br /><br /> 複数ノードの SharePoint ファームの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]にアップグレードするには、ファーム内の SharePoint 用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインのすべてのインスタンスを [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] のバージョンにアップグレードしてから [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共有サービスをアップグレードする必要があります。<br /><br /> レポートの表示に失敗するのは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共有サービスが [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] にアップグレードされていても、ファーム内の他の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントがまだバージョン [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] であるためです。<br /><br /> <br /><br /> 詳細については、「 [SQL Server 2014 Reporting Services の役立つヒントおよびトラブルシューティング](https://go.microsoft.com/fwlink/?LinkID=391254)」を参照してください。|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 」、「 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|  
|サイド バイ サイド インストール|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モードは、次のいずれのものともサイド バイ サイドで実行することはできません。<br /><br /> SharePoint 用 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドイン<br /><br /> SharePoint 共有サービス [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]<br /><br /> <br /><br /> サイドバイサイドインストールでは、ネイティブモードの Windows サービス [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]を開始できません。 次のようなエラー メッセージが Windows イベント ログに記録されます。<br /><br /> 説明: レポート サーバー データベースのバージョンが無効です。<br /><br /> 説明: レポート サーバー [server name] はレポート サーバー データベースに接続できません。|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ネイティブ モード|  
|失敗したアップグレードを修復しているときのエラー|**問題:** アップグレードが失敗した後で、修復を実行しようとしました。 修復操作も失敗し、セットアップ ログ ファイルに次のようなメッセージが記録されています。<br /><br /> `(01) 2011-10-27 12:23:15 Slp:` <br /> `(01) 2011-10-27 12:23:15 Slp: Exception type: System.Exception` <br /> `(01) 2011-10-27 12:23:15 Slp:     Message:`  <br /> `(01) 2011-10-27 12:23:15 Slp:         SQLPath element is missing` <br /> `(01) 2011-10-27 12:23:15 Slp:     Data:`  <br /> `(01) 2011-10-27 12:23:15 Slp:       SQL.Setup.FailureCategory = ConfigurationFailure`<br /><br /> ログファイルの詳細については、「 [SQL Server セットアップログファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。<br /><br /> **解決策:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をアンインストールし、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]を再インストールする必要があります。 アップグレードはできなくなります。|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 」、「 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|  
|最後の要求の対話情報のみが保存される|以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、ドリルスルー情報や切り替えの選択など、対話形式での選択で可能なすべての組み合わせがスナップショットに保存されていました。 たとえば、レポートの 5 ページ目を表示する一方で、プログラムでは切り替え用の正しい ID を追跡することで 1 ページ目のアイテムを切り替えることが可能でした。<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では、最後の表示要求の対話情報のみが生成されて保存されます。 あるページを表示しながら、プログラムで別のページ上のアイテムを切り替えることはできません。 現在のレポート ページのドリルダウン アイテムのみを切り替えることができます。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|表示およびページ割り当ての変更|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で、レンダリングオブジェクトモデル (ROM) が変更されました。 以前のバージョンの表示オブジェクト モデルはサポートされなくなりました。 マルチスレッドの表示拡張機能から表示オブジェクト モデルにアクセスすること (および複数スレッドからコンテキストを切り替えること) はできません。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|CSV エクスポート形式の設計変更|以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レポートを CSV ファイル形式にエクスポートするときに、レポート ページでのデータ表示方法を維持するようにデータが書式設定されていました。 マトリックス データ領域の場合、このように書式設定されたデータは、他のアプリケーションにインポートする場合に不便でした。<br /><br /> このリリースでは、レポートを CSV ファイルにエクスポートするときに、既定のモードと準拠モードの 2 つのサポート形式を選択できるようになりました。 既定のモードでは Excel 向けにデータの形式が最適化されます。 準拠モードでは、サードパーティのアプリケーション向けにデータの形式が最適化されます。<br /><br /> 以前の形式の CSV ファイルは使用できなくなります。 ただし、マトリックス データ領域を使用しないレポートの場合は、準拠モードを使用すれば、以前の CSV ファイル形式に最も近いファイル形式になります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|ページ ヘッダーとページ フッターでの条件付き表示による集計|以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、条件付き表示でレポート ページに含めるアイテムを決定する場合、レンダラーが異なれば使用するルールも異なりました。 たとえば、印刷レポートでは非表示アイテムの集計計算は行われませんでしたが、ブラウザーや [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel に表示されるレポートでは非表示アイテムも計算されていました。<br /><br /> このリリースでは、ページに含めるアイテムの判断に、すべてのレンダラーが同じルール セットを使用します。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|Excel の数式がサポートされない|以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、RDL の式を Excel の数式に変換する操作が限定的にサポートされていました。 このリリースでは、レポートを Excel にエクスポートするときに、RDL の式が Excel の数式に変換されません。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|重複する項目。|以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レポートのデザイン画面に重なり合うアイテムがある場合にレポートをパブリッシュすると、警告 ("レポート アイテムの重なりは、どのレンダラーでもサポートされていません。") が生成されましたが、レポート アイテムはデザイン画面の元の位置に配置されたままでした。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では、レポート アイテムの重なりをサポートしないレンダラーにレポートが表示またはエクスポートされると、アイテムが移動されて境界の重なりが解消されます。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|レポートオブジェクトモデルの名前空間の変更。|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、レポートオブジェクトモデルの名前空間が変更されています。 この名前空間では、カスタム コードから `Fields`、`Parameters`、`ReportItems` のようなグローバル コレクションへの読み取り専用アクセスが提供されます。 既存のカスタム コードで以前の名前空間への完全修飾参照を明示的に使用している場合は、この変更が重大な変更になります。<br /><br /> コードから組み込みコレクションにアクセスする場合は、完全修飾参照を使用しないことをお勧めします。 名前空間を明示的に指定していなければ、カスタム コードからの参照は、現在インストールされているバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のレポート オブジェクト モデルに解決されます。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 のレポート サーバー Windows Management Instrumentation (WMI) プロバイダーがサポートされない|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポート サーバーの実行環境をプログラムによって構成できる WMI プロバイダーが含まれています。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、以前のバージョンとは完全に異なるまったく新しい WMI プロバイダーを備えています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 および 2005 のバージョンの WMI プロバイダーは、このリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではサポートされません。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|アップグレードされたレポート サーバーでサービス プリンシパル名 (SPN) が再作成されない|レポート サーバー Web サービスに対して SPN を作成した場合は、アップグレードされたレポート サーバーでも制約付き委任が機能することを確認してください。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|カスタム アセンブリを新しいインストール フォルダーに手動で移動する必要があります。|カスタム アセンブリはアップグレード アドバイザーによって検出されません。また、カスタム機能を引き続きレポートで使用する場合は、カスタム アセンブリを新しいインストール フォルダーに手動で移動する必要があります。<br /><br /> これらのアセンブリがレポート サーバーのインストール フォルダーにインストールされている場合、アップグレードの完了後にアセンブリを新しいインストール フォルダーに移動する必要があります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
  
## <a name="see-also"></a>参照  
 [アップグレードに関する&#40;問題の Reporting Services アップグレードアドバイザー&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
