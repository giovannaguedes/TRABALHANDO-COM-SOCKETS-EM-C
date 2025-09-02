# TRABALHANDO-COM-SOCKETS-EM-C
permitir estabelecer conexao com alvo e fazer programas mais elaborado. olhar: man socket e man 7 ip.

⚠️ Uso exclusivo para fins educacionais • Desenvolvido por M!ss s3c

📝 Guia passo a passo: Criando e executando seu programa

1. Criar o arquivo do programa

No terminal, digite:

nano desec_socket.c


Adicione o seguinte código:

#include <stdio.h>
#include <sys/socket.h>
#include <netdb.h>
#include <arpa/inet.h>
#include <unistd.h>

int main(void) {

    int meusocket; 
    int conecta;
    struct sockaddr_in alvo;

    meusocket = socket(AF_INET, SOCK_STREAM, 0);
    if(meusocket < 0){
        printf("Erro ao criar socket\n");
        return 1;
    }

    alvo.sin_family = AF_INET;
    alvo.sin_port = htons(80);
    alvo.sin_addr.s_addr = inet_addr("192.168.0.1");

    conecta = connect(meusocket, (struct sockaddr *)&alvo, sizeof(alvo));
    if(conecta == 0){
        printf("Porta aberta\n");
    } else {
        printf("Porta fechada\n");
    }

    close(meusocket);

    return 0;
}

2. Compilar o programa

No terminal, digite:

gcc desec_socket.c -o desec_socket


gcc → compilador C

-o desec_socket → nome do executável gerado

3. Executar o programa
./desec_socket


Saída esperada:

Porta aberta


ou

Porta fechada

4. Observações e melhorias

É possível automatizar o código permitindo que o IP e a porta sejam passados como variáveis ou argumentos, em vez de usar apenas uma porta fixa.

Consulte man socket e man 7 ip para mais detalhes sobre funções de socket e programação de rede.

Sempre feche os sockets para liberar recursos do sistema.

👉 O que você aprendeu aqui

socket() → cria um socket TCP.

connect() → tenta estabelecer conexão com um IP e porta alvo.

struct sockaddr_in → armazena informações de IP e porta para a conexão.

htons() → converte a porta para formato de rede (network byte order).

inet_addr() → converte um IP em string para endereço de rede.

close() → fecha o socket após o uso.
