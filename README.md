#include <stdio.h>
#include <stdlib.h>

int main() {
    int a, b, r, q, c;

    // Demander a l'utilisateur de saisir les deux nombres
    printf("Donner a : ");
    scanf("%d", &a);

    printf("Donner b : ");
    scanf("%d", &b);

    // On garde les valeurs initiales
    int A = a, B = b;

    // Etape 1 : Calcul du PGCD avec l'algorithme d'Euclide
    printf("\n=== Etape 1 : Calcul du PGCD ===\n");
    while (b != 0) {
        q = a / b;
        r = a % b;
        printf("%d = %d * %d + %d\n", a, b, q, r);
        a = b;
        b = r;
    }

    int d = a; // PGCD
    printf("\nLe PGCD est : %d\n", d);

    // Verification si les deux nombres sont premiers entre eux
    if (d == 1) {
        printf("Les deux nombres sont premiers entre eux.\n");
    } else {
        printf("Les deux nombres ne sont pas premiers entre eux.\n");
    }

    // Etape 2 : Verification de l'existence de solutions
    printf("\nEntrez la valeur de c pour l'equation a*x + b*y = c : ");
    scanf("%d", &c);

    if (c % d != 0) {
        printf("Pas de solution entiere car %d ne divise pas %d.\n", d, c);
        return 0;
    }

    printf("Il existe au moins une solution entiere car %d divise %d.\n", d, c);

    // Etape 3 : Theoreme de Bezout (trouver x, y tels que A*x + B*y = d)
    printf("\n=== Etape 3 : Calcul des coefficients de Bezout ===\n");
    int aa = A, bb = B;
    int x0 = 1, y0 = 0; // coefficients initiaux
    int x1 = 0, y1 = 1;
    int temp;
    int step = 1;

    // Algorithme d'Euclide etendu
    while (bb != 0) {
        q = aa / bb;
        r = aa % bb;
        printf("Etape %d : %d = %d * %d + %d\n", step++, aa, bb, q, r);

        temp = x0 - q * x1;
        x0 = x1;
        x1 = temp;

        temp = y0 - q * y1;
        y0 = y1;
        y1 = temp;

        aa = bb;
        bb = r;
    }

    // A*x0 + B*y0 = d
    printf("\nSelon le theoreme de Bezout : %d * (%d) + %d * (%d) = %d\n", A, x0, B, y0, d);

    // Etape supplementaire : affichage du calcul du Bezout
    printf("\n=== Etape detaillee du calcul de Bezout ===\n");
    printf("On remonte les equations de l'algorithme d'Euclide :\n");
    printf("Exemple de forme : d = A*(x0) + B*(y0)\n");
    printf("Ici : %d = (%d)*(%d) + (%d)*(%d)\n", d, A, x0, B, y0);

    // Etape 4 : Calcul d'une solution particuliere
    int mult = c / d;
    int xp = x0 * mult;
    int yp = y0 * mult;

    printf("\nUne solution particuliere de %d*x + %d*y = %d est : (x0, y0) = (%d, %d)\n", A, B, c, xp, yp);

    // Etape 5 : Ecriture de la solution generale
    printf("\n=== Etape 5 : Solution generale ===\n");
    printf("x = %d + %d*k\n", xp, B / d);
    printf("y = %d - %d*k\n", yp, A / d);
    printf("ou k appartient a Z\n");

    return 0;
}
