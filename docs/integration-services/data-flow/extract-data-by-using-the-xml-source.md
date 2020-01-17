---
title: XML ソースを使用してデータを抽出する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], XML
- XML source [Integration Services]
ms.assetid: 5d5be54c-2b7e-4957-9193-c5ea5c5d6d15
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f149ca01b71b7611264f28d14532d7827554585f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292540"
---
# <a name="extract-data-by-using-the-xml-source"></a>XML ソースを使用してデータを抽出する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
9. エラー出力を構成するには、 **[エラー出力]** をクリックします。 詳細については、「 [データ フローのデバッグ](../../integration-services/troubleshooting/debugging-data-flow.md)」を参照してください。  
  
10. **[OK]** をクリックします。  
  
11. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [XML ソース](../../integration-services/data-flow/xml-source.md)   
 [Integration Services の変換](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](../../integration-services/data-flow/integration-services-paths.md)   
 [[データ フロー タスク]](../../integration-services/control-flow/data-flow-task.md)  
  
  
