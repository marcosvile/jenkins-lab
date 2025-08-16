# Laboratório Jenkins com Vagrant

Este projeto utiliza o Vagrant para provisionar uma máquina virtual com Ubuntu 24.04, Jenkins, Docker e Docker Compose.

## Pré-requisitos

-   [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
-   [Vagrant](https://www.vagrantup.com/downloads)

## Como Começar

### Clone o repositório

```bash
git clone <URL_DO_SEU_REPOSITORIO>
cd jenkins-lab
```

Isso criará os arquivos `id_rsa` (chave privada) e `id_rsa.pub` (chave pública) dentro do diretório `.ssh`.

### Inicie a Máquina Virtual

Execute o seguinte comando para criar e provisionar a VM. Isso pode levar alguns minutos.

```bash
vagrant up
```

## Acessando o Jenkins

Após a conclusão do provisionamento, o Jenkins estará disponível no seu navegador em [http://127.0.0.1:8080](http://127.0.0.1:8080).

Para desbloquear o Jenkins, você precisará da senha inicial do administrador. Você pode obtê-la conectando-se à VM via SSH e exibindo o conteúdo do arquivo de senha:

```bash
vagrant ssh -c "sudo cat /var/lib/jenkins/secrets/initialAdminPassword"
```

Copie a senha exibida no terminal e cole-a na tela de desbloqueio do Jenkins.

## Comandos Úteis do Vagrant

-   `vagrant up`: Inicia e provisiona a máquina virtual.
-   `vagrant ssh`: Conecta-se à máquina virtual via SSH.
-   `vagrant halt`: Desliga a máquina virtual.
-   `vagrant provision`: Executa novamente os scripts de provisionamento em uma VM em execução.
-   `vagrant destroy`: Remove completamente a máquina virtual e todos os seus recursos.

## Configuração da VM

A configuração da máquina virtual é definida no arquivo [Vagrantfile](Vagrantfile):

-   **Box**: `bento/ubuntu-24.04`
-   **Hostname**: `server-jenkins`
-   **Memória**: 2048MB
-   **Porta Redirecionada**: A porta 8080 do convidado é mapeada para a porta 8080 do host.

O script de provisionamento [provision.sh](provision.sh) é responsável por instalar:
-   OpenJDK 17
-   Jenkins
-   Docker e Docker Compose