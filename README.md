ARQUIVO = "clientes.txt"

def salvar(c):
    f = open(ARQUIVO, "a", encoding="utf-8")
    linha = c["nome"]+";"+c["tel"]+";"+c["bairro"]+";"+c["prod"]+";"+str(c["valor"])
    f.write(linha+"\n")
    f.close()

def carregar():
    try:
        f = open(ARQUIVO, "r", encoding="utf-8")
        lista = []
        for linha in f:
            if linha.strip() == "":
                continue
            p = linha.strip().split(";")
            if len(p) == 5:
                lista.append({"nome":p[0],"tel":p[1],"bairro":p[2],"prod":p[3],"valor":float(p[4])})
        f.close()
        return lista
    except:
        return []

print("LOJA SNIPER - FINAL")
op = ""
while op!= "5":
    print("")
    print("1 Cadastrar")
    print("2 Listar")
    print("3 Buscar")
    print("4 Total")
    print("5 Sair")
    op = input("Escolha: ")
    if op == "1":
        n = input("Nome: ")
        t = input("Tel: ")
        b = input("Bairro: ")
        pr = input("Produto: ")
        v = input("Valor: ")
        v = float(v)
        salvar({"nome":n,"tel":t,"bairro":b,"prod":pr,"valor":v})
        print("Salvo com sucesso!")
    if op == "2":
        clientes = carregar()
        if len(clientes) == 0:
            print("Nenhum cliente")
        else:
            for x in clientes:
                print(x["nome"]+" | "+x["prod"]+" | "+str(x["valor"])+" MT")
    if op == "3":
        busca = input("Buscar nome: ")
        for x in carregar():
            if busca.lower() in x["nome"].lower():
                print("Achou: "+x["nome"]+" - "+x["tel"])
    if op == "4":
        total = 0
        todos = carregar()
        for x in todos:
            total = total + x["valor"]
        print("Clientes: "+str(len(todos)))
        print("Faturamento: "+str(total)+" MT")
    if op == "5":
        print("Ate logo sniper!")
