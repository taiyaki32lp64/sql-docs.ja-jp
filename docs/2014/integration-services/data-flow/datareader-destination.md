---
title: DataReader 変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.datareaderdest.f1
helpviewer_keywords:
- DataReader destination
- destinations [Integration Services], DataReader
ms.assetid: 56fcc4bf-c901-42c3-a71d-110039293431
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 694e85a56686379d089f3c2fc11721e4dd6f8642
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827554"
---
# <a name="datareader-destination"></a>DataReader 変換先
  DataReader 変換先は、ADO.NET `DataReader` インターフェイスを使用して、データ フローのデータを公開します。 公開すると、そのデータを他のアプリケーションで使用できます。 たとえば、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポートのデータ ソースを構成して、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの実行結果を使用できます。 構成するには、DataReader 変換先を実装するデータ フローを作成します。  
  
 プログラムで DataReader 変換先にアクセスして値を読み取る方法の詳細については、「 [ローカル パッケージの出力の読み込み](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)」をご覧ください。  
  
## <a name="configuration-of-the-datareader-destination"></a>DataReader 変換先の構成  
 DataReader 変換先のタイムアウト値を指定して、タイムアウトが発生した場合に変換先が失敗になるようにするかどうかを指定できます。 タイムアウトは、アプリケーションが指定した時間内にデータを要求しない場合に発生します。  
  
 DataReader 変換先は 1 つの入力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
-   [DataReader 変換先のカスタム プロパティ](datareader-destination-custom-properties.md)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
  
