---
title: RAW ファイル ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfilesource.f1
helpviewer_keywords:
- sources [Integration Services], Raw File
- raw data [Integration Services]
- Raw File source
ms.assetid: 5b4daea5-7f76-4674-aa77-0a79f9f97f7d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1bedefd277f1be7f44d807e6539097dd24f5ab2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900912"
---
# <a name="raw-file-source"></a>RAW ファイル ソース (Raw File source)
  RAW ファイル ソースは、ファイルから生データを読み取ります。 データはソース ファイル固有の方法で表示されるため、変換の必要がなく、ほとんどの場合は解析の必要もありません。 したがって、RAW ファイル ソースは、フラット ファイルや OLE DB などの他のソースよりも、高速にデータを読み取ることができます。  
  
 RAW ファイル ソースは、以前 RAW ファイルの変換先に記述された生データを取得するために使用されます。 また、RAW ファイル ソースの参照先を、列のみを含む空の RAW ファイル (メタデータのみのファイル) にすることもできます。 パッケージを実行せずにメタデータのみのファイルを生成するには、RAW ファイル変換先を使用します。 詳細については、「 [RAW ファイル変換先](raw-file-destination.md)」を参照してください。  
  
 RAW ファイルの形式には、並べ替えの情報が含まれています。 RAW ファイル変換先には、文字列の列の比較フラグを含む並べ替えの情報がすべて保存されます。 RAW ファイル ソースは、並べ替えの情報を読み取って受け入れます。 詳細エディターを使用して、ファイル内の並べ替えのフラグを無視するように RAW ファイル ソースを構成するためのオプションが用意されています。 比較フラグの詳細については、「 [文字列データの比較](comparing-string-data.md)」を参照してください。  
  
 RAW ファイルを構成するには、RAW ファイル ソースが読み取るファイル名を指定します。  
  
> [!NOTE]  
>  このソースでは、接続マネージャーは使用されません。  
  
 このソースは、1 つの出力をとります。 エラー出力はサポートされていません。  
  
## <a name="configuration-of-the-raw-file-source"></a>RAW ファイル ソースの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
-   [RAW ファイルのカスタム プロパティ](raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 コンポーネントのプロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   sqlservercentral.com のブログ「 [RAW ファイルは最高](http://www.sqlservercentral.com/blogs/stratesql/archive/2011/1/1/31-days-of-ssis-_1320_-raw-files-are-awesome-_2800_1_2F00_31_2900_.aspx)」  
  
## <a name="see-also"></a>参照  
 [RAW ファイル変換先](raw-file-destination.md)   
 [データ フロー](data-flow.md)  
  
  
