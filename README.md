<a href="https://www.open.mp"><img src="https://raw.githubusercontent.com/adib-yg/openmp-server-installation/main/screenshots/open-mp-logo.png" width="128" height="128" align="left"></a><h1>Instalação Fácil de Servidor open.mp<br>(Para distros baseadas em Debian)</h1>
<br>
> [!NOTE] 
> *Se você está usando o servidor SA:MP e ainda não fez a conversão para open.mp, [não prossiga sem ler este guia](https://github.com/adib-yg/openmp-server-installation)!*

> [!NOTE] 
> *Se você está usando o plugin FCNPC, saiba que o plugin não funciona com o open.mp atualmente.<br>
> Mas não por muito tempo! [Você pode ajudar com uma doação aqui no Open Collective!](https://opencollective.com/openmultiplayer)*
<br>

## Introdução

Bem-vindo! Este repositório contém um guia completo sobre a instalação de um servidor open.mp no Ubuntu ou em outra distro Linux baseada em Debian.<br>
Seja você um iniciante ou alguém que deseja atualizar seus conhecimentos, este guia tem algo para você.

<br>

## Pré-requisitos
Antes de começar este guia, você deve ter:

- Um host rodando Ubuntu (20.04 ou mais recente recomendado) ou outra distribuição Linux baseada em Debian;
- Filezilla ou WinSCP para transferências de arquivos;
- PuTTY ou o terminal de SSH do seu host;<br>
> [!NOTE] 
>*Se você instalar o WinSCP, o instalador solicitará que você instale o PuTTY!<br>
>Fica a seu critério se deseja instalá-lo ou não, mas você pode sempre baixá-lo posteriormente!*
  
<br>

## Parte A - Conectar, atualizar e criar usuário

### Passo 1 - Abra o PuTTY ou o terminal de SSH do seu host e conecte-se
> [!NOTE] 
> *Existem guias completos na web ou até mesmo no site do seu host sobre como conectar via PuTTY.<br>
> Algumas conexões SSH exigem uma key, então não posso fornecer ajuda específica aqui, mas sinta-se à vontade para perguntar no Discord do open.mp ou buscar na web!*

<br>

### Passo 2 - Atualizar o Linux
  - Vamos garantir que o sistema está atualizado:
```sh
sudo apt update
```
```sh
sudo apt upgrade
```
<br>

### Passo 3 - Criar um novo usuário
  - Por razões de segurança, é uma boa prática criar um novo usuário especificamente para executar o servidor:
> [!NOTE] 
> *Substitua MyUserName por um nome de usuário de sua escolha!*
```sh
sudo adduser MyUserName
```
  - *[OPCIONAL]*  Após criar o usuário, adicione-o ao grupo sudo:
```sh
sudo usermod -aG sudo MyUserName
```
<br>

### Passo 4 - Conceder permissões ao usuário root
  - Precisamos conceder ao usuário root acesso à pasta para que, ao usar o Filezilla ou WinSCP, você possa ler e escrever os arquivos dentro da pasta do usuário:
```sh
chmod 775 /home/MyUserName
```
<br>

## Parte B- Baixar e instalar os arquivos do servidor

### Passo 5 - Baixe os arquivos do servidor
  - Podemos fazer isso de duas maneiras: o **método cego** ou o **método à prova de novato**...

<br>

### O método cego:
Eu chamo assim porque apenas precisamos usar o terminal!
  - Use wget para baixar os arquivos do repositório open.mp:
```sh
wget https://github.com/openmultiplayer/open.mp/releases/download/v1.2.0.2670/open.mp-linux-x86.tar.gz
```
> [!NOTE] 
> *Neste guia, estamos baixando a versão static!<br>
> Verifique a versão mais recente marcada com uma etiqueta verde dizendo "Latest" [aqui](https://github.com/openmultiplayer/open.mp/releases), em seguida, clique com o botão direito no arquivo desejado e copie o link!*

   - Extraia os arquivos baixados:
```sh
tar -xzf open.mp-linux-x86.tar.gz
```
   - Navegue até o diretório extraído:
```sh
cd Server
```

<br>

### O método à prova de novato:
Você sabe bem por que se chama assim... Eu acho...
  - [Vá aqui](https://github.com/openmultiplayer/open.mp/releases) e verifique a versão marcada com uma etiqueta verde dizendo "Latest";
  
  - Baixe o arquivo chamado "open.mp-linux-x86.tar.gz";
> [!NOTE] 
> *Neste guia, estamos baixando a versão static!*

  - Use o 7zip ou seu gerenciador de arquivos de sua escolha e extraia o arquivo baixado;
  - Abra o Filezilla ou o WinSCP e coloque a pasta "Server" dentro da pasta do usuário que você criou na **Parte A**
  
<br>

## Parte C - Finalizando para depois iniciar o servidor

### Passo 6 - Instale os arquivos x86
> [!NOTE] 
> *Se você usou o método à prova de novato, volte ao PuTTY ou terminal de SSH do seu host e navegue até a pasta do seu servidor usando:*
>```sh
>cd Server
>```
  - Precisamos atualizar o apt:
```sh
sudo apt update
```
  - Vamos habilitar o suporte para pacotes de 32 bits, já que estamos em um sistema de 64 bits:
```sh
sudo dpkg --add-architecture i386
```
  - Agora, para realmente instalá-lo:
```sh
sudo apt install libc6:i386
```
<br>

### Passo 7 - Iniciando o servidor
> [!NOTE] 
> *Isso é necessário apenas uma vez; depois disso, você pode pular para iniciar o servidor sem usar o chmod!*
>  - Precisamos alterar as permissões do omp-server, especificamente para torná-lo executável:
>```sh
>chmod +x omp-server
>```


- O comando para ligar o servidor:
```sh
nohup ./omp-server &
```
 - O terminal deve então exibir algo como isto:
```
[1] MyNumberHere
MyUserName@ip-123-45-67-89:/home/MyUserName$ nohup: ignoring input and appending output to 'nohup.out'
```
  - Anote o número que o terminal forneceu e depois pode fechar o terminal!

> [!NOTE] 
> *Se você esqueceu de anotar o número não é problema, iremos usar o comando 'top' no Passo 8!*

<br>

### Passo 8 - Fechar o servidor
Agora você já testou e sabe que o servidor está funcionando bem, mas agora quer fechar o servidor...
  - Se você anotou o número no Passo 7, basta digitar:
```sh
sudo kill MyNumberHere
```
> [!NOTE] 
> *Substitua MyNumberHere pelo número desejado!*

  - Se você esqueceu de copiar o número, digite:
```sh
top
```
  - Aguarde 2/3 segundos enquanto a lista é atualizada e veja algo como isto no topo:
```
MyNumberHere | MyUserName | 00 | 0 | 00 | 00 | 00 | S | 0.0  | 0.0 | 0:00.00 | omp-server
```
  - Anote ou memorize, pressione a tecla 'Q' para sair e depois digite:
```sh
sudo kill MyNumberHere
```
  
<br>

## Parte D - Upload do seu próprio gamemode e arquivos

- Leia [este guia](https://github.com/adib-yg/openmp-server-installation) para entender como transferir os seus arquivos do servidor para o seu host.

> [!NOTE] 
> *Não se esqueça de que o Linux não lê arquivos .dll, sempre baixe os arquivos .so correspondentes!*

<br>
<br>

# Ajuda
Se você tiver problemas com o servidor ou com este guia, [por favor, entre no servidor oficial do Discord do open.mp](https://discord.gg/samp) e use o canal [##pt-português-portuguese ](https://discord.com/channels/231799104731217931/570646134851108895).

<br>
<br>

# Palavras finais
Se você achar algo errado com este guia, sinta-se à vontade para me avisar me marcando @itsneufox no [Discord oficial do open.mp](https://discord.gg/samp)!<br>

### Obrigado à equipe do open.mp pelo trabalho incrível e pelo esforço para manter essa comunidade viva!
