#include <stdio.h>

#define MAX_PROCESSES 10
#define MAX_RESOURCES 10

int available[MAX_RESOURCES];
int max[MAX_PROCESSES][MAX_RESOURCES];
int allocation[MAX_PROCESSES][MAX_RESOURCES];
int need[MAX_PROCESSES][MAX_RESOURCES];
int num_processes, num_resources;

void input() {
    printf("Enter the number of processes: ");
    scanf("%d", &num_processes);

    printf("Enter the number of resources: ");
    scanf("%d", &num_resources);

    printf("Enter the available resources: ");
    for (int i = 0; i < num_resources; i++)
        scanf("%d", &available[i]);

    printf("Enter the Max resource matrix:\n");
    for (int i = 0; i < num_processes; i++)
        for (int j = 0; j < num_resources; j++)
            scanf("%d", &max[i][j]);

    printf("Enter the Allocation matrix:\n");
    for (int i = 0; i < num_processes; i++)
        for (int j = 0; j < num_resources; j++) {
            scanf("%d", &allocation[i][j]);
            need[i][j] = max[i][j] - allocation[i][j]; // Calculate Need matrix
        }
}

int is_safe() {
    int work[MAX_RESOURCES], finish[MAX_PROCESSES] = {0}, safe_seq[MAX_PROCESSES];
    for (int i = 0; i < num_resources; i++)
        work[i] = available[i];

    int count = 0;
    while (count < num_processes) {
        int found = 0;
        for (int i = 0; i < num_processes; i++) {
            if (!finish[i]) {
                int j;
                for (j = 0; j < num_resources; j++)
                    if (need[i][j] > work[j])
                        break;

                if (j == num_resources) { // If all needed resources are available
                    for (int k = 0; k < num_resources; k++)
                        work[k] += allocation[i][k];

                    safe_seq[count++] = i;
                    finish[i] = 1;
                    found = 1;
                }
            }
        }
        if (!found) {
            printf("System is in an unsafe state.\n");
            return 0;
        }
    }

    printf("System is in a safe state.\nSafe sequence: ");
    for (int i = 0; i < num_processes; i++)
        printf("%d ", safe_seq[i]);
    printf("\n");

    return 1;
}

int main() {
    input();
    is_safe();
    return 0;
}
