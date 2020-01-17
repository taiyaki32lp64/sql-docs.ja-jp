---
title: 影響を受ける ODBC コンポーネント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08997f610b00f22d436a5c91d34beb2a8fc2cc1d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944855"
---
# <a name="affected-odbc-components"></a>影響を受ける ODBC コンポーネント
旧バージョンとの互換性は、アプリケーション、ドライバー マネージャー、およびドライバーがドライバー マネージャーの新しいバージョンの導入によって影響を受ける方法について説明します。 これによって影響アプリケーションとドライバーは、古いバージョンのいずれかまたはその両方が残っているとします。 そのため、3 種類の旧バージョンとの互換性、考慮すべき次の表に示すように。  
  
|種類|DM のバージョン|アプリケーションのバージョン|ドライバーのバージョン|  
|----------|-------------------|----------------------------|-----------------------|  
|ドライバー マネージャーの旧バージョンとの互換性|*3.x*|*2.x*|*2.x*|  
|[1] のドライバーの下位互換性|*3.x*|*2.x*|*3.x*|  
|アプリケーションの旧バージョンとの互換性|*3.x*|*3.x*|*2.x*|  
  
 [1] のドライバーの下位互換性については付録 g: で主に説明します。旧バージョンとの互換性のためのガイドラインをドライバーです。  
  
> [!NOTE]
>  標準に準拠したアプリケーション - たとえば、Open Group または ISO CLI 標準 - に従って書き込まれているアプリケーションは保証 ODBC を使用する*3.x*ドライバーは ODBC *3.x*ドライバー マネージャー。 アプリケーションが使用している機能は、ドライバーで使用できることと見なされます。 標準に準拠したアプリケーションが、ODBC を使ってコンパイルされていると見なされますも*3.x*ヘッダー ファイル。
