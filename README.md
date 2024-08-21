# Projeto-algoritmo- main()
{
int soma = 1;
int tamanho = 0;
int resultado;

int soma_array(int array[], int tamanho) {
    int soma = 0;
    for (int i = 0; i < tamanho; i++) {
        soma += array[i];
    }
    return soma;
}

int main() {
    int n;

    printf("Digite o tamanho do array: ");
    scanf("%d", &n);

    int array[n];

    printf("Digite os %d números inteiros:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &array[i]);
    }

    int resultado = soma_array(array, n);

    printf("A soma dos elementos do array é: %d\n", resultado);

    return 0;
}

  
}






// questa 02

#include <stdio.h>


void multiplica_matrizes(int n, int mat1[][n], int mat2[][n], int resultado[][n]) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            resultado[i][j] = 0;
            for (int k = 0; k < n; k++) {
                resultado[i][j] += mat1[i][k] * mat2[k][j];
            }
        }
    }
}

int main() {
    int n = 2; 

    int mat1[2][2] = {
        {1, 2},
        {3, 4}
    };

    int mat2[2][2] = {
        {5, 6},
        {7, 8}
    };

    int resultado[2][2];

    multiplica_matrizes(n, mat1, mat2, resultado);

    printf("A matriz resultante da multiplicação é:\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("%d ", resultado[i][j]);
        }
        printf("\n");
    }

    return 0;
}





// Questa 03


#include <stdio.h>
#include <cs50.h> 
int numero_de_digitos(long numero) {
    int contagem = 0;
    while (numero > 0) {
        numero /= 10;
        contagem++;
    }
    return contagem;
}

bool e_valido(long numero) {
    int soma = 0;
    bool dobrar = false;

    while (numero > 0) {
        int digito = numero % 10;
        numero /= 10;

        if (dobrar) {
            digito *= 2;
            if (digito > 9) {
                digito -= 9;
            }
        }
        soma += digito;
        dobrar = !dobrar;
    }
    return (soma % 10 == 0);
}

void determinar_tipo(long numero) {
    int digitos = numero_de_digitos(numero);
    
    if (digitos == 15 && (numero / 10000000000000 == 34 || numero / 10000000000000 == 37)) {
        printf("AMEX\n");
    }
    else if (digitos == 16 && (numero / 1000000000000000 == 51 || numero / 1000000000000000 == 52 ||
                               numero / 1000000000000000 == 53 || numero / 1000000000000000 == 54 ||
                               numero / 1000000000000000 == 55)) {
        printf("MASTERCARD\n");
    }
    else if ((digitos == 13 || digitos == 16) && (numero / 1000000000000 == 4 || numero / 1000000000000000 == 4)) {
        printf("VISA\n");
    }
    else {
        printf("INVALID\n");
    }
}

int main() {
    long numero = get_long("Número do cartão de crédito: ");

    if (e_valido(numero)) {
        determinar_tipo(numero);
    } else {
        printf("INVALID\n");
    }

    return 0;
}





//Questao04

#include <stdio.h>

int main() {
    int troco = 68;
    int moedas = 0;

    moedas += troco / 25;
    troco %= 25;

    moedas += troco / 10;
    troco %= 10;

    moedas += troco / 5;
    troco %= 5;

    moedas += troco;

    printf("%d\n", moedas);

    return 0;
}






//Questao 05

#include <stdio.h>
#include <ctype.h>
#include <string.h>

int calcular_pontuacao(const char *palavra) {
    int pontuacao = 0;
    int valores[26] = {1, 3, 3, 2, 1, 4, 2, 4, 1, 8, 5, 1, 3, 1, 1, 3, 10, 1, 1, 1, 1, 4, 4, 8, 4, 10};
    
    for (int i = 0; palavra[i] != '\0'; i++) {
        char letra = toupper(palavra[i]);
        if (letra >= 'A' && letra <= 'Z') {
            pontuacao += valores[letra - 'A'];
        }
    }
    
    return pontuacao;
}

int main() {
    char palavra1[100], palavra2[100];
    
    printf("Jogador 1, insira sua palavra: ");
    fgets(palavra1, sizeof(palavra1), stdin);
    palavra1[strcspn(palavra1, "\n")] = '\0'; 
    
    printf("Jogador 2, insira sua palavra: ");
    fgets(palavra2, sizeof(palavra2), stdin);
    palavra2[strcspn(palavra2, "\n")] = '\0'; 
    
    int pontuacao1 = calcular_pontuacao(palavra1);
    int pontuacao2 = calcular_pontuacao(palavra2);
    
    if (pontuacao1 > pontuacao2) {
        printf("Jogador 1 venceu!\n");
    } else if (pontuacao2 > pontuacao1) {
        printf("Jogador 2 venceu!\n");
    } else {
        printf("Empate!\n");
    }
    
    return 0;
}







//Questao 06

#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <string.h>

int is_valid_key(const char *key) {
    if (strlen(key) != 26) {
        return 0; 
    }

    int freq[26] = {0}; 

    for (int i = 0; i < 26; i++) {
        if (!isalpha(key[i])) {
            return 0; 
        }

        char c = toupper(key[i]);
        if (freq[c - 'A'] > 0) {
            return 0; 
        }
        freq[c - 'A']++;
    }
    return 1;
}

int main(int argc, char *argv[]) {
    if (argc != 2) {
        printf("Usage: %s key\n", argv[0]);
        return 1;
    }

    if (!is_valid_key(argv[1])) {
        printf("Invalid key\n");
        return 1;
    }

    char key[26];
    for (int i = 0; i < 26; i++) {
        key[i] = toupper(argv[1][i]);
    }

    char map[26];
    for (int i = 0; i < 26; i++) {
        map[i] = key[i];
    }

    printf("Plaintext: ");
    char plaintext[1000]; 
    if (fgets(plaintext, sizeof(plaintext), stdin) == NULL) {
        printf("Error reading input\n");
        return 1;
    }

    size_t len = strlen(plaintext);
    if (len > 0 && plaintext[len - 1] == '\n') {
        plaintext[len - 1] = '\0';
    }

    printf("Ciphertext: ");
    for (size_t i = 0; i < strlen(plaintext); i++) {
        char c = plaintext[i];
        if (isalpha(c)) {
            char base = isupper(c) ? 'A' : 'a';
            printf("%c", toupper(map[c - base]));
        } else {
            printf("%c", c);
        }
    }
    printf("\n");

    return 0;
}





//Questao07

#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <string.h>

int is_digit_string(const char *str) {
    for (int i = 0; str[i] != '\0'; i++) {
        if (!isdigit(str[i])) {
            return 0;
        }
    }
    return 1;
}

int main(int argc, char *argv[]) {
    if (argc != 2) {
        printf("Usage: %s key\n", argv[0]);
        return 1;
    }

    if (!is_digit_string(argv[1])) {
        printf("Usage: %s key\n", argv[0]);
        return 1;
    }

    int key = atoi(argv[1]);

    printf("Plaintext: ");
    char plaintext[1000];
    if (fgets(plaintext, sizeof(plaintext), stdin) == NULL) {
        printf("Error reading input\n");
        return 1;
    }

    size_t len = strlen(plaintext);
    if (len > 0 && plaintext[len - 1] == '\n') {
        plaintext[len - 1] = '\0';
    }

    printf("Ciphertext: ");
    for (size_t i = 0; i < strlen(plaintext); i++) {
        char c = plaintext[i];
        if (isalpha(c)) {
            char base = isupper(c) ? 'A' : 'a';
            printf("%c", (c - base + key) % 26 + base);
        } else {
            printf("%c", c);
        }
    }
    printf("\n");

    return 0;
}




//Questão 08


#include <stdio.h>
#include <math.h>

int main() {
    double dados[][3] = {
        {8, 10, 20},
        {1, 10, 100},
        {10, 3, 100},
        {0, 0, 0}
    };
    
    double comprimento, largura, percentual;
    
    for (int i = 0; dados[i][0] != 0 || dados[i][1] != 0 || dados[i][2] != 0; i++) {
        comprimento = dados[i][0];
        largura = dados[i][1];
        percentual = dados[i][2];
        
        double area_casa = comprimento * largura;
        double area_terreno = (area_casa * 100) / percentual;
        double lado_terreno = sqrt(area_terreno);
        
        printf("Dados: %.2lf %.2lf %.2lf\n", comprimento, largura, percentual);
        printf("Tamanho mínimo do terreno necessário é: %.2lf metros\n\n", lado_terreno);
    }
    
    return 0;
}





//Questão 09

#include <stdio.h>
#include <string.h>

const char* determinar_resultado(const char* sheldon, const char* raj) {
    if (strcmp(sheldon, raj) == 0) {
        return "De novo!";
    }
    
    if ((strcmp(sheldon, "tesoura") == 0 && (strcmp(raj, "papel") == 0 || strcmp(raj, "lagarto") == 0)) ||
        (strcmp(sheldon, "papel") == 0 && (strcmp(raj, "pedra") == 0 || strcmp(raj, "spock") == 0)) ||
        (strcmp(sheldon, "pedra") == 0 && (strcmp(raj, "lagarto") == 0 || strcmp(raj, "tesoura") == 0)) ||
        (strcmp(sheldon, "lagarto") == 0 && (strcmp(raj, "papel") == 0 || strcmp(raj, "spock") == 0)) ||
        (strcmp(sheldon, "spock") == 0 && (strcmp(raj, "tesoura") == 0 || strcmp(raj, "pedra") == 0))) {
        return "Bazinga!";
    }
    
    return "Raj trapaceou!";
}

int main() {
    int T;
    scanf("%d", &T);
    
    for (int t = 1; t <= T; t++) {
        char sheldon[20], raj[20];
        scanf("%s %s", sheldon, raj);
        
        const char* resultado = determinar_resultado(sheldon, raj);
        
        printf("Caso #%d: %s\n", t, resultado);
    }
    
    return 0;
}



