# Instalação do Go

As instruções oficiais de instalação do Go estão disponíveis [aqui](http://www.golangbr.org/doc/instalacao).

Esse guia vai presumir que você está usando um gerenciador de pacotes como [Homebrew](https://brew.sh), [Chocolatey](https://chocolatey.org), [Apt](https://help.ubuntu.com/community/AptGet/Howto) ou [yum](https://access.redhat.com/solutions/9934).

## Instalação

### Mac OSX

O processo de instalação é bem simples. Primeiro, o que você precisa fazer é executar o comando abaixo pra instalar o homebrew \(brew\). O Brew depende do Xcode, então você deve se certificar de instalá-lo primeiro.

```bash
xcode-select --install
```

Depois, execute o comando a seguir para instalar o homebrew:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Agora você consegue instalar o Go:

```bash
brew install go
```

_Siga todas as instruções recomendadas pelo seu gerenciador de pacotes. **Nota** cada grupo de instruções varia de sistema operacional para sistema operacional._

Você pode verificar a instalação com:

```bash
$ go version
go version go1.10 darwin/amd64
```

### Linux

O processo de instalação é bem simples. Primeiro você precisa escolher e baixar a versão do Go que você deseja instalar. Para isso [acesse o site oficial](https://golang.org/) da linguagem e copie o da versão desejada \(Ex.: [https://golang.org/dl/go1.17.1.linux-amd64.tar.gz](https://golang.org/dl/go1.17.1.linux-amd64.tar.gz)\). Recomendamos instalar sempre a versão mais atual.

Para baixá-lo execute o seguinte comando no seu terminal.

```bash
# selecione a versão  que você deseja instalar, no nosso exemplo estamos utilizando a versão 1.13
VERSAO_GO=1.17
cd ~
curl -O "https://dl.google.com/go/go${VERSAO_GO}.linux-amd64.tar.gz"
```

Agora descompacte os arquivos com o seguinte comando.

```bash
tar -C /usr/local -xzf "go${VERSAO_GO}.linux-amd64.tar.gz"
```

Adicione `/usr/local/go/bin` à variável de ambiente PATH

```bash
export PATH=$PATH:/usr/local/go/bin
```

**Nota**: adicione isso em seu .bashrc ou .zshrc, dependendo de qual shell você usa

Agora teste a sua instalação.

```bash
go version
go version go1.17 linux/amd64
```

### Windows

Para usuários de Windows existem duas formas de instalação, através de um arquivo ZIP que requer que você configure algumas variáveis de ambiente ou uma arquivo MSI que faz toda a configuração automaticamente. Primeiro faça download da versão que você deseja instalar. Para isso [acesse o site oficial](https://golang.org/) da linguagem e copie o arquivo da versão desejada \(Ex.: [https://golang.org/dl/go1.17.1.windows-amd64.msi](https://golang.org/dl/go1.17.1.windows-amd64.msi)\). Recomendamos instalar sempre a versão mais atual.

#### Instalação via MSI

Abra o arquivo MSI e siga os passos da instalação. Por padrão o instalador adiciona o Go na pasta `C:\Go`.

O instalador adiciona o caminho `C:\Go\bin` na variável de ambiente "Path" e cria a variável de usuário "GOPATH" com o caminho `C:\Users\%USER%\go`.

#### Instalação via ZIP

Extraia os arquivos do arquivo ZIP no diretório de sua preferência.

Adicione na variável de ambiente "Path" o caminho para a pasta "bin" dos arquivos de Go. Na busca do menu Iniciar, digite "Variáveis" escolha a opção "Editar as variáveis de ambiente do sistema. Na aba "Avançado" clique em "Variáveis de Ambiente", localize a variável "Path" e clique em Editar &gt; Novo e preencha com o caminho escolhido \(Ex: `C:/minha-pasta-go/bin`\).

Quando ocorre alteração nas variáveis de ambiente no Windows é necessário reiniciar o sistema.

Nos próximos passos vamos configurar o ambiente Go. As [instruções abaixo](instalacao-do-go.md#o-ambiente-go) valem tanto para sistema operacional OSX quanto para o Linux. O ambiente Windows pode requisitar configurações a mais e por isso é importante seguir a documentação oficial.

## O Ambiente Go

### Módulos Go

Módulos foram introduzidos no Go 1.11. Essa abordagem é o modo de construção padrão desde o Go 1.16, portanto, o uso de GOPATH não é recomendado.

Os módulos visam resolver problemas relacionados ao gerenciamento de dependências, seleção de versões e compilações reproduzíveis. Eles também permitem que os usuários executem código Go fora do `GOPATH`.

Usar Módulos é bastante simples. Selecione qualquer diretório fora do GOPATH como a raiz do seu projeto e crie um novo módulo com o comando `go mod init`.

Um arquivo `go.mod` será gerado, contendo o caminho do módulo, a versão do Go e suas dependências, que são os outros módulos necessários para uma construção bem-sucedida.

Se nenhum `<caminho-modulo>` for especificado, `go mod init` tentará adivinhar o caminho do módulo a partir da estrutura de diretório. Ele também pode ser substituído fornecendo um argumento.

```bash
mkdir meu-projeto
cd meu-projeto
go mod init <caminho-modulo>
```

Um arquivo `go.mod` é parecido com isso:

```bash
module cmd

go 1.17
```

A documentação nativa fornece uma visão geral de todos os comandos `go mod` disponíveis.

```bash
go help mod
go help mod init
```

## Editor Go

A escolha de editor é bem pessoal. Você pode já ter um de sua preferência que tem suporte a Go. Se não tiver, leve em consideração um Editor como o [Visual Studio Code](https://code.visualstudio.com), que tem um suporte exceptional à linguagem.

Você pode instalá-lo com o comando a seguir:

```bash
brew install --cask visual-studio-code
```

Confirme que o VS Code foi instalado corretamente executando o seguinte comando:

```bash
code .
```

O VS Code é lançado com poucos softwares habilidados. Você pode habilitar novos softwares instalando extensões. Para adicionar o suporte a Go, você deve instalar uma extensão. Existem várias disponíveis para o VS Code, mas uma excepcional é a do [Luke Hoban](https://github.com/Microsoft/vscode-go). Instale-a da forma a seguir:

```bash
code --install-extension golang.go
```

Quando abrir um arquivo Go pela primeira vez no VS Code, ele vai indicar que ferramentas de análises estão faltando. Clique no botão para instalá-las. A lista de ferramentas que são instaladas \(e usadas\) pelo VS Code estão disponíveis [aqui](https://github.com/Microsoft/vscode-go/wiki/Go-tools-that-the-Go-extension-depends-on).

## Debugger do Go

Uma boa opção para debugar seus programas em Go \(que é integrado com o VS Code\) é o Delve. Ele pode ser instalado da seguinte maneira usando `go get`:

```bash
go get -u github.com/go-delve/delve/cmd/dlv
```

## Linter do Go

Uma melhoria sob o linter padrão pode ser configurada usando o [GolangCI-Lint](https://github.com/golangci/golangci-lint).

Que pode ser instalada da seguinte forma:

```bash
brew install golangci/tap/golangci-lint
```

## Refatoração e suas ferramentas

Uma grande ênfase nesse livro é dada na importância da refatoração.

Suas ferramentas podem te ajudar a fazer uma refatoração com maior confiança.

Você deve ter familiaridade o suficiente com seu editor para performar as ações a seguir com uma simples combinação de teclas:

* **Extrair/alinhar variável**. Ser capaz de pegar valores mágicos e dar um nome a eles vai simplificar seu código rapidamente.
* **Extrair método/função**. É crucial ser capaz de tirar uma seção do código e extrair funções/métodos.
* **Renomear**. Você deve se sentir capaz de renomear símbolos no decorrer dos arquivos com confiança.
* **go fmt**. O Go tem um formatador nativo chamado `go fmt`. Seu editor deve executar esse comando a cada vez que salvar o arquivo.
* **Executar testes**. Não precisa nem dizer que você deve ser capaz de fazer todos os pontos acima e então re-executar seus testes rapidamente para certificar que sua refatoração não quebrou nada.

Além disso, para te ajudar a trabalhar com seu código, você deve ser capaz de:

* **Verificar a assinatura da função**. Nunca tenha dúvida sobre a forma de chamar uma função em Go. Sua IDE deve descrever uma função em termos de sua documentação, seus parâmetros e o que ela retorna.
* **Ver a definição da função**. Se não tiver certeza sobre como uma função funciona, você deve ser capaz de ir para o código fonte de descobrir por si facilmente.
* **Encontrar usos de um símbolo**. Ser capaz de ver o contexto de uma função sendo chamada pode te ajudar com o processo de refatoração.

Dominar suas ferramentas vai te ajudar a concentrar no código e reduzir a troca de contexto.

## Resumindo

Nesse ponto você já deve ter o Go instalado, um editor disponível e algumas ferramentas básicas configuradas. O Go tem um ecossistema enorme de produtos feitos por outras pessoas. Identificamos alguns componentes úteis aqui, mas você pode encontrar uma lista mais completa no [Awesome Go](https://awesome-go.com).

