---
title: 手動コミット モード |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7189a0586ba4f62091d5eb209a56931627bc6f7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036402"
---
# <a name="manual-commit-mode"></a>手動コミット モード
*手動コミット モードで*アプリケーションを呼び出してトランザクションを完了する必要があります明示的に**SQLEndTran**にそれらをコミットまたはロールバックしています。 これは、ほとんどのリレーショナル データベースの通常のトランザクション モードです。  
  
 ODBC でのトランザクションは、明示的に開始する必要はありません。 代わりに、トランザクションは、データベースで動作しているアプリケーションを起動するたびに、暗黙的に開始します。 データ ソースの明示的なトランザクションの開始に使用する場合は、ドライバーはアプリケーションがトランザクションを必要とするステートメントを実行し、現在のトランザクションが存在しないときにそれを提供する必要があります。
