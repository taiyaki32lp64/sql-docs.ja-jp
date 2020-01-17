---
title: アップグレード プロセスの概要 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- upgrading SQL Server
- Upgrade Advisor [SQL Server], process description
- SQL Server Upgrade Advisor, process description
- upgrade process [Upgrade Advisor]
ms.assetid: f77ffbab-a195-4124-acce-9c538f7ca9ce
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fb4bfb2073427d0f48b3d4a7ac7b7ab496299030
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091518"
---
# <a name="upgrade-process-overview"></a>アップグレード プロセスの概要
  ここでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] アップグレード アドバイザーのベスト プラクティス情報、および [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードするための推奨プロセスの概要について説明します。  
  
## <a name="upgrade-process"></a>アップグレード プロセス  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] を実行しているサーバーは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードできます。 ただし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のコンポーネントには、適切にアップグレードできるもの、移行が必要なもの、新しいコンポーネントに置き換わるものがあります。 たとえば、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降、データ変換サービス (DTS) は [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) に置き換えられており、DTS は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ではサポートされなくなります。 アップグレード プランを作成する場合は、現在の DTS パッケージを [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージに更新する計画を立てることが必要になる場合があります。  
  
 アップグレード アドバイザーを使用すると、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール、コンポーネント、および関連ファイルを評価して、アップグレード中またはアップグレード後、あるいは [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] に移行後にエラーを引き起こす既知の問題を特定できます。 これらの既知の問題のいくつかのブロック、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]をアップグレードします。 アップグレード アドバイザーのレポートには、このような問題がアップグレード ブロッカーとして示されます。 セットアップを実行する前にアップグレード ブロッカーに対処していない場合は、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のセットアップが終了し、アップグレード アドバイザーを実行してアップグレードをブロックしている問題を特定するように勧めるメッセージが表示されます。  
  
 ベスト プラクティスとして、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードする前に、データとシステム設定をバックアップしておき、所属する組織向けに定義されている操作上のガイドラインに従って戦略的な手順を実行することをお勧めします。 次の手順に従ってアップグレードを完了してください。  
  
1.  「 [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)」を確認します。  
  
2.  データとシステム設定をバックアップします。  
  
3.  アップグレード アドバイザーを実行します。  
  
     アップグレード アドバイザーを実行しても、コンピューター上のデータや設定が変更されることはありません。  
  
4.  アップグレード アドバイザーのレポートで検出された問題を確認します。  
  
5.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] へのアップグレードに支障をきたす問題をすべて解決します。  
  
6.  その他のアップグレード前の問題を解決します。  
  
7.  アップグレード アドバイザーを実行して、既知の問題がすべて解消されたかどうか検証します。  
  
8.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップを実行します。  
  
9. アップグレード後の問題と移行の問題を解決します。  
  
## <a name="see-also"></a>関連項目  
 [アップグレード アドバイザーを実行している&#40;ユーザー インターフェイス&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [レポートの使用](../../../2014/sql-server/install/using-reports.md)   
 [アップグレード アドバイザーの使用](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
