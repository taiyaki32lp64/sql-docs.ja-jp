---
title: カスタム アセンブリをデバッグする方法 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- custom assemblies [Reporting Services], debugging
- debugging custom assemblies [Reporting Services]
- troubleshooting [Reporting Services], custom assemblies
ms.assetid: 3a3215b3-548c-4474-81ba-3a98dd3912bf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1ec4fb2f9d38997c7000e576a36fa8c6c1407e45
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194305"
---
# <a name="how-to-debug-custom-assemblies"></a>カスタム アセンブリをデバッグする方法
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] には、カスタム アセンブリ コードを分析してエラーを探すのに役立ついくつかのデバッグ ツールが用意されています。 どのツールが最適であるかは、何を実行するかによって異なります。 この例では [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]を使用します。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のカスタム アセンブリの設計、開発、およびテストに関して推奨する方法は、テスト レポートおよびカスタム アセンブリを含むソリューションを作成することです。  
  
### <a name="to-debug-assemblies-using-a-single-instance-of-visual-studio"></a>Visual Studio の 1 つのインスタンスを使用してアセンブリをデバッグするには  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] を使用して新しいレポート プロジェクトを作成します。  
  
     [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] でレポート プロジェクトを作成すると、そのプロジェクトを格納するソリューションも作成されます。  
  
2.  新しいクラス ライブラリ プロジェクトを既存のソリューションに追加します。 レポート プロジェクトがスタートアップ プロジェクトとして設定されていることを確認します。 この方法の詳細については、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のマニュアルを参照してください。  
  
3.  ソリューション エクスプローラーで、ソリューションを選択します。  
  
4.  **[表示]** メニューの **[プロパティ ページ]** をクリックします。  
  
     **[ソリューション プロパティ ページ]** ダイアログ ボックスが開きます。  
  
5.  必要に応じて、左側のペインで **[共通プロパティ]** を展開し、 **[プロジェクトの依存関係]** をクリックします。 **[プロジェクト]** ドロップダウン リストからレポート プロジェクトを選択します。 **[依存先]** の一覧でアセンブリ プロジェクトを選択します。  
  
6.  **[OK]** をクリックして変更内容を保存し、 **[プロパティ ページ]** ダイアログを閉じます。  
  
7.  ソリューション エクスプローラーで、カスタム アセンブリ プロジェクトを選択します。  
  
8.  **[表示]** メニューの **[プロパティ ページ]** をクリックします。  
  
     **[プロジェクト プロパティ ページ]** ダイアログ ボックスが開きます。  
  
9. C# プロジェクトの場合は **[ビルド]** タブをクリックし、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] プロジェクトの場合は **[コンパイル]** タブをクリックします。  
  
10. **[ビルド]** / **[コンパイル]** ページで、レポート デザイナー フォルダーへのパスを入力します。 既定では、 **[出力パス]** テキスト ボックスの C:\Program Files\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE になります。 これにより、レポートの実行前に、更新されたカスタム アセンブリのバージョンがレポート デザイナーに直接構築、配置されます。  
  
11. レポートを設計してカスタム アセンブリを開発したら、カスタム アセンブリ コードにブレークポイントを設定します。  
  
12. F5 キーを押して、 **[DebugLocal]** モードでレポートを実行します。 ポップアップ プレビュー ウィンドウでレポートを実行すると、デバッガーはアセンブリの実行可能コードに対応するブレークポイントに到達します。 F11&lt;/localizedText&gt; キーを使用して、カスタム アセンブリ コードを実行します。  
  
### <a name="to-debug-assemblies-using-two-instances-of-visual-studio"></a>Visual Studio の 2 つのインスタンスを使用してアセンブリをデバッグするには  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] を起動して、カスタム アセンブリ プロジェクトを開きます。  
  
2.  プロジェクトを構築し、カスタム アセンブリと付随する .pdb ファイルをレポート デザイナーに配置します。 配置の詳細については、「[カスタム アセンブリの配置](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)」を参照してください。  
  
3.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の別のインスタンスでカスタム アセンブリ コードを開いた状態で、カスタム アセンブリを使用するレポート プロジェクトを開きます。  
  
4.  カスタム アセンブリ プロジェクトを含む [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のインスタンスに移動し、コードに複数のブレークポイントを設定します。  
  
5.  カスタム アセンブリ プロジェクトのウィンドウを開いたまま、 **[デバッグ]** メニューの **[プロセスにアタッチ]** をクリックします。  
  
     **[プロセスにアタッチ]** ダイアログが開きます。  
  
6.  プロセスの一覧から、レポート プロジェクトに対応する devenv.exe プロセスを選択して、 **[アタッチ]** をクリックします。  
  
7.  カスタム アセンブリのレポートで使用する式を定義し、レポートを設計します。  
  
8.  レポートの設計が完了したら、 **[プレビュー]** タブをクリックします。  
  
     レポートが実行され、カスタム アセンブリ コードが定義済みのブレークポイントで停止します。  
  
    > [!NOTE]  
    >  **[プレビュー]** タブを使用すると、アセンブリのコード アクセス許可が適用されません。 コード アクセス セキュリティのエラーを含む完全なテストを行う場合は、 **[DebugLocal]** 構成設定のレポート プロジェクトを開始します。  
  
9. F11 キーを使用してコードを実行します。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] を使用したデバッグの詳細については、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のドキュメントを参照してください。  
  
## <a name="see-also"></a>参照  
 [レポートでのカスタム アセンブリの使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
