# Desafio-free-fire-
Desafio FreeFire 
#include <stdio.h>
#include <string.h>

#define MAX_ITENS 10

typedef struct {
    char nome[50];
    char tipo[30];
    int quantidade;
} Item;

Item mochila[MAX_ITENS];
int totalItens = 0;

void limparBuffer() {
    int c;
    while ((c = getchar()) != '\n' && c != EOF);
}

void adicionarItem() {
    if (totalItens >= MAX_ITENS) {
        printf("\nERRO: A mochila esta cheia! Nao e possivel adicionar mais itens.\n");
        return;
    }

    printf("\n--- Adicionar Novo Item ---\n");
    printf("Nome do item: ");
    scanf(" %[^\n]", mochila[totalItens].nome);
    limparBuffer();

    printf("Tipo do item (ex: Arma, Municao, Cura): ");
    scanf(" %[^\n]", mochila[totalItens].tipo);
    limparBuffer();

    printf("Quantidade: ");
    scanf("%d", &mochila[totalItens].quantidade);
    limparBuffer();

    totalItens++;
    printf("\nItem '%s' adicionado com sucesso!\n", mochila[totalItens-1].nome);
}

void removerItem() {
    if (totalItens == 0) {
        printf("\nA mochila esta vazia. Nao ha itens para remover.\n");
        return;
    }

    char nomeParaRemover[50];
    printf("\nDigite o nome do item que deseja remover: ");
    scanf(" %[^\n]", nomeParaRemover);
    limparBuffer();

    int indiceEncontrado = -1;
    for (int i = 0; i < totalItens; i++) {
        if (strcmp(mochila[i].nome, nomeParaRemover) == 0) {
            indiceEncontrado = i;
            break;
        }
    }

    if (indiceEncontrado != -1) {
        for (int i = indiceEncontrado; i < totalItens - 1; i++) {
            mochila[i] = mochila[i + 1];
        }
        totalItens--;
        printf("\nItem '%s' removido com sucesso!\n", nomeParaRemover);
    } else {
        printf("\nERRO: Item '%s' nao encontrado na mochila.\n", nomeParaRemover);
    }
}

void listarItens() {
    if (totalItens == 0) {
        printf("\nA mochila esta vazia.\n");
        return;
    }

    printf("\n------------------- ITENS NA MOCHILA -------------------\n");
    printf("| %-20s | %-15s | %-10s |\n", "NOME", "TIPO", "QUANTIDADE");
    printf("----------------------------------------------------------\n");
    for (int i = 0; i < totalItens; i++) {
        printf("| %-20s | %-15s | %-10d |\n", mochila[i].nome, mochila[i].tipo, mochila[i].quantidade);
    }
    printf("----------------------------------------------------------\n");
}

int main() {
    int opcao;

    do {
        printf("\n--- Mochila de Sobrevivencia (Nivel Novato) ---\n");
        printf("1. Adicionar item\n");
        printf("2. Remover item\n");
        printf("3. Listar itens\n");
        printf("0. Sair da ilha\n");
        printf("Escolha sua acao: ");
        
        scanf("%d", &opcao);
        limparBuffer();

        switch (opcao) {
            case 1:
                adicionarItem();
                break;
            case 2:
                removerItem();
                break;
            case 3:
                listarItens();
                break;
            case 0:
                printf("\nSaindo do sistema... Ate a proxima, sobrevivente!\n");
                break;
            default:
                printf("\nOpcao invalida! Tente novamente.\n");
        }

    } while (opcao != 0);

    return 0;
}
