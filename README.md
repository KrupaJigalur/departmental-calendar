# departmental-calendar
a simple use departmental calendar as a practice project to strengthen C fundamentals
#include<stdio.h>
#include<string.h>
#include<time.h>
struct Event {
int day;
int month;
char name[100];
};
// Function to print any month calendar
void printMonth(char name[], int daysInMonth, int startDay) {
printf("\n------ %s 2026 ------\n", name);
printf("Mon Tue Wed Thu Fri Sat Sun\n");
for(int i = 1; i < startDay; i++) {
printf(" ");
}
int currentDay = startDay;
for(int date = 1; date <= daysInMonth; date++) {
printf("%3d ", date);
currentDay++;
if(currentDay > 7) {
printf("\n");
currentDay = 1;
}
}
printf("\n");
}
// -------- NOTIFICATION FUNCTION --------
void checkNotifications(struct Event events[], int eventCount) {
time_t t = time(NULL);
struct tm today = *localtime(&t);

int d = today.tm_mday;
int m = today.tm_mon + 1; // tm_mon is 0–11
printf("\n----- NOTIFICATIONS -----\n");
int found = 0;
for(int i = 0; i < eventCount; i++) {
if(events[i].day == d && events[i].month == m) {
printf("🔔 TODAY (%02d/%02d): %s\n", d, m, events[i].name);
found = 1;
}
}
if(!found)
printf("No events today.\n");
}
int main()
{
struct Event events[100];
int eventCount = 12;
// ---- DEFAULT EVENTS ----
events[0] = (struct Event){5, 1, "Orientation Day"};
events[1] = (struct Event){12, 1, "C Programming Workshop"};
events[2] = (struct Event){26, 1, "Republic Day Celebration"};
events[3] = (struct Event){14, 2, "Tech Seminar: AI & Robotics"};
events[4] = (struct Event){8, 3, "Women’s Day Cultural Event"};
events[5] = (struct Event){10, 4, "Mid-Semester Exams Begin"};
events[6] = (struct Event){1, 5, "Maharashtra Day (Holiday)"};
events[7] = (struct Event){15, 7, "Freshers’ Welcome Event"};
events[8] = (struct Event){28, 8, "Project Exhibition Day"};
events[9] = (struct Event){5, 9, "Teachers’ Day Celebration"};
events[10] = (struct Event){20, 10, "Sports Day"};
events[11] = (struct Event){18, 12, "End-Semester Exams Begin"};
int op = 0;
while(op != 5)

{
// ---- SHOW NOTIFICATIONS Every Time ----
checkNotifications(events, eventCount);
printf("\n============================\n");
printf(" COLLEGE CALENDAR\n");
printf("============================\n");
printf("1. Print Calendar\n");
printf("2. Show All Events\n");
printf("3. Show Events by Month\n");
printf("4. Add Event\n");
printf("5. Exit\n");
printf("Enter your choice: ");
scanf("%d", &op);
getchar();
switch(op)
{
case 1: {
int month;
printf("\nEnter month number (1-12): ");
scanf("%d", &month);
switch(month) {
case 1: printMonth("January", 31, 4); break;
case 2: printMonth("February", 28, 7); break;
case 3: printMonth("March", 31, 3); break;
case 4: printMonth("April", 30, 7); break;
case 5: printMonth("May", 31, 3); break;
case 6: printMonth("June", 30, 6); break;
case 7: printMonth("July", 31, 1); break;
case 8: printMonth("August", 31, 4); break;
case 9: printMonth("September", 30, 6); break;
case 10: printMonth("October", 31, 2); break;
case 11: printMonth("November", 30, 4); break;
case 12: printMonth("December", 31, 6); break;
default: printf("Invalid month!\n");
}
break;
}

case 2:
printf("\n------ College Events 2026 ------\n");
for(int i = 0; i < eventCount; i++) {
printf("%02d/%02d - %s\n",
events[i].day,
events[i].month,
events[i].name);
}
break;
case 3: {
int m, found = 0;
printf("Enter month number (1-12): ");
scanf("%d", &m);
printf("\nEvents in month %d:\n", m);
for(int i = 0; i < eventCount; i++) {
if(events[i].month == m) {
printf("%02d/%02d - %s\n",
events[i].day, events[i].month, events[i].name);
found = 1;
}
}
if(!found) printf("No events this month.\n");
break;
}
case 4: {
struct Event newEvent;
printf("Enter day: ");
scanf("%d", &newEvent.day);
printf("Enter month: ");
scanf("%d", &newEvent.month);
getchar();

// ------ VALIDATION ------
// Invalid month
if(newEvent.month < 1 || newEvent.month > 12) {
printf("❌ Invalid month! Must be between 1 and 12.\n");
break;
}
// Days allowed in each month
int monthDays[] = {0,31,28,31,30,31,30,31,31,30,31,30,31};
// Invalid day
if(newEvent.day < 1 || newEvent.day > monthDays[newEvent.month]) {
printf("❌ Invalid day for this month!\n");
printf("Month %d has only %d days.\n",
newEvent.month, monthDays[newEvent.month]);
break;
}
printf("Enter event name: ");
fgets(newEvent.name, 100, stdin);
newEvent.name[strcspn(newEvent.name, "\n")] = '\0';
// Add to array
events[eventCount++] = newEvent;
printf("\n✔ Event Added Successfully!\n");
break;
}
case 5:
printf("Exiting... Goodbye!\n");
break;
default:
printf("Invalid choice.\n");
}
}
return 0;

}
