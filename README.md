# EEL-ACTIVITY-8
#include <stdio.h>
#include <string.h>

int isUpper(char c) {
    return (c >= 'A' && c <= 'Z');
}

int isLower(char c) {
    return (c >= 'a' && c <= 'z');
}

int isDigit(char c) {
    return (c >= '0' && c <= '9');
}

int isSpecial(char c) {
    return !isUpper(c) && !isLower(c) && !isDigit(c);
}

int stringCompare(char a[], char b[]) {
    int i = 0;
    while (a[i] != '\0' && b[i] != '\0') {
        if (a[i] != b[i])
            return 0;
        i++;
    }
    return (a[i] == '\0' && b[i] == '\0');
}

void removeNewline(char *s) {
    int i = 0;
    while (s[i] != '\0') {
        if (s[i] == '\n') {
            s[i] = '\0';
            break;
        }
        i++;
    }
}

int main() {
    char password[50];
    char correctPass[] = "Mahika@123";

    int hasUpper = 0, hasLower = 0, hasDigit = 0, hasSpecial = 0;

    printf("Enter your password: ");
    fgets(password, sizeof(password), stdin);

    removeNewline(password);

    if (strlen(password) < 8) {
        printf("Password too short! Must be at least 8 characters.\n");
        return 0;
    }

    for (int i = 0; i < strlen(password); i++) {
        char c = password[i];
        if (isUpper(c)) hasUpper = 1;
        if (isLower(c)) hasLower = 1;
        if (isDigit(c)) hasDigit = 1;
        if (isSpecial(c)) hasSpecial = 1;
    }

    if (!(hasUpper && hasLower && hasDigit && hasSpecial)) {
        printf("Weak password! Must contain:\n");
        printf(" - At least one uppercase letter\n");
        printf(" - At least one lowercase letter\n");
        printf(" - At least one digit\n");
        printf(" - At least one special character\n");
        return 0;
    }

    if (stringCompare(password, correctPass)) {
        printf("Login Successful! Strong password.\n");
    } else {
        printf("Password format is strong, but does not match the stored password.\n");
    }

    return 0;
}
