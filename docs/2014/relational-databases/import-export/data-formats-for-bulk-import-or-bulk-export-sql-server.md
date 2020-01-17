---
title: 一括インポートまたは一括エクスポートのデータ形式 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], choosing
- bulk importing [SQL Server], data formats
ms.assetid: 73fe6741-9437-4b26-b030-28b863e74399
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c43cb42cffba31f20b0e9717204f5475b5bb156d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012081"
---
# <a name="data-formats-for-bulk-import-or-bulk-export-sql-server"></a>一括インポートまたは一括エクスポートのデータ形式 (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データを文字データ形式でもネイティブ バイナリ データ形式でも受け取ることができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と別のアプリケーション ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel など) または別のデータベース サーバー (Oracle や [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]など) との間でデータを移動するときは、文字形式を使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス間でデータを転送する場合にのみ、ネイティブ形式を使用できます。  
  
 **このトピックの内容**  
  
-   [一括インポートまたは一括エクスポートのデータ形式](#ComponentsAndConcepts)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> 一括インポートまたは一括エクスポートのデータ形式  
 次の表は、データの表現方法や転送元または転送先に基づいて、一般的にどのデータ形式を使用するのが適切かを示しています。  
  
|操作|ネイティブ|Unicode ネイティブ|文字|Unicode 文字|  
|---------------|------------|--------------------|---------------|-----------------------|  
|拡張文字や 2 バイト文字セット (DBCS) の文字を含まないデータ ファイルを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンス間でデータを一括転送します。 フォーマット ファイルを使用する場合を除いて、これらのテーブルは同じように定義されている必要があります。|可<sup>1</sup>|-|-|-|  
|文字形式や Unicode 形式とは異なり、ネイティブ データ形式では各 `sql_variant` 値のメタデータが保持されるので、`sql_variant` 列ではネイティブ データ形式を使用することが最も適しています。|はい|-|-|-|  
|拡張文字や DBCS 文字を含むデータ ファイルを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンス間でデータを一括転送します。|-|はい|-|-|  
|別のプログラムで生成されたテキスト ファイルからデータを一括インポートします。|-|-|はい|-|  
|別のプログラムで使用するテキスト ファイルにデータを一括エクスポートします。|-|-|はい|-|  
|Unicode データを含み、拡張文字や DBCS 文字は含まないデータ ファイルを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンス間でデータを一括転送します。|-|-|-|はい|  
  
 <sup>1</sup>からのデータの一括エクスポートするための最も簡単な方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用する場合**bcp**します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [bcp を使用した互換性のためのデータ形式の指定 &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)  
  
  
