---
title: Visão geral do Fala Personalizada-serviço de fala
titleSuffix: Azure Cognitive Services
description: Fala Personalizada é um conjunto de ferramentas online que permite avaliar e melhorar a precisão de fala para texto da Microsoft para seus aplicativos, ferramentas e produtos.
services: cognitive-services
author: trevorbye
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 02/12/2021
ms.author: trbye
ms.custom: contperf-fy21q2; references_regions
ms.openlocfilehash: f2dca513b4413f1761ea1b21bf71f90bb27d3053
ms.sourcegitcommit: d4734bc680ea221ea80fdea67859d6d32241aefc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100388644"
---
# <a name="what-is-custom-speech"></a>O que é a Fala Personalizada?

[Fala personalizada](https://aka.ms/customspeech) é um conjunto de ferramentas baseadas na interface do usuário que permitem avaliar e melhorar a precisão da fala para o texto da Microsoft para seus aplicativos e produtos. Tudo o que é necessário para começar é um grande quantidade de arquivos de áudio de teste. Siga os links neste artigo para começar a criar uma experiência de fala em texto Personalizada.

## <a name="whats-in-custom-speech"></a>O que há de Fala Personalizada?

Para poder fazer qualquer coisa com Fala Personalizada, você precisará de uma conta do Azure e uma assinatura do serviço de fala. Depois de ter uma conta, você pode preparar seus dados, treinar e testar seus modelos, inspecionar a qualidade do reconhecimento, avaliar a precisão e, por fim, implantar e usar o modelo de fala em texto personalizado.

Este diagrama realça as partes que compõem a [área de fala personalizada do Speech Studio](https://aka.ms/customspeech). Use os links abaixo para saber mais sobre cada etapa.

![Diagrama que realça os componentes que compõem a área de Fala Personalizada do Speech Studio.](./media/custom-speech/custom-speech-overview.png)

1. [Assine e crie um projeto](#set-up-your-azure-account). Crie uma conta do Azure e assine o serviço de fala. Essa assinatura unificada fornece acesso a fala-para-texto, conversão de fala e fala do Speech [Studio](https://speech.microsoft.com/customspeech). Em seguida, use sua assinatura do serviço de fala para criar seu primeiro projeto de Fala Personalizada.

1. [Carregar dados de teste](./how-to-custom-speech-test-and-train.md). Carregue dados de teste (arquivos de áudio) para avaliar a oferta de fala a texto da Microsoft para seus aplicativos, ferramentas e produtos.

1. [Inspecione a qualidade do reconhecimento](how-to-custom-speech-inspect-data.md). Use o [Speech Studio](https://speech.microsoft.com/customspeech) para reproduzir áudio carregado e inspecione a qualidade do reconhecimento de fala de seus dados de teste. Para medições quantitativas, consulte [inspecionar dados](how-to-custom-speech-inspect-data.md).

1. [Avalie e aprimore a precisão](how-to-custom-speech-evaluate-data.md). Avalie e aprimore a precisão do modelo de conversão de fala em texto. O [Speech Studio](https://speech.microsoft.com/customspeech) fornecerá uma *taxa de erros do Word*, que você pode usar para determinar se o treinamento adicional é necessário. Se estiver satisfeito com a precisão, você poderá usar as APIs do serviço de fala diretamente. Se você quiser melhorar a precisão por uma média relativa de 5% a 20%, use a guia **treinamento** no portal para carregar dados de treinamento adicionais, como transcrições com rótulo humano e texto relacionado.

1. [Treine e implante um modelo](how-to-custom-speech-train-model.md). Melhore a precisão do seu modelo de fala para texto fornecendo transcrições escritas (10 a 1.000 horas) e texto relacionado (<200 MB) junto com seus dados de teste de áudio. Esses dados ajudam a treinar o modelo de conversão de fala em texto. Após o treinamento, teste novamente. Se estiver satisfeito com o resultado, você poderá implantar seu modelo em um ponto de extremidade personalizado.

## <a name="set-up-your-azure-account"></a>Configurar sua conta do Azure

Você precisa ter uma assinatura do serviço de fala e conta do Azure antes de poder usar o [Speech Studio](https://speech.microsoft.com/customspeech) para criar um modelo personalizado. Se você não tiver uma conta e uma assinatura, [experimente o serviço de Fala gratuitamente](overview.md#try-the-speech-service-for-free).

> [!NOTE]
> Se você planeja treinar um modelo personalizado com **dados de áudio**, escolha uma das seguintes regiões que têm hardware dedicado disponível para treinamento. Isso reduzirá o tempo necessário para treinar um modelo.

* Leste da Austrália
* Canadá Central
* Índia Central
* Leste dos EUA
* Leste dos EUA 2
* Centro-Norte dos EUA
* Norte da Europa
* Centro-Sul dos Estados Unidos
* Sudeste Asiático
* Sul do Reino Unido
* Governo dos EUA do Arizona
* Gov. dos EUA – Virgínia
* Europa Ocidental
* Oeste dos EUA 2

> [!NOTE]
> Certifique-se de criar uma assinatura padrão (S0). Não há suporte para assinaturas gratuitas (F0).

Depois de criar uma conta do Azure e uma assinatura do serviço de fala, você precisará entrar no [Speech Studio](https://speech.microsoft.com/customspeech) e conectar sua assinatura.

1. Entre no [Speech Studio](https://aka.ms/custom-speech).
1. Selecione a assinatura na qual você precisa trabalhar e crie um projeto de fala.
1. Se você quiser modificar sua assinatura, selecione o botão engrenagem no menu superior.

## <a name="how-to-create-a-project"></a>Como criar um projeto

Conteúdo como dados, modelos, testes e pontos de extremidade são organizados em *projetos* no [Speech Studio](https://speech.microsoft.com/customspeech). Cada projeto é específico de um domínio e país/idioma. Por exemplo, você pode criar um projeto para centros de chamadas que usam o inglês no Estados Unidos.

Para criar seu primeiro projeto, selecione **fala-para-texto/fala personalizada** e, em seguida, selecione **novo projeto**. Siga as instruções fornecidas pelo Assistente para criar seu projeto. Depois de criar um projeto, você deverá ver quatro guias: **dados**, **teste**, **treinamento** e **implantação**. Use os links fornecidos nas [próximas etapas](#next-steps) para aprender a usar cada guia.

> [!IMPORTANT]
> O [Speech Studio](https://aka.ms/custom-speech) , anteriormente conhecido como "portal de fala personalizada", foi atualizado recentemente! Se você criou dados, modelos, testes e pontos de extremidade publicados anteriores no portal do CRIS.ai ou com APIs, você precisa criar um novo projeto no novo portal para se conectar a essas entidades antigas.

## <a name="model-lifecycle"></a>Ciclo de vida do modelo

Fala Personalizada usa *modelos de base* e *modelos personalizados*. Cada idioma tem um ou mais modelos de base. Geralmente, quando um novo modelo de fala é liberado para o serviço de fala regular, ele também é importado para o serviço de Fala Personalizada como um novo modelo de base. Eles são atualizados a cada três a 6 meses. Modelos mais antigos normalmente se tornam menos úteis ao longo do tempo porque o modelo mais recente geralmente tem maior precisão.

Por outro lado, modelos personalizados são criados adaptando um modelo de base escolhido para um cenário de cliente específico. Você pode continuar usando um modelo personalizado específico por um longo período depois de ter um que atenda às suas necessidades. Mas é recomendável que você atualize periodicamente para o modelo base mais recente e retreine-o ao longo do tempo com dados adicionais. 

Outros termos principais relacionados ao ciclo de vida do modelo incluem:

* **Adaptação**: pegar um modelo base e personalizá-lo para seu domínio/cenário usando dados de texto e/ou dados de áudio.
* **Decodificação**: usando um modelo e executando o reconhecimento de fala (decodificando áudio em texto).
* **Ponto de extremidade**: uma implantação específica do usuário de um modelo base ou de um modelo personalizado que é acessível *somente* para um determinado usuário.

### <a name="expiration-timeline"></a>Linha do tempo de expiração

Conforme novos modelos e novas funcionalidades se tornam disponíveis e modelos mais antigos e menos precisos são desativados, consulte as seguintes linhas do tempo para expiração de modelo e ponto de extremidade:

**Modelos de base** 

* Adaptação: disponível por um ano. Depois que o modelo for importado, ele estará disponível por um ano para criar modelos personalizados. Após um ano, novos modelos personalizados devem ser criados a partir de uma versão mais recente do modelo base.  
* Decodificação: disponível por dois anos após a importação. Portanto, você pode criar um ponto de extremidade e usar a transcrição do lote por dois anos com esse modelo. 
* Pontos de extremidade: disponíveis na mesma linha do tempo que a decodificação.

**Modelos personalizados**

* Decodificação: disponível por dois anos após a criação do modelo. Portanto, você pode usar o modelo personalizado por dois anos (lote/tempo real/teste) após sua criação. Depois de dois anos, *você deve treinar novamente seu modelo* porque o modelo base normalmente terá sido preterido para adaptação.  
* Pontos de extremidade: disponíveis na mesma linha do tempo que a decodificação.

Quando um modelo de base ou modelo personalizado expira, ele sempre retorna para a *versão mais recente do modelo base*. Portanto, sua implementação nunca será interrompida, mas poderá se tornar menos precisa para *seus dados específicos se os* modelos personalizados atingirem a expiração. Você pode ver a expiração de um modelo nos seguintes locais na área de Fala Personalizada do Speech Studio:

* Resumo do treinamento de modelo
* Detalhes de treinamento do modelo
* Resumo de implantação
* Detalhes da implantação

Você também pode verificar as datas de expiração por meio das [`GetModel`](https://westus.dev.cognitive.microsoft.com/docs/services/speech-to-text-api-v3-0/operations/GetModel) [`GetBaseModel`](https://westus.dev.cognitive.microsoft.com/docs/services/speech-to-text-api-v3-0/operations/GetBaseModel) APIs de fala personalizadas e sob a `deprecationDates` Propriedade na resposta JSON.

Observe que você pode atualizar o modelo em um ponto de extremidade de fala personalizado sem tempo de inatividade alterando o modelo usado pelo ponto de extremidade na seção de implantação do Speech Studio ou por meio da API de fala personalizada.

## <a name="next-steps"></a>Próximas etapas

* [Preparar e testar seus dados](./how-to-custom-speech-test-and-train.md)
* [Inspecione seus dados](how-to-custom-speech-inspect-data.md)
* [Avaliar e melhorar a precisão do modelo](how-to-custom-speech-evaluate-data.md)
* [Treinar e implantar um modelo](how-to-custom-speech-train-model.md)
