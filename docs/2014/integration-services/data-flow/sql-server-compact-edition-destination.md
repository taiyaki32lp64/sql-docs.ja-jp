---
title: SQL Server Compact Edition 変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlservercompactdest.f1
helpviewer_keywords:
- destinations [Integration Services], SQL Server Compact
- SQL Server Compact, destination
- inserting data
ms.assetid: 697742ba-cc14-414d-8187-1845ad0dd99b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c59157c8d6beccdbb2d3e853cb6e035f9f89f61c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62901080"
---
# <a name="sql-server-compact-edition-destination"></a>SQL Server Compact Edition 変換先
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 変換先では、データが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースに書き込まれます。  
  
> [!NOTE]  
>  64 ビット コンピューターでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データ ソースに接続するパッケージを 32 ビット モードで実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact データ ソースへの接続に使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Provider は、32 ビット版でのみ使用できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 変換先を構成するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 変換先でデータが挿入されるテーブルの名前を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 変換先のカスタム プロパティ TableName には、テーブル名が含まれます。  
  
 この変換先ではデータ ソースへの接続に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 接続マネージャーが使用され、この接続マネージャーによって、使用する OLE DB プロバイダーが指定されます。 詳細については、「 [SQL Server Compact Edition 接続マネージャー](../connection-manager/sql-server-compact-edition-connection-manager.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 変換先には、パッケージの読み込み時にプロパティ式で更新できる、TableName カスタム プロパティがあります。 詳細については、「[Integration Services (SSIS) の式](../expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../expressions/use-property-expressions-in-packages.md)」、および「[SQL Server Compact Edition 変換先のカスタム プロパティ](sql-server-compact-edition-destination-custom-properties.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 変換先の入力は 1 つで、エラー出力はサポートされていません。  
  
## <a name="configuration-of-the-sql-server-compact-edition-destination"></a>SQL Server Compact Edition 変換先の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
-   [SQL Server 変換先のカスタム プロパティ](sql-server-destination-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 このコンポーネントのプロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ フロー](data-flow.md)  
  
  
