---
title: データ フロー内でコンポーネントを連結する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 70616a58-8921-4218-85bf-f3e90c5a9dbf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b6033c2d21b10755601f9ef82cabd829db5ad820
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293221"
---
# <a name="connect-components-in-a-data-flow"></a>データ フロー内でコンポーネントを連結する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  この手順は、データ フロー内のコンポーネントの出力を、同じデータ フロー内にある別のコンポーネントに連結する方法について説明します。  
パッケージ内にデータ フローを構築するには、 **デザイナーにある** [データ フロー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブのデザイン画面を使用します。 データ フローにデータ フロー コンポーネントが 2 つ含まれる場合、変換元または変換からの出力を変換または変換先への入力に連結することで、これらのコンポーネントを連結できます。 2 つのデータ フロー コンポーネント間のコネクタは、パスと呼ばれます。  
  
 次の図は、1 つの変換元コンポーネント、2 つの変換、1 つの変換先コンポーネント、およびこれらを連結するパスを持つ、簡単なデータ フローを示しています。  
  
 ![Data flow](../../integration-services/data-flow/media/mw-dts-08.gif "Data flow")  
  
 2 つのコンポーネントを連結したら、パスを移動するデータのメタデータおよびパスのプロパティを、 **[データ フロー パス エディター]** で表示できます。 詳細については、「 [Integration Services のパス](../../integration-services/data-flow/integration-services-paths.md)」を参照してください。  
  
 また、データ ビューアーをパスに追加することもできます。 データ ビューアーを使用すると、パッケージの実行時にデータ フロー コンポーネント間を移動するデータを表示できます。  
  
### <a name="connect-components-in-a-data-flow"></a>データ フロー内でコンポーネントを連結する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックし、コンポーネントを連結するデータ フローが含まれているデータ フロー タスクをダブルクリックします。  
  
4.  **[データ フロー]** タブのデザイン画面で、連結する変換または変換元を選択します。  
  
5.  変換または変換元の出力を表す緑の矢印を、変換または変換先にドラッグします。 一部のデータ フロー コンポーネントはエラー出力をとり、同様の方法で連結できます。  
  
    > [!NOTE]  
    >  一部のデータ フロー コンポーネントには複数の出力があります。これらの各出力は、それぞれ個別の変換または変換先に連結できます。  
  
6.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [データ フローでコンポーネントを追加または削除する](../../integration-services/data-flow/add-or-delete-a-component-in-a-data-flow.md)   
 [データ フローのデバッグ](../../integration-services/troubleshooting/debugging-data-flow.md) [データ フロー](../../integration-services/data-flow/data-flow.md)  
  
  
