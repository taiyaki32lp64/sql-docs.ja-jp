---
title: ロックの種類 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93436a5180f1a01269f1612f7e608b71b4c073e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923806"
---
# <a name="types-of-locks"></a>ロックの種類
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 オプティミスティックな一括更新を示します。 バッチ更新モードで必要です。  
  
 多くのアプリケーションでは、行の数を一度にフェッチし、挿入、更新、または削除する行のセット全体を含める更新プログラムを調整する必要があります。 バッチ カーソルを 1 つのみのサーバーへのラウンド トリップが必要な更新プログラムのパフォーマンスを向上させるため、ネットワーク トラフィックが減少します。 バッチのカーソル ライブラリを使用して、静的カーソルを作成し、データ ソースから切断できます。 この時点で、行に変更を加える再接続し、その後、バッチ内のデータ ソースに変更を投稿することができます。  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 プロバイダーがオプティミスティック ロックのレコードのロックを呼び出すときにのみ使用することを示します、 **Update**メソッド。 レコードとを呼び出したときに編集する別のユーザーが、時間の間でデータを変更することがあります可能性があることを意味**Update**、これにより、競合が発生します。 競合が発生する可能性が不足している状況でこの種類のロックを使用して、または競合がすぐに解決できます。  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 レコードごとの排他的ロックを示します。 プロバイダーは、新機能を確実に、レコードは、通常は編集する前に、すぐにデータ ソースのレコードのロックを編集するために必要です。 もちろん、つまりと呼び出すことによって、ロックが解放されるまで、編集を開始するには、レコードが他のユーザーに使用できないこと**更新します。** 予約システムなど、データへの同時変更が許容できないシステムでこの種類のロックを使用します。  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 読み取り専用レコードを示します。 データを変更することはできません。 読み取り専用ロックとは、レコードのロックを維持するために、サーバーが必要がないために、「最速」タイプのロック。  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 ロックの種類を指定しません。
