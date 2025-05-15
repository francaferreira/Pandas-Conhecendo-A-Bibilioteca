```markdown
# 🏘️ Análise de Dados de Imóveis do Rio de Janeiro com Pandas

![Pandas](https://img.shields.io/badge/Pandas-2.2.2-blueviolet) 
![Dados](https://img.shields.io/badge/Dados_Reais-Sim-success)

Um guia passo a passo para iniciantes aprenderem Pandas na prática usando dados reais de aluguéis. **Tudo explicado linha por linha!**

---

## 🛠️ **Configuração Inicial**

```python
# Instalação dos pacotes necessários (execute apenas uma vez)
!pip install pandas matplotlib

# Importando as ferramentas
import pandas as pd  # Para trabalhar com tabelas
import matplotlib.pyplot as plt  # Para criar gráficos
```

**Por que isso importa?**  
- `pandas` vai nos ajudar a organizar e analisar os dados  
- `matplotlib` será usado para visualizar informações

---

## 📥 **Importando os Dados**

```python
# Carregando os dados direto da internet
url = 'https://raw.githubusercontent.com/alura-cursos/pandas-conhecendo-a-biblioteca/main/base-de-dados/aluguel.csv'
dados = pd.read_csv(url)  # Transforma o link em uma tabela organizada

# Primeira visualização dos dados
dados.head(3)  # Mostra as 3 primeiras linhas
```

**Resultado Esperado:**  
Uma tabela com colunas como *Tipo*, *Bairro*, *Quartos*, *Aluguel*...

---

## 🔍 **Primeira Análise**

### 1. Estrutura da Base
```python
print("Total de Imóveis:", dados.shape[0])  # Número de linhas
print("Colunas Disponíveis:", dados.columns.tolist())  # Lista de características
```

### 2. Tipos de Dados
```python
print("\nTipos de Informações:\n", dados.dtypes)  # Verifica se valores são números/textos
```

### 3. Dados Faltantes
```python
print("\nValores Ausentes por Coluna:\n", dados.isna().sum())  # Conta campos vazios
```

---

## 🧼 **Limpando os Dados**

### 1. Removendo Colunas Desnecessárias
```python
# Supondo que 'ColunaXYZ' não seja útil
dados = dados.drop(columns=['ColunaXYZ'])  # Apaga coluna permanentemente
```

### 2. Lidando com Valores Vazios
```python
# Preenchendo quartos ausentes com a moda (valor mais comum)
dados['Quartos'] = dados['Quartos'].fillna(dados['Quartos'].mode()[0])
```

### 3. Filtrando Dados
```python
# Removendo imóveis comerciais (ex: 'Conjunto Comercial/Sala')
filtro_residencial = dados['Tipo'] != 'Conjunto Comercial/Sala'
dados_residencial = dados[filtro_residencial]
```

---

## 📈 **Análises Interessantes**

### 1. Valor Médio de Aluguel por Tipo
```python
# Calculando média para cada categoria
media_por_tipo = dados_residencial.groupby('Tipo')['Aluguel'].mean()
print("\n💵 Média de Aluguel por Tipo:\n", media_por_tipo)
```

### 2. Percentual de Cada Tipo de Imóvel
```python
# Calculando proporções
percentual_tipos = dados_residencial['Tipo'].value_counts(normalize=True) * 100
print("\n📊 Distribuição Percentual:\n", percentual_tipos)
```

### 3. Gráfico de Pizza Simplificado
```python
percentual_tipos.head(5).plot.pie(autopct='%1.1f%%')  # Top 5 tipos
plt.title('Tipos de Imóveis Mais Comuns')
plt.show()
```

---

## 🎯 **Filtros Avançados**

### 1. Apartamentos Econômicos
```python
filtro_1 = (dados_residencial['Tipo'] == 'Apartamento') 
filtro_2 = (dados_residencial['Quartos'] == 1)
filtro_3 = (dados_residencial['Aluguel'] < 1200)
apt_economicos = dados_residencial[filtro_1 & filtro_2 & filtro_3]
```

### 2. Apartamentos Familiares
```python
filtro_a = (dados_residencial['Quartos'] >= 2)
filtro_b = (dados_residencial['Aluguel'] < 3000)
filtro_c = (dados_residencial['Área'] > 70)
apt_familiares = dados_residencial[filtro_1 & filtro_a & filtro_b & filtro_c]
```

---

## ✨ **Criando Novas Colunas**

### 1. Coluna Numérica: Custo Total
```python
dados['Custo Total'] = dados['Aluguel'] + dados['Condomínio'] + dados['IPTU']
```

### 2. Coluna Categórica: Classe do Imóvel
```python
dados['Classe'] = pd.cut(dados['Custo Total'],
                         bins=[0, 2000, 5000, 10000, 20000],
                         labels=['Econômico', 'Médio', 'Alto', 'Luxo'])
```

---

## 💾 **Salvando Resultados**

```python
# Salvando apartamentos filtrados em novo arquivo
apt_familiares.to_csv('apartamentos_familiares.csv', index=False)
print("✅ Arquivo salvo com sucesso!")
```

---

## 📌 **Conclusão**

Neste projeto você aprendeu:
- Importar e explorar dados reais
- Limpar e filtrar informações
- Calcular métricas importantes
- Criar novas colunas personalizadas
- Salvar resultados para uso futuro

Próximos passos: 
- Explore outros filtros
- Crie gráficos mais complexos
- Adicione mais colunas calculadas

---

## 🔗 **Recursos Úteis**

- [Documentação do Pandas](https://pandas.pydata.org/docs/)
- [Galeria de Gráficos](https://matplotlib.org/stable/gallery/index.html)
- [Dataset Original](https://github.com/alura-cursos/pandas-conhecendo-a-biblioteca)

Desenvolvido com ❤️ por [Jefferson Ferreira]  
*Dúvidas? Contato: jfrancaferreira10@gmail.com*
```

Este README oferece:
- Explicações **simples** para cada comando
- Fluxo **lógico** de aprendizado
- Exemplos **práticos** do mundo real
- Visual **atraente** com emojis e formatação
- **Tudo que um iniciante precisa** para começar!

Cada seção contém:
1. Contexto do que está sendo feito
2. Código pronto para uso
3. Explicação em linguagem cotidiana
4. Dicas visuais para melhor compreensão
