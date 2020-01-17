---
title: '[プロパティ ページ] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rpt.rptdesigner.projectpropertypages.general.f1
helpviewer_keywords:
- Project Property Pages dialog box
ms.assetid: 209d9e22-37fc-418f-8739-83adcf447d3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a9d66e6e5317bef72be6bba254ccca0cc82aa026
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100038"
---
# <a name="project-property-pages-dialog-box"></a>[プロパティ ページ] ダイアログ ボックス
  プロジェクトのプロパティ ページを使用すると、レポート サーバー プロジェクトの配置プロパティを構成できます。 このダイアログ ボックスを開くには、 **[プロジェクト]** メニューの _[\<レポート プロジェクト名>_ **のプロパティ]** をクリックします。  
  
 構成プロパティを定義した後は、ツール バーの **[ソリューション構成]** ボックスの一覧から構成を選択できるようになります。  
  
## <a name="options"></a>および  
 **Configuration**  
 編集する構成を選択します。 最初に、次の構成を使用できます。**デバッグ**、 **DebugLocal**、および**リリース**します。 アクティブな構成が、 **Active(Debug)** のように最初に表示されます。  
  
 複数の構成のプロパティを同時に表示するには、 **[すべての構成]** または **[複数の構成]** を選択します。  
  
 新しく構成を作成するには、ツール バーの **[構成マネージャー]** をクリックします。  
  
 **[構成マネージャー]**  
 ソリューション全体の構成を管理するか、さらに構成を追加します。 詳細については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のドキュメントを参照してください。  
  
 **[OutputPath]**  
 ビルドの検証、配置、およびレポートのプレビューで使用されるレポート定義の保存先のパスを入力するか、貼り付けます。 このパスは、プロジェクトに使用するパス、およびプロジェクトのパスの下にある子フォルダーの相対パスとは異なる必要があります。  
  
> [!NOTE]  
>  複数の構成を使用して、実行するタスクに応じてパスを切り替えることができます。  
  
 **[ErrorLevel]**  
 エラーとしてレポートされるビルドの問題の重大度を入力します。 **[ErrorLevel]** の値以下の重大度レベルを持つ問題は、エラーとしてレポートされます。それ以外の問題は、警告としてレポートされます。 エラーが発生すると、ビルド タスクが失敗する原因になります。 有効な重大度レベルは、0 ～ 4 の範囲です。 既定値は 2 です。  
  
 **[StartItem]**  
 プロジェクトがレポート サーバーにパブリッシュされた後に Web ブラウザーに表示されるレポート、またはローカルでプロジェクトを実行するときにプレビュー ウィンドウに表示されるレポートを選択します。 開始アイテムは、プロジェクトをビルドしても配置しない構成の場合、および **[Debug]** コマンド (**F5**) を使用する場合に必要となります。 このアイテムは、プロジェクトを配置する構成では必須です。  
  
 **[OverwriteDataSources]**  
 レポートのパブリッシュ時に、サーバー上のデータ ソースをプロジェクト内のデータ ソースで上書きする場合は、 **[True]** を選択します。 サーバー上の既存のデータ ソースを残す場合は、 **[False]** を選択します。  
  
 **[TargetServerVersion]**  
 いずれかを選択、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]または[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]版[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]または選択**バージョンの検出**によって識別されるサーバーにインストールされているバージョンを自動的に決定する、 **TargetServer URL**プロパティ。 既定値は**SQL Server 2008 R2**します。  
  
 **[TargetDataSourceFolder]**  
 パブリッシュした共有データ ソースを保存するフォルダーの名前です。 フォルダーを指定しない場合、レポートと同じフォルダーにデータ ソースがパブリッシュされます。 フォルダーがレポート サーバー上に存在しない場合は、レポートのパブリッシュ時に、レポート デザイナーによってフォルダーが作成されます。  
  
 ネイティブ モードで実行されているレポート サーバーにパブリッシュする場合は、フォルダー階層の完全なパスをルートから指定します。 たとえば、「Folder1/Folder2/Folder3」のように指定します。  
  
 SharePoint 統合モードで実行されているレポート サーバーにパブリッシュする場合は、SharePoint ライブラリの URL を指定します。 たとえば、 http:// *\<servername >/\<サイト >*  //documents/MyFolder します。  
  
 **[TargetReportFolder]**  
 パブリッシュしたレポートを保存するフォルダーの名前です。 既定値は、レポート プロジェクトの名前です。 フォルダーがレポート サーバー上に存在しない場合は、レポートのパブリッシュ時に、レポート デザイナーによってフォルダーが作成されます。  
  
 ネイティブ モードで実行されているレポート サーバーにパブリッシュする場合は、フォルダー階層の完全なパスをルートから指定します。 フォルダーが別の場所に存在する場合は、フォルダーへのパスをルートから指定します。たとえば、「Folder1/Folder2/Folder3」のように指定します。  
  
 SharePoint 統合モードで実行されているレポート サーバーにパブリッシュする場合は、SharePoint ライブラリの URL を指定します。 たとえば、 http:// *\<servername >* / *\<サイト >*  //documents/MyFolder します。  
  
 **[TargetServerURL]**  
 対象レポート サーバーの URL です。 レポートをパブリッシュする前に、このプロパティを有効なレポート サーバーの URL に設定する必要があります。  
  
 ネイティブ モードで実行されているレポート サーバーにパブリッシュする場合は、レポート サーバーの仮想ディレクトリの URL を指定します。 たとえば、 http://\<server >/reportserver です。 これは、レポート マネージャーではなく、レポート サーバーの仮想ディレクトリです。 既定では、レポート サーバーは、"reportserver" という名前の仮想ディレクトリにインストールされます。  
  
 SharePoint 統合モードで動作しているレポート サーバーにパブリッシュする場合は、SharePoint トップレベル サイトまたはサブサイトの URL を使用します。 サイトを指定しなかった場合は、既定のトップレベル サイトが使用されます。 たとえば、 http://\<*servername >* 、 http://&lt*servername*/\<*サイト >* または http://\< *servername >* /\<*サイト >* /\<*サブサイト >* します。  
  
## <a name="see-also"></a>関連項目  
 [レポートのパブリッシュ](../publish-reports.md)   
 [SharePoint ライブラリへのレポートのパブリッシュ](../reports/publish-a-report-to-a-sharepoint-library.md)   
 [配置プロパティを設定する (Reporting Services)](set-deployment-properties-reporting-services.md)   
 [レポート デザイナーの F1 ヘルプ](report-designer-f1-help.md)  
  
  
