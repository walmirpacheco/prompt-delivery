Como eu criei um assistente de combinações no Amazon Bedrock e Step Functions

Pessoal, vou explicar como montei aquele assistente que sugere combinações completas de refeição. A ideia é simples: o usuário pede uma sugestão e o sistema retorna uma combinação com comida, bebida e uma ideia criativa.

A Arquitetura que usei:

Amazon Bedrock - Para a IA gerar as sugestões

Step Functions - Para orquestrar todo o fluxo

Lambda Functions - Para conectar tudo

O Fluxo Passo a Passo:

Primeiro: Criei um state machine no Step Functions com este esquema:

Passo 1: Recebe o pedido do usuário (ex: "quero uma sugestão para jantar")

Passo 2: Chama uma Lambda que usa o Bedrock para gerar ideias de comida

Passo 3: Outra Lambda que gera sugestões de bebida no Bedrock

Passo 4: Mais uma Lambda que cria uma ideia de combinação criativa

Passo 5: Retorna tudo organizado para o usuário

Como funciona o Bedrock nisso:

Eu configurei as Lambdas para chamar modelos como o Claude da Anthropic através do Bedrock. Cada Lambda tem um prompt específico:

Para comida: "Sugira um prato principal para [ocasião]"

Para bebida: "Recomende uma bebida que combine com [prato]"

Para combinação: "Dê uma ideia criativa de como servir isso"

O Pulso do Negócio:

O Step Functions é perfeito porque se uma etapa falhar, ele automaticamente tenta de novo. E eu consigo ver exatamente em qual passo está cada solicitação.

Exemplo de Uso:

Usuário pergunta: "Ideia para festa"
O sistema retorna:

Comida: Tacos

Bebida: Margarita

Combinação: "Festa mexicana com decoração colorida"