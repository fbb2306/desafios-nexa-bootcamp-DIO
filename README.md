# desafios-nexa-bootcamp-DIO
Neste repositório fizemos e executamos os códigos do desafio com sucesso. Desafio 1, 2 e 3.


----------------------------------------------------------------------------------
Desafio 1
----------------------------------------------------------------------------------

import sys

caracteristicas_modelos = {
    "automatizar tarefas": "Claude 3 Opus",
    "pesquisa e desenvolvimento": "Claude 3 Opus",
    "resposta rápida e capacidade de resposta quase instantânea": "Claude 3 Haiku",
    "motores de chatbots de lojas": "Claude 3 Haiku",
    "moderação de conteúdo": "Claude 3 Haiku",
    "processamento de tarefas mais básicas": "Claude 3 Haiku",
    "raciocínio cuidadoso": "Claude 3 Sonnet",
    "processamento de dados": "Claude 3 Sonnet",
    "aplicações de vendas": "Claude 3 Sonnet",
    "extração de texto de imagens": "Claude 3 Sonnet",
    "equilíbrio ideal entre inteligência e velocidade": "Claude 3 Sonnet",
}

def encontrar_modelo(caracteristica_fornecida, caracteristicas_modelos):
    for caracteristica, modelo in caracteristicas_modelos.items():
        if caracteristica.lower() in caracteristica_fornecida.lower():
            return modelo
    return "Modelo não encontrado."


caracteristica_fornecida = sys.stdin.readline().strip()

modelo_correspondente = encontrar_modelo(caracteristica_fornecida, caracteristicas_modelos)
print(modelo_correspondente)



-------------------------------------------------------------------------------------------------------------------------------
Desafio 2
-------------------------------------------------------------------------------------------------------------------------------

import sys

class ModeloIA:
    def __init__(self, nome, desempenho, velocidade, custo, capacidades):
        self.nome = nome
        self.desempenho = desempenho
        self.velocidade = velocidade
        self.custo = custo
        self.capacidades = capacidades
    
    def __str__(self):
        return self.nome

def recomendar_modelo(caracteristicas, modelos):
    modelo_recomendado = None
    capacidades_usuario = [capacidade.lower() for capacidade in caracteristicas['Capacidades']]

    for modelo in modelos:
        capacidades_modelo = [capacidade.lower() for capacidade in modelo.capacidades]
        
        if all(capacidade in capacidades_modelo for capacidade in capacidades_usuario):
            if modelo_recomendado is None or (
                modelo.desempenho >= caracteristicas['Desempenho'] and
                modelo.velocidade >= caracteristicas['Velocidade'] and
                modelo.custo <= caracteristicas['Custo']
            ):
                modelo_recomendado = modelo

    return modelo_recomendado if modelo_recomendado else "Nenhum modelo encontrado."

def gerar_explicacao(modelo, caracteristicas):
    if isinstance(modelo, ModeloIA):
        explicacao = f"O {modelo.nome} é o modelo recomendado."
        return explicacao
    else:
        return modelo

def obter_caracteristicas():
    caracteristicas = {}
    caracteristicas['Desempenho'] = int(sys.stdin.readline().strip())
    caracteristicas['Velocidade'] = int(sys.stdin.readline().strip())
    caracteristicas['Custo'] = int(sys.stdin.readline().strip())
    capacidades = sys.stdin.readline().strip().split(',')
    caracteristicas['Capacidades'] = [capacidade.strip() for capacidade in capacidades]
    return caracteristicas

modelos = [
    ModeloIA("Claude 3 Sonnet", 8, 10, 6, ["pesquisa", "desenvolvimento acelerado", "codificação", "recuperação de informações"]),
    ModeloIA("Claude 3 Haiku", 7, 9, 5, ["velocidade", "resumo de dados não estruturados"]),
    ModeloIA("Claude 3 Opus", 9, 10, 5, ["pesquisa", "desenvolvimento acelerado"]),
]

caracteristicas_entrada = obter_caracteristicas()
melhor_modelo = recomendar_modelo(caracteristicas_entrada, modelos)
explicacao = gerar_explicacao(melhor_modelo, caracteristicas_entrada)

print(explicacao)



-------------------------------------------------------------------------------------------------------------------------------------------------------
Desafio 3
-------------------------------------------------------------------------------------------------------------------------------------------------------

import sys

modelos_disponiveis = [
    {"nome": "Claude 3 Opus", "pontuacao_desempenho": 9, "preco_mensal": 600},
    {"nome": "Claude 3 Sonnet", "pontuacao_desempenho": 8, "preco_mensal": 450},
    {"nome": "Claude 3 Haiku", "pontuacao_desempenho": 7, "preco_mensal": 350},
]

def recomendar_modelo(modelos, orcamento):
    if orcamento < 250:
        return None, "Seu orçamento é muito baixo para recomendar um modelo adequado."

    modelos_dentro_orcamento = [modelo for modelo in modelos if modelo['preco_mensal'] <= orcamento]

    if not modelos_dentro_orcamento:
        modelo_mais_proximo = min(modelos, key=lambda x: abs(x['preco_mensal'] - orcamento))
        return modelo_mais_proximo['nome'], "Este modelo está mais próximo do seu orçamento."

    melhor_modelo = max(modelos_dentro_orcamento, key=lambda x: x['pontuacao_desempenho'])
    return melhor_modelo['nome'], "Melhor desempenho dentro do seu orçamento."

orcamento_usuario = float(sys.stdin.read().strip())

modelo_recomendado, motivo = recomendar_modelo(modelos_disponiveis, orcamento_usuario)

if modelo_recomendado:
    sys.stdout.write(modelo_recomendado + ". " + motivo + "\n")
else:
    sys.stdout.write(motivo + "\n")



