---
title: 互換性のないデータベースエンジンサーバーの照合順序 (アップグレードアドバイザー) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 80f499d6-2c90-49eb-a5b3-0bb5b7faaa3b
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: fbd4c1e55bb49c6ae8f75d3d12cc243df963018a
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952236"
---
# <a name="incompatible-database-engine-server-collation-upgrade-advisor"></a>互換性のないデータベース エンジン サーバーの照合順序 (アップグレード アドバイザー)
  互換性のないサーバー照合順序を使用するように構成されている [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスを使用している [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] がアップグレードアドバイザーによって検出されました。  
  
||  
|-|  
|SharePoint モード[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **[!INCLUDE[applies](../../includes/applies-md.md)]** ます。|  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>[説明]  
 互換性のないサーバー照合順序を使用するように構成されている [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスを使用している [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] がアップグレードアドバイザーによって検出されました。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint モードでは、SharePoint 共有サービスアーキテクチャを利用します。 SharePoint では、大文字と小文字の区別、サーバー照合順序、またはバイナリ サーバー照合順序用に構成された [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] はサポートされません。 互換性のない照合順序には、既定で大文字と小文字を区別するかバイナリである照合順序と、既定では互換性があるものの、次の照合順序指定子のいずれかで構成されている基本照合順序が含まれます。  
  
-   **Binary**  
  
-   **大文字と小文字を区別する**  
  
-   **バイナリコードポイント**  
  
 現在の [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] サーバー照合順序は互換性がないため、アップグレードがブロックされます。  
  
## <a name="corrective-action"></a>修正措置  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] サーバーの照合順序プロパティは変更できません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のアップグレードを完了できなくなります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストールを、互換性のあるサーバー照合順序を使用している新しいサーバーに移行する必要があります。 詳細については、以下をご覧ください。  
  
-   [Reporting Services のアップグレードと移行](https://go.microsoft.com/fwlink/?LinkId=233227)  
  
-   [SQL Server 照合順序の選択](https://go.microsoft.com/fwlink/?LinkId=233226)  
  
  
