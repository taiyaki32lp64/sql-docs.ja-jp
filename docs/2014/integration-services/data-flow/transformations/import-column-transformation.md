---
title: 列インポート変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.importcolumntrans.f1
helpviewer_keywords:
- Import Column transformation [Integration Services]
- columns [Integration Services], importing
- importing data, SSIS packages
- inserting data
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 13deb9b423ce20fd77e0853cba9d0f205905ca44
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770408"
---
# <a name="import-column-transformation"></a>列インポート変換
  列インポート変換は、ファイルのデータを読み取り、そのデータをデータ フローの列に追加します。 この変換を使用すると、パッケージは、別々のファイルに格納されているテキストや画像を 1 つのデータ フローに追加できます。 たとえば、製品情報を保存するテーブルにデータを読み込むデータ フローに列インポート変換を含めると、各製品に対する顧客評価をファイルからインポートし、データ フローに追加できます。  
  
 列インポート変換は、次の方法で構成できます。  
  
-   データを追加する列を指定します。  
  
-   バイト順マーク (BOM) が必要かどうかを指定します。  
  
    > [!NOTE]  
    >  BOM が必要になるのは、データが DT_NTEXT データ型の場合だけです。  
  
 変換入力の列には、データを保持するファイル名が含まれます。 データセットの各行には、異なるファイルを指定できます。 列インポート変換が行を処理すると、ファイル名を読み取り、ファイル システム内の対応するファイルを開き、ファイルの内容を出力列に読み込みます。 出力列のデータ型は、DT_TEXT、DT_NTEXT、または DT_IMAGE 型である必要があります。 詳細については、「 [Integration Services Data Types](../integration-services-data-types.md)」を参照してください。  
  
 この変換は、1 つの入力、1 つの出力、および 1 つのエラー出力をとります。  
  
## <a name="configuration-of-the-import-column-transformation"></a>列インポート変換の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 このコンポーネントのプロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [列エクスポート変換](export-column-transformation.md)   
 [データ フロー](../data-flow.md)   
 [Integration Services の変換](integration-services-transformations.md)  
  
  
