# krishna-codes
#stopwatch using c
#include <stdio.h>
#include <time.h>
#include <stdlib.h>

void stopwatch() {
    clock_t start, end;
    double elapsed = 0.0;
    int running = 0; // 0: stopped, 1: running
    char command;

    printf("Simple Stopwatch\n");
    printf("Press 's' to start, 'e' to stop, 'r' to reset, 'q' to quit.\n");

    while (1) {
        command = getchar();  // Use getchar for cross-platform input handling
        if (command == 's' && !running) {
            start = clock();
            running = 1;
            printf("Stopwatch started.\n");
        } else if (command == 'e' && running) {
            end = clock();
            elapsed += (double)(end - start) / CLOCKS_PER_SEC;
            running = 0;
            printf("Stopwatch stopped. Elapsed time: %.2f seconds\n", elapsed);
        } else if (command == 'r') {
            elapsed = 0.0;
            running = 0;
            printf("Stopwatch reset.\n");
        } else if (command == 'q') {
            printf("Exiting stopwatch. Final time: %.2f seconds\n", elapsed);
            break;
        }

        if (running) {
            printf("Elapsed time: %.2f seconds\r", elapsed + (double)(clock() - start) / CLOCKS_PER_SEC);
            fflush(stdout); // Ensures real-time update
        }
    }
}

int main() {
    stopwatch();
    return 0;
}

