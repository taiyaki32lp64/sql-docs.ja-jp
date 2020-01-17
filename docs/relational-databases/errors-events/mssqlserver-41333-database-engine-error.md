---
title: MSSQLSERVER_41333 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f137d859fa6f6233e14bc34c6bf50797a4360a98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123290"
---
# <a name="mssqlserver41333"></a>MSSQLSERVER_41333
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|41333|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|CROSS_CONTAINER_ISOLATION_FAILURE|  
|メッセージ テキスト|次に示すトランザクションは、スナップショット分離を使用したうえでメモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャにアクセスする必要があります。RepeatableRead トランザクション、Serializable トランザクション、RepeatableRead または Serializable 分離でメモリ最適化されていないテーブルにアクセスするトランザクション。|  
  
## <a name="explanation"></a>説明  
ディスク ベース トランザクションと XTP トランザクションの間の分離レベルが高いユーザーに対しては、制約があります。  
  
## <a name="user-action"></a>ユーザーの操作  
メモリ最適化テーブル (およびネイティブ コンパイル プロシージャ) とディスク ベース テーブルでは、高レベルの分離操作を実行しないでください。  
  
詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
