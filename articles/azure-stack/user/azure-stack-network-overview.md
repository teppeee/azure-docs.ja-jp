---
title: Azure Stack ネットワークの概要 | Microsoft Docs
description: Azure Stack ネットワークについて
services: azure-stack
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.topic: get-started-article
ms.date: 01/14/2019
ms.author: mabrigg
ms.reviewer: scottnap
ms.lastreviewed: 01/14/2019
ms.openlocfilehash: c54f1f8ed8447c69dbfa924469d854ebdd97407f
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2019
ms.locfileid: "55252202"
---
# <a name="introduction-to-azure-stack-networking"></a>Azure Stack ネットワークの概要

*適用対象:Azure Stack 統合システムと Azure Stack Development Kit*

Azure Stack には、単独でまたは組み合わせて使用できるさまざまなネットワーク機能が用意されています。

- **Azure Stack リソースの間の接続**  
    クラウド内の安全なプライベート仮想ネットワークで Azure のリソースを接続します。
- **インターネット接続**  
    インターネットを介して双方向で Azure Stack リソースと通信します。
- **オンプレミスの接続**  
    インターネット上の仮想プライベート ネットワーク (VPN) を介して、または Azure Stack への専用接続を介して、オンプレミスのネットワークを Azure Stack リソースに接続します。
- **負荷分散とトラフィックの方向**  
    同じ場所のサーバー間でトラフィックを負荷分散したり、異なる場所のサーバーにトラフィックを誘導したりします。
- **セキュリティ**  
    ネットワーク サブネット間や個々の仮想マシン (VM) 間のネットワーク トラフィックをフィルタリングします。
- **ルーティング**  
    Azure Stack リソースとオンプレミス リソースとの間で既定のルーティングまたは完全制御のルーティングを使用します。
- **管理の容易性**  
    Azure Stack のネットワーク リソースを監視したり管理したりします。
- **デプロイ ツールと構成ツール**  
    Web ベースのポータルまたはクロスプラットフォームのコマンド ライン ツールを使って、ネットワーク リソースのデプロイと構成を行います。


## <a name="next-steps"></a>次の手順

* [Azure Stack ネットワークに関する考慮事項](azure-stack-network-differences.md)