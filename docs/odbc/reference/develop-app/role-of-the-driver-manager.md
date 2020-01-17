---
title: ドライバー マネージャーの役割 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7184c8ac9e0ad1813999a276f1579351f98544ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020401"
---
# <a name="role-of-the-driver-manager"></a>ドライバー マネージャーのロール
ドライバー マネージャーは、最終的な順序で生成される状態レコードが返されるを決定します。 具体的を最初に返されます、ランクが最も高いレコードを決定します。 ドライバーは、生成される状態レコードの順序付けします。 状態レコードは、ドライバー マネージャーとドライバーの両方によって投稿された場合、ドライバー マネージャーが順序付ける責任を負います。 詳細については、次を参照してください。[状態レコードのシーケンス](../../../odbc/reference/develop-app/sequence-of-status-records.md)します。  
  
 ドライバー マネージャーは、できるだけエラー チェック可能な限りです。 これにより、同じエラーのチェックからすべてのドライバーが保存されます。 たとえば、関数の引数がなど不連続の数の値を受け入れる*操作*で**SQLSetPos**、ドライバー マネージャーは、指定した値が有効なことを確認します。  
  
 次のセクションでは、ドライバー マネージャーによってをチェックする条件の種類について説明します。 すべてを網羅します。 これらのものではありません。ドライバー マネージャーを返します SQLSTATEs の完全な一覧は、各関数の「診断」を参照してください。ドライバー マネージャーによって行われた各チェックの説明は、文字"(DM)"で始まる 状態遷移のテーブルにも表示[付録 b:ODBC の状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); ドライバー マネージャーによって検出されたエラーかっこ内に表示します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [引数の値のチェック](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [状態遷移の確認](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [一般的なエラー チェック](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [ドライバー マネージャーのエラーと警告の確認](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
