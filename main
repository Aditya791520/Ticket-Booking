#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

#define MOVIES 3
#define ROWS 5
#define COLS 6

typedef struct {
    int id;
    char name[20], time[10];
    float price;
    int seats[ROWS][COLS];
} Movie;

Movie movies[MOVIES] = {
    {1, "Avatar-2", "10:30AM", 250.0f, {{0}}},
    {2, "Oppenheimer", "02:30PM", 300.0f, {{0}}},
    {3, "Interstellar", "07:00PM", 280.0f, {{0}}}
};

void showMovies() {
    printf("\n=== Available Movies ===\n");
    for (int i = 0; i < MOVIES; i++)
        printf("%d. %-14s | %-8s | Rs. %.2f\n", movies[i].id, movies[i].name, movies[i].time, movies[i].price);
}

void showSeats(int mid) {
    printf("\n--- Screen This Way ---\n    ");
    for (int c = 1; c <= COLS; c++) printf("%d   ", c);
    printf("\n");
    for (int r = 0; r < ROWS; r++) {
        printf("%c  ", 'A' + r);
        for (int c = 0; c < COLS; c++) printf("[%c] ", movies[mid].seats[r][c] ? 'X' : ' ');
        printf("\n");
    }
    printf("[ ] = Available, [X] = Booked\n");
}

void bookTicket() {
    showMovies();
    int mid;
    printf("\nSelect Movie (1-3): ");
    if (scanf("%d", &mid) != 1 || mid < 1 || mid > MOVIES) return;
    mid--;
    showSeats(mid);

    char seat[5], name[30];
    printf("Enter Seat (e.g. A1): ");
    scanf("%4s", seat);
    int r = toupper(seat[0]) - 'A', c = seat[1] - '1';
    if (r < 0 || r >= ROWS || c < 0 || c >= COLS || movies[mid].seats[r][c]) {
        printf("Invalid or already booked seat!\n");
        return;
    }

    printf("Enter Customer Name: ");
    scanf("%29s", name);
    movies[mid].seats[r][c] = 1;
    seat[0] = toupper(seat[0]);

    FILE *fp = fopen("bookings.txt", "a");
    if (fp) {
        fprintf(fp, "%s %s %s %.2f\n", name, movies[mid].name, seat, movies[mid].price);
        fclose(fp);
    }
    printf("\n--- Ticket Confirmed ---\n");
    printf("Name: %s | Movie: %s | Seat: %s | Total: Rs. %.2f\n", name, movies[mid].name, seat, movies[mid].price);
}

void viewBookings() {
    FILE *fp = fopen("bookings.txt", "r");
    if (!fp) { printf("\nNo bookings found.\n"); return; }
    char name[30], movie[20], seat[5];
    float price;
    printf("\n=== All Bookings ===\n%-15s %-15s %-6s %-8s\n---------------------------------------------\n", "Name", "Movie", "Seat", "Price");
    while (fscanf(fp, "%s %s %s %f", name, movie, seat, &price) == 4)
        printf("%-15s %-15s %-6s Rs. %.2f\n", name, movie, seat, price);
    fclose(fp);
}

void cancelBooking() {
    char tName[30], tSeat[5], name[30], movie[20], seat[5];
    float price;
    int found = 0;
    printf("\nEnter Name: "); scanf("%29s", tName);
    printf("Enter Seat to cancel (e.g. A1): "); scanf("%4s", tSeat);
    tSeat[0] = toupper(tSeat[0]);

    FILE *fp = fopen("bookings.txt", "r");
    if (!fp) { printf("No bookings to cancel.\n"); return; }
    FILE *temp = fopen("temp.txt", "w");

    while (fscanf(fp, "%s %s %s %f", name, movie, seat, &price) == 4) {
        if (!found && strcmp(name, tName) == 0 && strcmp(seat, tSeat) == 0) {
            found = 1;
            int r = seat[0] - 'A', c = seat[1] - '1';
            for (int i = 0; i < MOVIES; i++)
                if (strcmp(movies[i].name, movie) == 0 && r >= 0 && r < ROWS && c >= 0 && c < COLS)
                    movies[i].seats[r][c] = 0;
        } else fprintf(temp, "%s %s %s %.2f\n", name, movie, seat, price);
    }
    fclose(fp); fclose(temp);
    remove("bookings.txt"); rename("temp.txt", "bookings.txt");
    printf(found ? "Booking cancelled successfully.\n" : "Booking not found.\n");
}

void loadBookings() {
    FILE *fp = fopen("bookings.txt", "r");
    if (!fp) return;
    char name[30], movie[20], seat[5];
    float price;
    while (fscanf(fp, "%s %s %s %f", name, movie, seat, &price) == 4) {
        int r = toupper(seat[0]) - 'A', c = seat[1] - '1';
        for (int i = 0; i < MOVIES; i++)
            if (strcmp(movies[i].name, movie) == 0 && r >= 0 && r < ROWS && c >= 0 && c < COLS)
                movies[i].seats[r][c] = 1;
    }
    fclose(fp);
}

int main() {
    loadBookings();
    int ch;
    while (1) {
        printf("\n============================\n MOVIE TICKET BOOKING SYSTEM\n============================\n");
        printf("1. View Movies\n2. View Seats\n3. Book Ticket\n4. View All Bookings\n5. Cancel Ticket\n6. Exit\nEnter choice: ");
        if (scanf("%d", &ch) != 1 || ch == 6) break;
        if (ch == 1) showMovies();
        else if (ch == 2) {
            showMovies();
            int m; printf("Select Movie (1-3): ");
            if (scanf("%d", &m) == 1 && m >= 1 && m <= MOVIES) showSeats(m - 1);
        }
        else if (ch == 3) bookTicket();
        else if (ch == 4) viewBookings();
        else if (ch == 5) cancelBooking();
        else printf("Invalid choice!\n");
    }
    return 0;
}
