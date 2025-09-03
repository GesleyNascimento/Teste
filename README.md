import tkinter as tk
from tkinter import messagebox

# Lista para armazenar usuários cadastrados
usuarios_cadastrados = []

# Função de cadastro
def cadastrar_usuario():
    nome = entrada_nome.get()
    id_usuario = entrada_id.get()
    senha = entrada_senha.get()

    if not nome or not id_usuario or not senha:
        messagebox.showwarning("Campos obrigatórios", "Preencha todos os campos.")
        return

    for usuario in usuarios_cadastrados:
        if usuario["id"] == id_usuario:
            messagebox.showerror("Erro", "ID de usuário já cadastrado.")
            return

    novo_usuario = {"nome": nome, "id": id_usuario, "senha": senha}
    usuarios_cadastrados.append(novo_usuario)
    messagebox.showinfo("Sucesso", f"Usuário '{nome}' cadastrado com sucesso!")

    entrada_nome.delete(0, tk.END)
    entrada_id.delete(0, tk.END)
    entrada_senha.delete(0, tk.END)

# Função que abre a janela de cadastro
def abrir_janela_cadastro():
    cadastro = tk.Toplevel()
    cadastro.title("Cadastro de Usuários")
    cadastro.geometry("300x250")

    tk.Label(cadastro, text="Nome:").pack(pady=5)
    global entrada_nome
    entrada_nome = tk.Entry(cadastro)
    entrada_nome.pack()

    tk.Label(cadastro, text="ID do Usuário:").pack(pady=5)
    global entrada_id
    entrada_id = tk.Entry(cadastro)
    entrada_id.pack()

    tk.Label(cadastro, text="Senha:").pack(pady=5)
    global entrada_senha
    entrada_senha = tk.Entry(cadastro, show="*")
    entrada_senha.pack()

    btn_cadastrar = tk.Button(cadastro, text="Cadastrar", command=cadastrar_usuario)
    btn_cadastrar.pack(pady=15)

# Janela principal
janela = tk.Tk()
janela.title("Biblioteca Read to Fly")
janela.geometry("500x300")
janela.configure(bg="#f0f8ff")

# Título
titulo = tk.Label(janela, text="📖 Bem-vindo à Biblioteca Read to Fly 🕊️", font=("Helvetica", 16, "bold"), bg="#f0f8ff", fg="#333")
titulo.pack(pady=30)

# Botão para abrir cadastro
btn_abrir_cadastro = tk.Button(janela, text="Cadastrar Usuário", command=abrir_janela_cadastro)
btn_abrir_cadastro.pack(pady=10)

# Rodapé
rodape = tk.Label(janela, text="Sistema de Gestão de Biblioteca", font=("Arial", 10), bg="#f0f8ff", fg="#666")
rodape.pack(side=tk.BOTTOM, pady=10)

janela.mainloop()

class Livro:
    def __init__(self, titulo, autor, isbn):
        self.titulo = titulo
        self.autor = autor
        self.isbn = isbn
        self.disponivel = True

    def emprestar(self):
        if self.disponivel:
            self.disponivel = False
            return True
        return False

    def devolver(self):
        self.disponivel = True


class Usuario:
    def __init__(self, nome, id_usuario):
        self.nome = nome
        self.id_usuario = id_usuario
        self.livros_emprestados = []

    def pegarLivro(self, livro):
        if livro.emprestar():
            self.livros_emprestados.append(livro)
            print(f"{self.nome} pegou o livro '{livro.titulo}'.")
        else:
            print(f"O livro '{livro.titulo}' não está disponível.")

    def devolverLivro (self, livro):
        if livro in self.livros_emprestados:
            livro.devolver()
            self.livros_emprestados.remove(livro)
            print(f"{self.nome} devolveu o livro '{livro.titulo}'.")
        else:
            print(f"{self.nome} não possui o livro '{livro.titulo}'.")


# Teste 1
livro1 = Livro("1984", "George Orwell", "1234567890")
usuario1 = Usuario("Ana", 1)

usuario1.pegarLivro(livro1)     # Deve emprestar o livro
usuario1.pegarLivro(livro1)     # Deve avisar que o livro não está disponível
usuario1.devolverLivro(livro1)  # Deve devolver o livro
usuario1.devolverLivro(livro1)  # Deve avisar que o livro  está com o usuário

# Teste 2
livro2 = Livro("Agile Scrum Master no gerenciamento avençado de projetos", "Vitor L. Massari", "978874529395")
usuario2 = Usuario("Pedro", 2)

usuario2.pegarLivro(livro2)     # Não Deve emprestar o livro
usuario2.pegarLivro(livro2)     # Deve avisar que o livro não está disponível
usuario2.devolverLivro(livro2)  # Deve devolver o livro
usuario2.devolverLivro(livro2)  # Deve avisar que o livro está com o usuário

livro1 = Livro("1984", "George Orwell", "1234567890")
usuario1 = Usuario("Ana", 1)

def emprestar_livro():
    if livro1.disponivel:
        usuario1.pegarLivro(livro1)
        messagebox.showinfo("Sucesso", f"Livro '{livro1.titulo}' emprestado!")
    else:
        messagebox.showwarning("Indisponível", "Livro já emprestado.")

def devolver_livro():
    usuario1.devolverLivro(livro1)
    messagebox.showinfo("Sucesso", f"Livro '{livro1.titulo}' devolvido!")

janela = tk.Tk()
janela.title("Sistema de Biblioteca")

btn_emprestar = tk.Button(janela, text="Emprestar Livro", command=emprestar_livro)
btn_emprestar.pack(pady=10)

btn_devolver = tk.Button(janela, text="Devolver Livro", command=devolver_livro)
btn_devolver.pack(pady=10)

janela.mainloop()

class Livro:
    def __init__(self, titulo, autor, isbn):
        self.titulo = titulo
        self.autor = autor
        self.isbn = isbn
        self.disponivel = True

    def emprestar(self):
        if self.disponivel:
            self.disponivel = False
            return True
        return False

    def devolver(self):
        self.disponivel = True


class Usuario:
    def __init__(self, nome, id_usuario):
        self.nome = nome
        self.id_usuario = id_usuario
        self.livros_emprestados = []

    def pegar_livro(self, livro):
        if livro.emprestar():
            self.livros_emprestados.append(livro)
            print(f"{self.nome} emprestou o livro '{livro.titulo}'.")
        else:
            print(f"O livro '{livro.titulo}' não está disponível.")

    def devolver_livro(self, livro):
        if livro in self.livros_emprestados:
            livro.devolver()
            self.livros_emprestados.remove(livro)
            print(f"{self.nome} devolveu o livro '{livro.titulo}'.")
        else:
            print(f"{self.nome} não possui o livro '{livro.titulo}'.")


class Livro:
    def __init__(self, titulo, autor, isbn):
        self.titulo = titulo
        self.autor = autor
        self.isbn = isbn
        self.disponivel = True

    def emprestar(self):
        if self.disponivel:
            self.disponivel = False
            return True
        return False

    def devolver(self):
        self.disponivel = True


class Usuario:
    def __init__(self, nome, id_usuario):
        self.nome = nome
        self.id_usuario = id_usuario
        self.livros_emprestados = []

    def pegar_livro(self, livro):
        if livro.emprestar():
            self.livros_emprestados.append(livro)
            print(f"{self.nome} emprestou o livro '{livro.titulo}'.")
        else:
            print(f"O livro '{livro.titulo}' não está disponível.")

    def devolver_livro(self, livro):
        if livro in self.livros_emprestados:
            livro.devolver()
            self.livros_emprestados.remove(livro)
            print(f"{self.nome} devolveu o livro '{livro.titulo}'.")
        else:
            print(f"{self.nome} não possui o livro '{livro.titulo}'.")


import tkinter as tk
from tkinter import messagebox

# Classes
class Livro:
    def __init__(self, titulo, autor, isbn):
        self.titulo = titulo
        self.autor = autor
        self.isbn = isbn
        self.disponivel = True

    def emprestar(self):
        if self.disponivel:
            self.disponivel = False
            return True
        return False

    def devolver(self):
        self.disponivel = True

class Usuario:
    def __init__(self, nome, id_usuario):
        self.nome = nome
        self.id_usuario = id_usuario
        self.livros_emprestados = []

    def pegar_livro(self, livro):
        if livro.emprestar():
            self.livros_emprestados.append(livro)
            return True
        return False

    def devolver_livro(self, livro):
        if livro in self.livros_emprestados:
            livro.devolver()
            self.livros_emprestados.remove(livro)
            return True
        return False

# Dados iniciais
livros = [
    Livro("1984", "George Orwell", "001"),
    Livro("Dom Casmurro", "Machado de Assis", "002"),
    Livro("O Pequeno Príncipe", "Saint-Exupéry", "003")
]

usuario = Usuario("Ana", 1)

# Funções da interface
def atualizar_lista():
    lista_livros.delete(0, tk.END)
    for livro in livros:
        status = "Disponível" if livro.disponivel else "Emprestado"
        lista_livros.insert(tk.END, f"{livro.titulo} - {status}")

def emprestar_livro():
    selecao = lista_livros.curselection()
    if selecao:
        livro = livros[selecao[0]]
        if usuario.pegar_livro(livro):
            messagebox.showinfo("Sucesso", f"Livro '{livro.titulo}' emprestado.")
        else:
            messagebox.showwarning("Indisponível", f"Livro '{livro.titulo}' já está emprestado.")
        atualizar_lista()

def devolver_livro():
    selecao = lista_livros.curselection()
    if selecao:
        livro = livros[selecao[0]]
        if usuario.devolver_livro(livro):
            messagebox.showinfo("Sucesso", f"Livro '{livro.titulo}' devolvido.")
        else:
            messagebox.showwarning("Erro", f"{usuario.nome} não possui o livro '{livro.titulo}'.")
        atualizar_lista()

# Interface gráfica
janela = tk.Tk()
janela.title("Sistema de Empréstimo de Livros")
janela.geometry("400x300")

tk.Label(janela, text="Selecione um livro:").pack(pady=5)

lista_livros = tk.Listbox(janela, height=8, width=40)
lista_livros.pack(pady=5)
atualizar_lista()

btn_emprestar = tk.Button(janela, text="Emprestar", command=emprestar_livro)
btn_emprestar.pack(pady=5)

btn_devolver = tk.Button(janela, text="Devolver", command=devolver_livro)
btn_devolver.pack(pady=5)

janela.mainloop()

import tkinter as tk
from tkinter import ttk

# Classe Livro
class Livro:
    def __init__(self, titulo, autor, isbn, disponivel=True):
        self.titulo = titulo
        self.autor = autor
        self.isbn = isbn
        self.disponivel = disponivel

    def status(self):
        return "Disponível" if self.disponivel else "Emprestado"

# Acervo de livros
acervo = [
    Livro("1984", "George Orwell", "001"),
    Livro("Dom Casmurro", "Machado de Assis", "002", False),
    Livro("O Pequeno Príncipe", "Saint-Exupéry", "003"),
    Livro("Capitães da Areia", "Jorge Amado", "004"),
    Livro("A Revolução dos Bichos", "George Orwell", "005", False)
]

# Função de busca
def buscar():
    termo = entrada_busca.get().lower()
    tipo = tipo_busca.get()
    lista_resultados.delete(*lista_resultados.get_children())

    for livro in acervo:
        if tipo == "Título" and termo in livro.titulo.lower():
            lista_resultados.insert("", "end", values=(livro.titulo, livro.autor, livro.status()))
        elif tipo == "Autor" and termo in livro.autor.lower():
            lista_resultados.insert("", "end", values=(livro.titulo, livro.autor, livro.status()))

# Função para mostrar todos
def mostrar_todos():
    lista_resultados.delete(*lista_resultados.get_children())
    for livro in acervo:
        lista_resultados.insert("", "end", values=(livro.titulo, livro.autor, livro.status()))

# Interface gráfica
janela = tk.Tk()
janela.title("Consulta ao Acervo")
janela.geometry("500x400")

# Campo de busca
frame_busca = tk.Frame(janela)
frame_busca.pack(pady=10)

tk.Label(frame_busca, text="Buscar por:").pack(side=tk.LEFT)
tipo_busca = ttk.Combobox(frame_busca, values=["Título", "Autor"], state="readonly")
tipo_busca.set("Título")
tipo_busca.pack(side=tk.LEFT, padx=5)

entrada_busca = tk.Entry(frame_busca, width=30)
entrada_busca.pack(side=tk.LEFT, padx=5)

btn_buscar = tk.Button(frame_busca, text="Buscar", command=buscar)
btn_buscar.pack(side=tk.LEFT)

btn_mostrar = tk.Button(janela, text="Mostrar Todos", command=mostrar_todos)
btn_mostrar.pack(pady=5)

# Tabela de resultados
colunas = ("Título", "Autor", "Status")
lista_resultados = ttk.Treeview(janela, columns=colunas, show="headings")
for col in colunas:
    lista_resultados.heading(col, text=col)
    lista_resultados.column(col, width=150)
lista_resultados.pack(expand=True, fill="both", pady=10)


mostrar_todos()
janela.mainloop()

# Classe Livro
class Livro:
    def __init__(self, titulo, autor, isbn):
        self.titulo = titulo
        self.autor = autor
        self.isbn = isbn
        self.disponivel = True

# Acervo de livros
acervo = [
    Livro("1984", "George Orwell", "001"),
    Livro("Dom Casmurro", "Machado de Assis", "002"),
    Livro("O Pequeno Príncipe", "Saint-Exupéry", "003")
]


# Simulação de acervo
class Livro:
    def __init__(self, titulo, disponivel=True):
        self.titulo = titulo
        self.disponivel = disponivel

acervo = [
    Livro("1984", True),
    Livro("Dom Casmurro", False),
    Livro("O Pequeno Príncipe", True),
    Livro("Capitães da Areia", False),
    Livro("A Revolução dos Bichos", True)
]

# Simulação de acervo
class Livro:
    def __init__(self, titulo, disponivel=True):
        self.titulo = titulo
        self.disponivel = disponivel

acervo = [
    Livro("1984", True),
    Livro("Dom Casmurro", False),
    Livro("O Pequeno Príncipe", True),
    Livro("Capitães da Areia", False),
    Livro("A Revolução dos Bichos", True)
]

# Classe Livro
class Livro:
    def __init__(self, titulo, autor, isbn):
        self.titulo = titulo
        self.autor = autor
        self.isbn = isbn
        self.disponivel = True

    def status(self):
        return "Disponível" if self.disponivel else "Emprestado"

import tkinter as tk
from tkinter import messagebox, ttk

# Classe Livro
class Livro:
    def __init__(self, titulo, autor, isbn):
        self.titulo = titulo
        self.autor = autor
        self.isbn = isbn
        self.disponivel = True

    def status(self):
        return "Disponível" if self.disponivel else "Emprestado"

# Lista de livros cadastrados
acervo = []

# Função para cadastrar livro
def cadastrar_livro():
    titulo = entrada_titulo.get().strip()
    autor = entrada_autor.get().strip()
    isbn = entrada_isbn.get().strip()

    if not titulo or not autor or not isbn:
        messagebox.showwarning("Campos obrigatórios", "Preencha todos os campos.")
        return

    novo_livro = Livro(titulo, autor, isbn)
    acervo.append(novo_livro)
    messagebox.showinfo("Cadastro realizado", f"Livro '{titulo}' cadastrado com sucesso.")
    atualizar_lista()
    limpar_campos()

# Função para limpar os campos
def limpar_campos():
    entrada_titulo.delete(0, tk.END)
    entrada_autor.delete(0, tk.END)
    entrada_isbn.delete(0, tk.END)

# Atualiza a lista de livros na interface
def atualizar_lista():
    lista_livros.delete(*lista_livros.get_children())
    for livro in acervo:
        lista_livros.insert("", "end", values=(livro.titulo, livro.autor, livro.isbn, livro.status()))

# Interface gráfica
janela = tk.Tk()
janela.title("Cadastro de Livros")
janela.geometry("550x400")

# Campos de entrada
frame_form = tk.Frame(janela)
frame_form.pack(pady=10)

tk.Label(frame_form, text="Título:").grid(row=0, column=0, sticky="e")
entrada_titulo = tk.Entry(frame_form, width=40)
entrada_titulo.grid(row=0, column=1, padx=5)

tk.Label(frame_form, text="Autor:").grid(row=1, column=0, sticky="e")
entrada_autor = tk.Entry(frame_form, width=40)
entrada_autor.grid(row=1, column=1, padx=5)

tk.Label(frame_form, text="ISBN:").grid(row=2, column=0, sticky="e")
entrada_isbn = tk.Entry(frame_form, width=40)
entrada_isbn.grid(row=2, column=1, padx=5)

# Botões
frame_botoes = tk.Frame(janela)
frame_botoes.pack(pady=10)

btn_cadastrar = tk.Button(frame_botoes, text="Cadastrar Livro", command=cadastrar_livro)
btn_cadastrar.grid(row=0, column=0, padx=10)

btn_limpar = tk.Button(frame_botoes, text="Limpar Campos", command=limpar_campos)
btn_limpar.grid(row=0, column=1, padx=10)

# Lista de livros cadastrados
colunas = ("Título", "Autor", "ISBN", "Status")
lista_livros = ttk.Treeview(janela, columns=colunas, show="headings")
for col in colunas:
    lista_livros.heading(col, text=col)
    lista_livros.column(col, width=120)
lista_livros.pack(expand=True, fill="both", pady=10)

janela.mainloop()

import tkinter as tk
from tkinter import ttk, messagebox
from datetime import datetime, timedelta

# Classe para representar um livro emprestado
class LivroEmprestado:
    def __init__(self, titulo, autor, data_devolucao):
        self.titulo = titulo
        self.autor = autor
        self.data_devolucao = data_devolucao

    def esta_atrasado(self):
        return datetime.now().date() > self.data_devolucao

# Lista simulada de empréstimos
emprestimos = [
    LivroEmprestado("1984", "George Orwell", datetime.now().date() - timedelta(days=2)),
    LivroEmprestado("Dom Casmurro", "Machado de Assis", datetime.now().date() + timedelta(days=3)),
    LivroEmprestado("O Pequeno Príncipe", "Saint-Exupéry", datetime.now().date() - timedelta(days=1)),
]

import tkinter as tk
from tkinter import ttk, messagebox
from datetime import datetime, timedelta

# Classe para representar um livro emprestado
class LivroEmprestado:
    def __init__(self, titulo, autor, usuario, data_devolucao):
        self.titulo = titulo
        self.autor = autor
        self.usuario = usuario
        self.data_devolucao = data_devolucao

    def esta_atrasado(self):
        return datetime.now().date() > self.data_devolucao

# Lista simulada de empréstimos
emprestimos = [
    LivroEmprestado("1984", "George Orwell", "Ana", datetime.now().date() - timedelta(days=2)),
    LivroEmprestado("Dom Casmurro", "Machado de Assis", "João", datetime.now().date() + timedelta(days=3)),
    LivroEmprestado("O Pequeno Príncipe", "Saint-Exupéry", "Maria", datetime.now().date() - timedelta(days=1)),
]

# Função para verificar atrasos
def verificar_atrasos():
    lista_resultados.delete(*lista_resultados.get_children())
    atrasados = []

    for livro in emprestimos:
        status = "Atrasado" if livro.esta_atrasado() else "No prazo"
        if status == "Atrasado":
            atrasados.append(livro)
        lista_resultados.insert(
            "", "end",
            values=(livro.titulo, livro.autor, livro.usuario, livro.data_devolucao.strftime("%d/%m/%Y"), status)
        )

    if atrasados:
        nomes = ", ".join(set(livro.usuario for livro in atrasados))
        messagebox.showwarning("Atenção", f"Há devoluções atrasadas de: {nomes}")
    else:
        messagebox.showinfo("Tudo certo", "Nenhum livro está atrasado.")

# Interface gráfica
janela = tk.Tk()
janela.title("Verificação de Devoluções Atrasadas")
janela.geometry("600x350")

tk.Label(janela, text="Livros emprestados:").pack(pady=10)

colunas = ("Título", "Autor", "Usuário", "Data de Devolução", "Status")
lista_resultados = ttk.Treeview(janela, columns=colunas, show="headings")
for col in colunas:
    lista_resultados.heading(col, text=col)
    lista_resultados.column(col, width=120)
lista_resultados.pack(expand=True, fill="both", pady=10)

btn_verificar = tk.Button(janela, text="Verificar Atrasos", command=verificar_atrasos)
btn_verificar.pack(pady=10)

janela.mainloop()

# Classe Livro
class Livro:
    def __init__(self, titulo, autor, isbn):
        self.titulo = titulo
        self.autor = autor
        self.isbn = isbn
        self.disponivel = True

    def status(self):
        return "Disponível" if self.disponivel else "Emprestado"

