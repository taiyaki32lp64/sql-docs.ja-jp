---
title: ADO 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ADO
- connection managers [Integration Services], ADO
- ADO connection manager [Integration Services]
ms.assetid: 490418bc-5ef1-41b8-a9c8-de38aa96e0f6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7fda014196d933ef9d5391ab4db798d821e43610
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833812"
---
# <a name="ado-connection-manager"></a>ADO 接続マネージャー
  ADO 接続マネージャーを使用すると、レコードセットなどの ADO (ActiveX データ オブジェクト) オブジェクトにパッケージを接続できます。 この接続マネージャーは、通常、Microsoft Visual Basic 6.0 などの以前のバージョンの言語で記述されたカスタム タスクや、ADO を使用してデータ ソースに接続する既存のアプリケーションの一部のカスタム タスクで使用されます。  
  
 ADO 接続マネージャーをパッケージに追加すると、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、実行時に ADO 接続を解決する接続マネージャーを作成し、接続マネージャーのプロパティを設定し、接続マネージャーをパッケージの `Connections` コレクションに追加します。 接続マネージャーの `ConnectionManagerType` プロパティは、`ADO` に設定されます。  
  
## <a name="troubleshooting-the-ado-connection-manager"></a>ADO 接続マネージャーのトラブルシューティング  
 ADO 接続マネージャーに読み込まれると、特定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日付データ型は次の表に示す結果を生成します。  
  
|SQL Server データ型|結果|  
|--------------------------|------------|  
|`time`, `datetimeoffset`|パッケージがパラメーター化 SQL コマンドを使用していない場合、パッケージは失敗します。 パラメーター化 SQL コマンドを使用するには、パッケージで SQL 実行タスクを使用します。 詳細については、「 [SQL 実行タスク](../control-flow/execute-sql-task.md) 」と「 [SQL 実行タスクのパラメーターとリターン コード](../parameters-and-return-codes-in-the-execute-sql-task.md)」を参照してください。|  
|`datetime2`|ADO 接続マネージャーは、ミリ秒の値を切り捨てます。|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型の詳細とそれを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型にマッピングする方法については、「[データ型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)」と「[Integration Services のデータ型](../data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="configuring-the-ado-connection-manager"></a>ADO 接続マネージャーの構成  
 ADO 接続マネージャーは、次の方法で構成できます。  
  
-   選択したプロバイダーの要件を満たすように構成された、特定の接続文字列を指定します。  
  
-   プロパイダによっては、接続先のデータ ソースの名前を指定します。  
  
-   選択したプロバイダーに適したセキュリティ資格情報を指定します。  
  
-   接続マネージャーから作成される接続を、実行時に保持するかどうかを指定します。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[OLE DB 接続マネージャーの構成]](ole-db-connection-manager.md)  
  
 プログラムによる接続マネージャーの構成の詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services &#40;SSIS&#41; の接続](integration-services-ssis-connections.md)  
  
  
