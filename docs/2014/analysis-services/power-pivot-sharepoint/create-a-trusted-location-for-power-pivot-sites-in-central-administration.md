---
title: サーバーの全体管理で PowerPivot サイト用の信頼できる場所を作成する |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a666f365-cd93-43a3-9d3d-e429dfc19b66
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c5dd66b72ff280431d29ae292af8fa1402095dc
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74684084"
---
# <a name="create-a-trusted-location-for-powerpivot-sites-in-central-administration"></a>サーバーの全体管理での PowerPivot サイト用の信頼できる場所の作成
  Excel Services では、SharePoint サーバーで開いたブックの有効なリポジトリの場所を指定できます。 これは「信頼できる場所」と呼ばれ、作成したそれぞれの信頼できる場所について異なる構成設定を使用できます。 PowerPivot for SharePoint の配置の場合、PowerPivot ブックが含まれるサイト用に信頼できる場所を作成し、ファームのその他の部分に対する既定値を保持しながら PowerPivot データ アクセスに対しては最適な設定を適用することを検討してください。  
  
  
  
## <a name="prerequisites"></a>前提条件  
 URL を信頼できる場所として指定するには、ファームまたはサービスの管理者である必要があります。  
  
 PowerPivot ギャラリー、またはブックが保存されている他のライブラリが含まれる SharePoint サイトの URL アドレスがわかっていることが必要です。 アドレスを取得するには、ライブラリが含まれているサイトを開き、[ **PowerPivot ギャラリー**] を右クリックします。次に、[**プロパティ**] を選択し、サーバー名とサイトパスを含むアドレス (URL) の最初の部分をコピーします。  
  
##  <a name="overview"></a>概要  
 Excel Services の最初のインストールでは、'http://' が信頼できる場所として指定されます。このため、ファームのどのサイトからアクセスしたブックもサーバーで開くことができます。 信頼できると見なされる場所の制御を厳しくする必要がある場合は、ファームの特定のサイトにマップする信頼できる場所を新しく作成し、各場所の設定とアクセス許可を変更します。  
  
 PowerPivot ブックをホストするサイト用に新しい信頼できる場所を作成すると、ファームのその他の部分に対する既定値を保持しながら PowerPivot データ アクセスに対しては最適な別の設定を適用する場合に特に便利です。 たとえば、PowerPivot ブック用に最適化された信頼できる場所で最大ブック サイズを 50 MB にし、ファームの残りで既定値の 10 MB を使用するように設定できます。  
  
 PowerPivot ギャラリー ライブラリを使用してパブリッシュ済みのブックをプレビューする場合に、予想したプレビュー イメージの代わりにデータ更新の警告が表示されるときは、信頼できる場所を作成することをお勧めします。 PowerPivot ギャラリーは、ドキュメント内のデータおよび表示情報を使用して、レポートとブックのサムネイル画像を表示します。 信頼できる場所で [データ更新に関する警告を表示する] が有効である場合は、PowerPivot ギャラリーに更新を実行するための十分な権限がなく、その結果、サムネイル画像の代わりにエラーが表示されることがあります。 PowerPivot ギャラリーを新しい信頼できる場所に持つサイトを追加すると、この問題は解消できます。  
  
##  <a name="create"></a>PowerPivot データアクセス用の信頼できる場所を作成する  
  
1.  サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  Excel Services サービス アプリケーションをクリックします。  
  
3.  
  **[信頼できるファイル保存場所]** をクリックします。  
  
4.  
  **[信頼できるファイル保存場所の追加]** をクリックします。  
  
5.  PowerPivot ギャラリー ライブラリがあるサイトの URL を入力します。  
  
6.  [場所の種類] で、 **[Microsoft SharePoint Foundation]** を選択します。  
  
    > [!IMPORTANT]  
    >  UNC および HTTP の場所の種類は PowerPivot データ アクセスではサポートされていません。  
  
7.  [セッションの管理]、[ブックのプロパティ]、および [計算動作] のプロパティの既定の設定をすべてそのまま使用します。  
  
8.  [ブックのプロパティ] で、 **[ブックの最大サイズ]** を「 **50**」に設定します。 これにより、ブックのファイル サイズの上限が、親 Web アプリケーションへのファイル アップロードの上限と同じになります。 ブックのサイズが 50 MB を超える場合は、ファイル サイズの上限をさらに増やす必要があります。 詳細については、「 [PowerPivot for SharePoint&#41;&#40;最大ファイルアップロードサイズを構成する](configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)」を参照してください。  
  
9. [外部データ] で、[外部データの許可] が **[信頼できるデータ接続ライブラリと、埋め込まれている接続]** に設定されていることを確認します。 この設定は、ブックでの PowerPivot データ アクセスに必要です。  
  
10. また、[外部データ] の [更新時の警告] で、 **[更新時の警告の有効化]** のチェック ボックスをオフにします。 このチェック ボックスをオフにすると、PowerPivot ギャラリーで、定型の警告メッセージの代わりにブックのプレビュー イメージが表示されるようになります。  
  
11. [**OK**] をクリックすると、  
  
## <a name="see-also"></a>参照  
 [PowerPivot ギャラリー](../../2014-toc/index.yml)  
 [PowerPivot ギャラリーの作成とカスタマイズ](create-and-customize-power-pivot-gallery.md)   
 [PowerPivot ギャラリーの使用](use-power-pivot-gallery.md)  
  
  
