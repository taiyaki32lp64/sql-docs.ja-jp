---
title: サーバーのプロパティ ([全般] ページ) - SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.setsapassword.f1
- sql13.swb.serverproperties.activedirectory.f1
- sql13.swb.serverproperties.prodinfo.f1
ms.assetid: 10ac57f1-b4bd-4528-bb66-3e47ccf663e7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: dbc306b3ec8d23c4ddc7aec6477c407f21e345a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025483"
---
# <a name="server-properties---general-page"></a>[サーバーのプロパティ] - [全般] ページ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このページを使用すると、インストールされている [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の読み取り専用情報を表示できます。  
  
## <a name="property-grid"></a>[プロパティ] グリッド  
 サーバー名、サーバーのオペレーティング システム、プロセッサ数など、選択したサーバーのプロパティを表示します。  
  
 **[名前]**  
 サーバー インスタンスの名前を表示します。  
  
 **Product**  
 現在実行中の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションを表示します。  
  
 **オペレーティング システム**  
 現在実行中の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows オペレーティング システムを表示します。  
  
 **プラットフォーム**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行しているオペレーティング システムとハードウェアを表示します。  
  
 **バージョン**  
 現在実行中の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エディションのバージョン番号を表示します。  
  
 **言語**  
 実行中の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスでサポートされる言語を表示します。  
  
 **[メモリ]**  
 サーバーに搭載されている RAM の容量を一覧表示します。  
  
 **[プロセッサ]**  
 搭載されている CPU の数を表示します。  
  
 **[ルート ディレクトリ]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのディレクトリのパスを表示します。通常は C:\Program Files\Microsoft SQL Server\\です。  
  
 **[サーバー照合順序]**  
 サーバーによりサポートされる照合順序を表示します。 照合順序によって、Unicode データと非 Unicode データに対して使用される特定のコード ページと並べ替え順が指定されます。  
  
 **[クラスター化]**  
 サーバー インスタンスが **フェールオーバー クラスターで構成されている場合は** [True] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を表示し、サーバー インスタンスがクラスター化されていない場合は **[False]** を表示します。  
  
 **[HADR が有効]**  
 **機能が有効の場合は** [True] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] を表示し、 **機能が無効の場合は** [False] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] を表示します。 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] の有効化または無効化については、「[AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)」をご覧ください。  
  
## <a name="description-field"></a>[説明] フィールド  
 サーバーのプロパティに関する追加情報を表示します。  
  
## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
