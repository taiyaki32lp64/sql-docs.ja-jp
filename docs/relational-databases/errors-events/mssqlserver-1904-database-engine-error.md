---
title: MSSQLSERVER_1904 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1904 (Database Engine error)
ms.assetid: 2a35d57d-74e2-45a2-8f67-3f2e51d69712
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ea12450aba44938a1333687d14aa0dc5dfc471e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896836"
---
# <a name="mssqlserver1904"></a>MSSQLSERVER_1904
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1904|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|KEYCOUNT|  
|メッセージ テキスト|テーブル'%.\*ls' の %S_MSG '%.*ls' の %S_MSG キー リストに %d 個の列名が含まれています。 インデックスまたは統計のキー列リストの上限は %d です。|  
  
## <a name="explanation"></a>説明  
指定したインデックスまたは統計のキー列リストが許容される最大列数を超えています。  
  
## <a name="user-action"></a>ユーザーの操作  
キー列リストの列数が指定された最大列数以下になるように変更します。  
  
非クラスター化インデックスの場合は、CREATE INDEX ステートメントの INCLUDE 句を使用して、列を非キー列としてインデックスに追加することを検討してください。 この方法を使用すると、キー列の数が現在のインデックス サイズの上限である 16 を超えないようにすることができます。 詳細については、「 [付加列インデックスの作成](~/relational-databases/indexes/create-indexes-with-included-columns.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[CREATE STATISTICS &#40;Transact-SQL&#41;](~/t-sql/statements/create-statistics-transact-sql.md)  
  
