## Sobre este setup

Este compose foi pensado para ambientes mais próximos de produção, onde o n8n precisa rodar de forma organizada, segura e preparada para crescimento.

O ambiente utiliza o Traefik como proxy reverso para fornecer HTTPS automático com Let's Encrypt, acesso via domínio personalizado e publicação do n8n em uma subpasta (ex: `/n8n`), permitindo compartilhar o mesmo domínio com outros serviços da VPS.

Além disso, o setup separa a execução dos workflows em runners externos, melhorando desempenho e estabilidade em automações mais pesadas, como integrações com IA, processamento de arquivos, webhooks de alto volume e múltiplos fluxos simultâneos.

### Principais objetivos deste setup

* Publicar o n8n com HTTPS automático
* Rodar o n8n em subpasta (`/n8n`)
* Facilitar ambientes com múltiplos serviços no mesmo domínio
* Evitar exposição direta da porta do n8n
* Melhorar segurança com headers HTTPS e proxy reverso
* Preparar o ambiente para escalabilidade futura
* Separar execução dos workflows da interface principal
* Facilitar deploys em VPS usando Docker Compose

### Exemplo de acesso

```txt
https://seudominio.com/n8n
```

### Indicado para

* Ambientes de produção
* VPS com múltiplos serviços
* Uso com Cloudflare
* Workflows pesados ou com IA
* Uso intensivo de webhooks
* Ambientes que exigem HTTPS confiável


## Iniciar

Para iniciar o n8n em uma subpasta, basta executar o docker-compose executando o seguinte
comando na pasta atual.

**IMPORTANTE:** Mas antes de fazer isso, altere os usuários e senhas padrão no arquivo `.env`!

```
 docker-compose up -d
```

Para interromper o processo, execute:

```
 docker-compose stop
```

