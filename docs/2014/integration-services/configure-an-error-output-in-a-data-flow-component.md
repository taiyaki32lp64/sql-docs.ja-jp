---
title: データ フロー コンポーネントでエラー出力の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- errors [Integration Services], data flow components
- components [Integration Services], data flow
- error outputs [Integration Services]
ms.assetid: 53d7eeea-927d-4b45-8ea9-084e65ad5390
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fa9df7d84a793c6825ba82b22c3b0cf567f42c3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060814"
---
# <a name="configure-an-error-output-in-a-data-flow-component"></a>データ フロー コンポーネントでエラー出力を構成する
  多くのデータ フロー コンポーネントがエラー出力をサポートしており、[!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでエラー出力を構成する方法は、コンポーネントに応じて異なります。 エラー出力の構成以外に、エラー出力の列を構成することもできます。 これには、コンポーネントによって追加される **[ErrorCode]** 列や **[ErrorColumn]** 列の構成が含まれます。  
  
## <a name="configuring-an-error-output"></a>エラー出力の構成  
 エラー出力を構成する場合、2 つのオプションがあります。  
  
-   **[エラー出力の構成]** ダイアログ ボックスを使用します。 このダイアログ ボックスを使用すると、エラー出力をサポートするデータ フロー コンポーネントでエラー出力を構成できます。  
  
-   コンポーネントのエディター ダイアログ ボックスを使用します。 いくつかのコンポーネントでは、エディター ダイアログ ボックスから直接エラー出力を構成できます。 ただし、ADO NET ソース、列インポート変換、OLE DB コマンド変換、または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 変換先のエディター ダイアログ ボックスからはエラー出力を構成できません。  
  
 次の手順では、これらのダイアログ ボックスを使用してエラー出力を構成する方法を説明します。  
  
#### <a name="to-configure-an-error-output-using-the-configure-error-output-dialog-box"></a>[エラー出力の構成] ダイアログ ボックスを使用してエラー出力を構成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーの **[データ フロー]** タブをクリックします。  
  
4.  赤い矢印で表示されているエラー出力を、エラー元のコンポーネントからデータ フローの別のコンポーネントにドラッグします。  
  
5.  **[エラー出力の構成]** ダイアログ ボックスで、コンポーネントの入力の各列について、 **[エラー]** 列および **[切り捨て]** 列のアクションを選択します。  
  
6.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
#### <a name="to-add-an-error-output-using-the-editor-dialog-box-for-the-component"></a>コンポーネントのエディター ダイアログ ボックスを使用してエラー出力を追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーの **[データ フロー]** タブをクリックします。  
  
4.  エラー出力を構成するデータ フロー コンポーネントをダブルクリックし、コンポーネントに応じて、次のいずれかの手順を実行します。  
  
    -   **[エラー出力の構成]** をクリックします。  
  
    -   **[エラー出力]** をクリックします。  
  
5.  各列の **[エラー]** オプションを設定します。  
  
6.  各列の **[切り捨て]** オプションを設定します。  
  
7.  **[OK]** をクリックします。  
  
8.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="configuring-error-output-columns"></a>エラー出力列の構成  
 エラー出力列を構成するには、 **[詳細エディター]** ダイアログ ボックスの **[入力プロパティと出力プロパティ]** タブを使用します。  
  
#### <a name="to-configure-error-output-columns"></a>エラー出力列を構成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーの **[データ フロー]** タブをクリックします。  
  
4.  構成するエラー出力列が含まれているコンポーネントを右クリックし、 **[詳細エディターの表示]** をクリックします。  
  
5.  **[入力プロパティと出力プロパティ]** タブをクリックして、 **[\<コンポーネント名> のエラー出力]** を展開してから **[出力列]** を展開します。  
  
6.  列をクリックして、プロパティを更新します。  
  
    > [!NOTE]  
    >  列の一覧には、コンポーネントの入力列、前のエラー出力で追加された **[ErrorCode]** 列と **[ErrorColumn]** 列、このコンポーネントによって追加された **[ErrorCode]** 列と **[ErrorColumn]** 列が表示されます。  
  
7.  **[OK]** をクリックします。  
  
8.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [データのエラー処理](data-flow/error-handling-in-data.md)  
  
  
