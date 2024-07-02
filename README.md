#include <stdio.h>
#include <string.h>

#define MAX_APPOINTMENTS 100

typedef struct {
    char patientName[50];
    char doctorName[50];
    char appointmentDate[20];
    char appointmentTime[10];
} Appointment;

Appointment appointments[MAX_APPOINTMENTS];
int appointmentCount = 0;

void addAppointment() {
    if (appointmentCount < MAX_APPOINTMENTS) {
        printf("Enter patient name: ");
        scanf("%s", appointments[appointmentCount].patientName);
        printf("Enter doctor name: ");
        scanf("%s", appointments[appointmentCount].doctorName);
        printf("Enter appointment date (YYYY-MM-DD): ");
        scanf("%s", appointments[appointmentCount].appointmentDate);
        printf("Enter appointment time (HH:MM): ");
        scanf("%s", appointments[appointmentCount].appointmentTime);
        
        appointmentCount++;
        printf("Appointment added successfully!\n");
    } else {
        printf("Appointment list is full!\n");
    }
}

void viewAppointments() {
    if (appointmentCount == 0) {
        printf("No appointments scheduled.\n");
    } else {
        for (int i = 0; i < appointmentCount; i++) {
            printf("Appointment %d:\n", i + 1);
            printf("  Patient Name: %s\n", appointments[i].patientName);
            printf("  Doctor Name: %s\n", appointments[i].doctorName);
            printf("  Date: %s\n", appointments[i].appointmentDate);
            printf("  Time: %s\n", appointments[i].appointmentTime);
        }
    }
}

void cancelAppointment() {
    int appointmentNumber;
    printf("Enter the appointment number to cancel: ");
    scanf("%d", &appointmentNumber);

    if (appointmentNumber < 1 || appointmentNumber > appointmentCount) {
        printf("Invalid appointment number.\n");
    } else {
        for (int i = appointmentNumber - 1; i < appointmentCount - 1; i++) {
            appointments[i] = appointments[i + 1];
        }
        appointmentCount--;
        printf("Appointment cancelled successfully!\n");
    }
}

int main() {
    int choice;

    while (1) {
        printf("\nDoctor Appointment System\n");
        printf("1. Add Appointment\n");
        printf("2. View Appointments\n");
        printf("3. Cancel Appointment\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addAppointment();
                break;
            case 2:
                viewAppointments();
                break;
            case 3:
                cancelAppointment();
                break;
            case 4:
                return 0;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
}
