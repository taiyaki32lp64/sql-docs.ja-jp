---
title: ライセンス条項に同意 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- license terms
helpviewer_keywords:
- Registration Information page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Registration Information page
ms.assetid: 08dd739d-5817-4418-bcff-74ab7f8bbd33
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99418b11eecdb3077e3def746eae56e43bab2d60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096834"
---
# <a name="accept-license-terms"></a>使用許諾条件への同意
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードの **[使用許諾条件への同意]** ページを使用して、このリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の使用許諾条件に同意します。  
  
 使用許諾契約書を印刷することも、クリップボードにコピーすることもできます。 処理を続行するには、使用許諾条件に同意し、 **[次へ]** をクリックします。 インストールしない場合は、 **[キャンセル]** をクリックします。  
  
## <a name="customer-experience-improvement-program-ceip"></a>カスタマー エクスペリエンス向上プログラム (CEIP)  
 CEIP のレポートを有効にすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[msCoName](../../includes/msconame-md.md)] に定期的にレポートを送信するように構成されます。 レポートには、ハードウェア構成に関する情報と、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] およびコンポーネントがどのように使用されているかを示す情報が含められます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、機能の使用状況データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能強化のために使用します。 この機能によって関しされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントは次のとおりです。  
  
-   、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   レプリケーション  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ  
  
 機能の使用に関する情報は [!INCLUDE[msCoName](../../includes/msconame-md.md)]に送信され、アクセスが制限された場所に格納されます。  
  
 セットアップの完了後、CEIP のレポートを無効にするには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **[構成ツール]** メニューにある **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーと使用状況レポート]** ツールを使用します。  
  
 インストール、アップグレード、修復などのセットアップ操作では、セットアップ プログラムの実行時にのみ情報が収集されアップロードされます。  
  
 他のすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントでは、情報はすべての有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで 1 日 1 回収集されます。 既定の収集時刻は、サーバーにかかる負荷を最小限に抑えるため、午前 0 時に設定されています。 収集時刻を変更する場合は、収集時刻を制御するレジストリ キーを手動で編集します。 各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスには、次のような専用のレジストリ キーがあります。  
  
 HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<INSTANCEID>\CPE\TimeofReporting  
  
 このレジストリ キーの値には、収集を実行する時刻が 00:00 (午前 0 時) から何分後であるかが示されています。 たとえば、値が 60 の場合は収集が午前 1 時に実行され、1200 の場合は午後 8 時に実行されます。  
  
## <a name="error-reporting"></a>[エラー報告]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に関する機能のエラーと使用状況のレポート機能を有効にするには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードの **[エラーと使用状況レポートの設定]** ページを使用します。  
  
### <a name="options"></a>および  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定では、機能の使用状況データ収集およびエラー レポート機能は、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] とそのコンポーネントで無効になっています。  
  
 [エラー報告]  
 エラー レポート機能を有効にすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は次の [!INCLUDE[msCoName](../../includes/msconame-md.md)] コンポーネントに重大なエラーが発生した場合に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に自動的にレポートを送信するように構成されます。  
  
-   、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   レプリケーション  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] はエラー レポートを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能の強化に使用し、すべての情報を機密情報として扱います。  
  
 エラーに関する情報はセキュリティで保護された接続 (https) を経由して [!INCLUDE[msCoName](../../includes/msconame-md.md)]に送信され、情報はアクセスが制限された場所に格納されます。 また、エラー レポートを独自の企業内エラー報告サーバーに送信することもできます。  
  
 エラー レポートには次の情報が含まれます。  
  
-   問題発生時の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の状態。  
  
-   オペレーティング システムのバージョンとコンピューター ハードウェアの情報。  
  
-   ライセンスの識別に使用されないデジタル プロダクト ID。  
  
-   コンピューターまたはプロキシ サーバーのネットワーク IP アドレス。  
  
-   エラーの原因となったプロセスのメモリまたはファイルからの情報。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] は、使用者のファイル、名前、住所、電子メール アドレス、またはその他の形式の個人情報を意図的に収集することはありません。 ただし、エラーの原因となったプロセスのメモリまたはファイルに格納されている個人情報が、エラー レポートとして送信される場合もあります。 この情報を使用者の ID を判断するために使用できる可能性がありますが、[!INCLUDE[msCoName](../../includes/msconame-md.md)] はこの情報をそのような目的に使用することはありません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプライバシーとデータ収集ポリシーについては、「[Microsoft SQL Server のプライバシーに関する声明](../../../2014/getting-started/microsoft-sql-server-privacy-statement.md)」を参照してください。  
  
 エラー レポートを有効にしている場合に重大なエラーが発生すると、そのエラーに関する [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポート技術情報の記事を示す [!INCLUDE[msCoName](../../includes/msconame-md.md)] からの応答が Windows イベント ログに表示されることがあります。  
  
 セットアップが完了した後で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とそのコンポーネントのすべてのインスタンスについて、エラー レポートと機能の使用状況レポートを無効にするには、 **[エラーと使用状況レポートの設定]** ダイアログ ボックスで、**機能の使用状況レポート**のチェック ボックスをオフにします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のコンポーネント ([!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、および共有コンポーネント) で**エラー レポート**が有効になっている場合は、エラー レポート機能を 1 つのコンポーネントのインスタンスごとに無効にできます。さらに、 **[その他]** と表示されている共有コンポーネントも無効にすることができます。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server の使用許諾条件について](../../../2014/getting-started/about-the-sql-server-license-terms.md)  
  
  
