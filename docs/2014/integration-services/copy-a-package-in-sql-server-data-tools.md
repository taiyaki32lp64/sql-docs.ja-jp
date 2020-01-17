---
title: SQL Server Data Tools でのパッケージのコピー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 673b69ea632108b889cc2f99b63c9c602ef05237
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829546"
---
# <a name="copy-a-package-in-sql-server-data-tools"></a>SQL Server Data Tools でのパッケージのコピー
  このトピックでは、既存のパッケージをコピーして新しい [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを作成する方法、および新しいパッケージの `Name` プロパティと `GUID` プロパティを更新する方法について説明します。  
  
### <a name="to-copy-a-package"></a>パッケージをコピーするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、コピーするパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックします。  
  
3.  コピーするパッケージがソリューション エクスプローラーで選択されていること、またはパッケージが含まれている SSIS デザイナーのタブがアクティブになっていることを確認します。  
  
4.  **[ファイル]** メニューの **[名前を付けて \<パッケージ名> を保存]** をクリックします。  
  
    > [!NOTE]  
    >  **[ファイル]** メニューに **[名前を付けて保存]** オプションを表示するには、SSIS デザイナーでパッケージを開いておく必要があります。  
  
5.  必要に応じて、別のフォルダーを参照します。  
  
6.  パッケージ ファイルの名前を更新します。 ファイル拡張子は、必ず .dtsx のままにしておきます。  
  
7.  **[保存]** をクリックします。  
  
8.  プロンプトで、パッケージ オブジェクトの名前をファイル名と一致するように更新するかどうかを選択します。 クリックすると**はい**、`Name`パッケージのプロパティを更新します。 新しいパッケージが [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトに追加され、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで開かれます。  
  
9. 必要に応じて、 **[制御フロー]** タブの背景をクリックし、 **[プロパティ]** をクリックします。  
  
10. プロパティ ウィンドウで、ID プロパティの値をクリックし、ドロップダウン リストの **[\<新しい ID の生成>]** をクリックします。  
  
11. **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックし、新しいパッケージを保存します。  
  
## <a name="see-also"></a>関連項目  
 [パッケージのコピーを保存する](../../2014/integration-services/save-a-copy-of-a-package.md)   
 [SQL Server データ ツールでのパッケージの作成](create-packages-in-sql-server-data-tools.md)   
 [Integration Services &#40;SSIS&#41; パッケージ](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
