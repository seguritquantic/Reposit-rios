import os, sys, time, hashlib, secrets, random, string

def superposicao():
    estado = ["Estado Inicial", "Colapsando Estados", "Codificando Quantum Bits", "Finalizando"]
    for ψ in estado:
        sys.stdout.write(f"\r{ψ}  ")
        sys.stdout.flush()
        time.sleep(random.uniform(0.5, 1.5))
    print("\nConcluido\n")

superposicao()

def tunelamento():
    alfabeto = string.ascii_letters + string.digits
    matriz = ''.join(random.choices(alfabeto, k=100))
    
    def colapso(ψ):
        return sum(ord(c) * (i + 1) ** 2 for i, c in enumerate(ψ)) % 10**8
    
    chave_qubit = colapso(matriz)
    chave_qubit_str = str(chave_qubit)
    return matriz, chave_qubit_str[::-1]  

qubit_hash = secrets.token_hex(32)

def deteccao_invasor():
    if sys.gettrace() is not None or "PYTHONINSPECT" in os.environ:
        print("Intrusao Detectada")
        sys.exit(1)

deteccao_invasor()

ψ1, ψ2 = tunelamento()

entrada = input("Insira o Vetor Quantico: ")
if hashlib.sha256(entrada.encode()).hexdigest() != hashlib.sha256(qubit_hash.encode()).hexdigest():
    print("Acesso Negado. Estado Colapsado")
    sys.exit(1)

tentativas = 0
while tentativas < 3:
    entrada_qubit = input(f"Insira a Chave Quantica ({tentativas+1}/3): ")
    
    if hashlib.sha256(entrada_qubit.encode()).hexdigest() == hashlib.sha256(ψ1.encode()).hexdigest():
        print("Estado Estabilizado. Acesso Concedido")
        break
    else:
        print("Estado Incoerente. Tentativa Falha")
        tentativas += 1

    if tentativas == 3:
        print("Decoerencia Total. Bloqueado")
        sys.exit(1)

print(f"Chave Quantum: {ψ2}")  
