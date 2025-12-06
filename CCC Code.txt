#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define CREDENTIAL_FILE "credentials.txt"
#define STUDENT_FILE "students.txt"

struct Student{
    int roll;
    char name[50];
    float marks;
}

int main(){
    if(loginSystem()){
        mainMenu();
    }
    else{
        printf("\nLogin Failed. Exiting...\n");
    }
    return 0;
}

int loginSystem(){
    char username[20],password[20];
    char fileUser[20],filePass[20],fileRole[10];
    printf("=============== Login Screen ==================\n");
    printf("Username : ");
    scanf("%s",username);
    printf("Password : ");
    scanf("%s",Password);
    FILE *fp = fopen(CREDENTIAL_FILE,"r");
    if(!fp){
        printf("Error : credentials.txt not found\n");
        return 0;
    }
    while (fscanf(fp, "%s %s %s", fileUser, filePass, fileRole) == 3) {
        if (strcmp(username, fileUser) == 0 && strcmp(password, filePass) == 0) {
            strcpy(currentRole, fileRole);
            strcpy(currentUser, fileUser);
            fclose(fp);
            return 1;
        }
    }

    fclose(fp);
    return 0;
}

void adminMenu() {
    int choice;

    do {
        printf("\n===== ADMIN MENU =====\n");
        printf("1. Add Student\n");
        printf("2. Display Students\n");
        printf("3. Search Student\n");
        printf("4. Update Student\n");
        printf("5. Delete Student\n");
        printf("6. Logout\n");
        printf("Enter choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: addStudent(); break;
            case 2: displays(); break;
            case 3: searchStudent(); break;
            case 4: updateStudent(); break;
            case 5: deleteStudent(); break;
            case 6: printf("Logging out...\n"); return;
            default: printf("Invalid choice!\n");
        }

    } while (1);
}

void addStudent() {
     File *fp = fopen(STUDENT_FILE, "a");
     struct Student st;

     if(!fp) {
          printf("Error opening file!\n");
          return;
}
     printf("Enter Roll Number: ");
     scanf("%d", &st.roll);
     printf("Enter Name: ");
     scanf("%s", st.name);
     printf("Enter Marks: ");
     scanf("%f", &st.marks);

     fprintf(fp, "%d %s %.2f\n", st.roll, st.name, st.marks);
     fclose(fp);
     printf("Student added successfully!\n");
}

void displayStudents() {
     FILE *fp = fopen(STUDENT_FILE, "r");
     struct Student st;

     if(!fp) {
          printf("Error opening file!\n");
          return;
     }
     printf("\n================= STUDENT RECORDS =================\n");
     printf("Roll\tName\tMarks\n");
     while(fscanf(fp, "%d %s %f", &st.roll, st.name, &st.marks) == 3) {
          printf("%d\t%s\t%.2f\n", st.roll, st.name, st.marks);
     }
     fclose(fp);
}  

void searchStudent() {
     int roll, found = 0;
     struct Student st;
     FILE *fp = fopen(STUDENT_FILE, "r");

     if(!fp) {
          printf("Error opening file!\n");
          return;
     }
     printf("Enter Roll Number to search: ");
     scanf("%d", &roll);

     while(fscanf(fp, "%d %s %f", &st.roll, st.name, &st.marks) == 3) {
          if(st.roll == roll) {
               printf("Record Found: Roll: %d, Name: %s, Marks: %.2f\n", st.roll, st.name, st.marks);
               found = 1;
               break;
          }
     }
     if(!found) {
          printf("Record with Roll Number %d not found.\n", roll);
     }
     fclose(fp);
}

