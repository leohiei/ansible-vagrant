# Projeto Ansible + Vagrant - Criação de Máquinas e Gestão com Ansible

Neste projeto, automatizei um script em Vagrant para a criação de uma máquina **master** e três máquinas **node**, com o intuito de simular um servidor.

Utilizei o **Ansible** para agrupar os hosts e fiz um pequeno arquivo YAML para testar a conexão com as máquinas via **ping** e, em seguida, instalar o pacote **Apache** na máquina master.

## Requisitos

- **Ansible** e **Vagrant** instalados no seu sistema.
- Acesso **SSH** ao(s) host(s) de destino.
- Usuário com permissões de **sudo** para executar tarefas administrativas (como instalar pacotes).

## Como Usar

### 1. Configuração do Inventário

Edite o arquivo `hosts.yaml` para incluir os seus hosts de destino ou use um arquivo de inventário dinâmico. O arquivo `hosts.yaml` pode ser configurado assim:

```
yaml
all:
  children:
    master:
      hosts:
        master.lab.org:
```


### 2. Configuração do Playbook

O playbook ping.yaml executa um teste de ping nos hosts especificados e, em seguida, instala o Apache (httpd) nos mesmos.

### 3. Executar o Playbook

Para executar o playbook, use o comando abaixo. Certifique-se de passar o inventário correto e de ter configurado a autenticação SSH para os hosts.

ansible-playbook -i hosts.yaml ping.yaml

Caso queira simular as mudanças sem realmente aplicar (modo de verificação), use o comando com a flag -C:

ansible-playbook -i hosts.yaml ping.yaml -C

Importante: Certifique-se de que o usuário configurado para autenticação SSH tenha permissões adequadas de sudo para realizar as tarefas de instalação.
Contribuindo

Sinta-se à vontade para abrir uma issue ou enviar um pull request para melhorar o projeto. Toda contribuição é bem-vinda!


