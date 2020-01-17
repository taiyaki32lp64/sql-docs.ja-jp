---
title: MSSQLSERVER_12304 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 12304 (Database Engine error)
ms.assetid: a2c252c2-e815-4ac8-a101-7af5b32e3233
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c50e4bdbfe6fd9af1c5e5a6d528a270c0b63c50f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62870210"
---
# <a name="mssqlserver12304"></a>MSSQLSERVER_12304
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|12304|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|HK_UNSUPPORTED_IDENTITY_TABLE_VAR|  
|メッセージ テキスト|ネイティブ コンパイル ストアド プロシージャのコンテキスト外にある型を使用する場合は、自らの任意の列と共に IDENTITY プロパティを使用するメモリ最適化テーブルを使用することはサポートされていません。|  
  
## <a name="user-action"></a>ユーザーの操作  
 自らの任意の列と共に IDENTITY プロパティを使用するメモリ最適化テーブル型を使用しないでください。  
  
## <a name="see-also"></a>関連項目  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
