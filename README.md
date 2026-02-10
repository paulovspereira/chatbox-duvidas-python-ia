# Assistente de Programação em Python com IA

## Visão Geral
Este projeto consiste em um assistente inteligente para programadores Python, desenvolvido para auxiliar na resolução de dúvidas técnicas, explicação de códigos e apoio ao aprendizado da linguagem.

A aplicação utiliza conceitos de Inteligência Artificial Generativa, integrando um modelo de linguagem (LLM) em nuvem para fornecer respostas contextuais por meio de um chat interativo.

## Objetivo do Projeto
- Criar um chatbot inteligente focado em programação Python
- Utilizar um modelo de linguagem (LLM) em cloud
- Demonstrar integração entre IA, backend Python e interface web
- Servir como projeto de portfólio para a área de Inteligência Artificial

## Tecnologias Utilizadas
- Python 3.x
- NumPy
- Groq (LLM em Cloud)
- Streamlit

## Ferramentas de Desenvolvimento
- Anaconda Python
- Editor de código (Notepad++ ou similar)
- Terminal / Prompt de Comando

## Arquitetura da Solução
1. Interface web desenvolvida com Streamlit
2. Entrada de texto do usuário via chat
3. Envio do prompt para o LLM hospedado na Groq
4. Processamento da resposta pelo modelo
5. Exibição da resposta em tempo real

## Configuração da API Groq
1. Acesse: https://www.groq.com
2. Crie uma conta gratuita
3. Vá em Developers → API Keys
4. Gere sua chave de API
5. No Playground, selecione o modelo: gpt-oss-20b
6. Configure a variável de ambiente com sua API Key

## Instalação e Execução

### Instalar o Anaconda
- https://www.anaconda.com/download
- Verifique a instalação:
python -V

### Criar ambiente virtual
conda create --name chatbox python=3.13
conda activate chatbox

### Instalar dependências
pip install -r requirements.txt

### Executar a aplicação
streamlit run python_assistente.py

## Resultados
- Chat funcional com respostas baseadas em IA
- Integração entre frontend e LLM em nuvem
- Aplicação prática de conceitos de IA Generativa
- Projeto escalável para novas funcionalidades

## Autor
Projeto desenvolvido por Paulo
Em transição de carreira para Analista de Inteligência Artificial
