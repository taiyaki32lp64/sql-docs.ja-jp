---
title: MSSQLSERVER_9532 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f811d554ea59539bd558e1c22c19fb118e54820f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912409"
---
# <a name="mssqlserver9532"></a>MSSQLSERVER_9532
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|9532|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|XMLERR_COLUMNSET_CANNOT_CONVERT_FROM_TO|  
|メッセージ テキスト|列セット '%.*ls' に関係するクエリ/DML 操作で、列 '%.\*ls' のデータ型 '%ls' をデータ型 '%ls' に変換する際に変換に失敗しました。|  
  
## <a name="explanation"></a>説明  
 列セットは、型指定されていない XML 表現であり、テーブルの複数の列を 1 つにまとめて構造化した出力です。 XML 列セットを使用してスパース列の値を挿入または更新する場合、基になるスパース列に挿入される値は、`xml` データ型から暗黙的に変換されます。 列のデータ型に変換できない値が指定されました。  
  
## <a name="user-action"></a>ユーザーの操作  
 指定された値は暗黙的に変換することができなかったため、無効なエントリとなる可能性があります。 エラーを修正して再試行してください。 値が正しい場合は、列セットではなく個々の列を使用するようにステートメントを変更します。 これにより、値を適切なデータ型に明示的にキャストすることができます。  
  
  
