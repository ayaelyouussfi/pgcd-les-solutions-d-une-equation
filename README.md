# pgcd-les-solutions-d-une-equation
programme c pour calculer le pgcd et solution d une equation

#include <stdio.h>

// Fonction pour calculer le PGCD de deux nombres (algorithme d'Euclide)

int pgcd(int a, int b) {

    while (b != 0) {
        int reste = a % b;
        a = b;
        b = reste;
    }
    return a;
}

// Algorithme d’Euclide étendu

int euclide_etendu(int a, int b, int *x, int *y) {
    if (b == 0) {
        *x = 1;
        *y = 0;
        return a;
    }

    int x1, y1;
    int d = euclide_etendu(b, a % b, &x1, &y1);

    *x = y1;
    *y = x1 - (a / b) * y1;

    return d;
}

int main() {

    int a, b, c;
    printf("=== Programme pour resoudre a*x + b*y = c ===\n\n");

    // 1. Lecture des valeurs
    
    printf("Entrer a : ");
    scanf("%d", &a);
    printf("Entrer b : ");
    scanf("%d", &b);
    printf("Entrer c : ");
    scanf("%d", &c);

    // 2. Calcul du PGCD et des coefficients
    
    int x0, y0;
    int d = euclide_etendu(a, b, &x0, &y0);

    printf("\nLe PGCD de (%d, %d) est : %d\n", a, b, d);

    // 3. Vérification de l'existence de solution
    
    if (c % d != 0) {
        printf("Pas de solution entiere car %d ne divise pas %d.\n", d, c);
        return 0;
    }

    // 4. Calcul d'une solution particulier
    
    int k = c / d;
    int xp = x0 * k;
    int yp = y0 * k;

    // 5. Affichage des résultats
    
    printf("\nil existe des solutions entieres !\n");
    printf("Solution particuliere : (x, y) = (%d, %d)\n", xp, yp);

    int alpha = b / d;
    int beta = -a / d;

    printf("Forme generale : (x, y) = (%d + %d*k, %d + %d*k), k appartient Z\n",
           xp, alpha, yp, beta);

    return 0;
}

