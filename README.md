- 👋 Hi, I’m @Vshah32
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Vshah32/Vshah32 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
library(nycflights13)
library(tidyverse) 
#Q)1A
#Since the arr_delay variable is measured in minutes
filter(flights,arr_delay>=120)

#Q)1B
filter(flights, dest == "IAH" | dest == "HOU") 
#flights that flew to houston are those 
#flights destinatiON is either "IAH" OR "HOU"

#Q)1C
filter(flights, carrier=="DL"|carrier=="AA"|carrier=="UA")
#The carrier code for Delta is "DL", for American is "AA", and for United is "UA".
#Using these carriers codes, we check whether carrier is one of those.

#Q)1D
#The variable month has the month, and it is numeric. 
#So, the summer flights are those that departed in 
#months 7 (July), 8 (August), and 9 (September).

filter(flights, month>=7,month<=9)
#Q)1E
#Flights that arrived more than two hours late, 
#but didn’t leave late will have an arrival delay of more than 120 minutes 
#(arr_delay > 120) and a non-positive departure delay (dep_delay <= 0).
filter(flights, arr_delay >120,dep_delay<=0)

##Q)1F
#Were delayed by at least an hour, but made up over 30 minutes in flight.
# If a flight was delayed by at least an hour, then dep_delay >= 60.
# If the flight didn’t make up any time in the air, then its arrival would be delayed by the same amount as its departure,
# meaning dep_delay == arr_delay,
filter(flights, dep_delay >=60,dep_delay==arr_delay>30)

#Q)1G
#finding flights that departed between midnight and 6 a.m. 
#is complicated by the way in which times are represented in the data.
#In dep_time, midnight is represented by 2400, not 0. 
#You can verify this by checking the minimum and maximum of dep_time
summary(flights$dep_time)

filter(flights, dep_time <= 600 | dep_time == 2400)


#Q)2
#The flights will first be sorted by desc(is.na(dep_time)). 
#Since desc(is.na(dep_time)) is either TRUE when dep_time is missing, or FALSE, 

arrange(flights, desc(is.na(dep_time)), dep_time)

#Q3
#Find the most delayed flights by sorting the table by departure 
#delay, dep_delay, in descending order.
arrange(flights, desc(dep_delay))

#Q4)A
#Another definition of the “fastest flight” is the flight with the highest average ground speed. 
#The ground speed is not included in the data, 
#but it can be calculated from the distance and air_time of the flight.
#des-descending order
head(arrange(flights, desc(distance / air_time)))

# find the longest flight,
# sort the flights by the distance column in descending order.
arrange(flights, desc(distance))


#find the shortest flight
arrange(flights,distance)

#Q4)B
#The select() call ignores the duplication. 
#Any duplicated variables are only included once, in the first location they appear.
select(flights, year,year, month,month, day, year, year)



#Q)5A
#Case is disregarded by contains() by default. 
#it may be the reason it is the default.
select(flights, contains("TIME"))



#Q6)
library(nycflights13)
library(ggplot2)
library(dplyr)
library(ggmap)
flights_table <- table(flights$carrier)
flights_table
sorted_flights <- sort(flights_table, decreasing = TRUE)
names(sorted_flights)
ggplot(data = flights, mapping = aes(x = carrier)) +
  geom_bar() +
  scale_x_discrete(limits = names(sorted_flights))

data = flights  
# Plot the time_hour variable 

ggplot(data, aes(x=time_hour, y= arr_delay)) +
  geom_point()
