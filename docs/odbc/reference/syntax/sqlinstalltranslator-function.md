---
title: SQLInstallTranslator 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslator
helpviewer_keywords:
- SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5b973332c2fe0fa541635d326a3a5adecf6ae91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076111"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 関数
**準拠**  
 バージョンが導入されました。ODBC 2.5、非推奨とされます。  
  
 **概要**  
 ODBC 3.0 で**SQLInstallTranslator**置き換わりました[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)します。 呼び出す**SQLInstallTranslator**にマップされる**SQLInstallTranslatorEx**します。 詳細については、次を参照してください。 **SQLInstallTranslatorEx**します。  
  
 **SQLInstallTranslator**アプリケーションは、ODBC で呼び出す場合は FALSE を返します*3.x*ドライバー マネージャーで、 *lpszInfFile*引数が NULL 以外の値に設定します。 ODBC で使用される Odbc.inf ファイル*2.x* ODBC ではサポートされなく*3.x*旧バージョンとの互換性のためであっても、します。
