---
title: 正常性ポリシーの構成 (SQL Server ユーティリティ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 030aac3b-8901-4c41-91ed-aba96420276c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c59138d5d1f06ffee0266f9e97d5faf46ef28f08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115438"
---
# <a name="configure-health-policies-sql-server-utility"></a>正常性ポリシーの構成 (SQL Server ユーティリティ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスおよびデータ層アプリケーションに関する [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ユーティリティのリソース パラメーターを表示するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのダッシュボードを使用します。 詳細については、「 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの正常性ポリシーの結果を表示するには、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]からユーティリティ コントロール ポイントに接続します。 詳細については、「 [ユーティリティ エクスプローラーを使用した SQL Server ユーティリティの管理](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの正常性ポリシーは、データ層アプリケーション、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のマネージド インスタンス用に構成できます。 正常性ポリシーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのデータ層アプリケーションおよびマネージド インスタンスに対してグローバルに定義できます。また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ層アプリケーションごと、およびマネージド インスタンスごとに個別に定義することもできます。  
  
## <a name="monitoring-policies-for-data-tier-applications"></a>データ層アプリケーションのポリシーの監視  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ層アプリケーションの過大使用ポリシーと過小使用ポリシーは次のとおりです。  
  
-   データ層アプリケーションのプロセッサ使用率  
  
-   データ層アプリケーションのデータベース ファイル用のファイル領域  
  
-   データ層アプリケーションの記憶域ボリューム用のファイル領域  
  
-   コンピューターのプロセッサ使用率  
  
> [!NOTE]  
>  データ層アプリケーションの場合、記憶域ボリュームとプロセッサ使用率は読み取り専用ポリシーです。  
  
 データ層アプリケーションのグローバルな監視ポリシーの表示および変更の詳細については、「[ユーティリティの管理 &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)」をご覧ください。  
  
 データ層アプリケーション個々の監視ポリシーの表示および変更の詳細については、「[配置済みのデータ層アプリケーションの詳細 &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)」をご覧ください。  
  
## <a name="monitoring-policies-for-managed-instances-of-sql-server"></a>SQL Server のマネージド インスタンスのポリシーの監視  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスの過大使用ポリシーと過小使用ポリシーは次のとおりです。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのプロセッサ使用率。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのデータベース ファイル用のファイル領域。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの記憶域ボリューム用のファイル領域。  
  
-   コンピューターのプロセッサ使用率  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスのグローバルな監視ポリシーの表示および変更の詳細については、「[ユーティリティの管理 &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)」をご覧ください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の個々のマネージド インスタンスの監視ポリシーの表示および変更の詳細については、「[マネージド インスタンスの詳細 &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [CPU 使用率のポリシーにおけるノイズの軽減 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
  
