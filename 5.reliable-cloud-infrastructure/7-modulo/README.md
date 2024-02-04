# Como criar sistemas confiáveis

## Visão Geral

Neste módulo, você aprenderá a projetar sistemas confiáveis. Vamos ensinar como projetar serviços para atender aos requisitos de disponibilidade, durabilidade e escalonabilidade. Mostraremos maneiras de implementar sistemas tolerantes a falhas, evitando pontos únicos de falha, falhas correlacionadas e falhas em cascata. 

A sobrecarga também representa um risco para os sistemas distribuídos, portanto, você aprenderá a evitar esse tipo de falha por meio de padrões de projeto, como disjuntores e espera exponencial truncada ¹. Além disso, você aprenderá a projetar sistemas de armazenamento de dados resilientes com exclusão lenta. Quando ocorrem problemas, é importante manter os sistemas sob controle. Portanto, abordaremos decisões de projeto para cenários de falha e estados operacionais diferentes, como normal e degradado. Por fim, discutiremos como analisar cenários de desastre e planejar, implementar e testar a recuperação de desastres.

---

¹ *A espera exponencial truncada (truncated exponential backoff) é uma estratégia que ajuda a lidar com problemas temporários em sistemas distribuídos. Quando ocorre um problema, como um servidor congestionado, o sistema espera um curto período antes de tentar novamente. Se a tentativa falhar, ele aumenta o tempo de espera, mas com um limite máximo. Isso evita sobrecarregar ainda mais o servidor e ajuda na recuperação automática de falhas temporárias. Em resumo, é uma abordagem para esperar e tentar novamente de forma inteligente quando algo dá errado. bem semelhante com 'retries'*