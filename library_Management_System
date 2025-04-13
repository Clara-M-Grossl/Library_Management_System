#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#include <time.h>

#define STR_TAM 100

typedef char string[STR_TAM];

//STRUCTS DE DADOS
struct dados_livro {
    string titulo;
    string editora;
    string autor;
    string local_pub;
    string palavra_chave;
    int ano_pub;
    int qtd_paginas;
    int edicao;
    int qtd_exem;
    int status; // 0 inativo 1 ativo
    int c_qtd_exem;
    struct dados_livro *p_prox;
};

struct dados_usuario {
    string nome;
    string endereco;
    string email;
    string telefone;
    string livro_1;
    string livro_2;
    int id;
    int qtd_livro;
    int status; // 0 inativo 1 ativo
    struct dados_usuario *p_prox;
};

struct dados_emprestimo {
    string usuario;
    string livro_1;
    string livro_2;
    int qtd_emprestimo_usuario;
    int dia;
    int mes;
    int ano;
    struct dados_emprestimo *p_prox;
};

typedef struct dados_livro dados_livro;
typedef struct dados_usuario dados_usuario;
typedef struct dados_emprestimo dados_emprestimo;

//CABEÇALHO DAS FUNÇÕES
//INSERIR DADOS
dados_livro *cadastrar_novo_livro();
dados_usuario *cadastrar_novo_usuario();
dados_emprestimo *cadastrar_novo_emprestimo(dados_usuario *usuario, dados_livro *livro);

//LOCALIZAR
dados_livro *localizar_livro_titulo(dados_livro *lista_livro, string titulo);
dados_livro *localizar_livro_palavra_chave(dados_livro *lista_livro, string palavra_chave);
dados_livro *localizar_livro_autor(dados_livro *lista_livro, string autor);
dados_usuario *localizar_usuario_nome(dados_usuario *lista_usuario, string nome);
dados_emprestimo *localizar_emprestimo(dados_emprestimo *lista_emprestimo, string nome);

//MENUS
int menu();
int menu_controle_emprestimo();
int menu_relatorio();
int menu_localizar_livro();
int menu_saida_relatorio();

//INSERIR NO ARQUIVO
void inserir_livro_inicio_lista(dados_livro **lista_livro, dados_livro *novo_livro);
void inserir_usuario_inicio_lista(dados_usuario **lista_usuario, dados_usuario *novo_usuario);
void inserir_emprestimo_inicio_lista(dados_emprestimo **lista_emprestimo, dados_emprestimo *novo_emprestimo);

//MOSTRAR DADOS
void mostrar_dados_livro(dados_livro *livro);
void mostrar_dados_usuario(dados_usuario *usuario);

//AÇÕES
void cadastrar_segundo_emprestimo(dados_usuario *usuario, dados_livro *livro, dados_emprestimo *emprestimo);
void devolucao_exemplar(dados_emprestimo *lista_emprestimo, dados_usuario *usuario, dados_livro *lista_livro);
void baixa_livro(dados_livro *livro);
void status_usuario(dados_usuario *usuario);

//RELATORIOS
void relatorio_livros(dados_livro *lista_livro);
void relatorio_usuarios(dados_usuario *lista_usuario);
void relatorio_emprestimos(dados_emprestimo *lista_emprestimo);
void relatorio_pendencias(dados_emprestimo *lista_emprestimo);
void relatorio_ano_publicacao(dados_livro *lista_livro, int inicial, int final);

//ARQUIVOS
//EXPORTAR PARA ARQUIVO BINARIO
void exportar_dados_livros_arquivo_binario(dados_livro *lista_livro, string nome_arq);
void exportar_dados_usuario_arquivo_binario(dados_usuario *lista_usuario, string nome_arq);
void exportar_dados_emprestimo_arquivo_binario(dados_emprestimo *lista_emprestimo, string nome_arq);

//IMPORTAR DO ARQUIVO BINARIO
void importar_dados_livros_arquivo_binario(dados_livro **lista_livro, string nome_arq);
void importar_dados_usuario_arquivo_binario(dados_usuario **lista_usuario, string nome_arq);
void importar_dados_emprestimo_arquivo_binario(dados_emprestimo **lista_emprestimo, string nome_arq);

//EXPORTAR PARA ARQUIVO TEXTO
void exportar_relatorio_acervo_csv(dados_livro *lista_livro, string nome_arq);
void exportar_relatorio_usuario_csv(dados_usuario *lista_usuario, string nome_arq);
void exportar_relatorio_emprestimo_csv(dados_emprestimo *lista_emprestimo, string nome_arq);
void exportar_relatorio_pendencia_csv(dados_emprestimo *lista_emprestimo, string nome_arq);
void exportar_relatorio_ano_publicaco_csv(dados_livro *lista_livro, string nome_arq, int inicial, int final);

//FORMATAÇÃO
void retirar_enter(string str);
void maiuscula(string str);
void formatacao(string str);

//DATAS
int dias_no_mes(int mes, int ano);
void gerar_data_aleatoria(int *dia, int *mes, int *ano);
void gerar_data_atual(int *dia, int *mes, int *ano);
int comparar_datas(int dia1, int dia2);


//FUNÇÃO PRINCIPAL
int main()
{
    //variaveis locais
    dados_livro *lista_livro = NULL;
    dados_usuario *lista_usuario = NULL;
    dados_emprestimo *lista_emprestimo = NULL;

    dados_livro *novo_livro = NULL;
    dados_usuario *novo_usuario = NULL;
    dados_emprestimo *novo_emprestimo = NULL;

    dados_usuario *usuario_encontrado = NULL;
    dados_livro *livro_encontrado = NULL;
    dados_emprestimo *emprestimo_encontrado = NULL;

    dados_usuario *usuario_encontrado_2 = NULL;
    dados_livro *livro_encontrado_2 = NULL;

    int opc;
    int opc_emprestimo;
    int opc_relatorio;
    int opc_busca;
    int opc_ativacao;
    int opc_inativacao;
    int opc_saida_1, opc_saida_2, opc_saida_3, opc_saida_4, opc_saida_5;

    int qtd_exemplar;

    int inicial;
    int final;

    string titulo;
    string nome;
    string autor;
    string palavra_chave;
    string nome_arquivo;

    srand(time(NULL));


    printf("\n-------------------------------------------------------------\n");  
    printf("\n*IMPORTANDO DADOS...........................................*\n");
    printf("\n-------------------------------------------------------------\n");

    importar_dados_livros_arquivo_binario(&lista_livro, "dados_livro.bin");
    importar_dados_usuario_arquivo_binario(&lista_usuario, "dados_usuario.bin");
    importar_dados_emprestimo_arquivo_binario(&lista_emprestimo, "dados_emprestimo.bin");

    do{
        opc = menu();

        switch (opc){
            case 1:
                printf("\n-------------------------------------------------------------\n");  
                printf("\n*CADASTRO DE EXEMPLARES*\n");
                printf("\n-------------------------------------------------------------\n");
                
                novo_livro = cadastrar_novo_livro;
                if(!novo_livro){
                    printf("\n-------------------------------------------------------------\n");
                    printf("Nao foi possivel alocar memoria.\n");
                    printf("\n-------------------------------------------------------------\n");
                }
                else {
                    inserir_livro_inicio_lista(&lista_livro, cadastrar_novo_livro());
                }
                break;
            case 2:
                printf("\n-------------------------------------------------------------\n");  
                printf("\n*CADASTRO DE USUARIOS*\n");
                printf("\n-------------------------------------------------------------\n");

                novo_usuario = cadastrar_novo_usuario();
                if(!novo_usuario){
                    printf("\n-------------------------------------------------------------\n");
                    printf("Nao foi possivel alocar memoria.\n");
                    printf("\n-------------------------------------------------------------\n");
                }
                else {
                    inserir_usuario_inicio_lista(&lista_usuario, novo_usuario);
                }
                break;
            case 3:
                printf("\n-------------------------------------------------------------\n");  
                printf("\n*CONTROLE DE EMPRESTIMOS*\n");
                printf("\n-------------------------------------------------------------\n");

                opc_emprestimo = menu_controle_emprestimo();
                switch(opc_emprestimo){
                    case 1:
                        printf("\n-------------------------------------------------------------\n");
                        printf("\n*CADASTRAR NOVO EMPRESTIMO*\n");
                        printf("\n-------------------------------------------------------------\n");

                        printf("Digite o titulo do livro..........................: ");
                        fgets(titulo, STR_TAM, stdin);
                        formatacao(titulo);

                        livro_encontrado_2 = localizar_livro_titulo(lista_livro, titulo);

                        if(!livro_encontrado_2){
                            printf("\n-------------------------------------------------------------\n");
                            printf("LIVRO NAO ENCONTRADO.\n");
                            printf("\n-------------------------------------------------------------\n");
                        }
                        else {
                            if(livro_encontrado_2->status == 0 || livro_encontrado_2->qtd_exem <= 0){
                                printf("\n-------------------------------------------------------------\n");
                                printf("LIVRO INDISPONIVEL.\n");
                                printf("\n-------------------------------------------------------------\n");
                            }
                            else {
                                printf("Digite o nome...................................: ");
                                fgets(nome, STR_TAM, stdin);
                                formatacao(nome);

                                usuario_encontrado_2 = localizar_usuario_nome(lista_usuario, nome);
                                
                                if(!usuario_encontrado_2) {
                                    printf("\n-------------------------------------------------------------\n");
                                    printf("USUARIO NAO ENCONTRADO.\n");
                                    printf("\n-------------------------------------------------------------\n");
                                }
                                else {
                                    if(usuario_encontrado_2->status == 0){
                                        printf("\n-------------------------------------------------------------\n");
                                        printf("USUARIO INATIVO.\n");
                                        printf("\n-------------------------------------------------------------\n");
                                    }
                                    else {
                                        if(usuario_encontrado_2->qtd_livro == 0)
                                        {
                                            novo_emprestimo = cadastrar_novo_emprestimo(usuario_encontrado_2, livro_encontrado_2);
                                            if(!novo_emprestimo){
                                                printf("\n-------------------------------------------------------------\n");
                                                printf("Nao foi possivel alocar memoria.\n");
                                                printf("\n-------------------------------------------------------------\n");
                                            }
                                            else {
                                                inserir_emprestimo_inicio_lista(&lista_emprestimo, novo_emprestimo);
                                            }
                                        }
                                        else if(usuario_encontrado_2->qtd_livro == 1){
                                            emprestimo_encontrado = localizar_emprestimo(lista_emprestimo, usuario_encontrado_2->nome);
                                            cadastrar_segundo_emprestimo(usuario_encontrado_2, livro_encontrado_2, emprestimo_encontrado);
                                        }  
                                        else if(usuario_encontrado_2->qtd_livro == 2){
                                            printf("\n-------------------------------------------------------------\n");
                                            printf("EMPRESTIMO NAO REALIZADO\n");
                                            printf("CAPACIDADE MAXIMA DE EMPRESTIMOS");
                                            printf("\n-------------------------------------------------------------\n");
                                        }
                                    }            
                                }
                            }
                        }
                        break;
                    case 2:
                        printf("\n-------------------------------------------------------------\n");
                        printf("\n*DEVOLUCAO DE EXEMPLAR*\n");
                        printf("\n-------------------------------------------------------------\n");

                        printf("Digite o nome...................................: ");
                        fgets(nome, STR_TAM, stdin);
                        formatacao(nome);

                        usuario_encontrado = localizar_usuario_nome(lista_usuario, nome);
                        
                        if(!usuario_encontrado) {
                            printf("\n-------------------------------------------------------------\n");
                            printf("USUARIO NAO ENCONTRADO.\n");
                            printf("\n-------------------------------------------------------------\n");
                        }
                        else {
                            if(usuario_encontrado->status == 0){
                                printf("\n-------------------------------------------------------------\n");
                                printf("USUARIO INATIVO.\n");
                                printf("\n-------------------------------------------------------------\n");
                            }
                            devolucao_exemplar(lista_emprestimo, usuario_encontrado, lista_livro);
                            usuario_encontrado = NULL;
                        }
                        break;
                    case 0:
                        printf("\n-------------------------------------------------------------\n");
                        printf("Voltando ao menu principal......................................");
                        printf("\n-------------------------------------------------------------\n");
                        break;
                    default:
                        printf("*OPCAO INVALIDA*");
                        printf("\n-------------------------------------------------------------\n");
                }
                break;
            case 4:
                printf("\n-------------------------------------------------------------\n");  
                printf("\n*BAIXA DE EXEMPLARES*\n");
                printf("\n-------------------------------------------------------------\n");

                printf("Digite o titulo do livro.........................: ");
                fgets(titulo, STR_TAM, stdin);
                formatacao(titulo);
                
                livro_encontrado = localizar_livro_titulo(lista_livro, titulo);

                if(!livro_encontrado){
                    printf("\n-------------------------------------------------------------\n");
                    printf("LIVRO NAO ENCONTRADO");
                    printf("\n-------------------------------------------------------------\n");
                }
                else {
                    if(livro_encontrado->status == 0){
                        printf("Voce deseja ativar o livro [%s]?\n", livro_encontrado->titulo);
                        printf("[1] - Sim.\n");
                        printf("[2] - Nao.\n");
                        scanf("%i", &opc_ativacao);
                        getchar();

                        switch(opc_ativacao){
                            case 1:
                                livro_encontrado->status = 1;
                                break;
                            case 2:                            
                                break;
                            default: 
                                printf("\n-------------------------------------------------------------\n");
                                printf("OPCAO INVALIDA.\n");
                                printf("\n-------------------------------------------------------------\n");
                        }
                    }
                    else {
                        printf("Voce deseja fazer qual acao no livro [%s]?\n", livro_encontrado->titulo);
                        printf("[1] - Dar baixa nos exemplares .\n");
                        printf("[2] - Adicionar novos exemplares.\n");
                        printf("[0] - Voltar ao menu principal.\n");
                        scanf("%i", &opc_ativacao);
                        getchar();

                        switch(opc_ativacao){
                            case 1:
                                baixa_livro(livro_encontrado);
                                break;
                            case 2:
                                printf("Voce deseja adicionar quantos exemplares?\n");
                                printf(">>> ");
                                scanf("%i", &qtd_exemplar);
                                livro_encontrado->qtd_exem += qtd_exemplar;
                                break;
                            case 0:
                                printf("\n-------------------------------------------------------------\n");
                                printf("VOLTANDO AO MENU PRINCIPAL.");
                                printf("\n-------------------------------------------------------------\n");
                                break;
                            default: 
                                printf("\n-------------------------------------------------------------\n");
                                printf("OPCAO INVALIDA.\n");
                                printf("\n-------------------------------------------------------------\n");
                        }
                    }
                }
                break;
            case 5:
                printf("\n-------------------------------------------------------------\n");  
                printf("\n*LOCALIZAR EXEMPLAR*\n");
                printf("\n-------------------------------------------------------------\n");

                do{
                    opc_busca = menu_localizar_livro();

                    switch(opc_busca) {
                        case 1:
                            printf("Digite o titulo do livro.........................: ");
                            fgets(titulo, STR_TAM, stdin);
                            formatacao(titulo);
                            
                            livro_encontrado = lista_livro;

                            do{ 
                                livro_encontrado = localizar_livro_titulo(livro_encontrado, titulo);
                                if(!livro_encontrado){
                                    printf("\n-------------------------------------------------------------\n");
                                    printf("LIVRO NAO ENCONTRADO");
                                    printf("\n-------------------------------------------------------------\n");
                                    break;
                                }
                                else {
                                    mostrar_dados_livro(livro_encontrado);
                                    livro_encontrado = livro_encontrado->p_prox;
                                }
                            }while(livro_encontrado);
                            break;
                        case 2:
                            printf("Digite as palavras-chaves........................: ");
                            fgets(palavra_chave, STR_TAM, stdin);
                            formatacao(palavra_chave);

                            livro_encontrado = lista_livro;

                            do{ 
                                livro_encontrado = localizar_livro_palavra_chave(livro_encontrado, palavra_chave);
                                if(!livro_encontrado){
                                    printf("\n-------------------------------------------------------------\n");
                                    printf("LIVRO NAO ENCONTRADO");
                                    printf("\n-------------------------------------------------------------\n");
                                    break;
                                }
                                else {
                                    mostrar_dados_livro(livro_encontrado);
                                    livro_encontrado = livro_encontrado->p_prox;
                                }
                            }while(livro_encontrado);
                            break;
                        case 3:
                            printf("Digite o nome do autor...........................: ");
                            fgets(autor, STR_TAM, stdin);
                            formatacao(autor);

                            livro_encontrado = lista_livro;

                            do{ 
                                livro_encontrado = localizar_livro_autor(livro_encontrado, autor);
                                if(!livro_encontrado){
                                    printf("\n-------------------------------------------------------------\n");
                                    printf("LIVRO NAO ENCONTRADO");
                                    printf("\n-------------------------------------------------------------\n");
                                    break;
                                }
                                else {
                                    mostrar_dados_livro(livro_encontrado);
                                    livro_encontrado = livro_encontrado->p_prox;
                                }
                            }while(livro_encontrado);
                            break;
                        case 0:
                            printf("\n-------------------------------------------------------------\n");
                            printf("Voltando ao menu principal");
                            printf("\n-------------------------------------------------------------\n");
                            break;
                        default:
                            printf("\n-------------------------------------------------------------\n");
                            printf("Opcao invalida");
                            printf("\n-------------------------------------------------------------\n");
                    }
                }while(opc_busca != 0);

                break;
            case 6:
                printf("\n-------------------------------------------------------------\n");  
                printf("\n*LOCALIZAR USUARIO*\n");
                printf("\n-------------------------------------------------------------\n");
                
                printf("Digite o nome...................................: ");
                fgets(nome, STR_TAM, stdin);
                formatacao(nome);

                usuario_encontrado = localizar_usuario_nome(lista_usuario, nome);
                
                if(!usuario_encontrado) {
                    printf("\n-------------------------------------------------------------\n");
                    printf("USUARIO NAO ENCONTRADO.\n");
                    printf("\n-------------------------------------------------------------\n");
                }
                else {
                    mostrar_dados_usuario(usuario_encontrado);
                    usuario_encontrado = NULL;
                }
                break;
            case 7:
                printf("\n-------------------------------------------------------------\n");  
                printf("\n*ATIVAR/INATIVAR USUARIOS*\n");
                printf("\n-------------------------------------------------------------\n");

                printf("Digite o nome...................................: ");
                fgets(nome, STR_TAM, stdin);
                formatacao(nome);

                usuario_encontrado = localizar_usuario_nome(lista_usuario, nome);
                
                if(!usuario_encontrado) {
                    printf("\n-------------------------------------------------------------\n");
                    printf("USUARIO NAO ENCONTRADO.\n");
                    printf("\n-------------------------------------------------------------\n");
                }
                else {
                    if(usuario_encontrado->status == 0){
                        printf("Voce deseja ativar o usuario [%s]?\n", usuario_encontrado->nome);
                        printf("[1] - Sim.\n");
                        printf("[2] - Nao.\n");
                        scanf("%i", &opc_ativacao);
                        getchar();

                        switch(opc_ativacao){
                            case 1:
                                status_usuario(usuario_encontrado);
                                break;
                            case 2:
                                printf("\n-------------------------------------------------------------\n");
                                printf("Voltando ao menu principal");
                                printf("\n-------------------------------------------------------------\n"); 
                                break;
                            default:
                                printf("\n-------------------------------------------------------------\n");
                                printf("OPCAO INVALIDA.\n");
                                printf("\n-------------------------------------------------------------\n");
                        }
                    }
                    else if(usuario_encontrado->status == 1){
                        printf("Voce deseja inativar o usuario [%s]?\n", usuario_encontrado->nome);
                        printf("[1] - Sim.\n");
                        printf("[2] - Nao.\n");
                        scanf("%i", &opc_inativacao);

                        switch(opc_inativacao){
                            case 1:
                                status_usuario(usuario_encontrado);
                                break;
                            case 2: 
                                printf("\n-------------------------------------------------------------\n");
                                printf("Voltando ao menu principal");
                                printf("\n-------------------------------------------------------------\n");
                                break;
                            default: 
                                printf("\n-------------------------------------------------------------\n");
                                printf("OPCAO INVALIDA.\n");
                                printf("\n-------------------------------------------------------------\n");
                        }
                    }
                }
                break;
            case 8:
                printf("\n-------------------------------------------------------------\n");  
                printf("\n*RELATORIOS*\n");
                printf("\n-------------------------------------------------------------\n");

                do {
                    opc_relatorio = menu_relatorio();

                    switch(opc_relatorio) {
                    case 1:
                        printf("\n-------------------------------------------------------------\n");  
                        printf("\n*RELATORIO DE ACERVO*\n");
                        printf("\n-------------------------------------------------------------\n");
                        
                        opc_saida_1 = menu_saida_relatorio();
                        switch (opc_saida_1) {
                            case 1:
                                relatorio_livros(lista_livro);
                                break;
                            case 2:
                                printf("Digite o nome do arquivo..........: ");
                                fgets(nome_arquivo, STR_TAM, stdin);
                                retirar_enter(nome_arquivo);

                                exportar_relatorio_acervo_csv(lista_livro, nome_arquivo);
                                break;
                            case 0:
                                printf("\n-------------------------------------------------------------\n");
                                printf("VOLTANDO AO MENU PRINCIPAL\n");
                                printf("\n-------------------------------------------------------------\n");
                                break;
                            default: 
                                printf("\n-------------------------------------------------------------\n");
                                printf("OPCAO INVALIDA\n");
                                printf("\n-------------------------------------------------------------\n");
                        }
                        break;
                    case 2:
                        printf("\n-------------------------------------------------------------\n");  
                        printf("\n*RELATORIO DE USUARIOS*\n");
                        printf("\n-------------------------------------------------------------\n");

                        opc_saida_2 = menu_saida_relatorio();

                        switch (opc_saida_2) {
                            case 1:
                                relatorio_usuarios(lista_usuario);
                                break;
                            case 2:
                                printf("Digite o nome do arquivo..........: ");
                                fgets(nome_arquivo, STR_TAM, stdin);
                                retirar_enter(nome_arquivo);

                                exportar_relatorio_usuario_csv(lista_usuario, nome_arquivo);         
                                break;
                            case 0:
                                printf("\n-------------------------------------------------------------\n");
                                printf("VOLTANDO AO MENU PRINCIPAL\n");
                                printf("\n-------------------------------------------------------------\n");
                                break;
                            default: 
                                printf("\n-------------------------------------------------------------\n");
                                printf("OPCAO INVALIDA\n");
                                printf("\n-------------------------------------------------------------\n");
                        }
                        break;
                    case 3:
                        printf("\n-------------------------------------------------------------\n");  
                        printf("\n*RELATORIO DE EMPRESTIMOS*\n");
                        printf("\n-------------------------------------------------------------\n");

                        opc_saida_3 = menu_saida_relatorio();

                        switch (opc_saida_3) {
                            case 1:
                                relatorio_emprestimos(lista_emprestimo);
                                break;
                            case 2:
                                printf("Digite o nome do arquivo..........: ");
                                fgets(nome_arquivo, STR_TAM, stdin);
                                retirar_enter(nome_arquivo);

                                exportar_relatorio_emprestimo_csv(lista_emprestimo, nome_arquivo);
                                break;
                            case 0:
                                printf("\n-------------------------------------------------------------\n");
                                printf("VOLTANDO AO MENU PRINCIPAL\n");
                                printf("\n-------------------------------------------------------------\n");
                                break;
                            default: 
                                printf("\n-------------------------------------------------------------\n");
                                printf("OPCAO INVALIDA\n");
                                printf("\n-------------------------------------------------------------\n");
                        }
                        break;
                    case 4:
                        printf("\n-------------------------------------------------------------\n");  
                        printf("\n*RELATORIO DE PENDENCIAS*\n");
                        printf("\n-------------------------------------------------------------\n");

                        opc_saida_4 = menu_saida_relatorio();

                        switch (opc_saida_4) {
                            case 1:
                                relatorio_pendencias(lista_emprestimo);
                                break;
                            case 2:
                                printf("Digite o nome do arquivo..........: ");
                                fgets(nome_arquivo, STR_TAM, stdin);
                                retirar_enter(nome_arquivo);

                                exportar_relatorio_pendencia_csv(lista_emprestimo, nome_arquivo);
                                break;
                            case 0:
                                printf("\n-------------------------------------------------------------\n");
                                printf("VOLTANDO AO MENU PRINCIPAL\n");
                                printf("\n-------------------------------------------------------------\n");
                                break;
                            default: 
                                printf("\n-------------------------------------------------------------\n");
                                printf("OPCAO INVALIDA\n");
                                printf("\n-------------------------------------------------------------\n");
                        }
                        break;
                    case 5:
                        printf("\n-------------------------------------------------------------\n");  
                        printf("\n*RELATORIO DE ANO DE PUBLICACAO*\n");
                        printf("\n-------------------------------------------------------------\n");

                        printf("Digite o ano inicial..............: ");
                        scanf("%i", &inicial);
                        printf("Digite o ano final..............: ");
                        scanf("%i", &final);

                        opc_saida_5 = menu_saida_relatorio();

                        switch (opc_saida_5) {
                            case 1:
                                relatorio_ano_publicacao(lista_livro, inicial, final);
                                break;
                            case 2:
                                printf("Digite o nome do arquivo..........: ");
                                fgets(nome_arquivo, STR_TAM, stdin);
                                retirar_enter(nome_arquivo);

                                exportar_relatorio_ano_publicaco_csv(lista_livro, nome_arquivo, inicial, final);
                                break;
                            case 0:
                                printf("\n-------------------------------------------------------------\n");
                                printf("VOLTANDO AO MENU PRINCIPAL\n");
                                printf("\n-------------------------------------------------------------\n");
                                break;
                            default:
                                printf("\n-------------------------------------------------------------\n"); 
                                printf("OPCAO INVALIDA\n");
                                printf("\n-------------------------------------------------------------\n");
                        }                      
                        break;
                    case 0:
                        printf("\n-------------------------------------------------------------\n");
                        printf("Voltando ao menu principal\n");
                        printf("\n-------------------------------------------------------------\n");
                        break;
                    default : 
                        printf("\n-------------------------------------------------------------\n");
                        printf("Opcao invalida");
                        printf("\n-------------------------------------------------------------\n");
                    }
                }while(opc_relatorio != 0);
                break;
            case 0:
                printf("\n-------------------------------------------------------------\n");
                printf("EXPORTANDO DADOS...............................................\n");  
                printf("Saindo.........................................................");
                printf("\n-------------------------------------------------------------\n");

                exportar_dados_livros_arquivo_binario(lista_livro, "dados_livro.bin");
                exportar_dados_usuario_arquivo_binario(lista_usuario, "dados_usuario.bin");
                exportar_dados_emprestimo_arquivo_binario(lista_emprestimo, "dados_emprestimo.bin");

                break;
            default:
                printf("*OPCAO INVALIDA*");
                printf("\n-------------------------------------------------------------\n");
        }
    }while(opc != 0);

    return 0;
}

//FUNÇÕES PARA INSERIR DADOS
dados_livro *cadastrar_novo_livro()
{
    dados_livro *novo_livro = (dados_livro*)malloc(sizeof(dados_livro));

    if (novo_livro == NULL){
        return NULL;
    }
    printf("Digite o titulo do livro..........................: ");
    fgets(novo_livro->titulo, STR_TAM, stdin);
    formatacao(novo_livro->titulo);

    printf("Digite o nome(s) do(s) autor(es)..................: ");
    fgets(novo_livro->autor, STR_TAM, stdin);
    formatacao(novo_livro->autor);

    printf("Digite o nome da editora..........................: ");
    fgets(novo_livro->editora, STR_TAM, stdin);
    formatacao(novo_livro->editora);

    printf("Digite o local de publicacao......................: ");
    fgets(novo_livro->local_pub, STR_TAM, stdin);
    formatacao(novo_livro->local_pub);

    printf("Digite as palavras chaves (separe por ';')........: ");
    fgets(novo_livro->palavra_chave, STR_TAM, stdin);
    formatacao(novo_livro->palavra_chave);

    printf("Digite o ano de publicacao........................: ");
    scanf("%i", &novo_livro->ano_pub);
    getchar();

    printf("Digite o numero da edicao........................: ");
    scanf("%i", &novo_livro->edicao);
    getchar();

    printf("Digite a quantidade de paginas...................: ");
    scanf("%i", &novo_livro->qtd_paginas);
    getchar();

    printf("Digite a quantidade de exemplares................: ");
    scanf("%i", &novo_livro->qtd_exem);
    getchar();

    novo_livro->c_qtd_exem = 0; //inicia em zero a copia da quantidade de exemplar

    novo_livro->status = 1; //livro disponivel

    novo_livro->p_prox = NULL;

    return novo_livro;
}
dados_usuario *cadastrar_novo_usuario()
{
    dados_usuario *novo_usuario = (dados_usuario*)malloc(sizeof(dados_usuario));

    if(novo_usuario == NULL){
        return NULL;
    }

    printf("Digite o nome...................................: ");
    fgets(novo_usuario->nome, STR_TAM, stdin);
    formatacao(novo_usuario->nome);

    printf("Digite o endereco...............................: ");
    fgets(novo_usuario->endereco, STR_TAM, stdin);
    formatacao(novo_usuario->endereco);

    printf("Digite o email..................................: ");
    fgets(novo_usuario->email, STR_TAM, stdin);
    formatacao(novo_usuario->email);

    printf("Digite o telefone...............................: ");
    fgets(novo_usuario->telefone, STR_TAM, stdin);
    formatacao(novo_usuario->telefone);

    printf("Digite o numero do cracha.......................: ");
    scanf("%i", &novo_usuario->id);

    novo_usuario->status = 1;
    novo_usuario->qtd_livro = 0;
    novo_usuario->livro_1[0] = '\0';
    novo_usuario->livro_2[0] = '\0';

    novo_usuario->p_prox = NULL;

    return novo_usuario;
}
dados_emprestimo *cadastrar_novo_emprestimo(dados_usuario *usuario, dados_livro *livro)
{
    dados_emprestimo *novo_emprestimo = (dados_emprestimo*)malloc(sizeof(dados_emprestimo));
    
    if(novo_emprestimo == NULL){
        return NULL;
    }

    strcpy(usuario->livro_1, livro->titulo);
    strcpy(novo_emprestimo->usuario, usuario->nome);
    strcpy(novo_emprestimo->livro_1, usuario->livro_1);
    usuario->qtd_livro = 1;
    livro->qtd_exem --;
    novo_emprestimo->qtd_emprestimo_usuario = 1;

    gerar_data_aleatoria(&novo_emprestimo->dia, &novo_emprestimo->mes, &novo_emprestimo->ano);

    printf("\n-------------------------------------------------------------\n");
    printf("\n*LIVRO EMPRESTADO COM SUCESSO*\n");
    printf("\n-------------------------------------------------------------\n");
    novo_emprestimo->p_prox = NULL;
    return novo_emprestimo;
}

//FUNÇÕES PARA LOCALIZAR
dados_livro *localizar_livro_titulo(dados_livro *lista_livro, string titulo)
{
    while(lista_livro) {
        if(strcmp(lista_livro->titulo, titulo) == 0){
            return lista_livro;
        }
        lista_livro = lista_livro->p_prox;
    }
    return NULL;
}
dados_livro *localizar_livro_palavra_chave(dados_livro *lista_livro, string palavra_chave)
{
    string c_palavra_chave;
    string *tokens;
    string lim[] = {";"};

    while(lista_livro) {
        strcpy(c_palavra_chave, lista_livro->palavra_chave);
        tokens = strtok(c_palavra_chave, lim);
        while(tokens){
            while(tokens == ' '){
                tokens ++;
            }
            if(strcmp(tokens, palavra_chave) == 0){
                return lista_livro;
            }
            tokens = strtok(NULL, "; ");
        }
        lista_livro = lista_livro->p_prox;
    }
    return NULL;
}
dados_livro *localizar_livro_autor(dados_livro *lista_livro, string autor)
{
    string c_autor;
    string *tokens;
    string lim[] = {";"};

    while(lista_livro) {
        strcpy(c_autor, lista_livro->autor);
        tokens = strtok(c_autor, lim);
        while(tokens){
            while(tokens == ' '){
                tokens ++;
            }
            if(strcmp(tokens, autor) == 0){
                return lista_livro;
            }
            tokens = strtok(NULL, "; ");
        }
        lista_livro = lista_livro->p_prox;
    }
    return NULL;
}
dados_usuario *localizar_usuario_nome(dados_usuario *lista_usuario, string nome)
{
    while(lista_usuario){
        if(strcmp(lista_usuario->nome, nome) == 0) {
            return lista_usuario;
        }
        lista_usuario = lista_usuario->p_prox;
    }
    return NULL;
}
dados_emprestimo *localizar_emprestimo(dados_emprestimo *lista_emprestimo, string nome)
{
    while(lista_emprestimo){
        if(strcmp(lista_emprestimo->usuario, nome) == 0) {
            return lista_emprestimo;
        }
        lista_emprestimo= lista_emprestimo->p_prox;
    }
    return NULL;
}

//FUNÇÕES MENU
int menu()
{
    int opc;

    printf("\n-------------------------------------------------------------\n");  
    printf("\n*MENU*\n");
    printf("\n-------------------------------------------------------------\n");  
    printf("Escolha uma opcao: \n");
    printf("[1] Cadastros de exemplares.\n");
    printf("[2] Cadastro de pessoas.\n");
    printf("[3] Controle de emprestimos. \n");
    printf("[4] Baixa de exemplares. \n");
    printf("[5] Localizar exemplar. \n");
    printf("[6] Localizar usuario. \n");
    printf("[7] Ativar/Inativar usuarios.\n");
    printf("[8] Gerar relatorios. \n");
    printf("[0] Sair.\n");
    printf(">>> ");
    scanf("%i", &opc);
    getchar();

    return opc;
}
int menu_controle_emprestimo()
{ 
    int opc;

    printf("Escolha uma opcao: \n");
    printf("[1] - Cadastrar novo emprestimo.\n");
    printf("[2] - Devolucao do livro.\n");
    printf("[0] - Sair do menu.\n");
    printf(">>> ");
    scanf("%i", &opc);
    getchar();

    return opc;
}
int menu_relatorio()
{
    int opcao;

    printf("Escolha uma opcao: \n");
    printf("[1] Relatorio de acervo;\n");
    printf("[2] Relatorio de usuarios.\n");
    printf("[3] Relatorio de emprestimos.\n");
    printf("[4] Relatorio de pendencias.\n");
    printf("[5] Relatorio de publicacoes em cada ano.\n");
    printf("[0] Sair.\n");
    printf(">>> ");
    scanf("%i", &opcao);
    getchar();

    return opcao;
}
int menu_localizar_livro()
{
    int opc;

    printf("Escolha uma opcao: \n");
    printf("[1] - Localizar por titulo.\n");
    printf("[2] - Localizar por palavra-chave.\n");
    printf("[3] - Localizar por autor.\n");
    printf("[0] - Sair do menu.\n");
    printf(">>> ");
    scanf("%i", &opc);
    getchar();

    return opc;
    
}
int menu_saida_relatorio()
{
    int opc;

    printf("Escolha uma opcao: \n");
    printf("[1] - Saida na tela.\n");
    printf("[2] - Saida em arquivo (.csv).\n");
    printf("[0] - Sair do menu.\n");
    printf(">>> ");
    scanf("%i", &opc);
    getchar();

    return opc;
}

//FUNÇÕES PARA INSERIR LIVROS NA LISTA
void inserir_livro_inicio_lista(dados_livro **lista_livro, dados_livro *novo_livro)
{
    if(*lista_livro){
        novo_livro->p_prox = *lista_livro;
    }
    *lista_livro = novo_livro;
}
void inserir_usuario_inicio_lista(dados_usuario **lista_usuario, dados_usuario *novo_usuario)
{
    if(*lista_usuario != NULL){
        novo_usuario->p_prox = *lista_usuario;
    }
    *lista_usuario = novo_usuario;
}
void inserir_emprestimo_inicio_lista(dados_emprestimo **lista_emprestimo, dados_emprestimo *novo_emprestimo)
{
    if(*lista_emprestimo != NULL){
        novo_emprestimo->p_prox = *lista_emprestimo;
    }
    *lista_emprestimo = novo_emprestimo;
}

//FUNÇÕES PARA MOSTRAR OS DADOS
void mostrar_dados_livro(dados_livro *livro)
{
    printf("\n-------------------------------------------------------------\n");
    printf("Titulo do livro.............................: %s\n", livro->titulo);
    printf("Nome(s) do(s) autor(es).....................: %s\n", livro->autor);
    printf("Nome da editora.............................: %s\n", livro->editora);
    printf("Local de publicacao.........................: %s\n", livro->local_pub);
    printf("Palavras chaves.............................: %s\n", livro->palavra_chave);
    printf("Ano de publicacao...........................: %i\n", livro->ano_pub);
    printf("Numero da edicao............................: %i\n", livro->edicao);
    printf("Quantidade de paginas.......................: %i\n", livro->qtd_paginas);
    printf("Quantidade de exemplares....................: %i\n", livro->qtd_exem);
    printf("STATUS......................................: %i\n", livro->status);
    printf("\n-------------------------------------------------------------\n");
}
void mostrar_dados_usuario(dados_usuario *usuario)
{
    printf("\n-------------------------------------------------------------\n");
    printf("Nome do usuario............................: %s\n", usuario->nome);
    printf("Endereco do usuario....................... : %s\n", usuario->endereco);
    printf("Email para contado.........................: %s\n", usuario->email);
    printf("Telefone...................................: %s\n", usuario->telefone);
    printf("Numero do cracha...........................: %i\n", usuario->id);
    printf("STATUS.....................................: %i\n", usuario->status);
    printf("\n-------------------------------------------------------------\n");
}

//FUNÇÕES PARA AÇÕES
void cadastrar_segundo_emprestimo(dados_usuario *usuario, dados_livro *livro, dados_emprestimo *emprestimo)
{
    strcpy(usuario->livro_2, livro->titulo);
    strcpy(emprestimo->livro_2, usuario->livro_2);
    usuario->qtd_livro = 2;
    emprestimo->qtd_emprestimo_usuario = 2;
    livro->qtd_exem --;

    printf("\n-------------------------------------------------------------\n");
    printf("\n*LIVRO EMPRESTADO COM SUCESSO*\n");
    printf("\n-------------------------------------------------------------\n");

}
void devolucao_exemplar(dados_emprestimo *lista_emprestimo, dados_usuario *usuario, dados_livro *lista_livro)
{
    int opc;
    dados_livro *livro_emprestado_1 = NULL;
    dados_livro *livro_emprestado_2 = NULL;
    dados_emprestimo *emprestimo_encontrado = NULL;

    emprestimo_encontrado = localizar_emprestimo(lista_emprestimo, usuario->nome);

    if(usuario->qtd_livro == 1){
        printf("Deseja devolver o livro [%s]?\n", usuario->livro_1);
        printf("[1] - Sim.\n");
        printf("[2] - Nao.\n");
        printf(">>> ");
        scanf("%i", &opc);
        getchar();

        if(opc == 1){
            livro_emprestado_1 = localizar_livro_titulo(lista_livro, usuario->livro_1);
            if(!emprestimo_encontrado){
                printf("\n-------------------------------------------------------------\n");
                printf("SEM EMPRESTIMOS");
                printf("\n-------------------------------------------------------------\n");
            }
            else {
                emprestimo_encontrado->qtd_emprestimo_usuario --;
                usuario->qtd_livro = 0;
                livro_emprestado_1->qtd_exem ++;
                printf("\n-------------------------------------------------------------\n");
                printf("LIVRO DEVOLVIDO COM SUCESSO");
                printf("\n-------------------------------------------------------------\n");
            }
        }
        else if(opc == 2){
            printf("\n-------------------------------------------------------------\n");
            printf("Voltando ao menu principal.\n");
            printf("\n-------------------------------------------------------------\n");
        }
        else if(opc != 1 && opc != 2){
            printf("\n-------------------------------------------------------------\n");
            printf("Opcao invalida");
            printf("\n-------------------------------------------------------------\n");
        }
    }
    else if(usuario->qtd_livro == 2){
        printf("Qual livro voce deseja devolver?\n");
        printf("[1] - %s\n", usuario->livro_1);
        printf("[2] - %s\n", usuario->livro_2);
        printf("[3] - Os livros [%s] e [%s].\n", usuario->livro_1, usuario->livro_2);
        printf(">>> ");
        scanf("%i", &opc);
        getchar();

        switch(opc){
            case 1:
                livro_emprestado_1 = localizar_livro_titulo(lista_livro, usuario->livro_1);
                emprestimo_encontrado->qtd_emprestimo_usuario --;
                usuario->qtd_livro = 1;
                livro_emprestado_1->qtd_exem ++;

                strcpy(usuario->livro_1, usuario->livro_2);
                strcpy(emprestimo_encontrado->livro_1, emprestimo_encontrado->livro_2);

                printf("\n-------------------------------------------------------------\n");
                printf("LIVRO DEVOLVIDO COM SUCESSO");
                printf("\n-------------------------------------------------------------\n");
                break;
            case 2:
                livro_emprestado_1 = localizar_livro_titulo(lista_livro, usuario->livro_2);
                emprestimo_encontrado->qtd_emprestimo_usuario --;
                usuario->qtd_livro = 1;
                livro_emprestado_1->qtd_exem ++;

                printf("\n-------------------------------------------------------------\n");
                printf("LIVRO DEVOLVIDO COM SUCESSO");
                printf("\n-------------------------------------------------------------\n");
                break;
            case 3:
                livro_emprestado_1 = localizar_livro_titulo(lista_livro, usuario->livro_1);
                livro_emprestado_2 = localizar_livro_titulo(lista_livro, usuario->livro_2);
                usuario->qtd_livro = 0;
                livro_emprestado_1->qtd_exem ++;
                livro_emprestado_2->qtd_exem ++;
                emprestimo_encontrado->qtd_emprestimo_usuario = 0;
                
                printf("\n-------------------------------------------------------------\n");
                printf("LIVROS DEVOLVIDOS COM SUCESSO");
                printf("\n-------------------------------------------------------------\n");
                break;
            default:
                printf("\n-------------------------------------------------------------\n");
                printf("Opcao invalida.\n");
                printf("\n-------------------------------------------------------------\n");
        }
    }
}
void baixa_livro(dados_livro *livro)
{
    int qtd_baixa;

    printf("O livro [%s] tem um total de [%i] exemplares.\n", livro->titulo, livro->qtd_exem);
    printf("Digite o numero de exemplares para dar baixa....: ");
    scanf("%i", &qtd_baixa);

    if(livro->qtd_exem < qtd_baixa) {
        printf("\n-------------------------------------------------------------\n");
        printf("\nBAIXA NAO REALIZADA\n");
        printf("Quantidade desejada maior do que a quantidade real de livros.\n");
        printf("\n-------------------------------------------------------------\n");
    }
    else if(livro->qtd_exem > qtd_baixa) {
        livro->c_qtd_exem = livro->qtd_exem;
        livro->qtd_exem = livro->qtd_exem - qtd_baixa;
        printf("\n-------------------------------------------------------------\n");
        printf("\nBAIXA DE EXEMPLARES REALIZADA COM SUCESSO\n");
        printf("\n-------------------------------------------------------------\n");
    }
    else if(livro->qtd_exem == qtd_baixa) {
        livro->c_qtd_exem = livro->qtd_exem;
        livro->status = 0;
        livro->qtd_exem = 0;
        printf("\n-------------------------------------------------------------\n");
        printf("\nBAIXA REALIZADA COM SUCESSO\n");
        printf("\n-------------------------------------------------------------\n");
    }
}
void status_usuario(dados_usuario *usuario)
{
    if(usuario->status == 0) {
        usuario->status = 1;
        printf("\n-------------------------------------------------------------\n");
        printf("USUARIO ATIVADO");
        printf("\n-------------------------------------------------------------\n");
    }
    else if(usuario->status == 1) {
        usuario->status = 0;
        printf("\n-------------------------------------------------------------\n");
        printf("USUARIO INATIVADO");
        printf("\n-------------------------------------------------------------\n");
    }
}

//FUNÇÕES PARA RELATORIOS
void relatorio_livros(dados_livro *lista_livro)
{
    while(lista_livro){
        mostrar_dados_livro(lista_livro);
        lista_livro = lista_livro->p_prox;
    }
}
void relatorio_usuarios(dados_usuario *lista_usuario)
{
    while(lista_usuario) {
        mostrar_dados_usuario(lista_usuario);
        lista_usuario = lista_usuario->p_prox;
    }
}
void relatorio_emprestimos(dados_emprestimo *lista_emprestimo)
{
    int i = 0;
    while(lista_emprestimo){
        if(lista_emprestimo->qtd_emprestimo_usuario >= 1) {
            printf("\n-------------------------------------------------------------\n");
            printf("LIVRO EMPRESTADO\n");
            printf("Nome do usuario....................: %s\n", lista_emprestimo->usuario);
            printf("Titulo do livro....................: %s\n", lista_emprestimo->livro_1);
            if(lista_emprestimo->qtd_emprestimo_usuario == 2){
                printf("Titulo do livro....................: %s\n", lista_emprestimo->livro_2);
            }
            printf("Data de devolucao.................: %02i/%02i/%04i", lista_emprestimo->dia, lista_emprestimo->mes, lista_emprestimo->ano);
            printf("\n-------------------------------------------------------------\n");
            i++;
        }  
        lista_emprestimo = lista_emprestimo->p_prox;
    }
    printf("TOTAL DE LIVROS EMPRESTADOS................: %i", i);
    printf("\n-------------------------------------------------------------\n");
}
void relatorio_pendencias(dados_emprestimo *lista_emprestimo)
{   
    int dia_atual, mes_atual, ano_atual;
    int resultado;
    int i = 0;

    while(lista_emprestimo){

        gerar_data_atual(&dia_atual, &mes_atual, &ano_atual);
        resultado = comparar_datas(lista_emprestimo->dia, dia_atual);
        
        if(resultado == 0){
            if(lista_emprestimo->qtd_emprestimo_usuario >= 1) {
                printf("LIVRO(S) QUE VENCEM HOJE:\n");
                printf("\n-------------------------------------------------------------\n");
                printf("LIVRO EMPRESTADO\n");
                printf("Nome do usuario....................: %s\n", lista_emprestimo->usuario);
                printf("Titulo do livro....................: %s\n", lista_emprestimo->livro_1);
                if(lista_emprestimo->qtd_emprestimo_usuario == 2){
                    printf("Titulo do livro....................: %s\n", lista_emprestimo->livro_2);
                }
                printf("Data de devolucao.................: %02i/%02i/%04i", lista_emprestimo->dia, lista_emprestimo->mes, lista_emprestimo->ano);
                printf("\n-------------------------------------------------------------\n");
                i++;
            }  
        }
        if(resultado == -1){
            if(lista_emprestimo->qtd_emprestimo_usuario >= 1) {
                printf("LIVROS PENDENTES:\n");
                printf("\n-------------------------------------------------------------\n");
                printf("LIVRO EMPRESTADO\n");
                printf("Nome do usuario....................: %s\n", lista_emprestimo->usuario);
                printf("Titulo do livro....................: %s\n", lista_emprestimo->livro_1);
                if(lista_emprestimo->qtd_emprestimo_usuario == 2){
                    printf("Titulo do livro....................: %s\n", lista_emprestimo->livro_2);
                }
                printf("Data de devolucao.................: %02i/%02i/%04i", lista_emprestimo->dia, lista_emprestimo->mes, lista_emprestimo->ano);
                printf("\n-------------------------------------------------------------\n");
                i++;
            }  
        }
        lista_emprestimo = lista_emprestimo->p_prox;
    }
    printf("TOTAL DE LIVROS PENDENTES................: %i", i);
    printf("\n-------------------------------------------------------------\n");
}
void relatorio_ano_publicacao(dados_livro *lista_livro, int inicial, int final)
{
    while(lista_livro){
        if(lista_livro->ano_pub >= inicial && lista_livro->ano_pub <= final){
            mostrar_dados_livro(lista_livro);
        }
        else {
            printf("SEM LIVROS NA FAIXA DE [%i] A [%i] ANOS.\n", inicial, final);
        }
        lista_livro = lista_livro->p_prox;
    }
}

//ARQUIVOS:
//EXPORTAR PARA BINARIO
void exportar_dados_livros_arquivo_binario(dados_livro *lista_livro, string nome_arq)
{
    FILE *fp = fopen(nome_arq, "wb");

    if(fp == NULL) {
        printf("\n-------------------------------------------------------------\n");
        printf("NAO FOI POSSIVEL ABRIR O ARQUIVO\n");
        printf("\n-------------------------------------------------------------\n");
        return;
    }
    while(lista_livro) {
        fwrite(lista_livro, sizeof(dados_livro), 1, fp);
        lista_livro = lista_livro->p_prox;
    }
    fclose(fp);
}
void exportar_dados_usuario_arquivo_binario(dados_usuario *lista_usuario, string nome_arq)
{
    FILE *fp = fopen(nome_arq, "wb");

    if(fp == NULL) {
        printf("\n-------------------------------------------------------------\n");
        printf("NAO FOI POSSIVEL ABRIR O ARQUIVO\n");
        printf("\n-------------------------------------------------------------\n");
        return;
    }
    while(lista_usuario) {
        fwrite(lista_usuario, sizeof(dados_usuario), 1, fp);
        lista_usuario = lista_usuario->p_prox;
    }
    fclose(fp);
}
void exportar_dados_emprestimo_arquivo_binario(dados_emprestimo *lista_emprestimo, string nome_arq)
{
    FILE *fp = fopen(nome_arq, "wb");

    if(fp == NULL) {
        printf("\n-------------------------------------------------------------\n");
        printf("NAO FOI POSSIVEL ABRIR O ARQUIVO\n");
        printf("\n-------------------------------------------------------------\n");
        return;
    }
    while(lista_emprestimo) {
        fwrite(lista_emprestimo, sizeof(dados_emprestimo), 1, fp);
        lista_emprestimo = lista_emprestimo->p_prox;
    }
    fclose(fp);
}

//IMPORTAR DADOS DO ARQUIVO BINARIO
void importar_dados_livros_arquivo_binario(dados_livro **lista_livro, string nome_arq)
{
    FILE *fp = fopen(nome_arq, "rb");
    dados_livro *aux = NULL;

    if(fp == NULL) {
        printf("\n-------------------------------------------------------------\n");
        printf("NAO FOI POSSIVEL ABRIR O ARQUIVO\n");
        printf("\n-------------------------------------------------------------\n");
        return;
    }
    while(!feof(fp)) {
        aux = (dados_livro*)malloc(sizeof(dados_livro));
        fread(aux, sizeof(dados_livro), 1, fp);
        aux->p_prox = NULL;
        if(!feof(fp)) {
            inserir_livro_inicio_lista(lista_livro, aux);
        }
        else {
            free(aux);
        }
    }
    fclose(fp);
}
void importar_dados_usuario_arquivo_binario(dados_usuario **lista_usuario, string nome_arq)
{
    FILE *fp = fopen(nome_arq, "rb");
    dados_usuario *aux = NULL;

    if(fp == NULL) {
        printf("NAO FOI POSSIVEL ABRIR O ARQUIVO\n");
        return;
    }
    while(!feof(fp)) {
        aux = (dados_usuario*)malloc(sizeof(dados_usuario));
        fread(aux, sizeof(dados_usuario), 1, fp);
        aux->p_prox = NULL;
        if(!feof(fp)) {
            inserir_usuario_inicio_lista(lista_usuario, aux);
        }
        else {
            free(aux);
        }
    }
    fclose(fp);
}
void importar_dados_emprestimo_arquivo_binario(dados_emprestimo **lista_emprestimo, string nome_arq)
{
    FILE *fp = fopen(nome_arq, "rb");
    dados_emprestimo *aux = NULL;

    if(fp == NULL) {
        printf("NAO FOI POSSIVEL ABRIR O ARQUIVO\n");
        return;
    }
    while(!feof(fp)) {
        aux = (dados_emprestimo*)malloc(sizeof(dados_emprestimo));
        fread(aux, sizeof(dados_emprestimo), 1, fp);
        aux->p_prox = NULL;
        if(!feof(fp)) {
            inserir_emprestimo_inicio_lista(lista_emprestimo, aux);
        }
        else {
            free(aux);
        }
    }
    fclose(fp);
}

//EXPORTAR RELATORIOS PARA ARQUIVO TEXTO
void exportar_relatorio_acervo_csv(dados_livro *lista_livro, string nome_arq)
{
    FILE *fp = fopen(nome_arq, "w");
    if(fp == NULL){
        printf("NAO FOI POSSIVEL ABRIR O ARQUIVO.\n");
    }
    while(lista_livro) {
        fprintf(fp, "\n-------------------------------------------------------------\n");  
        fprintf(fp, "\n*RELATORIO DE ACERVO*\n");
        fprintf(fp, "\n-------------------------------------------------------------\n");
        fprintf(fp, "Titulo do livro.............................: %s\n", lista_livro->titulo);
        fprintf(fp, "Nome(s) do(s) autor(es).....................: %s\n", lista_livro->autor);
        fprintf(fp, "Nome da editora.............................: %s\n", lista_livro->editora);
        fprintf(fp, "Local de publicacao.........................: %s\n", lista_livro->local_pub);
        fprintf(fp, "Palavras chaves.............................: %s\n", lista_livro->palavra_chave);
        fprintf(fp, "Ano de publicacao...........................: %i\n", lista_livro->ano_pub);
        fprintf(fp, "Numero da edicao............................: %i\n", lista_livro->edicao);
        fprintf(fp, "Quantidade de paginas.......................: %i\n", lista_livro->qtd_paginas);
        fprintf(fp, "Quantidade de exemplares....................: %i\n", lista_livro->qtd_exem);
        fprintf(fp, "STATUS......................................: %i\n", lista_livro->status);
        fprintf(fp, "\n-------------------------------------------------------------\n");
        lista_livro = lista_livro->p_prox;
    }
    fclose(fp);
    printf("\n-------------------------------------------------------------\n");
    printf("ARQUIVO GERADO.");
    printf("\n-------------------------------------------------------------\n");
}
void exportar_relatorio_usuario_csv(dados_usuario *lista_usuario, string nome_arq)
{
    FILE *fp = fopen(nome_arq, "w");
    if(fp == NULL){
        printf("\n-------------------------------------------------------------\n");
        printf("NAO FOI POSSIVEL ABRIR O ARQUIVO.\n");
        printf("\n-------------------------------------------------------------\n");
    }

    while(lista_usuario) {
        fprintf(fp, "\n-------------------------------------------------------------\n");  
        fprintf(fp, "\n*RELATORIO DE USUARIOS*\n");
        fprintf(fp, "\n-------------------------------------------------------------\n");
        fprintf(fp, "Nome do usuario............................: %s\n", lista_usuario->nome);
        fprintf(fp, "Endereco do usuario....................... : %s\n", lista_usuario->endereco);
        fprintf(fp, "Email para contado.........................: %s\n", lista_usuario->email);
        fprintf(fp, "Telefone...................................: %s\n", lista_usuario->telefone);
        fprintf(fp, "Numero do cracha...........................: %i\n", lista_usuario->id);
        fprintf(fp, "STATUS.....................................: %i\n", lista_usuario->status);
        fprintf(fp, "\n-------------------------------------------------------------\n");
        lista_usuario = lista_usuario->p_prox;
    }
    fclose(fp);
    printf("\n-------------------------------------------------------------\n");
    printf("ARQUIVO GERADO");
    printf("\n-------------------------------------------------------------\n");
}
void exportar_relatorio_emprestimo_csv(dados_emprestimo *lista_emprestimo, string nome_arq)
{
    FILE *fp = fopen(nome_arq, "w");
    int i = 0; 

    if(fp == NULL){
        printf("\n-------------------------------------------------------------\n");
        printf("NAO FOI POSSIVEL ABRIR O ARQUIVO.\n");
        printf("\n-------------------------------------------------------------\n");
    }
    fprintf(fp, "\n-------------------------------------------------------------\n");  
    fprintf(fp, "\n*RELATORIO DE EMPRESTIMOS*\n");
    while(lista_emprestimo) {
        if(lista_emprestimo->qtd_emprestimo_usuario >= 1) {
            fprintf(fp, "\n-------------------------------------------------------------\n");
            fprintf(fp, "LIVRO EMPRESTADO\n");
            fprintf(fp, "Nome do usuario....................: %s\n", lista_emprestimo->usuario);
            fprintf(fp, "Titulo do livro....................: %s\n", lista_emprestimo->livro_1);
            if(lista_emprestimo->qtd_emprestimo_usuario == 2){
                fprintf(fp, "Titulo do livro....................: %s\n", lista_emprestimo->livro_2);
            }
            fprintf(fp, "Data de devolucao.................: %02i/%02i/%04i", lista_emprestimo->dia, lista_emprestimo->mes, lista_emprestimo->ano);
            fprintf(fp, "\n-------------------------------------------------------------\n");
            i++;
        }  
        lista_emprestimo = lista_emprestimo->p_prox;
    }
    fprintf(fp, "TOTAL DE LIVROS EMPRESTADOS................: %i", i);
    fprintf(fp, "\n-------------------------------------------------------------\n");

    fclose(fp);
    printf("\n-------------------------------------------------------------\n");
    printf("ARQUIVO GERADO");
    printf("\n-------------------------------------------------------------\n");
}
void exportar_relatorio_pendencia_csv(dados_emprestimo *lista_emprestimo, string nome_arq)
{
    FILE *fp = fopen(nome_arq, "w");
    int dia_atual, mes_atual, ano_atual;
    int resultado;
    int i = 0;
    
    if(fp == NULL){
        printf("\n-------------------------------------------------------------\n");
        printf("NAO FOI POSSIVEL ABRIR O ARQUIVO.\n");
        printf("\n-------------------------------------------------------------\n");
    }
    fprintf(fp, "\n-------------------------------------------------------------\n");  
    fprintf(fp, "\n*RELATORIO DE PENDENCIAS*\n");

    while(lista_emprestimo){
        gerar_data_atual(&dia_atual, &mes_atual, &ano_atual);
        resultado = comparar_datas(lista_emprestimo->dia, dia_atual);
        
        if(resultado == 0){
            fprintf(fp, "\n-------------------------------------------------------------\n");
            fprintf(fp, "LIVRO(S) QUE VENCEM HOJE.\n");
            if(lista_emprestimo->qtd_emprestimo_usuario >= 1) {
                fprintf(fp, "\n-------------------------------------------------------------\n");
                fprintf(fp, "LIVRO EMPRESTADO\n");
                fprintf(fp, "Nome do usuario....................: %s\n", lista_emprestimo->usuario);
                fprintf(fp, "Titulo do livro....................: %s\n", lista_emprestimo->livro_1);
            if(lista_emprestimo->qtd_emprestimo_usuario == 2){
                fprintf(fp, "Titulo do livro....................: %s\n", lista_emprestimo->livro_2);
            }
            fprintf(fp, "Data de devolucao.................: %02i/%02i/%04i", lista_emprestimo->dia, lista_emprestimo->mes, lista_emprestimo->ano);
            fprintf(fp, "\n-------------------------------------------------------------\n");
            }  
        }
        if(resultado == -1){
            fprintf(fp, "\n-------------------------------------------------------------\n");
            fprintf(fp, "LIVROS PENDENTES.\n");
            if(lista_emprestimo->qtd_emprestimo_usuario >= 1) {
                fprintf(fp, "\n-------------------------------------------------------------\n");
                fprintf(fp, "LIVRO EMPRESTADO\n");
                fprintf(fp, "Nome do usuario....................: %s\n", lista_emprestimo->usuario);
                fprintf(fp, "Titulo do livro....................: %s\n", lista_emprestimo->livro_1);
            if(lista_emprestimo->qtd_emprestimo_usuario == 2){
                fprintf(fp, "Titulo do livro....................: %s\n", lista_emprestimo->livro_2);
            }
            fprintf(fp, "Data de devolucao.................: %02i/%02i/%04i", lista_emprestimo->dia, lista_emprestimo->mes, lista_emprestimo->ano);
            fprintf(fp, "\n-------------------------------------------------------------\n");
            } 
            i++;
        }
        lista_emprestimo = lista_emprestimo->p_prox;
    }
    fprintf(fp, "TOTAL DE LIVROS PENDENTES................: %i", i);
    fprintf(fp, "\n-------------------------------------------------------------\n");

    fclose(fp);

    printf("\n-------------------------------------------------------------\n");
    printf("ARQUIVO GERADO");
    printf("\n-------------------------------------------------------------\n");
}
void exportar_relatorio_ano_publicaco_csv(dados_livro *lista_livro, string nome_arq, int inicial, int final)
{
    FILE *fp = fopen(nome_arq, "w");
    int i = 0;

    if(fp == NULL){
        printf("\n-------------------------------------------------------------\n");
        printf("NAO FOI POSSIVEL ABRIR O ARQUIVO.\n");
        printf("\n-------------------------------------------------------------\n");
    }
    fprintf(fp, "\n-------------------------------------------------------------\n");  
    fprintf(fp, "\n*RELATORIO DE ANO DE PUBLICACAO*\n");
    fprintf(fp, "DE %i ATE %i:\n", inicial, final);
    while(lista_livro) {
        if(lista_livro->ano_pub >= inicial && lista_livro->ano_pub <= final) {
            fprintf(fp, "\n-------------------------------------------------------------\n");
            fprintf(fp, "Titulo do livro.............................: %s\n", lista_livro->titulo);
            fprintf(fp, "Nome(s) do(s) autor(es).....................: %s\n", lista_livro->autor);
            fprintf(fp, "Nome da editora.............................: %s\n", lista_livro->editora);
            fprintf(fp, "Local de publicacao.........................: %s\n", lista_livro->local_pub);
            fprintf(fp, "Palavras chaves.............................: %s\n", lista_livro->palavra_chave);
            fprintf(fp, "Ano de publicacao...........................: %i\n", lista_livro->ano_pub);
            fprintf(fp, "Numero da edicao............................: %i\n", lista_livro->edicao);
            fprintf(fp, "Quantidade de paginas.......................: %i\n", lista_livro->qtd_paginas);
            fprintf(fp, "Quantidade de exemplares....................: %i\n", lista_livro->qtd_exem);
            fprintf(fp, "STATUS......................................: %i\n", lista_livro->status);
            fprintf(fp, "\n-------------------------------------------------------------\n");
            i++;
        }
        lista_livro = lista_livro->p_prox;
    }
    fprintf(fp, "\n-------------------------------------------------------------\n");
    fprintf(fp, "TOTAL DE LIVROS ENCONTRADOS..........................: %i\n", i);
    fprintf(fp, "\n-------------------------------------------------------------\n");
    
    fclose(fp);
    printf("\n-------------------------------------------------------------\n");
    printf("ARQUIVO GERADO.");
    printf("\n-------------------------------------------------------------\n");
}

//FORMATAÇÃO
void retirar_enter(string str)
{
    int tamanho;

    tamanho = strlen(str);

    str[tamanho - 1] = '\0';
}
void maiuscula(string str)
{
    int i;
    int tamanho;

    tamanho = strlen(str);

    for(i = 0; i < tamanho; i++){
        str[i] = toupper(str[i]);
    }
}
void formatacao(string str)
{
    retirar_enter(str);
    maiuscula(str);
}

//DATAS
int dias_no_mes(int mes, int ano)
{
    int dia[] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

    // Verifica ano bissexto para fevereiro
    if (mes == 2 && ((ano % 4 == 0 && ano % 100 != 0) || (ano % 400 == 0))) {
        return 29;
    }
    return dia[mes - 1];
}
void gerar_data_aleatoria(int *dia, int *mes, int *ano)
{   
    *ano = 2024;
    *mes = 12;
    *dia = rand() % dias_no_mes(*mes, *ano) + 1;
}
void gerar_data_atual(int *dia, int *mes, int *ano)
{
    time_t t = time(NULL);
    struct tm *data_atual = localtime(&t);

    *dia = data_atual->tm_mday;
    *mes = data_atual->tm_mon + 1;
    *ano = data_atual->tm_year + 1900;
}
int comparar_datas(int dia1, int dia2)
{
    if(dia1 > dia2) {
        return 1;
    }
    else if (dia1 == dia2) {
        return 0;
    }
    else {
        return -1;
    } 
}
