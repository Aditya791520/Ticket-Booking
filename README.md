[README.md](https://github.com/user-attachments/files/34238677/README.md)
# 🎬 Movie Ticket Booking System in C

A concise, basic **Movie Ticket Booking System** written in standard **C (C99 / ANSI C)**. Designed specifically for college projects, lab submissions, and viva presentations.

---

## ✨ Features

- **Movies List:** Displays available movies with showtimes and prices.
- **Visual Seating Grid:** Displays 5 rows (A-E) $\times$ 6 columns (1-6) with `[ ]` (Available) and `[X]` (Booked).
- **Seat Booking:** Enter seat code (e.g., `A1`, `B4`), customer name, and confirm booking.
- **File Persistence (`bookings.txt`):** Stores bookings permanently and reloads them on program start.
- **View All Bookings:** Displays table of booked tickets.
- **Cancel Ticket:** Cancels a booking by customer name and seat, and frees up the seat.

---

## 🚀 How to Run

### Method 1: Code::Blocks or Dev-C++
1. Open [`main.c`](file:///c:/Users/adity/OneDrive/Desktop/movie/main.c) in Code::Blocks or Dev-C++.
2. Press **F9** (Code::Blocks) or **F11** (Dev-C++) to compile and run.

### Method 2: GCC Terminal
```cmd
gcc main.c -o movie_booking.exe
.\movie_booking.exe
```

### Method 3: Online C Compiler
Copy the entire code from [`main.c`](file:///c:/Users/adity/OneDrive/Desktop/movie/main.c) into [OnlineGDB C Compiler](https://www.onlinegdb.com/online_c_compiler) and click **Run**.

---

## 📋 Menu Options

```text
============================
 MOVIE TICKET BOOKING SYSTEM
============================
1. View Movies
2. View Seats
3. Book Ticket
4. View All Bookings
5. Cancel Ticket
6. Exit
```
