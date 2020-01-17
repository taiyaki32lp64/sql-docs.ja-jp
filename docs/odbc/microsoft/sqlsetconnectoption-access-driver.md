---
title: SQLSetConnectOption (Access ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bea124a78e2a180180c59de3577fe1db7637e110
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897783"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (Access ドライバー)
> [!NOTE]  
>  このトピックでは、Access ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
|fOption|解説|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption SQL_MODE_READ_ONLY または SQL_MODE_READ_WRITE のいずれかに設定できます。 ただし、SQL_ACCESS_MODE が SQL_MODE_READ_ONLY に設定されている場合、ドライバーは更新を禁止できません。|  
|SQL_AUTOCOMMIT|Microsoft Access ドライバーを使用すると、Microsoft Access ドライバーは [1] のトランザクションをサポートしているために、SQL_AUTOCOMMIT オプションが sql_autocommit_on の状態または SQL_AUTOCOMMIT_OFF のいずれかに設定する可能性があります。|  
|SQL_CURRENT_QUALIFIER|サポートされています。|  
|SQL_LOGIN_TIMEOUT|サポートされていません。|  
|SQL_OPT_TRACE|サポートされています。|  
|SQL_OPT_TRACEFILE|サポートされています。|  
|SQL_PACKET_SIZE|サポートされていません。|  
|SQL_QUIET_MODE|サポートされていません。|  
|SQL_TRANSLATE_DLL|サポートされていません。|  
|SQL_TRANSLATION_OPTION|サポートされていません。|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION は SQL_TXN_READ_COMMITTED では常にします。|  
  
 [1] は、アトミック トランザクションは、Microsoft Access ドライバーによってサポートされていません。 有限の遅延が、トランザクションがコミットされた時刻と値が書き込まれた時間の間に存在する Microsoft Access ドライバーを使用してトランザクションをコミットするときにディスクにします。 この遅延は、Microsoft Jet エンジン固有の遅延によって決定されます。 ページのタイムアウトはできません、最小値より小さい場合でも、その値を下回る PageTimeout オプションが設定されます。 その結果があるデータをコミットするという保証はありません、安定した遅延中に変更を行うためです。
