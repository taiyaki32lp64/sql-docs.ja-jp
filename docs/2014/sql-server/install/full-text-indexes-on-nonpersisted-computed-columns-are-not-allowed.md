---
title: 保存されない計算列でフルテキスト インデックスは許可されません |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: cba737f7-b187-47d0-8458-23dc18d18aca
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 417ca3c2e5e477960c4c905543f3a712a5ec7453
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095169"
---
# <a name="full-text-indexes-on-nonpersisted-computed-columns-are-not-allowed"></a>保存されない計算列にフルテキスト インデックスを使用できない
  非決定的な計算列と不正確な計算列に対してフルテキスト インデックスを作成できません。 このような列は、型列やフルテキスト キー列として使用できません。  
  
## <a name="description"></a>説明  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] では、非決定的な計算列と不正確な計算列を型列やフルテキスト キー列として使用してフルテキスト インデックスを作成できます。 この機能はサポートされません。 アップグレードすると、古くて互換性のない、サポート対象外のフルテキスト インデックスは無効になります。  
  
## <a name="corrective-action"></a>修正措置  
 このようなフルテキスト インデックスを有効にするには、列の定義を変更して決定的かつ正確にします。  
  
## <a name="see-also"></a>関連項目  
 [アップグレード アドバイザーの使用](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
