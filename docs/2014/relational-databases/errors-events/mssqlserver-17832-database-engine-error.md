---
title: MSSQLSERVER_17832 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17828 (Database Engine error)
- maxtokensize
- 17832 (Database Engine error)
- login packet (bad)
ms.assetid: bd56ffe4-0855-4ada-8aca-251fbc6ff2ce
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1280bb44d11ce4f8234d544bf113e796a9c3c85c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915430"
---
# <a name="mssqlserver17832"></a>MSSQLSERVER_17832
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|17832|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SRV_BAD_LOGIN_PKT|  
|メッセージ テキスト|接続を開くのに使用したログイン パケットの構造は無効です。接続が閉じられました。 クライアント ライブラリのベンダーに問い合わせてください。%.*ls|  
  
## <a name="explanation"></a>説明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターはクライアントのログイン パケットを処理できませんでした。 パケットが正しく作成されなかったか、パケットが転送中に破損した可能性があります。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターの構成が原因である可能性もあります。 表示される IP アドレスは、クライアント コンピューターのアドレスです。  
  
### <a name="more-information"></a>詳細情報  
 Kerberos 環境で Windows 認証を使用する場合、クライアントは特権属性証明 (PAC) を含む Kerberos チケットを受け取ります。 PAC には、ユーザーがメンバーとなっているグループ、ユーザーが持つ権限、ユーザーに適用されるポリシーなど、さまざまな種類の承認データが含まれます。 クライアントが Kerberos チケットを受け取ると、PAC に含まれる情報を使用してユーザーのアクセス トークンが生成されます。 クライアントは、このトークンをログイン パケットの一部として [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターに提供します。  
  
 トークンが正しく作成されなかったか、転送中に破損した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は問題に関する追加情報を提供できません。  
  
 ユーザーが多数のグループのメンバーであるか、多数のポリシーを持つ場合、それらすべてを一覧表示するトークンは通常よりも大きくなる可能性があります。 トークンがサーバー コンピューターの **MaxTokenSize** 値よりも大きくなると、クライアントは一般的なネットワーク エラー (GNE) によって接続に失敗し、エラー 17832 が発生することがあります。 この問題は、多数のグループに属しているか、多数のポリシーを持つ一部のユーザーのみに影響します。 問題の原因がサーバー コンピューターの **MaxTokenSize** 値である場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログのエラー 17832 は、状態 9 のエラーを伴います。 Kerberos および **MaxTokenSize** の詳細については、[KB327825](https://support.microsoft.com/kb/327825) を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
 この問題を解決するには、サーバー コンピューターの **MaxTokenSize** 値を、組織内のユーザーの最も大きなトークンを格納できるサイズに増やします。 組織に適したトークン サイズを調べるには、**Tokensz** アプリケーションの使用を検討してください。   
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 **サーバー コンピューターの MaxTokenSize を変更するには**  
  
1.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。  
  
2.  型`regedit`、 をクリックし、 **OK**します。 ( **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[続行]** をクリックします)。  
  
3.  **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa\Kerberos\Parameters** に移動します。  
  
4.  **MaxTokenSize** パラメーターが存在しない場合は、 **[Parameters]** を右クリックし、 **[新規]** をポイントして、 **[DWORD (32 ビット) 値]** をクリックします。 レジストリ エントリに **MaxTokenSize** という名前を付けます。  
  
5.  **[MaxTokenSize]** を右クリックし、 **[修正]** をクリックします。  
  
6.  **[値のデータ]** ボックスに、目的の **MaxTokenSize** 値を入力します。  
  
    > [!NOTE]  
    >  最大推奨トークン サイズは、16 進数値 ffff (10 進数値 65535) です。 この値を指定することで、ほとんどの場合は問題が解決しますが、コンピューター全体のパフォーマンスに悪影響が出る可能性があります。 組織のユーザーの最も大きなトークンに対応する最小限の **MaxTokenSize** 値を確認し、その値を入力することをお勧めします。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  **レジストリ エディター**を閉じます。  
  
9. コンピューターを再起動します。  
  
  
