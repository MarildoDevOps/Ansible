stop all containers:
docker kill $(docker ps -q)

remove all containers
docker rm $(docker ps -a -q)

remove all docker images
docker rmi $(docker images -q)


# Ansible
#ansible CFG
[defaults]

#--- General settings
forks                   = 5                             ; Quantidade de processos.
log_path                = /var/log/ansible.log          ; Arquivo de log.
module_name             = command                       ; Modulo padrao.
executable              = /bin/bash                     ; Shell padrao.
ansible_managed         = Ansible managed               ; Permite utilizacao de strings, timestamp em suas playbok/tasks.

#--- Files/Directory settings
inventory               = /etc/ansible/hosts            ; Arquivo de Hosts do ansible.
library                 = /usr/share/my_modules         ; Diretorio onde contÃ©m os mÃ³dulos do ansible.
remote_tmp              = ~/.ansible/tmp                ; Onde serao armazenados os arquivos temporarios nos hosts de destino (inventory).
local_tmp               = ~/.ansible/tmp                ; Diretorio temporario local.
roles_path              = /etc/ansible/roles            ; Diretorio padrao de roles do ansible.

#--- Users settings
remote_user             = root                          ; Usuario padrao - se nao especificado.
sudo_user               = root                          ; Usuario sudo padrao.
ask_pass                = no                            ; Perguntar por padrao a senha durante a execucao das tasks. 
ask-sudo_pass           = no                            ; Similar ao ask_pass.

#--- SSH settings
remote_port             = 22                            ; Porta padrao de conexao remota (SSH).
timeout                 = 10                            ; SSH Timeout.
host_key_checking       = False                         ; Validacao de chave SSH durante a conexao
ssh_executable          = /usr/bin/ssh                  ; Binario ssh. Utiliza-se a variavel ansible_ssh_executable.
private_key_file        = ~/.ssh/id_rsa                 ; Private key

[privilege_scalation]

become                  = True                          ; Permite elevacao de privilegio.
become_method           = sudo                          ; Metodo padrao.
become_user             = root                          ; Usuario padrao.
become_ask_pass         = False                         ; Perguntar a senha.

[ssh_connection]

scp_if_ssh              = smart                         ; Executa sftp e se nao conseguir tenta com scp (Padrao).
transfer_method         = smart                         ; Ordem de execucao: sftp --> scp (padrao).
retries                 = 3                             ; Tempo para nova tentativa de conxao com um host.


#comando valida inv
ansible all -m gather_facts --tree /tmp/facts


#comando valida sintax
ansible-playbook playbooks/install-httpd.yml --syntax-check
