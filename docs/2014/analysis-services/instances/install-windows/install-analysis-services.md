---
title: 表形式モードで Analysis Services のインストール |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bf1a8ee0d5dd3dde585a027fd08fd833fb40304
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079911"
---
# <a name="install-analysis-services-in-tabular-mode"></a>表形式モードでの Analysis Services のインストール
  新しい表形式のモデリング機能を使用して Analysis Services をインストールする場合、この種類のモデルを使用できるサーバー モードで Analysis Services をインストールする必要があります。 そのサーバー モードは "表形式" であり、インストール時に構成されます。  
  
 このモードでサーバーをインストールすると、表形式モデル デザイナーで作成したホスト ソリューションで使用できます。 ネットワーク上で表形式のモデル データにアクセスする場合は、表形式モードのサーバーが必要です。  
  
 表形式モードは、インストール ウィザードまたはコマンド ライン セットアップで指定できます。 次のセクションでは、それぞれの方法について説明します。  
  
## <a name="installation-wizard"></a>インストール ウィザード  
 Analysis Services を表形式モードでインストールする場合に使用する SQL Server インストール ウィザードのページを次の一覧に示します。  
  
1.  セットアップの機能ツリーで **[Analysis Services]** をクリックします。  
  
     ![セットアップの機能ツリー Analsyis サービスを示す](../../../sql-server/install/media/ssas-setupas.gif "Analsyis サービスを示すセットアップの機能ツリー")  
  
2.  Analysis Services の構成 ページで、選択することを確認する**表形式モード**します。  
  
     ![Analysis Services の構成オプションを使用してセットアップ ページ](../../../sql-server/install/media/ssas-setupasconfig.gif "Analysis Services の構成オプションを使用してセットアップ ページ")  
  
 表形式モードでは xVelocity メモリ内分析エンジン (VertiPaq) を使用します。このエンジンは Analysis Services に配置するテーブル モデルの既定のストレージです。 サーバーにテーブル モデル ソリューションを配置すると、表形式ソリューションを構成する際に、メモリ負荷の高いストレージの代わりに DirectQuery ディスク ストレージを使用することもできます。  
  
## <a name="command-line-setup"></a>コマンド ライン セットアップ  
 SQL Server セットアップにはサーバー モードを指定する新しいパラメーター (`ASSERVERMODE`) があります。 次の例は、Analysis Services を表形式サーバー モードでインストールするコマンド ライン セットアップを示しています。  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 `INSTANCENAME` は 17 文字未満にする必要があります。  
  
 プレースホルダー アカウント値はすべて、有効なアカウントおよびパスワードに置き換える必要があります。  
  
 SQL Server Management Studio や [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] などのツールは、提供されているコマンド ライン構文の例ではインストールされません。 機能の追加に関する詳細については、次を参照してください。[コマンド プロンプトから SQL Server 2014 のインストール](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)します。  
  
 `ASSERVERMODE` では、大文字と小文字が区別されます。  値はすべて大文字で指定する必要があります。 次の表に、`ASSERVERMODE` の有効な値を示します。  
  
|値|説明|  
|-----------|-----------------|  
|MULTIDIMENSIONAL|これが既定値です。 `ASSERVERMODE` を設定しない場合、サーバーは多次元サーバー モードでインストールされます。|  
|POWERPIVOT|この値は省略可能です。 実際には、`ROLE` パラメーターを設定した場合、サーバー モードは自動的に 1 に設定され、SharePoint のインストール時に PowerPivot の `ASSERVERMODE` が省略可能になります。 詳細については、次を参照してください。[コマンド プロンプトから PowerPivot をインストール](../../../sql-server/install/install-powerpivot-from-the-command-prompt.md)します。|  
|TABULAR|コマンド ライン セットアップを使用して Analysis Services を表形式モードでインストールする場合、この値は必須です。|  
  
## <a name="see-also"></a>参照  
 [Analysis Services インスタンスのサーバー モードの決定](../determine-the-server-mode-of-an-analysis-services-instance.md)   
 [メモリ内またはテーブル モデル データベース用 DirectQuery アクセスを構成します。](../../tabular-models/enable-directquery-mode-in-ssms.md)   
 [テーブル モデリング&#40;SSAS 表形式&#41;](../../tabular-models/tabular-models-ssas.md)  
  
  
