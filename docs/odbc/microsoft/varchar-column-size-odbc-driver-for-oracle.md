---
title: VARCHAR 列のサイズ (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3a3156c3f71eb4b3f7b8319da5d5fec7514f08b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087964"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 列のサイズ (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 Oracle8 varchar 型の列の最大サイズは 4,000 バイトに 2000年からに増加しました。 Oracle 7.3.x クライアント ソフトウェアには、2000 バイトを超えるパラメーター値をバインドする方法はありません。 そのため、2000 バイトを超えるの VARCHAR 列を含むテーブルを作成する場合は、ことをパラメーター化された挿入、更新、削除、およびクライアント ソフトウェアの 2000 バイトの制限を超えるデータに対してクエリを実行できません。 両方の ODBC Driver for Oracle、OLE DB Provider for Oracle は、パラメーター化された挿入、更新、削除、およびクエリを使用するため ORA 01026 エラーをここでは、報告されます。 Oracle クライアント ソフトウェアによって適用される制限内にあるデータは動作します。 この 2000 バイトの制限を回避するためには、Oracle8 にクライアント ソフトウェアをアップグレードする必要があります (8.0.4.1.1c またはそれ以降)。
