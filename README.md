# Define posições
def define_posicoes(linha, coluna, orientacao, tamanho):
    posicao = []
    posicao.append([linha, coluna])
    if orientacao == 'horizontal':
        while (tamanho -1) > 0:
            coluna += 1
            posicao.append([linha, coluna])
            tamanho -= 1
    elif orientacao == 'vertical':
        while (tamanho -1) > 0:
            linha += 1
            posicao.append([linha, coluna])
            tamanho -= 1
    return posicao
    
 # Preenche Frota
 def define_posicoes(linha, coluna, orientacao, tamanho):
    posicao = []
    posicao.append([linha, coluna])
    if orientacao == 'horizontal':
        while (tamanho -1) > 0:
            coluna += 1
            posicao.append([linha, coluna])
            tamanho -= 1
    elif orientacao == 'vertical':
        while (tamanho -1) > 0:
            linha += 1
            posicao.append([linha, coluna])
            tamanho -= 1
    return posicao

def preenche_frota(frota, nome_navio, linha, coluna, orientacao, tamanho):
    if nome_navio in frota:
        frota[nome_navio].append((define_posicoes(linha, coluna, orientacao, tamanho)))
    if nome_navio not in frota:
        nome = nome_navio
        posicao = (define_posicoes(linha, coluna, orientacao, tamanho))
        frota[nome] = [posicao]
    return frota
    
# Faz jogada
def faz_jogada(tabuleiro, linha, coluna):
    if tabuleiro[linha][coluna] == 1:
        tabuleiro [linha][coluna] = 'X'
    if tabuleiro[linha][coluna] == 0:
        tabuleiro[linha][coluna] = '-'
    return tabuleiro
    
# Posiciona Frota 
def posiciona_frota(frota):
    tabuleiro = [0]*10
    for i in range(len(tabuleiro)):
        tabuleiro[i] = [0]*10
    for coordenadas in frota.values():
        for j in coordenadas:
            for i in j:
                linha = i[0]
                coluna = i[1]
                tabuleiro[linha][coluna]=1
    return tabuleiro
    
 # Afundados
 def afundados(frota, tabuleiro):
    total = 0
    for navios in frota.values():
        for navio in navios:
            numero = 0
            for coordenadas in navio:
                linha = coordenadas[0]
                coluna = coordenadas[1]
                if tabuleiro[linha][coluna] == 'X':
                    numero += 1
                    if numero == (len(navio)):
                        total += 1
    return total
    
 # Posicao válida
 def define_posicoes(linha, coluna, orientacao, tamanho):
        posicao = []
        posicao.append([linha, coluna])
        if orientacao == 'horizontal':
            while (tamanho -1) > 0:
                coluna += 1
                posicao.append([linha, coluna])
                tamanho -= 1
        elif orientacao == 'vertical':
            while (tamanho -1) > 0:
                linha += 1
                posicao.append([linha, coluna])
                tamanho -= 1
        return posicao

def posicao_valida(frota, linha, coluna, orientacao, tamanho):
    posicoes = define_posicoes(linha, coluna, orientacao, tamanho)
    for navios in frota.values():
        for navio in navios:
                for posicao in posicoes:
                    if posicao in navio:
                        return False
    for i in range(len(posicoes)):
        if posicoes[i][0] > 9 or posicoes[i][0] < 0 or posicoes[i][1] > 9 or posicoes[i][1] < 0:
            return False
    return True

# Posicionando Frota
def define_posicoes(linha, coluna, orientacao, tamanho):
    posicoes = []
    if orientacao == "vertical":
        for i in range(tamanho):
            posicoes.append([linha+i, coluna])
    else:
        for i in range(tamanho):
            posicoes.append([linha, coluna+i])
    return posicoes

def preenche_frota(frota, nome_navio, linha, coluna, orientacao, tamanho):
    if nome_navio in frota:
        frota[nome_navio].append((define_posicoes(linha, coluna, orientacao, tamanho)))
    if nome_navio not in frota:
        nome = nome_navio
        posicao = (define_posicoes(linha, coluna, orientacao, tamanho))
        frota[nome] = [posicao]
    return frota

def faz_jogada(tabuleiro, linha, coluna):
    if tabuleiro[linha][coluna] == 1:
        tabuleiro [linha][coluna] = 'X'
    if tabuleiro[linha][coluna] == 0:
        tabuleiro[linha][coluna] = '-'
    return tabuleiro


def afundados(frota, tabuleiro):
    navios_afundados = 0
    
    for navio,  posicoes in frota.items():
        for posicoes in posicoes:
            afundado = True
            for posicao in posicoes:
                linha, coluna = posicao
                if tabuleiro[linha][coluna] != 'X':
                    afundado = False
                    break
            if afundado:
                navios_afundados += 1
                
    return navios_afundados

def posicao_valida(dicio_navios, linha, coluna, orientacao, tamanho):
    navio=define_posicoes(linha, coluna,orientacao,tamanho)
    for n in navio:
        if n[0]<0 or n[1]<0 or n[0]>9 or n[1]>9:
            return False
        for i in dicio_navios.values():
            for j in range(len(i)):
                if n in i[j]:
                    return False
    if dicio_navios=={}:
        return True
    return True

frota = {
    "porta-aviões":[],
    "navio-tanque":[],
    "contratorpedeiro":[],
    "submarino": [],
}

dicionario_embarcacoes = {'porta-aviões': [1, 4], 'navio-tanque': [2, 3], 'contratorpedeiro': [3, 2], 'submarino': [4, 1]}

for embarcacao, qtde in dicionario_embarcacoes.items():
    
    for i in range(0, qtde[0]):
        print(f'Insira as informações referentes ao navio {embarcacao} que possui tamanho {qtde[1]}')

        linha = int(input('Linha: '))
        coluna = int(input('Coluna: '))

        if embarcacao != 'submarino':
            orientacao = int(input('[1] Vertical [2] Horizontal > '))

            if orientacao == 1:
                orientacao = 'vertical'
            if orientacao == 2:
                orientacao = 'horizontal'

            if posicao_valida(frota, linha, coluna, orientacao, qtde[1]) == False:
                while posicao_valida(frota, linha, coluna, orientacao, qtde[1]) == False:

                    print('Esta posição não está válida!')
                    print(f'Insira as informações referentes ao navio {embarcacao} que possui tamanho {qtde[1]}')

                    linha = int(input('Linha: '))
                    coluna = int(input('Coluna: '))

                    if embarcacao != 'submarino':
                        orientacao = int(input('[1] Vertical [2] Horizontal > '))

                        if orientacao == 1:
                            orientacao = 'vertical'
                        if orientacao == 2:
                            orientacao = 'horizontal'
                
                frota = preenche_frota(frota, embarcacao, linha, coluna, orientacao, qtde[1])
            
            else:
                frota = preenche_frota(frota, embarcacao, linha, coluna, orientacao, qtde[1])

        else:
            orientacao = 'horizontal'

            if posicao_valida(frota, linha, coluna, orientacao, qtde[1]) == False:
                while posicao_valida(frota, linha, coluna, orientacao, qtde[1]) == False:

                    print('Esta posição não está válida!')
                    print(f'Insira as informações referentes ao navio {embarcacao} que possui tamanho {qtde[1]}')

                    linha = int(input('Linha: '))
                    coluna = int(input('Coluna: '))

                    if embarcacao != 'submarino':
                        orientacao = int(input('[1] Vertical [2] Horizontal > '))

                        if orientacao == 1:
                            orientacao = 'vertical'
                        if orientacao == 2:
                            orientacao = 'horizontal'

                frota = preenche_frota(frota, embarcacao, linha, coluna, orientacao, qtde[1])
                
            else:
                frota = preenche_frota(frota, embarcacao, linha, coluna, orientacao, qtde[1])

print(frota)
