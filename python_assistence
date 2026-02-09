# Carrega recursos para manipulação de funcionalidades do sistema operacional
import os

# Importa o Streamlit, framework usado para criação de aplicações web interativas em Python
import streamlit as st

# Importa o cliente Groq responsável pela comunicação com a API do modelo de linguagem
from groq import Groq

# Define as configurações iniciais da aplicação Streamlit
# Inclui título da página, tipo de layout e estado da barra lateral

st.set_page_config(
    page_title="Chat para python",
    layout="wide",
    initial_sidebar_state="expanded"
)

# Prompt base que orienta o comportamento do modelo de IA durante a conversa
CUSTOM_PROMPT = """
Você é um assistente de IA especialista em programação, com foco principal em Python. 
Sua missão é ajudar desenvolvedores iniciantes com dúvidas de programação de forma clara, precisa e útil.
"""
# Construção da barra lateral da aplicação
with st.sidebar:
    
    # Exibe o título principal da sidebar
    st.title("🐍 Chat para python")
    
    # Texto informativo descrevendo a finalidade do assistente
    st.markdown("Um assistente de IA focado em programação Python para ajudar iniciantes.")
    
    # Campo de entrada para o usuário informar a chave da API Groq
    groq_api_key = st.text_input(
        "Insira sua API Key Groq", 
        type="password",
        help="Obtenha sua chave em https://console.groq.com/keys"
    )

    # Separadores visuais e mensagens informativas adicionais
    st.markdown("---")
    st.markdown(
        "Aplicação desenvolvida para auxiliar dúvidas em programação Python. "
        "Respostas geradas por IA podem conter erros. Sempre valide as informações."
    )

    st.markdown("---")
    st.markdown("Acesse a documentação oficial da linguagem Python:")

    # Link direto para a documentação oficial do Python
    st.markdown("🔗 https://docs.python.org/pt-br/3/")
    
# Define o título principal exibido no corpo da aplicação
st.title("Dúvidas de Python 🐍")

# Texto complementar exibido abaixo do título principal
st.caption("Chat utilizando LLM para apoiar desenvolvedores com dúvidas em Python")

# Cria o histórico de mensagens na sessão do usuário, caso ainda não exista
if "messages" not in st.session_state:
    st.session_state.messages = []

# Renderiza todas as mensagens já armazenadas na sessão
for message in st.session_state.messages:
    with st.chat_message(message["role"]):
        st.markdown(message["content"])

# Inicializa a variável que armazenará o cliente da API Groq
client = None

# Valida se o usuário informou a chave da API
if groq_api_key:
    
    try:
        # Instancia o cliente Groq utilizando a chave fornecida
        client = Groq(api_key=groq_api_key)
    
    except Exception as e:
        # Exibe erro caso a criação do cliente falhe
        st.sidebar.error(f"Erro ao inicializar o cliente Groq: {e}")
        st.stop()

# Caso existam mensagens, mas nenhuma chave tenha sido informada
elif st.session_state.messages:
    st.warning("Por favor, insira sua API Key da Groq.")

# Captura a mensagem digitada pelo usuário no campo de chat
if prompt := st.chat_input("Estou aqui para ajudar em qualquer dúvidas em Python?"):
    
    # Impede a continuação caso o cliente da API não esteja configurado
    if not client:
        st.warning("Insira sua API Key da Groq.")
        st.stop()

    # Salva a mensagem do usuário no histórico da sessão
    st.session_state.messages.append(
        {"role": "user", "content": prompt}
    )
    
    # Exibe a mensagem do usuário na interface do chat
    with st.chat_message("user"):
        st.markdown(prompt)

    # Monta a lista de mensagens enviadas para o modelo, incluindo o prompt de sistema
    messages_for_api = [{"role": "system", "content": CUSTOM_PROMPT}]
    for msg in st.session_state.messages:
        messages_for_api.append(msg)

    # Cria o bloco de resposta do assistente
    with st.chat_message("assistant"):
        
        # Exibe indicador visual enquanto a IA processa a resposta
        with st.spinner("Analisando sua pergunta..."):
            
            try:
                # Realiza a chamada à API da Groq para gerar a resposta
                chat_completion = client.chat.completions.create(
                    messages=messages_for_api,
                    model="openai/gpt-oss-20b",
                    temperature=0.7,
                    max_tokens=2048,
                )
                
                # Obtém o texto da resposta retornada pelo modelo
                ai_resposta = chat_completion.choices[0].message.content
                
                # Exibe a resposta gerada no chat
                st.markdown(ai_resposta)
                
                # Armazena a resposta do assistente no histórico da sessão
                st.session_state.messages.append(
                    {"role": "assistant", "content": ai_resposta}
                )

            # Trata falhas de comunicação ou erros da API
            except Exception as e:
                st.error(
                    f"Ocorreu um erro ao se comunicar com a API da Groq: {e}"
                )

st.markdown(
    """
    <style>
    .stApp {
        background-color: #0E1117;
    }
    </style>
    """,
    unsafe_allow_html=True
)

