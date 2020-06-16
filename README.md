Introduction
This assignment uses data from the UC Irvine Machine Learning Repository, a popular repository for machine learning datasets. In particular, we will be using the "Individual household electric power consumption Data Set" which I have made available on the course web site:

Loading the data
eda <- read.table("household_power_consumption.txt", header = TRUE, sep = ";", na.strings = "?")

eda$Date <- as.Date(eda$Date, format = "%d/%m/%Y")#convert date

#subset needed data 1st of Feb., 2007 to 2nd of Feb., 2007 eda1 <- subset(eda, Date >= as.Date("2007-2-1") & Date <= as.Date("2007-2-2"))

eda1 <- eda1[complete.cases(eda1),] #remove incomplete observations

datetime <- paste(eda1$Date, eda1$Time) #join date and time column

datetime <- setNames(datetime, "datetime") #name the new vector

eda1 <- subset(eda1, select = -c(Date, Time)) #remove Date and Time columns

eda1 <- cbind(datetime, eda1) #Add the new vector

eda1$datetime <- as.POSIXct(datetime) #Format datetime column

Making Plots
Plot 1
hist(eda1$Global_active_power, main = "GLobal Active Power", xlab = "GLobal Active Power (Kilowatts)", ylab = "Frequency", 
col = "red") 

dev.copy(png, "plot1.png", width = 480, height = 480) #copying the output 
dev.off() 
![Plot1.png](Images/Plot1.png) 

Plot 2
plot(eda1$Global_active_power ~ eda1$datetime, type = "l", xlab = "", ylab = "Global Active Power (Kilowatts)") 

dev.copy(png, "Plot2.png", width = 480, height = 480) #copying the output dev.off() 
![Plot2.png](Images/Plot2.png) 

Plot 3
with(eda1, { plot(Sub_metering_1datetime, type="l", xlab = "", ylab="Global Active Power (kilowatts)") 
lines(Sub_metering_2datetime,col='Red') 
lines(Sub_metering_3~datetime,col='Blue') }) 
legend("topright", col=c("black", "red", "blue"), 
legend = c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), lwd = 1, cex = 0.5)

dev.copy(png, file="Plot3.png", width = 480, height = 480) #copying the output 
dev.off() 
![Plot3.png](Images/Plot3.png)

Plot 4
par(mfrow=c(2,2), mar=c(4,4,2,2), oma=c(0,0,2,2)) with(eda1, { plot(Global_active_powerdatetime, type="l", xlab="", ylab="Global Active Power (kilowatts)") 
plot(Voltagedatetime, type="l", xlab="datetime", ylab="Voltage (volt)") plot(Sub_metering_1datetime, type="l", xlab="", ylab="Global Active Power (kilowatts)") 
lines(Sub_metering_2datetime,col='Red') 
lines(Sub_metering_3datetime,col='Blue') 
legend("topright", col=c("black", "red", "blue"), lty=1, lwd=2, bty="n", 
legend=c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3")) plot(Global_reactive_powerdatetime, type="l", xlab="datetime", ylab="Global Rective Power (kilowatts)") 
}) 

dev.copy(png, file="plot4.png", height=480, width=480) #copying the output 
dev.off() 
![Plot4.png](Images/Plot4.png)

©
