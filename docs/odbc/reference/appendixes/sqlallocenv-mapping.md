---
title: SQLAllocEnv のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afbd1404cb40408166ecfc59993db7b183ae5ed2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065014"
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv のマッピング
アプリケーションを呼び出すと**SQLAllocEnv** ODBC を通じて*3.x*ドライバーでは、呼び出し**SQLAllocEnv**(*phenv*)にマップされて**SQLAllocHandle**次のようにします。  
  
1.  ドライバー マネージャーは、環境ハンドルを割り当てるし、アプリケーションに返します。 ドライバー マネージャー呼び出し**SQLSetEnvAttr** SQL_OV_ODBC2 を SQL_ATTR_ODBC_VERSION 環境属性を設定します。  
  
2.  ドライバー マネージャーは、アプリケーションがドライバーには、最初の接続を確立する場合  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     ドライバーで*OutputHandlePtr*設定*phenv*します。
