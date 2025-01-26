# MOVIE-TICKET-BOOKING-SYSTEM
#include <stdio.h>
#include <string.h>
#include <ctype.h>

void under() {
    for (int i = 0; i < 26; i++) {
        printf("-----+");
    }
    printf("\n\n");
}

void payment() {
    printf("Enter UPI ID: ");
    char a[50];
    scanf("%s", a);
    printf("Amount will be deducted from your account.\n");
    printf("PAYMENT SUCCESSFUL\n");
}

void movie() {
    FILE *mov = fopen("movie.txt", "r");
    if (mov == NULL) {
        printf("Error opening movie file.\n");
        return;
    }
    char movie[100];
    while (fgets(movie, 100, mov)) {
        printf("%s", movie);
    }
    printf("\n");
    fclose(mov);
}

void book() {
    movie();
    char c[20];
    printf("Enter movie: ");
    scanf("%s", c);
    printf("The entered movie is %s\n", c);
    printf("Enter '1' to confirm: ");
    int ab;
    scanf("%d", &ab);
    if (ab == 1) {
        payment();
        printf("Movie \"%s\" has been successfully booked\n\n", strupr(c));
        under();
    } else {
        return;
    }
}

void cancel() {
    movie();
    char c[20];
    printf("Enter movie which has to be cancelled: ");
    scanf("%s", c);
    printf("Enter '1' to confirm: ");
    int ab;
    scanf("%d", &ab);
    if (ab == 1) {
        printf("Movie \"%s\" has been successfully cancelled\nAmount paid will be refunded\n\n", strupr(c));
        under();
    } else {
        return;
    }
}

void regis(int x) {
    FILE *reg = fopen("user.txt", "a");
    if (reg == NULL) {
        printf("Error opening user file.\n");
        return;
    }
    struct structure {
        char name[50];
        char u_name[50];
        char pass_wd[50];
    } temp;
    printf("Name: ");
    scanf("%s", temp.name);
    printf("User Name: ");
    scanf("%s", temp.u_name);
    printf("Password: ");
    scanf("%s", temp.pass_wd);
    fprintf(reg, "%s %s %s\n", temp.name, temp.u_name, temp.pass_wd);
    fclose(reg);
    printf("!! Registration successful !!\n\n");
    under();
    while (1) {
        printf("1. Book Ticket\n2. Cancel Ticket\n3. Log Out\n");
        int ch;
        printf("Enter your choice: ");
        scanf("%d", &ch);
        printf("\n");
        if (ch == 1) {
            book();
        } else if (ch == 2) {
            cancel();
        } else if (ch == 3) {
            printf("Logged out\n\n");
            under();
            return;
        } else {
            printf("Invalid input\n\n");
        }
    }
}

int main() {
    while (1) {
        printf("1. Registration\n");
        printf("2. Exit\n");
        int ch;
        printf("Enter your choice: ");
        scanf("%d", &ch);
        printf("\n");
        if (ch == 1) {
            regis(ch);
        } else if (ch == 2) {
            printf("Thank you\n");
            break;
        } else {
            printf("Invalid choice\n\n");
        }
    }
    return 0;
}
