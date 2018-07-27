---
title: Data Profile Viewer | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], output viewer
ms.assetid: b9043428-ce26-45bb-910c-588d07579565
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8a869a295b1a1a5f039a7f0e7ead5a93fa9b4e6b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306222"
---
# <a name="data-profile-viewer"></a>Data Profile Viewer (Data Profile Viewer)
  データのプロファイル処理では、次に、データ プロファイルを表示して分析します。 このプロファイルは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ内でデータ プロファイル タスクを実行してデータ プロファイルを計算した後に表示できます。 データ プロファイル タスクの設定方法および実行方法の詳細については、「 [データ プロファイル タスクのセットアップ](data-profiling-task.md)」をご覧ください。  
  
> [!IMPORTANT]  
>  出力ファイルには、データベースに関する機密データやデータベースに格納されているデータが含まれる場合があります。 このファイルの安全性を高める方法の推奨事項については、「 [パッケージで使用されるファイルへのアクセス](../access-to-files-used-by-packages.md)」をご覧ください。  
  
## <a name="data-profiles"></a>データ プロファイル  
 データ プロファイルを表示するには、出力をファイルに送信するようにデータ プロファイル タスクを構成し、スタンドアロンの Data Profile Viewer を使用します。 Data Profile Viewer を開くには、次のいずれかの操作を行います。  
  
-   **デザイナーの** [データ プロファイル] [!INCLUDE[ssIS](../../includes/ssis-md.md)] でタスクを右クリックし、 **[編集]** をクリックします。 **データ プロファイル タスク エディター** の **[全般]** ページで、 **[プロファイル ビューアーを開く]** をクリックします。  
  
-   *\<ドライブ>*:\Program Files (x86) | Program Files\Microsoft SQL Server\110\DTS\Binn フォルダーの DataProfileViewer.exe を実行します。  
  
 このビューアーでは、複数のペインを使用して、要求したプロファイルと計算結果が表示されます。また、詳細情報を表示するための機能やドリル ダウン機能をオプションで使用できます。  
  
 **[プロファイル]** ペイン  
 **[プロファイル]** ペインには、データ プロファイル タスクで要求されたプロファイルが表示されます。 **[プロファイル]** ペインでプロファイルを選択すると、プロファイルの計算結果がビューアーの他のペインに表示されます。  
  
 **[結果]** ペイン  
 **[結果]** ペインでは、プロファイルの計算結果が 1 行にまとめられます。 たとえば、 **[列長分布プロファイル]** を要求すると、この行には最小長、最大長、および行数が表示されます。 ほとんどのプロファイルでは、 **[結果]** ペインでこの行を選択すると、オプションの **[詳細]** ペインに追加の詳細を表示できます。  
  
 **[詳細]** ペイン  
 ほとんどの種類のプロファイルの **[詳細]** ペインには、 **[結果]** ペインで選択したプロファイルの結果に関する追加情報が表示されます。 たとえば、 **[列長分布プロファイル]** を要求すると、 **[詳細]** ペインには検出された各列の長さが表示されます。 また、列の値の長さがこのペインに表示された列の長さである行の数および割合も表示されます。  
  
 複数の列に対して計算される 3 種類のプロファイル (候補キー、機能依存、および値包含) の **[詳細]** ペインには、想定されているリレーションシップの違反が表示されます。 たとえば、[候補キー プロファイル] を要求すると、[詳細] ペインには候補キーの一意性に違反している重複値が表示されます。  
  
 プロファイルの計算に使用したデータ ソースが使用可能な場合、 **[詳細]** ペインの行をダブルクリックすると、 **[ドリル ダウン]** ペインに、一致するデータ行を表示できます。  
  
 **[ドリル ダウン]** ペイン  
 次の条件に当てはまる場合、 **[詳細]** ペインの行をダブルクリックすると、 **[ドリル ダウン]** ペインに、一致するデータ行を表示できます。  
  
-   計算に使用したデータ ソースが利用可能であること。  
  
-   データを表示する権限があること。  
  
 Data Profile Viewer では、ドリル ダウン要求のためのソース データベースへの接続に、Windows 認証と現在のユーザーの資格情報が使用されます。 データ プロファイル タスクを実行したパッケージに格納されている接続情報は使用されません。  
  
> [!IMPORTANT]  
>  Data Profile Viewer に用意されているドリル ダウン機能は、元のデータ ソースにライブ クエリを送信します。 これらのクエリは、サーバーのパフォーマンスに悪影響を及ぼす場合があります。  
>   
>  最近作成されたものではない出力ファイルからドリル ダウンした場合、ドリル ダウン クエリは、元の出力の計算に使用された行セットとは異なる行セットを返す場合があります。  
  
 Data Profile Viewer のユーザー インターフェイスの詳細については、「 [Data Profile Viewer の F1 ヘルプ](../data-profile-viewer-f1-help.md)」をご覧ください。  
  
  