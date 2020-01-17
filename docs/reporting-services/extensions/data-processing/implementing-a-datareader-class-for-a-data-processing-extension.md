---
title: データ処理拡張機能の DataReader クラスの実装 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1367774e84dd10c2749f46a1ee6c38b8d5f6dd7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193905"
---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>データ処理拡張機能の DataReader クラスの実装
  クライアントは **DataReader** オブジェクトを使用して、読み取り専用、順方向専用のデータ ストリームをデータ ソースから取得できます。 クエリを実行すると結果が返され、結果は **DataReader** クラスの **Read** メソッドを使用して要求するまではクライアントのネットワーク バッファーに格納されます。 **DataReader** クラスを作成するには、<xref:Microsoft.ReportingServices.DataProcessing.IDataReader> を実装し、必要に応じて <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> を実装します。 **DataReader** オブジェクトを使用すると、アプリケーションのパフォーマンスが向上します。これは、クエリの結果全体が返されるまで待機するのではなく、データが使用可能になりしだい取得することと、メモリに一度に 1 行のみが格納されるため (既定)、システムのオーバーヘッドが小さくなることにより実現します。  
  
 **Command** クラスのインスタンスを作成した後に、**Command.ExecuteReader** を呼び出してデータ ソースから行を取得することによって、**DataReader** オブジェクトを作成します。 **DataReader** の実装によって、コマンドの実行により取得した結果セットへの順方向専用アクセス、および各行内の列型、名前、および値へのアクセスという 2 つの基本機能が提供されます。 クライアントは **DataReader** オブジェクトの **Read** メソッドを使用して、クエリの結果から行を取得します。  
  
 レポート デザイナーでは、**DataReader** オブジェクトを使用して、フィールドの一覧の他に結果セットに関するスキーマ情報も取得します。 このためには、<xref:Microsoft.ReportingServices.DataProcessing.IDataReader> インターフェイスの **GetName**、**GetValue**、**GetFieldType、** および **GetOrdinal** の各メソッドを実装します。  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> インターフェイスでは、結果セットに関する特定の集計情報を指定できます。 **DataReader** クラス実装の例については、「[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)」 (SQL Server Reporting Services 製品サンプル) を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [データ処理拡張機能の実装](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
