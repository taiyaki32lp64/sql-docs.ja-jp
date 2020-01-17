---
title: ODBC Jet エラー メッセージ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85e0f9a8bc7015a0ad5b12ce46a6c94ab31ca43c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915814"
---
# <a name="odbc-jet-error-messages"></a>ODBC Jet エラー メッセージ
データ ソースで発生するエラーの場合は、ODBC ドライバーは ODBC ファイルのライブラリによって返されたエラー メッセージを返します。 ODBC ドライバーまたはドライバー マネージャーで発生するエラー、SQLSTATE と関連付けられたエラー メッセージがテキストに基づくドライバーを返します。  
  
 エラー メッセージには、次の形式があります。  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 角かっこ () 内のプレフィックスは、エラーの場所を特定します。 ドライバー マネージャーで、エラーの発生時*データ ソース*は付与しません。 データ ソースでエラーが発生した場合、[*仕入先*] と [*ODBC コンポーネント*] プレフィックスを識別、仕入先とデータ ソースからのエラーを受信した ODBC コンポーネントの名前。  
  
 次の表は、ドライバー マネージャーとドライバー ISAM によって返されるエラー メッセージを示しています。  
  
|エラー メッセージ|エラーの場所|  
|-------------------|--------------------|  
|[Microsoft][ODBC ドライバー マネージャー]*メッセージ テキスト*|ドライバー マネージャー (Odbc32.dll)|  
|[Microsoft][ODBC*ドライバー名*]*メッセージ テキスト*|ドライバー ISAM (ドライバーの Isam を参照してください)|
