---
title: SQL Server オブジェクトとバージョンの DAC サポート | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data-tier application [SQL Server], supported objects
- objects [SQL Server], data-tier applications
ms.assetid: b1b78ded-16c0-4d69-8657-ec57925e68fd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b528a7a9efb91bb99cb7c2b0a32c71dc0de7785b
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811270"
---
# <a name="dac-support-for-sql-server-objects-and-versions"></a>SQL Server オブジェクトとバージョンの DAC サポート
  データ層アプリケーション (DAC) では、よく使用される [!INCLUDE[ssDE](../../includes/ssde-md.md)] オブジェクトがサポートされます。  
  
 **このトピックの内容**  
  
-   [サポート対象の SQL Server オブジェクト](#SupportedObjects)  
  
-   [SQL Server の各バージョンでのデータ層アプリケーション サポート](#SupportByVersion)  
  
-   [データ配置の制限](#DeploymentLimitations)  
  
-   [配置操作に関するその他の注意点](#Considerations)  
  
##  <a name="SupportedObjects"></a> サポート対象の SQL Server オブジェクト  
 作成時または編集時にデータ層アプリケーションで指定できるのは、サポート対象オブジェクトのみです。 DAC でサポートされていないオブジェクトを含む既存のデータベースから DAC の抽出、登録、およびインポートを行うことはできません。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、DAC の以下のオブジェクトがサポートされています。  
  
|||  
|-|-|  
|DATABASE ROLE|FUNCTION:インライン テーブル値|  
|FUNCTION:複数ステートメント テーブル値|FUNCTION:Scalar|  
|INDEX:クラスター化インデックス|INDEX:非クラスター化インデックス|  
|INDEX:空間|INDEX:[一意]|  
|Login|アクセス許可|  
|ロールのメンバーシップ|SCHEMA|  
|統計|STORED PROCEDURE:Transact-SQL|  
|シノニム|TABLE:CHECK 制約|  
|TABLE:[照合順序]|TABLE:列 (計算列も含む)|  
|TABLE:制約、DEFAULT|TABLE:制約、FOREIGN KEY|  
|TABLE:制約、INDEX|TABLE:制約、PRIMARY KEY|  
|TABLE:制約、UNIQUE|TRIGGER:DML|  
|種類 :HIERARCHYID、GEOMETRY、GEOGRAPHY|種類 :ユーザー定義データ型|  
|種類 :ユーザー定義テーブル型|User|  
|VIEW||  
  
##  <a name="SupportByVersion"></a> SQL Server の各バージョンでのデータ層アプリケーション サポート  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンによって、DAC 操作に対するサポート レベルが異なります。 特定のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされるすべての DAC 操作は、そのバージョンのすべてのエディションでサポートされます。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスでは、次の DAC 操作がサポートされています。  
  
-   サポートされているすべてのバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で、エクスポートと抽出がサポートされています。  
  
-   [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] と、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、および [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]のすべてのバージョンで、すべての操作がサポートされています。  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Service Pack 2 (SP2) 以降と [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 以降で、すべての操作がサポートされています。  
  
 DAC Framework は、DAC パッケージとエクスポート ファイルのビルドおよび処理用のクライアント側ツールで構成されています。 以下の製品には、DAC Framework が含まれています。  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] および [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] には DAC Framework 3.0 が含まれており、これによってすべての DAC 操作がサポートされます。  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 と Visual Studio 2010 SP1 には DAC Framework 1.1 が含まれており、これによって、エクスポートとインポートを除くすべての DAC 操作がサポートされます。  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] と Visual Studio 2010 には DAC Framework 1.0 が含まれており、これによって、エクスポート、インポート、およびインプレース アップグレードを除くすべての DAC 操作がサポートされます。  
  
-   SQL Server または Visual Studio の以前のバージョンのクライアント ツールでは、DAC 操作はサポートされていません。  
  
 あるバージョンの DAC Framework でビルドされた DAC パッケージまたはエクスポート ファイルは、それ以前のバージョンの DAC Framework では処理できません。 たとえば、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] クライアント ツールを使用して抽出された DAC パッケージは、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] クライアント ツールでは配置できません。  
  
 あるバージョンの DAC Framework でビルドされた DAC パッケージまたはエクスポート ファイルは、それ以降の任意のバージョンの DAC Framework で処理できます。 たとえば、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] クライアント ツールを使用して抽出された DAC パッケージは、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 以降のクライアント ツールを使用して配置できます。  
  
##  <a name="DeploymentLimitations"></a> データ配置の制限  
 SQL Server 2012 SP1 の DAC Framework データ配置エンジンには、忠実性に関してここで述べるような制限があることに注意してください。 制限が適用される DAC Framework 操作は、.dacpac ファイルの展開またはパブリッシュ、および .bacpac ファイルのインポートです。  
  
1.  sql_variant 列内の特定の条件と基本データ型によるメタデータの消失。 影響を受ける場合は、次のような警告メッセージが表示されます:"**DAC Framework によって配置される場合、sql_variant 列内で使用される特定のデータ型の特定のプロパティは保持されません。** "  
  
    -   MONEY、SMALLMONEY、NUMERIC、DECIMAL の各基本データ型:有効桁数は保持されません。  
  
        -   有効桁数 38 桁の DECIMAL/NUMERIC 基本データ型: "TotalBytes" という sql_variant のメタデータは常に 21 に設定されます。  
  
    -   すべてのテキスト基本データ型:データベースの既定の照合順序がすべてのテキストに適用されます。  
  
    -   BINARY 基本データ型:最大長プロパティは保持されません。  
  
    -   TIME、DATETIMEOFFSET の各基本データ型:有効桁数は常に 7 桁に設定されます。  
  
2.  sql_variant 列内のデータの消失。 影響を受ける場合は、 **"3 より大きなスケールを持つ sql_variant DATETIME2 列の値が DAC Framework によって配置されると、データが失われます。配置中、DATETIME2 値は 3 と等しいスケールに制限されます。"** という警告メッセージが表示されます。  
  
    -   スケールが 3 を超える DATETIME2 基本データ型: スケールが 3 に制限されます。  
  
3.  sql_variant 列内で以下に述べる条件が成立すると、配置操作が失敗します。 影響を受ける場合は、次のようなメッセージが表示されます: **"DAC Framework のデータ制限のため操作に失敗しました。"**  
  
    -   DATETIME2、SMALLDATETIME、DATE の各基本データ型:値が DATETIME の範囲外である場合 (年が 1753 未満であるなど)。  
  
    -   DECIMAL、NUMERIC の各基本データ型: 値の有効桁数が 28 を超える場合。  
  
##  <a name="Considerations"></a> 配置操作に関するその他の注意点  
 DAC Framework のデータ配置操作に関して次の点に注意してください。  
  
-   **抽出、エクスポート** - DAC Framework を使用してデータベースからパッケージを作成する操作 (たとえば、.dacpac ファイルの抽出や .bacpac ファイルのエクスポート) では、ここで述べた制限は適用されません。 パッケージのデータは、ソース データベースのデータを完全に忠実に再現しています。 ここで述べた条件のいずれかがパッケージに存在する場合、抽出およびエクスポート ログに、上で述べたメッセージによって問題の概要が記録されます。 これは、作成したパッケージが潜在的なデータ配置の問題を抱えていることをユーザーに警告するためです。 ログには次のような概要メッセージも記録されます: **"これらの制限は、DAC Framework によって作成された DAC パッケージに格納されたデータ型および値の忠実性には影響しません。DAC パッケージをデータベースに配置した結果のデータ型および値に対してのみ適用されます。"影響を受けるデータおよびこの制限の回避方法の詳細については、** [このトピック](https://go.microsoft.com/fwlink/?LinkId=267086)を参照してください。  
  
-   **配置、パブリッシュ、インポート** - DAC Framework を使用してパッケージをデータベースに配置する操作 (たとえば、.dacpac ファイルの配置またはパブリッシュ、.bacpac ファイルのインポート) では、ここで述べた制限が適用されます。 対象データベースに作成されるデータが、パッケージのデータを完全に忠実に再現していない可能性があります。 配置およびインポートのログには、問題が発生したすべてのインスタンスに関して、上記のメッセージが記録されます。 操作はエラーによってブロックされます (上記の分類 3 を参照)。しかし、他の警告では続行されます。  
  
     この場合に影響を受けるデータおよび、配置、パブリッシュ、インポートの各操作時におけるこの制限の対処方法の詳細については、 [こちらのトピック](https://go.microsoft.com/fwlink/?LinkId=267087)を参照してください。  
  
-   **回避策** - 抽出およびエクスポート操作では、完全に忠実な BCP データ ファイルが .dacpac ファイルまたは .bacpac ファイルに書き出されます。 制限を回避するには、SQL Server の BCP.exe コマンド ライン ユーティリティを使用して、完全に忠実なデータを DAC パッケージから対象データベースに配置します。  
  
## <a name="see-also"></a>参照  
 [データ層アプリケーション](data-tier-applications.md)  
  
  
