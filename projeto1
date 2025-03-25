import sqlite3

conexao = sqlite3.connect("estoque.db")
cursor = conexao.cursor()

cursor.execute("""
  CREATE TABLE IF NOT EXISTS produtos(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT UNIQUE NOT NULL,
    qnt INTEGER NOT NULL,
    preco FLOAT
    )
""")

#Criacao das funcoes de CRUD!!
def inserir_produto(nome,qnt,preco):
    try:
        cursor.execute("INSERT INTO produtos (nome,qnt,preco) VALUES(?,?,?)",
                       (nome,qnt,preco))
        conexao.commit()
        print("Produto foi inserido")
    except sqlite3.IntegrityError:
        print("Erro: Produto já existe!!")


def listar_produtos():
    cursor.execute("SELECT * FROM produtos")
    produtos = cursor.fetchall()
    for p in produtos:
        print(p)


def atualizar_produto(id_produto,novo_nome,nova_qnt, novo_preco):
    cursor.execute("UPDATE produtos SET nome =?, qnt=?,preco=? WHERE id=?",
      (novo_nome,nova_qnt, novo_preco, id_produto))

    if cursor.rowcount > 0:
        print("Item atualizado com sucesso!")
    else:
        print("Item não encontrado!")


def excluir_produto(id_produto):
    cursor.execute("DELETE FROM produtos WHERE id = ?",(id_produto,))

    if cursor.rowcount > 0:
        print("Produto foi excluido !!")
    else:
        print("Produto não foi encontrado!")


#Criacao do menu interativo
#nome,qnt,preco
print("Bem vindo ao banco de dados do estoque de produtos!")

while True:
    print("\n--- Menu de Estoque ---")
    print("1. Listar produtos")
    print("2. Inserir produto")
    print("3. Atualizar produto")
    print("4. Excluir produto")
    print("0. Sair")
    opcao = input("Qual sua opcao?")

    if opcao == '1':
        listar_produtos()

    elif opcao == '2':
        nome = input("Qual o nome do novo produto?")
        while True:
            try:
                qnt = int(input("Qual a quantidade desse produto? "))
                break
            except ValueError:
                print("Quantidade deve ser um número inteiro.")
        while True:
            try:
                preco = float(input("Qual o preco dele?"))
                break
            except ValueError:
                print("Preço deve ser um número qualquer.")

        inserir_produto(nome=nome, qnt=qnt, preco=preco)

    elif opcao == '3':
        id = input("Primeiramente,qual o id do produto que voce quer atualizar?")
        novo_nome = input("Qual é o novo nome dele?")
        while True:
            try:
                nova_qnt = int(input("Qual a nova quantidade?"))
                break
            except ValueError:
                print("Quantidade deve ser um número inteiro.")
        while True:
            try:
                novo_preco = float(input("Qual é o novo preco dele?"))
                break
            except ValueError:
                print("Preço deve ser um número qualquer.")

        atualizar_produto(id_produto=id, novo_nome=novo_nome, nova_qnt=nova_qnt, novo_preco=novo_preco)

    elif opcao == '4':
        id_excluido = input("Id do produto que deseja excluir:")

        excluir_produto(id_produto=id_excluido)

    elif opcao == '0':
        break
    else:
        print("Opcao invalida!!")

conexao.close()
