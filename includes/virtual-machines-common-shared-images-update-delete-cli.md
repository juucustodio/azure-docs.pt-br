---
title: incluir arquivo
description: incluir arquivo
services: virtual-machines
author: cynthn
ms.service: virtual-machines
ms.topic: include
ms.date: 04/25/2019
ms.author: cynthn
ms.custom: include file, devx-track-azurecli
ms.openlocfilehash: fe37b0c9dbc16520a0dcb0993236db2797da6b68
ms.sourcegitcommit: c95e2d89a5a3cf5e2983ffcc206f056a7992df7d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95556551"
---
## <a name="update-resources"></a>Atualizar recursos

Há algumas limitações sobre o que pode ser atualizado. Os seguintes itens podem ser atualizados: 

Galeria de imagens compartilhadas:
- Descrição

definição da imagem:
- vCPUs recomendadas
- Memória recomendada
- Descrição
- Data de fim da vida útil

Versão da imagem:
- Contagem de réplicas regionais
- Regiões de destino
- Exclusão da mais recente
- Data de fim da vida útil

Se você planeja adicionar regiões de réplica, não exclua a imagem gerenciada de origem. A imagem gerenciada de origem é necessária para replicar a versão da imagem para regiões adicionais. 

Atualize a descrição de uma galeria usando o ([AZ SIG Update](/cli/azure/sig?view=azure-cli-latest#az-sig-update). 

```azurecli-interactive
az sig update \
   --gallery-name myGallery \
   --resource-group myGalleryRG \
   --set description="My updated description."
```


Atualize a descrição de uma definição de imagem usando [AZ SIG Image-Definition Update](/cli/azure/sig/image-definition?view=azure-cli-latest#az-sig-image-definition-update).

```azurecli-interactive
az sig image-definition update \
   --gallery-name myGallery\
   --resource-group myGalleryRG \
   --gallery-image-definition myImageDefinition \
   --set description="My updated description."
```

Atualize uma versão de imagem para adicionar uma região a ser replicada usando [AZ SIG Image-Version Update](/cli/azure/sig/image-definition?view=azure-cli-latest#az-sig-image-definition-update). Essa alteração levará algum tempo, pois a imagem será replicada para a nova região.

```azurecli-interactive
az sig image-version update \
   --resource-group myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition \
   --gallery-image-version 1.0.0 \
   --add publishingProfile.targetRegions  name=eastus
```

Este exemplo mostra como usar [AZ SIG Image-Version Update](/cli/azure/sig/image-definition?view=azure-cli-latest#az-sig-image-definition-update) para excluir essa versão da imagem de ser usada como a imagem *mais recente* .

```azurecli-interactive
az sig image-version update \
   --resource-group myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition \
   --gallery-image-version 1.0.0 \
   --set publishingProfile.excludeFromLatest=true
```

Este exemplo mostra como usar [AZ SIG Image-Version Update](/cli/azure/sig/image-definition?view=azure-cli-latest#az-sig-image-definition-update) para incluir essa versão de imagem em ser considerada para a imagem *mais recente* .

```azurecli-interactive
az sig image-version update \
   --resource-group myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition \
   --gallery-image-version 1.0.0 \
   --set publishingProfile.excludeFromLatest=false
```

## <a name="delete-resources"></a>Excluir recursos

Você precisa excluir os recursos na ordem inversa, excluindo a versão da imagem primeiro. Após excluir todas as versões da imagem, você poderá excluir a definição da imagem. Após excluir todas as definições da imagem, você poderá excluir a galeria. 

Exclua uma versão de imagem usando [AZ SIG Image-Version Delete](/cli/azure/sig/image-version?view=azure-cli-latest#az-sig-image-version-delete).

```azurecli-interactive
az sig image-version delete \
   --resource-group myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition \
   --gallery-image-version 1.0.0 
```

Exclua uma definição de imagem usando [AZ SIG Image-Definition Delete](/cli/azure/sig/image-definition?view=azure-cli-latest#az-sig-image-definition-delete).

```azurecli-interactive
az sig image-definition delete \
   --resource-group myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition
```


Exclua uma galeria de imagens usando [AZ SIG Delete](/cli/azure/sig?view=azure-cli-latest#az-sig-delete).

```azurecli-interactive
az sig delete \
   --resource-group myGalleryRG \
   --gallery-name myGallery
```