import tkinter as tk
import re

def validar_telefone(telefone):
    # Expressão regular para validar telefone no formato (XX) 9XXXX-XXXX
    padrao = re.compile(r'^\(\d{2}\) 9\d{4}-\d{4}$')
    return padrao.match(telefone) is not None

def validar_cpf(cpf):
    # Expressão regular para validar CPF no formato XXX.XXX.XXX-XX
    padrao = re.compile(r'^\d{3}\.\d{3}\.\d{3}-\d{2}$')
    return padrao.match(cpf) is not None

def on_press_tecla(event):
    # Função para aceitar apenas números e limitar o comprimento do campo
    widget = event.widget
    if event.char.isnumeric() and len(widget.get()) < 11:
        return True
    return False

def on_press_tecla_cpf(event):
    # Função para aceitar apenas números e limitar o comprimento do campo
    widget = event.widget
    if event.char.isnumeric() and len(widget.get()) < 14:
        return True
    return False

def enviar_formulario():
    # Obter os valores dos campos
    nome = entry_nome.get()
    telefone = entry_telefone.get()
    cpf = entry_cpf.get()

    # Validar telefone e CPF
  if not validar_telefone(telefone):
        print("Telefone inválido!")
        return

  if not validar_cpf(cpf):
        print("CPF inválido!")
        return

    # Exibir os valores no console (você pode salvar em um banco de dados ou fazer o que for necessário)
  print("Nome:", nome)
    print("Telefone:", telefone)
    print("CPF:", cpf)

# Criar janela principal
janela = tk.Tk()
janela.title("Formulário")

# Adicionar rótulos e campos de entrada
tk.Label(janela, text="Nome:").pack()
entry_nome = tk.Entry(janela)
entry_nome.pack()

tk.Label(janela, text="Telefone:").pack()
entry_telefone = tk.Entry(janela)
entry_telefone.pack()
entry_telefone.bind('<KeyPress>', on_press_tecla)

tk.Label(janela, text="CPF:").pack()
entry_cpf = tk.Entry(janela)
entry_cpf.pack()
entry_cpf.bind('<KeyPress>', on_press_tecla_cpf)

# Adicionar botão de envio
botao_enviar = tk.Button(janela, text="Enviar", command=enviar_formulario)
botao_enviar.pack()

# Iniciar loop da interface gráfica
janela.mainloop()
