---
title: リモート パーティション - 詳細設定 ダイアログ ボックス (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.advancedrestoresettings.f1
ms.assetid: a03bb7e1-efaf-47c8-b0ee-f3e4438311cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1ca3f12ff53c4291d8bbe7c8eb97ce8e47172ea3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070378"
---
# <a name="remote-partitions---advanced-settings-dialog-box-analysis-services---multidimensional-data"></a>[リモート パーティション - 詳細設定] ダイアログ ボックス (Analysis Services - 多次元データ)
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] で **[リモート パーティション - 詳細設定]** ダイアログ ボックスを使用すると、 **[データベースの復元]** ダイアログ ボックスでリモート バックアップ ファイルから [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースへリモート パーティションを復元する際に、リモート パーティションを維持するリモート [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースを表すデータ ソースの接続文字列などの詳細設定を編集できます。 **[リモート パーティション - 詳細設定]** ダイアログ ボックスを表示するには、 **[データベースの復元]** ダイアログ ボックスの **[パーティション]** ページで **[リモート パーティションを復元する]** オプションを選択した後、リモート パーティションの参照ボタン ( **[...]** ) をクリックします。  
  
## <a name="options"></a>および  
  
|項目|定義|  
|----------|----------------|  
|**[データ ソース名]**|一覧表示されたリモート パーティションを管理するリモート [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースを表すデータ ソースの名前を表示します。|  
|**[バックアップ ファイル]**|一覧表示されたリモート パーティションに対して復元されるデータを含むリモート バックアップ ファイルの名前を表示します。<br /><br /> 注:リモート バックアップ ファイルが指定されている場合にバックアップ ファイルが表示されない、**バックアップ ファイル**列に、**パーティション**のページ、 **Restore Database**  ダイアログ ボックス。|  
|**[接続文字列]**|**[データ ソース名]** に表示されているデータ ソースの接続文字列を表示します。|  
|**[編集]**|**データ リンク プロパティ** のダイアログ ボックスを表示し、接続文字列に含まれるプロパティを編集します。|  
|**パーティションの一覧**|リモート パーティションの復元先となる別の場所を指定します。 キューブ内のリモート パーティションに既定以外の場所を指定していた場合、リモート パーティションの復元フォルダーのみを変更できます。 各リモート パーティションに対して復元フォルダーを指定するには、このオプションが選択されている場合に有効となる次のグリッドを使用します。<br /><br /> **[キューブ]** :リモート パーティションを含むキューブの名前を表示します。<br /><br /> **[MeasureGroup]** :リモート パーティションを含むメジャー グループの名前を表示します。<br /><br /> **[パーティション]** :リモート パーティションの名前を表示します。<br /><br /> **[サイズ (MB)]** :リモート パーティションのサイズを MB 単位で表示します。<br /><br /> **[元のフォルダー]** :リモート パーティションが格納されていた元のフォルダーの名前を表示します。<br /><br /> **[復元フォルダー]** :リモート パーティションの復元フォルダーの名前を入力するか、参照ボタン ( **[...]** ) をクリックして **[リモート フォルダーの参照]** ダイアログ ボックスで使用するフォルダーのパスを選択します。 **[リモート フォルダーの参照]** ダイアログ ボックスの詳細については、「[[リモート フォルダーの参照] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [Analysis Services のデザイナーおよびダイアログ ボックス&#40;多次元データ&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [パーティション&#40;データベースの復元 ダイアログ ボックス&#41; &#40;Analysis Services - 多次元データ&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Analysis Services データベースのバックアップと復元](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
