---
title: データ処理拡張機能を実装する準備 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- interfaces [Reporting Services]
- data processing extensions [Reporting Services], implementing
ms.assetid: 698817e4-33da-4eb5-9407-4103e1c35247
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3ae11d41956f37f1a203235abad71639f942ae7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193895"
---
# <a name="preparing-to-implement-a-data-processing-extension"></a>データ処理拡張機能を実装する準備
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能を実装する前に、実装するインターフェイスを定義しておく必要があります。 インターフェイスのセット全体にわたって拡張機能固有の実装を行うことができます。<xref:Microsoft.ReportingServices.DataProcessing.IDataReader> インターフェイスや <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> インターフェイスなど、サブセットだけを実装することもできます。このようなインターフェイスでは、クライアントが **DataReader** オブジェクトとして主に結果セットと対話し、[!INCLUDE[ssRS](../../../includes/ssrs.md)] データ処理拡張機能を結果セットとデータ ソース間のブリッジとして使用します。  
  
 データ処理拡張機能は、次の 2 種類の方法のいずれかで実装できます。  
  
-   データ処理拡張機能のクラスは [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] データ プロバイダー インターフェイスを実装でき、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] によって提供される拡張されたデータ処理拡張機能インターフェイスをオプションで実装できます。  
  
-   データ処理拡張機能のクラスは、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] によって提供されるデータ処理拡張機能インターフェイスを実装でき、拡張されたデータ処理拡張機能インターフェイスをオプションで実装できます。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能が特定のプロパティやメソッドをサポートしない場合は、プロパティやメソッドを非操作として実装します。 クライアントが特定の動作を必要とする場合は、**NotSupportedException** 例外をスローします。  
  
> [!NOTE]  
>  プロパティやメソッドの非操作実装は、実装することを選択したインターフェイスのプロパティとメソッドにのみ適用されます。 オプションのインターフェイスを実装しないことを選択した場合は、そのインターフェイスをデータ処理拡張機能アセンブリから除外してください。 インターフェイスが必須またはオプションのいずれであるかの詳細については、後述する表を参照してください。  
  
## <a name="required-extension-functionality"></a>必須の拡張機能  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のすべてのデータ処理拡張機能は、次の機能を提供する必要があります。  
  
-   データ ソースへの接続を開きます。  
  
-   クエリを分析し、結果セットにフィールド名の一覧を返します。  
  
-   データ ソースに対してクエリを実行し、行セットを返します。  
  
-   1 つの値を持つパラメーターをクエリに渡します。  
  
-   行セットの行を反復処理し、データを取得します。  
  
 各データ処理拡張は、次の機能を含めるように拡張できます。  
  
-   クエリを分析し、クエリで使用したパラメーター名の一覧を返します。  
  
-   クエリを分析し、クエリをグループ化するフィールドの一覧を返します。  
  
-   クエリを分析し、クエリを並べ替えるフィールドの一覧を返します。  
  
-   接続文字列と無関係なデータ ソースと接続するために、ユーザー名とパスワードを指定します。  
  
-   行セットの行を反復処理し、データ値に関する補助メタデータを取得します。  
  
-   サーバーでデータを集計します。  
  
## <a name="available-extension-interfaces"></a>使用可能な拡張機能インターフェイス  
 以下は使用可能なインターフェイスの一覧です。実装が必須かどうかも記載されています。  
  
|インターフェイス|[説明]|実装|  
|---------------|-----------------|--------------------|  
|IDbConnection|データソースとの一意のセッションを表します。 クライアント/サーバー データベース システムの場合は、セッションがサーバーとのネットワーク接続と同じことがあります。|Required|  
|IDbConnectionExtension|[!INCLUDE[ssRS](../../../includes/ssrs.md)] データ処理拡張機能によって実装できる、セキュリティと承認に関する追加の接続プロパティを表します。|省略可|  
|IDbTransaction|ローカル トランザクションを表します。|Required|  
|IDbTransactionExtension|[!INCLUDE[ssRS](../../../includes/ssrs.md)] データ処理拡張機能によって実装できる追加のトランザクション プロパティを表します。|省略可|  
|IDbCommand|データ ソースと接続するときに使用するクエリまたはコマンドを表します。|Required|  
|IDbCommandAnalysis|クエリを分析し、クエリで使用されるパラメーター名の一覧を返す追加コマンド情報を表します。|省略可|  
|IDataParameter|コマンドまたはクエリに渡すパラメーターまたは名前と値のペアを表します。|Required|  
|IDataParameterCollection|コマンドまたはクエリに関連するすべてのパラメーターのコレクションを表します。|Required|  
|IDataReader|データ ソースから順方向専用、読み取り専用のデータのストリームを読み取るメソッドを提供します。|Required|  
|IDataReaderExtension|データ ソースでコマンドを実行することによって取得された、順方向専用の結果セットのストリームを 1 つ以上読み取るメソッドを提供します。 このインターフェイスは、フィールド集計の追加サポートを提供します。|省略可|  
|IExtension|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能の基本クラスです。 ローカライズされた拡張機能名を追加し、構成ファイルから拡張機能へ構成設定を渡すインプリメンタも有効にします。|Required|  
  
 データ処理拡張機能インターフェイスは、可能な場合は [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] データ プロバイダーのインターフェイス、メソッド、およびプロパティのサブセットと同じです。 完全な [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] データ プロバイダーの実装の詳細については、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Software Development Kit (SDK) ドキュメントの「.NET Framework データ プロバイダーの実装」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [データ処理拡張機能の実装](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
