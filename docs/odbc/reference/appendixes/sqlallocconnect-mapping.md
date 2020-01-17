---
title: SQLAllocConnect のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65c23f41ea9176c460c8fb32ece5e74dfb803541
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065025"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect のマッピング
アプリケーションを呼び出すと**SQLAllocConnect**を通じて、ODBC 3 *。x*ドライバーでは、呼び出し**SQLAllocConnect**(*henv*、 *phdbc*) にマップされて**SQLAllocHandle**次のようにします。  
  
1.  ドライバー マネージャーは、接続を割り当てるし、アプリケーションに返します。  
  
2.  ドライバー マネージャーは、アプリケーションでは、接続を確立するときに  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     ドライバーで*InputHandle*に設定*henv*、および*OutputHandlePtr*に設定*phdbc*します。
