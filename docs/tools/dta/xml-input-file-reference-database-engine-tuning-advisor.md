---
title: XML 入力ファイル リファレンス (データベース エンジン チューニング アドバイザー) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], XML input files
- input file reference [Database Engine Tuning Advisor]
- XML input files [Database Engine Tuning Advisor]
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0572c0aa0b4a49a3c0ce471cb8194124fef73cdb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105781"
---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>XML 入力ファイル リファレンス (データベース エンジン チューニング アドバイザー)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、XML 入力ファイルを使用してデータベースをチューニングできます。 この XML ファイルでは、チューニング セッションで使用するデータベース、テーブル、ワークロード ファイルまたはワークロード テーブル、およびチューニング オプションを指定します。 このファイルを使用して、ユーザー指定の構成を指定し、"what-if" 分析を実行することもできます。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーの XML 入力ファイルには XML 要素の階層が含まれており、各要素には、チューニング セッションの設定を指定するテキスト、またはその他の要素が含まれています。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーの XML 入力ファイルは整形式 XML の標準に準拠する必要があるため、すべての要素名で大文字と小文字が区別されます。 要素の大文字と小文字の記述は Pascal 形式にします。つまり、最初の文字を大文字で表記し、結合されている後に続く単語の最初の文字も大文字で表記します。  
  
 すべての要素の値は、XML の名前付け規則に準拠している必要があります。 これらの規則の詳細については、MSDN ライブラリの「 [XML テキストの内容](https://go.microsoft.com/fwlink/?LinkId=7614) 」を参照してください。  
  
 このリファレンスは包括的なものではないことに注意してください。 XML 入力を定義するために使用できるすべての要素の詳細については、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーの XML スキーマ DTASchema.xsd を参照してください。  
  
## <a name="xml-declaration"></a>XML 宣言  
  
-   [XML データ &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>DTAXML ルート要素  
  
-   [DTAXML 要素 &#40;DTA&#41;](../../tools/dta/dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>DTAInput 要素  
  
-   [DTAInput 要素 &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)  
  
-   [Server 要素 &#40;DTA&#41;](../../tools/dta/server-element-dta.md)  
  
-   [Workload 要素 &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)  
  
-   [TuningOptions 要素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
-   [Configuration 要素 &#40;DTA&#41;](../../tools/dta/configuration-element-dta.md)  
  
## <a name="server-elements"></a>サーバー要素  
  
-   [Server の Name 要素 &#40;DTA&#41;](../../tools/dta/name-element-for-server-dta.md)  
  
-   [Server の Database 要素 &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>Workload 要素  
  
-   [File 要素 &#40;DTA&#41;](../../tools/dta/file-element-dta.md)  
  
-   [Workload の Database 要素 &#40;DTA&#41;](../../tools/dta/database-element-for-workload-dta.md)  
  
-   [EventString 要素 &#40;DTA&#41;](../../tools/dta/eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>チューニング オプションの要素  
  
-   [TuningTimeInMin 要素 &#40;DTA&#41;](../../tools/dta/tuningtimeinmin-element-dta.md)  
  
-   [StorageBoundInMB 要素 &#40;DTA&#41;](../../tools/dta/storageboundinmb-element-dta.md)  
  
-   [TestServer 要素 &#40;DTA&#41;](../../tools/dta/testserver-element-dta.md)  
  
-   [FeatureSet 要素 &#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Partitioning 要素 &#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [DropOnlyMode 要素 &#40;DTA&#41;](../../tools/dta/droponlymode-element-dta.md)  
  
-   [KeepExisting 要素 &#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md)  
  
-   [OnlineIndexOperation 要素 &#40;DTA&#41;](../../tools/dta/onlineindexoperation-element-dta.md)  
  
-   [DatabaseToConnect 要素 &#40;DTA&#41;](../../tools/dta/databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>構成の要素  
  
-   [Configuration の Server 要素 &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)  
  
-   [Configuration の Database 要素 &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)  
  
-   [Recommendation 要素 &#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)  
  
-   [Create 要素 &#40;DTA&#41;](../../tools/dta/create-element-dta.md)  
  
-   [Index 要素 &#40;DTA&#41;](../../tools/dta/index-element-dta.md)  
  
-   [Index の Name 要素 &#40;DTA&#41;](../../tools/dta/name-element-for-index-dta.md)  
  
-   [Index の Column 要素 &#40;DTA&#41;](../../tools/dta/column-element-for-index-dta.md)  
  
-   [Column の Name 要素 &#40;DTA&#41;](../../tools/dta/name-element-for-column-dta.md)  
  
-   [Index の Filegroup 要素 &#40;DTA&#41;](../../tools/dta/filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>データベースの要素  
  
-   [Database の Name 要素 &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)  
  
-   [Database の Schema 要素 &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)  
  
-   [Schema の Name 要素 &#40;DTA&#41;](../../tools/dta/name-element-for-schema-dta.md)  
  
-   [Schema の Table 要素 &#40;DTA&#41;](../../tools/dta/table-element-for-schema-dta.md)  
  
-   [Table の Name 要素 &#40;DTA&#41;](../../tools/dta/name-element-for-table-dta.md)  
  
## <a name="see-also"></a>参照  
 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
