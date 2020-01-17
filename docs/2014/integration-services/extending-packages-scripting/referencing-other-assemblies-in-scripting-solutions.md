---
title: スクリプティング ソリューションでの他のアセンブリの参照 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, .NET Framework
- Script task [Integration Services], adding references
- referencing custom assemblies
- SSIS Script task, VisualBasic namespace
- assemblies [Integration Services]
- VisualBasic namespace
- Script task [Integration Services], VisualBasic namespace
- Microsoft.VisualBasic namespace
- Script task [Integration Services], .NET Framework
- .NET Framework [Integration Services]
- referencing Web services
ms.assetid: 9b655bcd-19f6-43d8-9f89-1b4d299c6380
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a6f942e1afe40467e331519f276b360f87f9a6da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62894736"
---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>スクリプティング ソリューションでの他のアセンブリの参照
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] クラス ライブラリには、スクリプトの開発者が [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージにカスタム機能を実装するための強力なツール セットが用意されています。 スクリプト タスクとスクリプト コンポーネントでは、カスタム マネージド アセンブリも使用できます。  
  
> [!NOTE]  
>  Web サービスのオブジェクトやメソッドをパッケージで使用できるようにするには、[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) の **[Web 参照の追加]** コマンドを使用します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の以前のバージョンでは、Web サービスを使用するためにプロキシ クラスを生成する必要がありました。  
  
## <a name="using-a-managed-assembly"></a>マネージド アセンブリの使用  
 デザイン時に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によってマネージド アセンブリが検出されるようにするには、次の手順を実行する必要があります。  
  
1.  マネージド アセンブリをコンピューター上の任意のフォルダーに格納します。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の以前のバージョンで追加できたのは、%windir%\Microsoft.NET\Framework\vx.x.xxxxx フォルダーか %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies フォルダーにあるマネージド アセンブリへの参照のみでした。  
  
2.  マネージド アセンブリへの参照を追加します。  
  
     参照を追加するには、VSTA の **[参照の追加]** ダイアログ ボックスにある **[参照]** タブで、マネージド アセンブリを探して追加します。  
  
 実行時に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によってマネージド アセンブリが検出されるようにするには、次の手順を実行する必要があります。  
  
1.  マネージド アセンブリに厳密な名前で署名します。  
  
2.  パッケージが実行されるコンピューターのグローバル アセンブリ キャッシュに、そのアセンブリをインストールします。  
  
     詳細については、「[カスタム オブジェクトのビルド、配置、デバッグ](../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)」を参照してください。  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Microsoft .NET Framework クラス ライブラリの使用  
 スクリプト タスクおよびスクリプト コンポーネントは、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] クラス ライブラリによって公開されている他のすべてのオブジェクトおよび機能を利用することができます。 たとえば、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] を使用すると、ユーザーの環境に関する情報を取得し、パッケージを実行中のコンピューターとやり取りできます。  
  
 使用頻度の高い [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] クラスを次に示します。  
  
-   `System.Data` ADO.NET のアーキテクチャが含まれています。  
  
-   `System.IO` ファイル システムとストリームへのインターフェイスを提供します。  
  
-   `System.Windows.Forms` フォームの作成を提供します。  
  
-   `System.Text.RegularExpressions` 正規表現を操作するためのクラスを提供します。  
  
-   `System.Environment` ローカル コンピューターでは、現在のユーザーおよびコンピューターとユーザー設定に関する情報を返します。  
  
-   `System.Net` ネットワーク通信を提供します。  
  
-   `System.DirectoryServices` Active Directory を公開します。  
  
-   `System.Drawing` 広範な画像操作ライブラリを提供します。  
  
-   `System.Threading` マルチ スレッド プログラミングを有効にします。  
  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の詳細については、MSDN ライブラリを参照してください。  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [スクリプトによるパッケージの拡張](extending-packages-with-scripting.md)  
  
  
