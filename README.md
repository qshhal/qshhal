- 👋 Hi, I’m @qshhal
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
qshhal/qshhal is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
#CODE FOR UBER DATA ANALYSIS
# Define CSV data as a string
csv_data <- "Date,Rides
2024-01-01 08:00:00,10
2024-01-01 09:00:00,15
2024-01-02 10:00:00,20
2024-01-02 11:00:00,25
2024-01-03 12:00:00,30
2024-01-03 13:00:00,35
2024-01-04 14:00:00,40
2024-01-04 15:00:00,45
2024-01-05 16:00:00,50
2024-01-05 17:00:00,55"

# Read CSV data
uber_data <- read.csv(text = csv_data)

# Check the structure of the data
str(uber_data)

# Summary statistics
summary(uber_data)

# Convert the date/time column to POSIXct format
uber_data$Date <- as.POSIXct(uber_data$Date, format = "%Y-%m-%d %H:%M:%S")

# Extract additional columns like day of the week, hour of the day, etc.
uber_data$DayOfWeek <- weekdays(uber_data$Date)
uber_data$HourOfDay <- as.integer(format(uber_data$Date, "%H"))

# Example analysis: Number of Uber trips by day of the week
trips_by_day <- aggregate(Rides ~ DayOfWeek, data = uber_data, FUN = length)

# Plotting the number of trips by day of the week
barplot(trips_by_day$Rides, names.arg = trips_by_day$DayOfWeek, 
        col = "skyblue", main = "Number of Uber Trips by Day of the Week",
        xlab = "Day of the Week", ylab = "Total Trips")

# Example analysis: Average number of trips by hour of the day
trips_by_hour <- aggregate(Rides ~ HourOfDay, data = uber_data, FUN = mean)

# Plotting the average number of trips by hour of the day
plot(trips_by_hour$HourOfDay, trips_by_hour$Rides, type = "l", 
     col = "red", main = "Average Number of Uber Trips by Hour of the Day",
     xlab = "Hour of the Day", ylab = "Average Trips")
