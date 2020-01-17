---
title: XML ソースを使用してデータを抽出する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], XML
- XML source [Integration Services]
ms.assetid: 5d5be54c-2b7e-4957-9193-c5ea5c5d6d15
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3c7a9b107a05b0645f2286f534f457d46a1b6f11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771098"
---
# <a name="extract-data-by-using-the-xml-source"></a>XML ソースを使用してデータを抽出する
  XML ソースを追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクがあらかじめ含まれている必要があります。  
  
### <a name="to-extract-data-using-an-xml-source"></a>XML ソースを使用してデータを抽出するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、XML ソースをデザイン画面にドラッグします。  
  
4.  XML ソースをダブルクリックします。  
  
5.  **[XML ソース エディター]** の **[接続マネージャー]** ページで、データ アクセス モードを次のうちから選択します。  
  
    -   **[XML ファイルの場所]** アクセス モードでは、 **[参照]** をクリックし、XML ファイルが含まれるフォルダーを探します。  
  
    -   **[変数からの XML ファイル]** アクセス モードでは、XML ファイルのパスが含まれるユーザー定義変数を選択します。  
  
    -   **[変数からの XML データ]** アクセス モードでは、XML データが含まれるユーザー定義変数を選択します。  
  
    > [!NOTE]  
    >  変数は、XML ソースが含まれるデータ フロー タスクのスコープ内、またはパッケージのスコープ内で定義する必要があります。また、変数は文字列データ型である必要があります。  
  
6.  必要に応じて、 **[インライン スキーマを使用する]** を選択し、スキーマ情報が含まれる XML ドキュメントを指定します。  
  
7.  XML ファイルに対して、外部の XML Schema Definition Language (XSD) スキーマを指定するには、次のいずれかの操作を行います。  
  
    -   **[参照]** をクリックして既存の XSD ファイルを探します。  
  
    -   **[XSD の生成]** をクリックして、XML ファイルから XSD を作成します。  
  
8.  出力列の名前を更新するには、 **[列]** をクリックし、 **[出力列]** 一覧の値を編集します。  
  
9. エラー出力を構成するには、 **[エラー出力]** をクリックします。 詳細については、「 [データ フロー コンポーネントでエラー出力を構成する](../configure-an-error-output-in-a-data-flow-component.md)」を参照してください。  
  
10. **[OK]** をクリックします。  
  
11. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [XML ソース](xml-source.md)   
 [Integration Services の変換](transformations/integration-services-transformations.md)   
 [Integration Services のパス](integration-services-paths.md)   
 [[データ フロー タスク]](../control-flow/data-flow-task.md)  
  
  
