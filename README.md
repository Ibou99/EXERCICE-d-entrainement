#include <stdio.h>
#include <stdint.h>
#include <string.h>

// Fonction de chiffrement
void chiffrer(char *message, uint8_t cle, uint8_t *C)
{
    for (int i = 0; i < strlen(message); i++)
    {
        C[i] = (uint8_t)message[i] ^ cle;
    }
}

// Fonction de dechiffrement
void dechiffrer(uint8_t *C, uint8_t cle, char *L, int taille)
{
    for (int i = 0; i < taille; i++)
    {
        L[i] = C[i] ^ cle;
    }

    L[taille] = '\0';
}

int main()
{
    char message[100];
    char L[100];
    uint8_t C[100];
    unsigned int choix_cle = 6;
    uint8_t cle;

    // Saisie du message
    printf("Entrez un message : ");
    fgets(message, sizeof(message), stdin);

    // Suppression du retour a la ligne
    message[strcspn(message, "\n")] = '\0';

    // Saisie de la cle
    printf("Entrez une cle (0-255) : ");
    scanf("%u", &choix_cle);

    if (choix_cle > 255)
    {
        printf("Cle invalide !");
        return 1;
    }

    cle = (uint8_t)choix_cle;

    int taille = strlen(message);

    // Chiffrement
    chiffrer(message, cle, C);

    printf("\nMessage chiffre :\n");

    for (int i = 0; i < taille; i++)
    {
        printf("%u ", C[i]);
    }

    // Dechiffrement
    dechiffrer(C, cle, L, taille);

    printf("\n\nMessage dechiffre :\n");
    printf("%s\n", L);

    return 0;
}
