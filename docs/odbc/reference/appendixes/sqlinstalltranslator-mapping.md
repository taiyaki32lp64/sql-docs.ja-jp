---
title: SQLInstallTranslator のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6433df796c88abd7873915266d1a2ca4041a5c62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125725"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator のマッピング
ときに、ODBC *2.x*アプリケーション呼び出し**SQLInstallTranslator** ODBC を通じて*3.x*ドライバー、ドライバー マネージャーは、マップへの呼び出し**SQLInstallTranslatorEx**します。アプリケーションは呼び出さないでください**SQLInstallTranslator** ODBC で*3.x*ドライバー マネージャーで、 *lpszInfFile*引数が NULL 以外の値に設定します。 ODBC です。ODBC で使用される INF ファイル*2.x* ODBC ではサポートされなく*3.x*旧バージョンとの互換性のためであっても、します。
