---
title: ODBC フロー コンポーネント | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cf751f1e-2348-4a77-904c-bd92c0d7d0ae
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e7035802b5b4e13c2696af9d76c6a2904547ea25
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292285"
---
# <a name="odbc-flow-components"></a>ODBC フロー コンポーネント

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  このトピックでは、SQL Server 2016 Integration Services (SSIS) を使用して ODBC データ フローを作成するために必要な概念について説明します。 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]  
  
 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 用の Connector for Open Database Connectivity (ODBC) を使用すると、SSIS 開発者は、ODBC でサポートされているデータベースからのデータの読み込みおよびアンロードを実行するパッケージを簡単に作成できます。  
  
 ODBC コネクタは、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]のコンテキストで、ODBC でサポートされているデータベースへのデータの読み込みやデータのアンロードを実行するときに、最適なパフォーマンスを得ることができるように設計されています。  
  
## <a name="benefits"></a>利点  
 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] の ODBC 入力元および ODBC 入力先を使用することで、ODBC でサポートされるデータベースへのデータ読み込みまたはデータのアンロードを処理するプロジェクトで、SSIS に関する競争力がもたらされます。  
  
 ODBC 入力元と ODBC 入力先を共に使用することで、ODBC 対応データベースとの高パフォーマンスのデータ統合が可能になります。 どちらのコンポーネントも、行方向のパラメーター配列バインド モードをサポートする機能豊富な ODBC プロバイダーでこのバインド機能を使用するように構成することや、機能が少ない ODBC プロバイダーで単一行のパラメーター バインド機能を使用するように構成することができます。  
  
## <a name="getting-started-with-the-odbc-source-and-destination"></a>ODBC 入力元および入力先の概要  
 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]を使用するパッケージをセットアップする前に、以下のコンポーネントを使用できることを確認する必要があります。  
  
-   [ODBC 入力元](../../integration-services/data-flow/odbc-source.md)  
  
-   [ODBC 変換先](../../integration-services/data-flow/odbc-destination.md)  
  
 ODBC 入力元および ODBC 入力先を使用すると、データのアンロードと読み込み、ODBC でサポートされているソース データベースからのデータ転送、ODBC でサポートされている入力先データベースへのデータ転送を簡単に実行できます。  
  
 データの読み込みまたはアンロードに入力元または入力先を使用するには、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] で [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]プロジェクトを開きます。 次に、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]のデザイン画面上に、入力元または入力先をドラッグします。  
  
-   ODBC 入力元コンポーネントは、ODBC でサポートされているソース データベースからデータを読み取ります。  
  
 ODBC 入力元は、SSIS によってサポートされている、任意の入力先または変換コンポーネントに接続できます。  
  
 **関連項目:**  
  
 ODBC 入力元  
  
 [ODBC ソース エディター] ([接続マネージャー] ページ)  
  
 [ODBC ソース エディター] ([エラー出力] ページ)  
  
-   ODBC 入力先は、ODBC でサポートされているデータベースにデータを読み込みます。 入力先を、SSIS によってサポートされている、任意の入力元または変換コンポーネントに接続することはできません。  
  
 **関連項目:**  
  
 ODBC 入力先  
  
 [ODBC 変換先エディター]\([接続マネージャー] ページ)  
  
 ODBC 変換先エディター ([エラー出力] ページ)  
  
## <a name="operating-scenarios"></a>操作シナリオ  
 このセクションでは、ODBC 入力元コンポーネントおよび入力先コンポーネントの主な使用方法の一部について説明します。  
  
### <a name="bulk-copy-data-from-sql-server-tables-to-any-odbc-supported-database-table"></a>SQL Server テーブルから ODBC でサポートされているデータベース テーブルへデータを一括コピーする  
 コンポーネントを使用して、1 つ以上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルから単一の ODBC でサポートされるデータベース テーブルへデータを一括コピーできます。  
  
 次の例は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルからデータを抽出し、それを DB2 テーブルへ読み込む SSIS データ フロー タスクを作成する方法です。  
  
-   [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] で [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]プロジェクトを作成します。  
  
-   コピーするデータが格納されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続するための OLE DB 接続マネージャーを作成します。  
  
-   ローカルまたはリモートの DB2 データベースをポイントする DSN が設定された、ローカルにインストールされている DB2 ODBC ドライバーを使用する ODBC 接続マネージャーを作成します。 このデータベースに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータが読み込まれます。  
  
-   OLE DB ソースをデザイン画面にドラッグし、抽出するデータが格納されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースおよびテーブルからデータを取得するようにソースを構成します。 前の手順で作成した OLE DB 接続マネージャーを使用します。  
  
-   ODBC 入力先をデザイン画面にドラックし、ソース出力を ODBC 入力先に接続します。次に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースから抽出したデータを DB2 テーブルに読み込むように入力先を構成します。 前の手順で作成した ODBC 接続マネージャーを使用します。  
  
### <a name="bulk-copy-data-from-odbc-supported-database-tables-to-any-sql-server-table"></a>ODBC でサポートされているデータベースから SQL Server テーブルへデータを一括コピーする  
 コンポーネントを使用して、ODBC でサポートされている 1 つ以上のデータベース テーブルから単一の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース テーブルへデータを一括コピーできます。  
  
 次の例は、Sybase データベース テーブルからデータを抽出し、それを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース テーブルへ読み込む SSIS データ フロー タスクを作成する方法です。  
  
-   SQL Server Data Tools で [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] プロジェクトを作成します。 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
-   ローカルまたはリモートの Sybase データベースをポイントする DSN が設定された、ローカルにインストールされている Sybase ODBC ドライバーを使用する ODBC 接続マネージャーを作成します。 このデータベースに、データが抽出されます。  
  
-   データの読み込み先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続するための OLE DB 接続マネージャーを作成します。  
  
-   ODBC 入力元をデザイン画面にドラッグし、コピーするデータが格納されている Sybase データベースからデータを取得するように入力元を構成します。 前の手順で作成した ODBC 接続マネージャーを使用します。  
  
-   OLE DB 変換先をデザイン画面にドラックし、ソース出力を OLE DB 変換先に接続します。次に、Sybase データベースから抽出したデータを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに読み込むように変換先を構成します。 前の手順で作成した OLE DB 接続マネージャーを使用します。  
  
## <a name="supported-data-types"></a>サポートされるデータ型  
 ODBC 一括 SSIS コンポーネントは、ラージ オブジェクト (CLOB および BLOB) を含む、すべての組み込み ODBC データ型をサポートします。  
  
ODBC 3.8 仕様で規定されている 拡張 C 型はサポートされません。次の表に、各 ODBC SQL 型に対応する SSIS データ型を示します。 SSIS 開発者は既定のマッピングをオーバーライドして、入出力列で使用する SSIS データ型を個別に指定できます。このときに必要となるデータ変換によって、パフォーマンスが影響を受けることはありません。  
  
|ODBC SQL 型|SSIS データ型|コメント|  
|-----------------|------------------|------------|  
|SQL_BIT|DT_BOOL||  
|SQL_TINYINT|DT_I1<br /><br />DT_UI1|ODBC ドライバーで SQL データ型の UNSIGNED_ATTRIBUTE が SQL_TRUE に設定されている場合、その SQL データ型は SSIS の符号なしのデータ型 (DT_UI1、DT_UI2、DT_UI4、DT_UI8) にマッピングされます。|  
|SQL_SMALLINT|DT_I2<br /><br />DT_UI2|ODBC ドライバーで SQL データ型の UNSIGNED_ATTRIBUTE が SQL_TRUE に設定されている場合、その SQL データ型は SSIS の符号なしのデータ型 (DT_UI1、DT_UI2、DT_UI4、DT_UI8) にマッピングされます。|  
|SQL_INTEGER|DT_I4<br /><br />DTUI4|ODBC ドライバーで SQL データ型の UNSIGNED_ATTRIBUTE が SQL_TRUE に設定されている場合、その SQL データ型は SSIS の符号なしのデータ型 (DT_UI1、DT_UI2、DT_UI4、DT_UI8) にマッピングされます。|  
|SQL_BIGINT|DT_I8<br /><br />DT_UI8|ODBC ドライバーで SQL データ型の UNSIGNED_ATTRIBUTE が SQL_TRUE に設定されている場合、その SQL データ型は SSIS の符号なしのデータ型 (DT_UI1、DT_UI2、DT_UI4、DT_UI8) にマッピングされます。|  
|SQL_DOUBLE|DT_R8|  
|SQL_FLOAT|DT_R8|  
|SQL_REAL|DT_R4|  
|SQL_NUMERIC (p,s)|DT_NUMERIC (p,s)|P が 38 以上で、S が 0 以上または P 以下の場合、数値データ型は DT_NUMERIC にマッピングされます。|  
||DT_R8|以下の条件が少なくとも 1 つ満たされる場合、数値データ型は DT_R8 にマッピングされます。<br /><br />有効桁数が 38 より大きい<br /><br />小数点以下桁数が 0 より小さい<br /><br />小数点以下桁数が 38 より大きい<br /><br />小数点以下桁数が有効桁数より大きい|  
||DT_CY|money データ型として宣言されている場合、数値データ型は DT_CY にマッピングされます。|  
|SQL_DECIMAL (p,s)|DT_NUMERIC (p,s)|P が 38 以上で、S が 0 以上または P 以下の場合、10 進データ型は DT_NUMERIC にマッピングされます。|  
||DT_R8|以下の条件が少なくとも 1 つ満たされる場合、10 進データ型は DT_R8 にマッピングされます。<br /><br />有効桁数が 38 より大きい<br /><br />小数点以下桁数が 0 より小さい<br /><br />小数点以下桁数が 38 より大きい<br /><br />小数点以下桁数が有効桁数より大きい|  
||DT_CY|money データ型として宣言されている場合、10 進データ型は DT_CY にマッピングされます。|  
|SQL_DATE<br /><br />SQL_TYPE_DATE|DT_DBDATE|  
|SQL_TIME<br /><br />SQL_TYPE_TIME|DT_DBTIME|  
|SQL_TIMESTAMP<br /><br />SQL_TYPE_TIMESTAMP|DT_DBTIMESTAMP<br /><br />DT_DBTIMESTAMP2|小数点以下桁数が 3 より大きい場合、SQL_TIMESTAMP データ型は DT_DBTIMESTAMP2 にマッピングされます。 それ以外の場合は、DT_DBTIMESTAMP にマッピングされます。|  
|SQL_CHAR<br /><br />SQLVARCHAR|DT_STR<br /><br />DT_WSTR<br /><br />DT_TEXT<br /><br />DT_NTEXT|列の長さが 8000 以下で、 **ExposeStringsAsUnicode** プロパティが false の場合に DT_STR が使用されます。<br /><br />列の長さが 8000 以下で、 **ExposeStringsAsUnicode** プロパティが true の場合に DT_WSTR が使用されます。<br /><br />列の長さが 8000 より長く、 **ExposeStringsAsUnicode** プロパティが false の場合に DT_TEXT が使用されます。<br /><br />列の長さが 8000 より長く、 **ExposeStringsAsUnicode** プロパティが true の場合に DT_NTEXT が使用されます。|  
|SQL_LONGVARCHAR|DT_TEXT<br /><br />DT_NTEXT|**ExposeStringsAsUnicode** プロパティが true の場合に DT_NTEXT が使用されます。|  
|SQL_WCHAR<br /><br />SQL_WVARCHAR|DT_WSTR<br /><br />DT_NTEXT|列の長さが 4000 以下の場合に DT_NTEXT が使用されます。<br /><br />列の長さが 4000 より長い場合に DT_NTEXT が使用されます。|  
|SQL_WLONGVARCHAR|DT_NTEXT|  
|SQL_BINARY|DT_BYTE<br /><br />DT_IMAGE|列の長さが 8000 以下の場合に DT_BYTES が使用されます。<br /><br />列の長さが 8000 より長い場合に DT_IMAGE が使用されます。|  
|SQL_LONGVARBINARY|DT_IMAGE|  
|SQL_GUID|DT_GUID|  
|SQL_INTERVAL_YEAR<br /><br />SQL_INTERVAL_MONTH<br /><br />SQL_INTERVAL_DAY<br /><br />SQL_INTERVAL_HOUR<br /><br />SQL_INTERVAL_MINUTE<br /><br />SQL_INTERVAL_SECOND<br /><br />SQL_INTERVAL_YEAR_TO_MONTH<br /><br />SQL_INTERVAL_DAY_TO_HOUR<br /><br />SQL_INTERVAL_DAY_TO_MINUTE<br /><br />SQL_INTERVAL_DAY_TO_SECOND<br /><br />SQL_INTERVAL_HOUR_TO_MINUTE<br /><br />SQL_INTERVAL_HOUR_TO_SECOND<br /><br />SQL_INTERVAL_MINUTE_TO_SECOND|DT_WSTR|  
|プロバイダー固有のデータ型|DT_BYTES<br /><br />DT_IMAGE|列の長さが 8000 以下の場合に DT_BYTES が使用されます。<br /><br />列の長さが 0 または 8000 より長い場合に DT_IMAGE が使用されます。|  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [ODBC 変換元](../../integration-services/data-flow/odbc-source.md)  
  
-   [ODBC 入力先](../../integration-services/data-flow/odbc-destination.md)  
  
 
