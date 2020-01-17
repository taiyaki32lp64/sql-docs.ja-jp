---
title: データを更新し、永続化する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26fabdc205018b8e94575cfb5bd5e945a8fb28ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923725"
---
# <a name="updating-and-persisting-data"></a>データの更新と保持
前の章は、ADO を使用して、データ ソース内のデータを取得する方法、データ内を移動する方法、およびデータを編集する方法も説明してきました。 もちろん、アプリケーションの目的がデータを変更するユーザーを許可する場合は、これらの変更を保存する方法を理解する必要があります。 永続化することができますか、**レコード セット**を使用してファイルへの変更、**保存**メソッド、またはを使用してストレージのデータ ソースをバックアップを作成、変更を送信できます、 **Update**または**UpdateBatch**メソッド。  
  
 複数の行のデータの変更前の章で、 **Recordset**します。 ADO では、追加、削除、および行のデータの変更に関連する 2 つの基本的な概念をサポートします。  
  
 最初の概念に変更が行われませんすぐに、**レコード セット**。 代わりに、内部に行われる*コピー バッファー*します。 変更をしたくない場合は、コピー バッファー内の変更は破棄されます。 コピー バッファー内の変更を適用、変更を保持する場合、 **Recordset**します。  
  
 2 つ目の概念は、操作を宣言する行を完了するとすぐに変更がデータ ソースに反映するか (つまり、*即時*モード)、または一連の行に対するすべての変更が、セットの操作を宣言するまでに収集されます完全な (つまり、*バッチ*モード)。 **LockType**プロパティを基になるデータ ソースに変更が行われたときに決定します。 **adLockOptimistic**または**adLockPessimistic**イミディ エイト モードを指定します、 **adLockBatchOptimistic**バッチ モードを指定します。 **CursorLocation**プロパティが影響する**LockType**設定を使用できます。 たとえば、 **adLockPessimistic**場合、設定がサポートされていません、 **CursorLocation**プロパティに設定されて**adUseClient**します。  
  
 イミディ エイト モードの各呼び出しで、 **Update**メソッドには、データ ソースに変更が反映されます。 バッチ モードでは、各呼び出しで**Update**現在の行位置の移動、コピー バッファーにのみ、変更を保存しますか、 **UpdateBatch**メソッドには、データ ソースに変更が反映されます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [データの更新](../../../ado/guide/data/updating-data.md)  
  
-   [データの保持](../../../ado/guide/data/persisting-data.md)
