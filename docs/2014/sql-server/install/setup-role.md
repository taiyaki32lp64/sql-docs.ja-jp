---
title: セットアップ ロール |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c7e9db15-89f2-4d4d-8860-1e64c5821c4d
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: b1cf8c6f8442fc69669c10106f671040733e48ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092230"
---
# <a name="setup-role"></a>セットアップ ロール
  [機能の選択] ページを使用して個々の機能を選択するか、セットアップ ロールを使用してインストールするかを指定するには、このページを使用します。  
  
 `setup role` とは、事前定義された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成の実装に必要なすべての機能および共有コンポーネントを選択するために用意されている設定です。  
  
## <a name="options"></a>および  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能のインストール**  
 個々の機能と共有コンポーネントを選択するには、このオプションを選択します。 インスタンス機能には、データベース エンジン サービス、Analysis Services (ネイティブ モード)、Reporting Services などがあります。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot for SharePoint**  
 SharePoint 2010 ファームに Analysis Services サーバー コンポーネントをインストールするには、このオプションを選択します。 このオプションを使用すると、PowerPivot System サービスおよび Analysis Services サーバーをファームに配置して、埋め込まれた [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データを含むパブリッシュ済みの Excel ブックを対象としたクエリおよびデータ処理を有効にできます。  
  
 必要に応じて、SharePoint ファームでデータベースをホストするために必要なリレーショナル データベース エンジンのインスタンスをインストールに追加することもできます。 既にファームが構成されている場合は、このオプションをスキップできます。  
  
 セットアップが完了すると、次の方法のいずれかを使用してソフトウェアを構成する必要があります。PowerPivot 構成ツール、PowerShell コマンドレット、または SharePoint 2010 サーバーの全体管理。 以前のリリースとは異なり、セットアップでは PowerPivot インストールの構成タスクが実行されなくなりました。  
  
 ロール ベースのインストールには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot for Excel クライアント アプリケーションは含まれません。 クライアント アプリケーションは個別にインストールします。  
  
 **既定値を持つすべての機能**  
 このリリースで使用できるすべての機能をインストールするには、このセットアップ ロールを選択します。 PowerPivot for SharePoint はこのロールから除外される点に注意してください。 PowerPivot for SharePoint をインストールするには、PowerPivot for SharePoint セットアップ ロールを使用する必要があります。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は **NT AUTHORITY\NETWORK SERVICE** アカウントを使用して開始するように構成されています。 現在のユーザーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**sysadmin** ロールのメンバーとなります。 このオプションで設定した値は、他のコマンド ライン パラメーターを指定してオーバーライドできます。  
  
 オペレーティング システムがドメイン コントローラーでない場合、既定ではデータベース エンジンおよび Reporting Services は NTAUTHORITY\NETWORK SERVICE アカウントを、Integration Services は NTAUTHORITY\NETWORK SERVICE アカウントを、SQL フルテキスト フィルター デーモン ランチャーは NTAUTHORITY\LOCAL SERVICE アカウントを使用します。  
  
## <a name="see-also"></a>関連項目  
 [PowerPivot for SharePoint インストール](https://go.microsoft.com/fwlink/?LinkId=206906)   
 [ハードウェアとソフトウェア要件 (PowerPivot for SharePoint](https://go.microsoft.com/fwlink/?LinkId=216823)   
 [機能の選択](../../../2014/sql-server/install/feature-selection.md)  
  
  
