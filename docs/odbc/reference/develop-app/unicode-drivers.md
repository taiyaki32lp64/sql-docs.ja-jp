---
title: Unicode ドライバー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ca9b70ee6a96759e496b831f7c12dc3ee78419b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087869"
---
# <a name="unicode-drivers"></a>Unicode ドライバー
ドライバーが、ANSI、Unicode ドライバーにするかどうかは、データ ソースの性質に完全に依存します。 データ ソースは、Unicode データをサポートする場合、ドライバーが Unicode ドライバーにあります。 データ ソースは、ANSI データのみをサポートする場合ドライバーは、ANSI ドライバーを維持する必要があります。  
  
 Unicode ドライバーをエクスポートする必要があります**SQLConnectW**ドライバー マネージャーによって Unicode ドライバーとして認識されるようにします。  
  
 Unicode ドライバーには、Unicode 関数がそのまま使用する必要があります (のサフィックスを持つ*W*) し、Unicode データを格納します。 ANSI 関数では、受け入れることもできますが、する必要はありません。 (ドライバー マネージャーは、ANSI 関数呼び出しを渡さない、 *A*ドライバーをドライバーが ANSI に関数を呼び出すことがなく、サフィックスと、パスに変換するサフィックスです)。  
  
 Unicode ドライバーは、Unicode または ANSI のいずれかで、アプリケーションのバインドによって結果セットを返すできる必要があります。 アプリケーションは、SQL_C_CHAR にバインドした場合、Unicode ドライバーは SQL_WCHAR データを SQL_CHAR に変換する必要があります。 ドライバー マネージャーは、ANSI ドライバーは、SQL_C_CHAR の SQL_C_WCHAR マップされますが、Unicode ドライバーのマッピングは行われません。  
  
> [!NOTE]  
>  ドライバー マネージャーを呼び出すが、ドライバーの種類を決定するときに**SQLSetConnectAttr**し、接続時に SQL_ATTR_ANSI_APP 属性を設定します。 SQL_ATTR_ANSI_APP SQL_AA_TRUE に設定されます、アプリケーションでの ANSI Api を使用している場合と SQL_AA_FALSE の値に設定することにより、Unicode が使用されている場合。 この属性を使用できるように、ドライバー、アプリケーションの種類に基づいて異なる動作が発生することができます。 属性をアプリケーションによって、直接設定することはできずではサポートされていません**SQLGetConnectAttr**します。 ドライバーは、ANSI と Unicode の両方のアプリケーションと同じ動作を示す場合、は、SQL_ERROR をこの属性を返します。 ドライバーは SQL_SUCCESS を返します、ドライバー マネージャーは、接続プールを使用する場合に、ANSI と Unicode の接続を区切ります。
