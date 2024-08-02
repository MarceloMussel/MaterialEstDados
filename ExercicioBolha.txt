#include <iostream>

using namespace std;

const int TAM = 20;

void Bolha(int vet[], int *comp, int *troca){
    int i, j, aux;
    for(i = 0; i < TAM; i++){
        for(j = 0; j < TAM-1; j++){
            (*comp)++;
            if(vet[j] > vet[j+1]){
                (*troca)++;
                aux = vet[j];
                vet[j] = vet[j+1];
                vet[j+1] = aux;
            }
        }
    }
}
void BolhaMelhorado(int vet[], int *comp, int *trocas){
    int i = 1, j, aux;
    bool troca = true;
    while((i <= TAM) && (troca)){
        troca = false;
        for(j = 0; j < TAM-1; j++){
            (*comp)++;
            if(vet[j] > vet[j+1]){
                (*trocas)++;
                troca = true;
                aux = vet[j];
                vet[j] = vet[j+1];
                vet[j+1] = aux;
            }
        }
        i++;
    }
}
void geraVetor(int v1[], int v2[]){
    for(int i = 0; i < TAM; i++){
        v1[i] = rand() % 100 + 1;
        v2[i] = v1[i];
    }
}

int main()
{
    srand(time(NULL));
    int v1[TAM], v2[TAM], compBolha, trocasBolha, comBmelhor, trocaBmelhor;
    int k, m, somaCompBolha = 0, somaTrocaBolha = 0, somaCompBmelhor = 0, somaTrocaBmelhor = 0;
    for(k = 1; k <= 10; k++){
        geraVetor(v1, v2);
        cout << "Rodada " << k << ": vetor original: ";
        for(m = 0; m < TAM; m++)
            cout << v1[m] << " ";
        compBolha = 0;
        trocasBolha = 0;
        Bolha(v1, &compBolha, &trocasBolha);
        cout << "Ordenado pelo Bolha: ";
        for(m = 0; m < TAM; m++)
            cout << v1[m] << " ";
        cout << endl << "Comparações: " << compBolha << " | Trocas: " << trocasBolha << endl;
        somaCompBolha += compBolha;
        somaTrocaBolha += trocasBolha;
        comBmelhor = 0;
        trocaBmelhor = 0;
        BolhaMelhorado(v2, &comBmelhor, &trocaBmelhor);
        cout << "\nOrdenado pelo Bolha melhorado: ";
        for(m = 0; m < TAM; m++)
            cout << v2[m] << " ";
        cout << endl << "Comparações: " << comBmelhor << " | Trocas: " << trocaBmelhor << endl;
        somaCompBmelhor += comBmelhor;
        somaTrocaBmelhor += trocaBmelhor;
    }
    somaCompBolha /= 10;
    somaTrocaBolha /= 10;
    somaCompBmelhor /= 10;
    somaTrocaBmelhor /= 10;
    cout << "Bolha: Media comparações: " << somaCompBolha << " trocas: " << somaTrocaBolha << endl;
    cout << "BolhaM: Media comparações: " << somaCompBmelhor << " trocas: " << somaTrocaBmelhor << endl;


    return 0;
}

