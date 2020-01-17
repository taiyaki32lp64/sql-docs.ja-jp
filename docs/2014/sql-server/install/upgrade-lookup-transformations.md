---
title: 参照変換のアップグレード |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation and upgrading
- upgrading caching for Lookup transformation
- upgrading Lookup transformation
ms.assetid: d9b2c281-91ee-4e20-bdf0-0cd77d4a4241
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: eae7433569972c217161f1681b2f7089c7604335
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091507"
---
# <a name="upgrade-lookup-transformations"></a>参照変換のアップグレード
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] を [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードする場合、パッケージに変更を加え、参照変換でこれらの新しい機能を利用することを検討してください。 この変換では、[!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] で使用可能なキャッシュの種類とデータ出力オプションがサポートされます。 詳細については追加のキャッシュとデータの出力を参照してください[参照変換](../../integration-services/data-flow/transformations/lookup-transformation.md)します。  
  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] で使用可能なキャッシュの種類は、完全キャッシュ、部分キャッシュ、およびキャッシュなしです。 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] では、これらのいずれかの種類のキャッシュを使用するように参照変換を構成できます。 部分的なキャッシュを実装する方法の詳細についてまたはキャッシュなしの場合、次を参照してください。[キャッシュなしモードまたは部分キャッシュ モードの参照を実装](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)します。 完全なキャッシュを実装する方法については、次を参照してください[キャッシュ接続マネージャーを使用してフル キャッシュ モードで参照変換を実装](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)と[フル キャッシュ モードを使用して、OLE で参照変換を実装します。DB 接続マネージャー](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)します。  
  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] では、参照変換は 1 つの入力、1 つの出力、および 1 つのエラー出力になっていました。 参照データセットに一致するエントリがある入力の行は、出力で処理されていました。 一致するエントリがない入力の行はエラーとして処理され、エラー出力にリダイレクトされていました。 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] では、参照変換の出力は 2 つ (一致する出力と一致しない出力) になります。  
  
 既定では、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で作成された参照変換を実行すると、[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] では一致するエントリのない行はエラーとして処理され、その行はエラー出力にリダイレクトできます。 行をエラーではないものとして処理し、それらの行を、一致しない出力にリダイレクトするように参照変換を構成することもできます。  
  
 詳細については、次を参照してください。[参照変換エディター &#40;[全般] ページ&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)します。  
  
## <a name="see-also"></a>参照  
 [Lookup Transformation](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
