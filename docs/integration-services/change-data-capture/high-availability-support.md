---
title: 高可用性のサポート | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2e0f6d3f-0536-46d9-8630-835e199515bf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 13a86cc2d5cdd02ded0cece1e08ed8d95f802ed4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298769"
---
# <a name="high-availability-support"></a>高可用性のサポート

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  CDC Service for Oracle は高可用性向けに設計されています。 次の機能は、高可用性のサポートの一部を形成します。  
  
-   CDC Service for Oracle はファイル リソース (ローカルまたはそれ以外) を使用しません。 CDC Service for Oracle のすべての状態は、対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに格納されます。 これにより、サービスが実行されているコンピューターに障害が発生した場合、同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを使用する別のコンピューターでサービスを簡単に開始できます。 復旧時間を軽減するために、長い Oracle トランザクションまたは実行時間のかかる Oracle トランザクションは対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のステージング テーブルに保持されます。これにより、障害 (またはサービスの再起動) 後に多数の Oracle トランザクション ログを再度スキャンする必要がなくなります。  
  
-   CDC Service for Oracle では、クラスター化された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを使用できます。そのため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが別のクラスター ノードにフェールオーバーした後の復元が可能です。 Oracle CDC Service のコンピューターの管理者は、Oracle CDC サービスを作成するときに、クラスター化された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの接続情報のみを指定する必要があります。  
  
-   CDC Service for Oracle では [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**Always On** データベース ミラーリング機能を使用できます。 このサポートを利用するには、MSXDBCDC データベースとすべての CDC データベースが同じ可用性グループ内に存在している必要があります。 また、Oracle CDC Service のコンピューターの管理者が **可用性グループへの適切な** Always On [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続情報を指定する必要があります (接続プロパティ `Failover_Partner and Network=dbmssocn`など)。 これにより、フェールオーバー後のデータベースのセカンダリ レプリケーションで CDC サービスが処理を自動的に再開することが可能になります。  
  
-   CDC Service for Oracle は、( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と共に、または独立して) Windows フェールオーバー クラスター上の汎用サービス リソースとして構成し、クラスターでの CDC 処理のフェールオーバーとフォールバックを簡素化することができます。 CDC Service for Oracle をフェールオーバー クラスターのリソースとして構成するには、システム管理者が CDC Service for Oracle をフェールオーバー クラスターの各ノードで汎用サービス リソースとして設定する必要があります。  
  
-   CDC Service for Oracle は Oracle RAC をサポートします。これにより、いずれかの Oracle RAC ノードがダウンしている場合でも、Oracle データベースと通信し、ログを処理できます。  
  
  
