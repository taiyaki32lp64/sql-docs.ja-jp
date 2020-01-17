---
title: IIS で仮想サーバーの構成 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5888cb9666488ced6f9e112d21c48d0265f5c25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922833"
---
# <a name="configuring-virtual-servers-on-iis"></a>IIS での仮想サーバーの構成
Internet Information Services 4.0 での仮想サーバーを作成するときに、RDS を使用する仮想サーバーを構成するには、次の 2 つの余分な手順が必要です。  
  
1.  サーバーを設定する場合は、「Execute アクセスを許可する」。 を確認してください。  
  
2.  移動する msadcs.dll *vroot*\msadc、場所*vroot* virtual server のホーム ディレクトリは。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="see-also"></a>関連項目  
 [RDS の基礎](../../../ado/guide/remote-data-service/rds-fundamentals.md)


