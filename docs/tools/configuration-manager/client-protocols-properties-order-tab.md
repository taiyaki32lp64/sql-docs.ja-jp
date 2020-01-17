---
title: クライアントプロトコルのプロパティ ([順序] タブ) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- client protocols [SQL Server]
ms.assetid: 64fd7135-1756-4885-bed9-9ab8997ecc6c
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: bbf7795da30f2a274201ce51e9774390b7611b48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010240"
---
# <a name="client-protocols-properties-order-tab"></a>[クライアント プロトコルのプロパティ] ダイアログ ボックス ([順序] タブ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  **[クライアント プロトコルのプロパティ]** ダイアログ ボックスの **[順序]** ページでは、クライアント プロトコルの表示や有効の設定を行います。  
  
 プロトコルをクリックして **[有効化]** または **[無効化]** をクリックすると、選択したプロトコルが **[無効なプロトコル]** 一覧または **[有効なプロトコル]** 一覧に移動します。  
  
 プロトコルは一覧内の順序で試行されます。つまり、まず最上位のプロトコルで接続が試みられ、次に 2 番目のプロトコルで接続が試みられます。 **[有効なプロトコル]** 一覧のプロトコルを上下に移動するには、上下の矢印ボタンをクリックします。 **共有メモリ** プロトコルが有効になっている場合、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に同じコンピューター上のクライアントから接続するときには常にそのプロトコルが最初に試行されます。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET SqlClient は、これらの設定を使用しません。 .NET SqlClient のプロトコルの順序は、最初に TCP、次に名前付きパイプであり、この順序は変更できません。  
  
## <a name="options"></a>オプション  
 **[無効なプロトコル]**  
 インストールされているが現在使用されていないプロトコルが一覧表示されます。  
  
 **[有効なプロトコル]**  
 このコンピューターの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]クライアントが使用できる[!INCLUDE[msCoName](../../includes/msconame-md.md)]プロトコルの一覧を表示します。  
  
 **>**  
 **[無効なプロトコル]** ボックス内で現在強調表示されているプロトコルを有効にし、 **[有効なプロトコル]** ボックスに移動します。  
  
 **\<**  
 **[有効なプロトコル]** ボックス内で現在強調表示されているプロトコルを無効にし、 **[無効なプロトコル]** ボックスに移動します。  
  
 上矢印  
 強調表示されているプロトコルを一覧内で上に移動します。 これにより、Net-Library が接続のためにプロトコルを使用するときの優先順位が上がります。  
  
 下矢印  
 強調表示されているプロトコルを一覧内で下に移動します。 この場合、ネットワーク ライブラリが接続のためにプロトコルを使用するときの優先順位が下がります。  
  
 **[共有メモリ プロトコルを有効にする]**  
 共有メモリ プロトコルを有効にします。共有メモリ プロトコルが有効になっている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に同じコンピューター上のクライアントから接続するときには常にそのプロトコルが最初に試行されます。  
  
> [!NOTE]  
>  プロトコルをプレフィックスによって指定した場合や、接続文字列の一部として指定した場合は、その指定したプロトコルだけが試行されます。  
  
## <a name="see-also"></a>参照  
 [ネットワーク プロトコルの選択](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
