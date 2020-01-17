---
title: データの読み込み
description: Integration Services、bcp ユーティリティ、dwloader、または SQL INSERT ステートメントを使用して、SQL Server 並列データウェアハウス (PDW) にデータを読み込んだり、挿入したりすることができます。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd161820fd53d45642848697bce9589a98dec4ca
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401047"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>並列データウェアハウスへのデータの読み込み
Integration Services、 [Bcp ユーティリティ](../tools/bcp-utility.md)、 **Dwloader**コマンドラインローダー、または SQL insert ステートメントを使用して、SQL Server 並列データウェアハウス (PDW) にデータを読み込んだり、挿入したりすることができます。  

## <a name="loading-environment"></a>環境を読み込んでいます  
データを読み込むには、1つまたは複数の読み込みサーバーが必要です。 独自の既存の ETL や他のサーバーを使用することも、新しいサーバーを購入することもできます。 詳細については、「[読み込みサーバーの取得と構成](acquire-and-configure-loading-server.md)」を参照してください。 これらの手順には、読み込みのための適切なソリューションを計画する際に役立つ、[サーバー容量計画の読み込みワークシート](loading-server-capacity-planning-worksheet.md)が含まれています。  
  
## <a name="load-with-dwloader"></a>Dwloader を使用した読み込み  
データを PDW に読み込む最速の方法は、 [Dwloader コマンドラインローダー](dwloader.md)を使用することです。  
  
![処理の読み込み](media/loading-process.png "処理の読み込み")  
  
dwloader は、コントロールノードを介してデータを渡さずに、コンピューティングノードにデータを直接読み込みます。 データを読み込むには、dwloader はまずコントロールノードと通信して、コンピューティングノードの連絡先情報を取得します。 dwloader は、各コンピューティングノードとの通信チャネルを設定し、256 KB のデータチャンクをラウンドロビン方式でコンピューティングノードに送信します。  
  
各コンピューティングノードで、データ移動サービス (DMS) は、データのチャンクを受信して処理します。 データの処理には、各行を SQL Server ネイティブ形式に変換し、ディストリビューションハッシュを計算して、各行が属する計算ノードを決定することが含まれます。  
  
これらの行を処理した後、DMS はシャッフル移動を使用して、各行を適切なコンピューティングノードと SQL Server のインスタンスに転送します。 SQL Server は、行を受信すると、dwloader の **-b**バッチサイズパラメーターセットに従ってバッチをバッチ処理し、バッチを一括読み込みします。  

## <a name="load-with-prepared-statements"></a>準備されたステートメントを使用して読み込む

準備されたステートメントを使用して、分散テーブルとレプリケートテーブルにデータを読み込むことができます。 入力データが対象のデータ型と一致しない場合、暗黙的な変換が実行されます。 PDW の準備されたステートメントでサポートされる暗黙の変換は、SQL Server によってサポートされる変換のサブセットです。 つまり、変換のサブセットのみがサポートされますが、サポートされている変換は SQL Server 暗黙の変換に一致します。 読み込み先のテーブルが分散テーブルまたはレプリケートテーブルとして定義されているかどうかにかかわらず、必要に応じて、ターゲットテーブルに存在するすべての列に暗黙的な変換が適用されます。 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスク|説明|  
|--------|---------------|  
|ステージングデータベースを作成します。|[ステージングデータベースの作成](staging-database.md)|  
|Integration Services で読み込みます。|[Integration Services での読み込み](load-with-ssis.md)|  
|Dwloader の型変換について説明します。|[dwloader のデータ型の変換規則](dwloader-data-type-conversion-rules.md)|  
|Dwloader を使用してデータを読み込みます。|[dwloader コマンドラインローダー](dwloader.md)|  
|INSERT の型変換について説明します。|[INSERT を使用したデータの読み込み](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
