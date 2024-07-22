# Chat-interativo
Chat interativo virtual
#  Título: techat
# Botão: inicial chat
    # Popup/modal/alerta
        # Título: Bem vindo ao Techat
        # Campo de texto: Escreva seu nome no chat
        # Botão: Entrar no chat
            # Sumir com o título e o botão inicial
            # fechar o popup
            # Criar o chat (com a mensagem de "nome do usuatio entrou no chat")
            # Embaixo do chat:
                # Compo de texto: Digite sua mensagem
                # Botão Enviar
                    # Vai aparecer a mensagem no chat com o nome de usuario
                    # Sthefani: Sf


#flet -> aplicativo/site/programa de computador

# pip install flet


# importa o flet
import flet as ft

# criar a função principal do seu sistema
def main(pagina):
    # Criar alguma coisa
    # criar o titulo
    titulo = ft.Text("TeChat")

    def enviar_mensagem_tunel(mensagem):
        chat.controls.append(ft.Text(mensagem))
        pagina.update()

    pagina.pubsub.subscribe(enviar_mensagem_tunel) #cria o tunel de comunicação

    titulo_janela = ft.Text("Bem vindo ao TeChat")
    campo_nome_usuario = ft.TextField(label="Escreva seu nome no chat")



    def enviar_mensagem(evento):
        texto = f"{campo_nome_usuario.value}: {texto_mensagem.value}"
        # envia a mensagem no chat:
        # Usuario: mensagem
        
        # enviar uma mensagem 
        pagina.pubsub.send_all(texto) # enviar uma mensagem no tunel

        #Limpar o campo de mensagem
        texto_mensagem.value = ""
        pagina.update()

    texto_mensagem = ft.TextField(label="Digite sua mensagem", on_submit=enviar_mensagem)
    botao_enviar = ft.ElevatedButton("enviar", on_click=enviar_mensagem)
    chat = ft.Column()

# columa e linha
    linha_mensagem = ft.Row([texto_mensagem, botao_enviar])

    def entrar_chat(evento):
        # tirar o titulo da página
        pagina.remove(titulo)
        # tirar o botao_iniciar
        pagina.remove(botao_inicial)
        # Fechar o popup/janela
        janela.open = False
        # criar o chat
        pagina.add(chat)
        # adicionar a linha de mensagem
        pagina.add(linha_mensagem)

        # escrever a mensagem: usuario entrou no chat
        texto_entrou_chat = f"{campo_nome_usuario.value} entrou no chat"
        pagina.pubsub.send_all(texto_entrou_chat)

        pagina.update()

    botao_entra = ft.ElevatedButton("entrar no chat", on_click=entrar_chat)


    janela = ft.AlertDialog(
        title=titulo_janela,
        content=campo_nome_usuario,
        actions=[botao_entra]
    )


    def abrir_popup(evento):
        pagina.dialog = janela
        janela.open = True
        pagina.update()



        print("O chat foi acessado")

    botao_inicial = ft.ElevatedButton("Iniciar Chat", on_click=abrir_popup)


    # Colocar essa coisa na página
    # Adicionar o titulo na página
    pagina.add(titulo)
    pagina.add(botao_inicial)



# Executar o seu sistema
ft.app(main, view=ft.WEB_BROWSER)


