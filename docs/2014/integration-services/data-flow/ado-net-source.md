---
title: ADO NET ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 296163b64d565ae3a65a16f1dbbf002bfc464bee
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153959"
---
# <a name="ado-net-source"></a>ADO NET ソース
  ADO NET ソースは .NET プロバイダーのデータを呼び出し、そのデータをデータ フローで使用できるようにします。  
  
 ADO NET 変換元を使用して [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]に接続できます。 OLE DB を使用した [!INCLUDE[ssSDS](../../includes/sssds-md.md)] への接続はサポートされていません。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] の詳細については、「[一般的な制限事項とガイドライン (Azure SQL Database)](https://go.microsoft.com/fwlink/?LinkId=248228)」を参照してください。  
  
## <a name="data-type-support"></a>データ型のサポート  
 ソースは、特定の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型にマップされないデータ型を DT_NTEXT [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型に変換します。 この変換はデータ型が `System.Object` である場合でも行われます。  
  
 DT_NTEXT データ型から DT_WSTR データ型に、または DT_WSTR データ型から DT_NTEXT データ型に変更できます。 データ型を変更するには、ADO NET ソースの **[詳細エディター]** ダイアログ ボックスで **DataType** プロパティを設定します。 詳細については、「 [Common Properties](../common-properties.md)」(共通プロパティ) を参照してください。  
  
 ADO NET ソースの後にデータ変換の変換を使用することによって、DT_NTEXT データ型を DT_BYTES データ型または DT_STR データ型に変換することもできます。 詳細については、「 [Data Conversion Transformation](transformations/data-conversion-transformation.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、日付データ型 DT_DBDATE、DT_DBTIME2、DT_DBTIMESTAMP2、および DT_DBTIMESTAMPOFFSET は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の特定の日付データ型にマップされます。 ADO NET ソースを構成して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が使用する日付データ型を [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が使用する日付データ型に変換できます。 このような日付データ型を変換する ADO NET ソースを構成するには、 **接続マネージャーの** Type System Version [!INCLUDE[vstecado](../../includes/vstecado-md.md)] プロパティを **[最新]** に設定します ( **Type System Version** プロパティは、 **[接続マネージャー]** ダイアログ ボックスの **[すべて]** ページにあります。 **[接続マネージャー]** ダイアログ ボックスを開くには、 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを右クリックし、 **[編集]** をクリックします)。  
  
> [!NOTE]  
>  **接続マネージャーの** Type System Version [!INCLUDE[vstecado](../../includes/vstecado-md.md)] プロパティが **[SQL Server 2005]** に設定されていると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日付データ型は DT_WSTR に変換されます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 接続マネージャーで、プロバイダーを .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient) と指定すると、システムはユーザー定義データ型 (UDT) は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バイナリ ラージ オブジェクト (BLOB) に変換されます。 UDT データ型の変換時には、次の規則が適用されます。  
  
-   データが大きくない UDT の場合、データは DT_BYTES に変換されます。  
  
-   データが大きくない UDT の場合、データベースの列の **[長さ]** プロパティは -1 または 8,000 バイトより大きい値に設定され、データは DT_IMAGE に変換されます。  
  
-   データが大きい UDT の場合、データは DT_IMAGE に変換されます。  
  
    > [!NOTE]  
    >  ADO NET ソースがエラー出力を使用するように構成されていない場合、データは DT_IMAGE 列に 8,000 バイトのチャンク単位でストリームされます。 ADO NET ソースがエラー出力を使用するように構成されている場合、バイトの配列全体が DT_IMAGE 列に渡されます。 エラー出力を使用するコンポーネントを構成する方法の詳細については、「 [Error Handling in Data](error-handling-in-data.md)」(データのエラー処理) を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型、サポートされるデータ型変換、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を含む特定のデータベース間でのデータ型マッピングの詳細については、「 [Integration Services のデータ型](integration-services-data-types.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型をマネージド データ型にマッピングする方法については、「[データ フロー内のデータ型の処理](../extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)」を参照してください。  
  
## <a name="ado-net-source-troubleshooting"></a>ADO NET ソースのトラブルシューティング  
 ADO NET ソースによる外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、ADO NET ソースによる外部データ ソースからのデータ読み込みに関するトラブルシューティングを行うことができます。 ADO NET ソースによる外部データ プロバイダーの呼び出しのログを記録するには、パッケージ ログ記録を有効にして、パッケージ レベルで **Diagnostic** イベントを選択します。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。  
  
## <a name="ado-net-source-configuration"></a>ADO NET ソースの構成  
 ADO NET ソースを構成するには、結果セットを定義する SQL ステートメントを使用します。 たとえば、 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] データベースに接続し、SQL ステートメント `SELECT * FROM Production.Product` を使用する ADO NET ソースは、 **Production.Product** テーブルのすべての行を抽出し、データセットを下流コンポーネントに提供します。  
  
> [!NOTE]  
>  SQL ステートメントを使用して、一時テーブルから結果を返すストアド プロシージャが呼び出す場合は、WITH RESULT SETS オプションを使用して結果セットのメタデータを定義します。  
  
> [!NOTE]  
>  SQL ステートメントを使用してストアド プロシージャを実行する際に、パッケージが次のエラーで失敗した場合は、EXEC ステートメントの前に `SET FMTONLY OFF` ステートメントを追加すると、エラーを解決できることがあります。  
>   
>  **列 <column_name> がデータ ソースに見つかりません。**  
  
 ADO NET ソースは [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを使用してデータ ソースに接続します。この接続マネージャーは .NET プロバイダーを指定します。 詳細については、「 [ADO.NET Connection Manager](../connection-manager/ado-net-connection-manager.md)」(ADO.NET 接続マネージャー) を参照してください。  
  
 ADO NET ソースは、1 つの標準出力と 1 つのエラー出力をとります。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](../common-properties.md)  
  
-   [ADO NET カスタム プロパティ](ado-net-custom-properties.md)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [DataReader 変換先](datareader-destination.md)   
 [ADO NET 変換先](ado-net-destination.md)   
 [データ フロー](data-flow.md)  
  
  
