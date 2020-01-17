---
title: オプティミスティック同時実行制御 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f5f4b7101718ea8372c9635a064dc81e1d8f6c1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023394"
---
# <a name="optimistic-concurrency"></a>オプティミスティック コンカレンシー
*オプティミスティック同時実行制御*オプティミスティックな仮定からその名前の派生元には、トランザクションの間に競合が発生することはほとんどありません別のトランザクションが更新または読み取られるまでの間のデータの行を削除するときに発生した競合といいます。現在のトランザクションが更新または削除します。 反対の*ペシミスティック同時実行性、* ロック、またはをアプリケーション開発者と考えています、このような競合当たり前にします。  
  
 オプティミスティック同時実行制御、行は左側の時刻になると更新または削除するまでロックを解除します。 その時点では、行を再度読み取るし、チェックするかどうかは変更されている最後の読み取り以降を参照してください。 場合は、行が変更された、更新または削除が失敗して、再実行する必要があります。  
  
 行が変更されたかどうかを確認するのには、その新しいバージョンは、行のキャッシュされたバージョンに対してチェックされます。 このチェックは、SQL Server、または行の各列の値にタイムスタンプ列などの行のバージョンに基づくことができます。 多くの Dbms は、行のバージョンをサポートしていません。  
  
 データ ソースまたはアプリケーションによっては、オプティミスティック同時実行制御を実装できます。 どちらの場合、アプリケーションが少ないトランザクション分離レベル Read Committed; などを使用します。高いレベルを使用してオプティミスティック同時実行制御を使用して同時実行の向上を否定します。  
  
 データ ソースでオプティミスティック同時実行制御が実装されている場合、アプリケーションは、SQL_CONCUR_ROWVER、SQL_CONCUR_VALUES したり、SQL_ATTR_CONCURRENCY ステートメント属性を設定します。 行の削除を更新または位置指定の update または delete ステートメントの呼び出しを実行**SQLSetPos**ドライバーまたはデータ ソースが場合に、SQLSTATE 01001 (カーソル操作の競合) を返します、ペシミスティック同時実行制御; と同様、update または delete は、競合しているのために失敗します。  
  
 アプリケーション自体では、オプティミスティック同時実行制御を実装する場合、また、ステートメント属性 SQL_ATTR_CONCURRENCY を SQL_CONCUR_READ_ONLY 行を読み取るに設定します。 行のバージョンの比較は行バージョン列が把握していない場合、呼び出す**SQLSpecialColumns**この列の名前を特定する SQL_ROWVER オプションを使用します。  
  
 アプリケーションを更新または SQL_CONCUR_LOCK (行への書き込みアクセスを取得する) を実行して、同時実行性を増やすことで、行を削除、 **UPDATE**または**WHERE**ステートメントを**WHERE**句をバージョンを指定しますまたは、行の値は、アプリケーションで読み取られるときに必要があります。 その後、行が変更された場合、ステートメントは失敗します。 場合、**WHERE**句が行を一意に識別されない、ステートメントを更新または他の行を削除する可能性がありますも; 行のバージョンでは、行を常に一意に識別するが、行の値は行を一意に識別、主キーが含まれる場合にのみです。
