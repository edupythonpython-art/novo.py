novo.py
import sys

def gerar_orcamento():
    print("\n" + "="*35)
    print("   GERADOR DE ORÇAMENTOS ATIVO   ")
    print("="*35)
    
    nome_cliente = input("Nome do cliente: ").strip()
    if not nome_cliente:
        nome_cliente = "Cliente"
        
    produto = input("Nome do produto/serviço: ").strip()
    if not produto:
        produto = "Produto Geral"
    
    # Proteção para a Quantidade (só aceita números inteiros válidos)
    while True:
        try:
            quantidade = int(input("Quantidade: "))
            if quantidade <= 0:
                print("❌ A quantidade deve ser maior que zero!")
                continue
            break
        except ValueError:
            print("❌ Erro: Digite apenas números inteiros (ex: 1, 2, 5).")

    # Proteção para o Preço (converte vírgula para ponto e aceita decimais)
    while True:
        try:
            preco_raw = input("Preço unitário: ").replace(",", ".")
            preco_unitario = float(preco_raw)
            if preco_unitario < 0:
                print("❌ O preço não pode ser negativo!")
                continue
            break
        except ValueError:
            print("❌ Erro: Digite um valor numérico válido (ex: 49.90).")

    # Proteção para o Desconto
    while True:
        try:
            desc_raw = input("Valor do desconto (ou 0): ").replace(",", ".")
            desconto = float(desc_raw)
            if desconto < 0:
                print("❌ O desconto não pode ser negativo!")
                continue
            break
        except ValueError:
            print("❌ Erro: Digite um valor numérico válido.")

    # Cálculos automáticos
    valor_total = (quantidade * preco_unitario) - desconto
    if valor_total < 0:
        valor_total = 0.0

    # Layout final profissional pronto para cópia
    mensagem_whatsapp = f"""
*Olá, {nome_cliente}! Seu orçamento ficou pronto!* 🎉

📦 *Resumo do Pedido:*
• Produto: {produto}
• Qtd: {quantidade}x
• Valor Unitário: R$ {preco_unitario:.2f}
• Desconto aplicado: R$ {desconto:.2f}

💰 *Total a pagar:* R$ {valor_total:.2f}

*Deseja confirmar o pedido?* 🚀
"""

    print("\n" + "-"*15 + " COPIE ABAIXO " + "-"*15)
    print(mensagem_whatsapp)
    print("-"*44)

# Loop principal para manter o programa rodando até o usuário decidir sair
while True:
    gerar_orcamento()
    continuar = input("\nDeseja gerar outro orçamento? (S/N): ").strip().upper()
    if continuar != 'S':
        print("\nSaindo do sistema... Obrigado por utilizar! 👋")
        break
