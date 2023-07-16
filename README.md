# Pratica-infrastructure-as-code

## Cenário

O dono de todos os diretórios criados será o usuário root;

Todos os usuários terão permissão total dentro do diretório publico;

Os usuários de cada grupo terão permissão total dentro de seu respectivo diretório;

Os usuários não poderão ter permissão de leitura, escrita e execução em diretórios de departamentos que eles não pertencem;

&nbsp;
&nbsp;

## Visualização da infraestrutura
&nbsp;
![image](https://github.com/vnmoliveira/pratica-infrastructure-as-code/assets/76496863/a765d310-8150-4d37-8a57-252cf12ef9e4)

&nbsp;


## Solução do problema

OBS: Para solução do problema foi utilizado o ubuntu server 20.04.6

Logue como super usuário 


```sudo su```

Crie um diretório no diretório raiz ```/```

```mkdir /scripts```

Utilize o nano para criar o seu arquivo shell script, ele que vai automatizar todo o seu trabalho

```nano <nome_script>.sh```



![img1](https://github.com/vnmoliveira/pratica-infrastructure-as-code/assets/76496863/6aef21e9-055d-420d-97c3-fc8cbca3eba8)


Note que o script ainda está com a cor branca, indicando que ele ainda não tem permissão de execução, para dar permissão, execute ```chmod +x script-infrastructure-as-code.sh```


![img2](https://github.com/vnmoliveira/pratica-infrastructure-as-code/assets/76496863/f3749f2c-482c-4df6-b8c1-75dc462fe9a4)

E ele mudará de cor para verde.

Dentro do seu arquivo cole os seguintes comandos:

```

#!/bin/bash

echo "Criando diretórios..."

mkdir /publico
mkdir /adm
mkdir /ven
mkdir /sec


echo "Criando grupos..."

groupadd GRP_ADM
groupadd GRP_VEN
groupadd GRP_SEC

echo "Criando usuários..."

useradd joao -c "João da Silva" -m -s /bin/bash -p $(openssl passwd -crypt  senha123)
useradd carlos -c "Carlos Santos" -m -s /bin/bash -p $(openssl passwd -crypt senha123)
useradd maria -c "Maria Melo" -m -s /bin/bash -p $(openssl passwd -crypt senha123)

useradd debora -c "Débora Carla" -m -s /bin/bash -p $(openssl passwd -crypt senha123)
useradd sebastiao -c "Sebastião Silva" -m -s /bin/bash -p $(openssl passwd -crypt senha123)
useradd roberto -c "Roberto Firmino" -m -s /bin/bash -p $(openssl passwd -crypt senha123)

useradd josefina -c "Josefina Maria" -m -s /bin/bash -p $(openssl passwd -crypt senha123)
useradd amanda -c "Amanda Melo" -m -s /bin/bash -p $(openssl passwd -crypt senha123)
useradd rogerio -c "Rogério Carlos" -m -s /bin/bash -p $(openssl passwd -crypt senha123)

echo "Adicionando usuários aos grupos..."

usermod -G GRP_ADM joao
usermod -G GRP_ADM carlos
usermod -G GRP_ADM maria

usermod -G GRP_VEN debora
usermod -G GRP_VEN sebastiao
usermod -G GRP_VEN roberto

usermod -G GRP_SEC josefina
usermod -G GRP_SEC amanda
usermod -G GRP_SEC rogerio

echo "Adicionando permissões..."

chown root:GRP_ADM /adm
chown root:GRP_VEN /ven
chown root:GRP_SEC /sec

chmod 770 /adm
chmod 770 /ven
chmod 770 /sec
chmod 777 /publico

echo "FIM DO SCRIPT!"

```

Pronto. Agora é só executar o comando com ```./<nome_script>.sh``` que ele irá automaticamente criar toda sua infrastrutura com as devidas permissões.

![img4](https://github.com/vnmoliveira/pratica-infrastructure-as-code/assets/76496863/1cc110a4-b88d-4272-b225-37a81c6bc51b)

Agora é só verificar se os resultados saíram como planejados

### GRUPOS E SEUS USUÁRIOS:

![img3](https://github.com/vnmoliveira/pratica-infrastructure-as-code/assets/76496863/2eedbac3-bce1-4994-9ab9-efc0acba54b1)

### PERMISSÕES PARA USUÁRIOS E GRUPOS ESPECÍFICOS:

![img5 1](https://github.com/vnmoliveira/pratica-infrastructure-as-code/assets/76496863/9302d026-7dce-45b9-b46e-c6ca39be62d1)




