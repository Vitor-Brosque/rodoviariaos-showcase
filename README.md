# RodoviariaOS

**O sistema que organiza uma revenda de carros seminovos: do primeiro "oi" no WhatsApp até o dinheiro no caixa de cada sócio.**

Nasceu na revenda da minha família, onde eu cuidava do atendimento e dos anúncios. Hoje é usado todos os dias na loja.

> 🔒 Este repositório é uma vitrine. O código é fechado porque quero transformar o sistema em produto para outras revendas.

---

## Para quem é

Para revendas pequenas e médias, em geral com mais de um sócio, alguns vendedores e um financeiro que até hoje vive em planilha.

## Como era antes

- O cliente mandava mensagem no WhatsApp pessoal de um vendedor. Se o vendedor esquecia de responder, ninguém ficava sabendo.
- A loja pagava anúncio no Instagram e no Facebook, mas não sabia qual anúncio tinha trazido o cliente que comprou.
- Cada sócio tinha os próprios carros, mas as despesas da loja eram divididas à mão no fim do mês.
- Custo do carro, comissão do banco no financiamento e impostos ficavam espalhados em planilhas.

## Como fica: a vida de um carro e de um cliente

```mermaid
flowchart LR
    A[A loja compra<br/>um carro] --> B[Cliente manda<br/>mensagem]
    B --> C[Vendedor<br/>atende]
    C --> D[Venda<br/>fechada]
    D --> E[Dinheiro no caixa<br/>do sócio certo]
```

1. **A loja compra um carro.** Ele ganha uma ficha com o preço pago, a tabela FIPE e tudo o que se gasta para deixá-lo pronto para venda. Antes da compra, o sistema ajuda a avaliar oportunidades em portais de classificados e mostra os defeitos mais conhecidos do modelo.
2. **Um cliente manda mensagem.** Pode vir de um anúncio ou direto no WhatsApp da loja. A conversa entra no sistema sozinha, vai para a fila de um vendedor e fica marcada com o anúncio e o carro que trouxeram o cliente.
3. **O vendedor atende.** Ele vê quem precisa de resposta agora e quem precisa de um novo contato. Se o cliente desiste, o vendedor registra o motivo. Se chega à loja um carro que outro cliente estava procurando, o sistema avisa.
4. **A venda fecha.** A proposta junta entrada, financiamento e carro na troca, e o contrato sai do sistema. Quando o último pagamento cai, a venda é encerrada sozinha. Se a venda é desfeita, o histórico continua guardado.
5. **O dinheiro chega ao sócio certo.** O resultado do carro vai para o caixa do sócio dono dele, e as despesas da loja são divididas entre os sócios automaticamente. O sistema também calcula a comissão que o banco paga pelo financiamento e os impostos. O extrato do banco pode ser importado, e o sistema aprende a classificar cada lançamento.

## O que cada pessoa vê

| Quem | O que vê no sistema |
|---|---|
| **Vendedor** | A fila de clientes, as conversas e o estoque. Não vê custo nem margem dos carros. |
| **Sócio** | Os próprios carros, o próprio caixa e o resultado do mês. Os carros do outro sócio aparecem só como catálogo. |
| **Marketing** | Os anúncios e quantos clientes e vendas cada um trouxe. |
| **Contabilidade** | Lançamentos, impostos e extratos. |

A equipe também pode perguntar ao sistema pelo WhatsApp sobre estoque, clientes e números. Quando o pedido muda alguma coisa, ele só executa depois de uma pessoa confirmar. Esse assistente é opcional: a loja usa tudo sem ele.

## Em que pé está

**Em uso na loja:** atendimento pelo WhatsApp, origem dos clientes, ficha dos carros, vendas, financeiro por sócio, perfis de acesso, assistente no WhatsApp e avaliação de compra.

**Pronto, esperando a loja conectar as contas:** criar o anúncio a partir da ficha do carro e pausá-lo quando o carro é vendido, além de publicar no Instagram, Facebook, TikTok, YouTube e Google Meu Negócio. Gastar com anúncio sempre pede confirmação e respeita um limite de verba.

**Em andamento:**
- simulação de financiamento direto nos sites dos bancos;
- site da loja mostrando o estoque atualizado;
- publicação automática nos portais de classificados.

---

## Por dentro (para quem é da área)

| Parte | Tecnologia |
|---|---|
| Telas | Next.js, React, TypeScript, Tailwind CSS |
| API | Fastify, TypeScript, Zod |
| Banco de dados | PostgreSQL, Drizzle ORM |
| WhatsApp | WAHA, com mensagens recebidas por webhook assinado |
| Atualização em tempo real | Server-Sent Events |
| Testes | Vitest, rodando contra um banco de verdade |

Algumas decisões que tomei:

- **Separação entre sócios no próprio banco.** O que cada sócio pode ver é garantido pelo PostgreSQL (Row Level Security), e não só escondido na tela. Se alguém criar uma tabela nova sem essa proteção, um teste quebra.
- **Dinheiro só entra como lançamento.** Venda, despesa e comissão viram lançamentos com dono definido. Quando uma venda é desfeita, o sistema cria lançamentos novos em vez de apagar os antigos.
- **O passado não muda.** Alterar uma taxa hoje não mexe nas vendas que já foram feitas.

## Contato

Vitor Brosque · [LinkedIn](https://www.linkedin.com/in/vitorbrosque) · [Portfólio](https://vitor-brosque.github.io)
