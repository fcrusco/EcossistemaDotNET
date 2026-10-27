# 🚀 Introdução ao Ecossistema .NET: Do Código ao Executável

Guia prático e conceitual sobre a arquitetura de execução do .NET, CLI (`dotnet`), SDK vs. Runtime e configuração do ambiente de desenvolvimento.

---

## ⚙️ 1. Como o Código C# Vira um Executável?

O processo de compilação e execução no .NET não gera diretamente código de máquina na primeira etapa. Ele passa por uma camada intermediária gerenciada.

```text
┌─────────────────┐
│   Código C#     │  (arquivo .cs)
└────────┬────────┘
         │
         ▼  [Compilador Roslyn]
┌─────────────────┐
│       IL        │  Intermediate Language (.dll)
└────────┬────────┘
         │
         ▼  [Carregado pelo Runtime / CLR]
┌─────────────────┐
│ Compilador JIT  │  Just-In-Time Compiler
└────────┬────────┘
         │
         ▼  [Traduz em tempo de execução]
┌─────────────────┐
│Código de Máquina│  Instruções nativas da CPU
└────────┬────────┘
         │
         ▼
     [Execução]
```

### O Fluxo Passo a Passo

1. **C# Compila → Vira IL:** O compilador transforma o código-fonte C# em uma linguagem intermediária universal (**IL** ou **CIL**), empacotada em uma `.dll`.
2. **Runtime Carrega:** O **CLR** (*Common Language Runtime*) lê e gerencia o assembly compilado.
3. **JIT Converte → Código de Máquina:** O compilador interno **JIT** (*Just-In-Time*) traduz as instruções IL para linguagem nativa do processador (x64, ARM, etc.).
4. **Execução:** O processador roda o código nativo.

> **💬 Pergunta para a turma:**  
> *“Se eu apagar o Runtime da máquina, o programa roda?”*  
> 👉 **Resposta esperada:** **Não.** O programa compilado contém apenas IL. Sem o Runtime e o compilador JIT, o sistema operacional não sabe o que fazer com as instruções.

---

## 🛠️ 2. Criar e Executar Projeto via Terminal

A interface de linha de comando (**CLI**) permite gerenciar todo o ciclo de vida da aplicação sem depender de interface visual.

### Passo a passo rápido:

```bash
# 1. Cria um projeto do tipo Console
dotnet new console -n MeuAppConsole

# 2. Entra na pasta criada
cd MeuAppConsole

# 3. Compila e executa
dotnet run
```

---

## 🧠 3. Explicando Cada Parte do Comando

### `dotnet new console -n MeuAppConsole`

* `dotnet`: Ferramenta principal de linha de comando do .NET (**CLI**). Usada para criar, compilar, restaurar e rodar projetos.
* `new`: Subcomando para inicializar um novo projeto a partir de templates do SDK.
* `console`: Tipo de template selecionado. Cria uma aplicação de terminal básica.
* `-n MeuAppConsole`: Define o nome do projeto (cria a pasta com esse nome e define o nome da solução/projeto internamente).

### Parâmetros úteis adicionais:

* **Definir caminho de saída (`-o`):**  
  Permite salvar em um diretório específico sem precisar criar pastas manualmente.
  ```bash
  dotnet new console -n MeuAppConsole -o Dev/CSharp/MeuAppConsole
  ```

* **Definir a versão do .NET (`-f`):**  
  Força a versão do Framework desejada.
  ```bash
  dotnet new console -f net8.0
  ```

### Outros templates comuns:

| Template | Descrição |
| :--- | :--- |
| `webapi` | API HTTP / REST |
| `mvc` | Aplicação Web ASP.NET Core MVC |
| `classlib` | Biblioteca de classes (gera apenas `.dll` reutilizável) |
| `winforms` | Aplicação Desktop Windows Forms |

> **Dica:** Para listar todos os templates disponíveis no seu computador, digite:
> ```bash
> dotnet new list
> ```

---

## 🔍 4. Inspecionando o Ambiente: SDK vs. Runtime

Para verificar quais versões estão instaladas na máquina:

```bash
dotnet --info
```

Esse comando lista:
* **SDKs instalados** (Ferramentas de desenvolvimento e compilação)
* **Runtimes instalados** (Motores de execução)
* **Informações do sistema operacional e arquitetura**

### O que acontece nos bastidores?

```text
dotnet new   ──► Usa templates prontos do SDK
dotnet build ──► Compila C# para IL (gera arquivo .dll)
dotnet run   ──► Aciona o Runtime ──► JIT converte IL ──► Executa
```

> **💬 Pergunta para a turma:**  
> *“Ao usar esses comandos no terminal, estamos usando IDE ou CLI?”*  
> 👉 **Resposta:** **CLI** (*Command Line Interface*).

---

## 📦 5. Compilação Explícita (`dotnet build`)

```bash
dotnet build
```

* **`build`:** Gera a linguagem intermediária (**IL**).
* **`.dll`:** Contém o código IL empacotado (localizado na pasta `bin/Debug/...`).

---

## 💻 6. Ambiente de Desenvolvimento

### Visual Studio Code

Hoje não é necessário instalar vários plugins avulsos. Basta instalar a extensão recomendada pela Microsoft:

* **C# Dev Kit (Microsoft):**
  * Pacote completo oficial.
  * Já inclui suporte ao C#, explorador de soluções e ferramentas de teste.
  * Substitui as extensões básicas antigas.

Para abrir o projeto no VS Code diretamente pelo terminal:
```bash
code .
```

### Visual Studio 2022

* Abra o arquivo `.csproj` ou a pasta do projeto diretamente pela interface do Visual Studio.

> **💬 Pergunta para a turma:**  
> *“O que usamos para desenvolver: Runtime ou SDK?”*  
> 👉 **Resposta:** **SDK** (pois precisamos dos compiladores, templates e ferramentas de build. O Runtime serve apenas para executar).

---

## 🧾 Frases Fortes para Fixar o Conteúdo

* 💡 **“Tudo no .NET vira IL antes de executar.”**
* 💡 **“O JIT traduz o código para a linguagem da máquina.”**
* 💡 **“O Runtime é quem realmente executa tudo.”**
* 💡 **“O SDK é para criar; o Runtime é para rodar.”**
