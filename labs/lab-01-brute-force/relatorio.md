# RELATÓRIO INCIDENTE 01 
Data: 17/11/2026

## Resumo Executivo: 
Ocorreu um ataque de SSH força bruta do IP 172.20.10.12 na máquina de IP 172.20.10.10 comprometendo as credenciais.

## Cenário e Ambiente: 
IP da vítima 172.20.10.10, Usuário: vboxuser.
Atacante: Máquina Isolada, IP: 172.20.10.12

## Linha do Tempo: 
Início da Atividade Maliciosa: 15:41:48. 
Às 15:41:52 foi detectado SSHD brute force, regra 5763.
Às 15:42:02 foi detectado depois de múltiplas falhas de autenticação o sucesso, regra 40112.
Às 15:42:04 o ataque terminou.

## Evidências:
![Evidência de Alertas Wazuh - Brute Force](Evidencias/alertas-wazuh-brute_force-1.png)
![Evidência do Ataque pelo Terminal](Evidencias/ataque-brute_force-1.png)

## Mapeamento MITRE ATT&CK: 
A tática usada foi credential access. cód: TA0006
A técnica foi Brute Force. cód: T1110

## IOCs:
IP(IPV4) do atacante: 172.20.10.12
Conta Alvo: vboxuser

## Classificação e Severidade:
Tivemos vários alertas verdadeiro positivo level 5 de severidade baixa, cód: 5557(unix_chkpwd: Password failed) e 5760(sshd: authentication failed).
Tivemos um alerta verdadeiro positivo level 12 de severidade crítica comprometendo a conta vboxuser, cód: 40112(Multiple authentication failures followed by a success).
Tivemos três alertas level 10 com severidade alta , cód: 2502(syslog: User missed the password more than one time).
Tivemos um alerta verdadeiro positivo level 10 de severidade alta, cód: 5763(sshd: brute force trying to get access to the system. Authentication failed)

## Lições Aprendidas: 
1- Resposta Imediata: 1) Recomenda-se trocar a senha do usuário(vboxuser). 
2) Encerramento de sessões ativas e auditoria de persistência executados após o login.

2- Recomendações de Prevenção: 1) Recomenda-se restringir IPs desconhecidos e permitir acessos ssh somente a IPs previamente autorizados; 2) Bloquear tentativas de acesso a contas após 3 tentativas em intervalo muito curto de tempo. 