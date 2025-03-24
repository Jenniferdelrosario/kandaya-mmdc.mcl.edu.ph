/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */

package com.mycompany.timecalculation;

// Import
import java.text.DateFormat;
import java.text.DecimalFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.time.LocalDate;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;
import java.util.Date;
import java.util.Scanner;


/**
 *
 * @Jennifer Del Rosario 
 */
public class TimeCalculation {

    public static void main(String[] args) {
        
        Scanner timeScanner = new Scanner(System.in);
        //Time
        int hours = 0;
        int minutes = 0;
        DateTimeFormatter timeFmt1 = DateTimeFormatter.ofPattern("HH:MM");
        DateTimeFormatter timeFmt2 = DateTimeFormatter.ofPattern("HH");
        
        //Time-in
        System.out.println("Time-in: ");
        LocalTime timeIn = LocalTime.parse(timeScanner.nextLine(), timeFmt1);
        
        //Time-out
        System.out.println("Time-out: ");
        LocalTime timeOut = LocalTime.parse(timeScanner.nextLine(), timeFmt1);
        
        //Total No. of Hours
        int hoursWorked = timeOut.getHour() - timeIn.getHour();
        int minWorked = timeOut.getMinute() - timeIn.getMinute();    
        
        //Rounded
            int roundedTime = hoursWorked;
            if (minWorked > 0){
                roundedTime++;
            }
        
        //Salary
        DecimalFormat df = new DecimalFormat ("##,##0.00");
        
        double hourlyRate = 200;
        double minuteRate = hourlyRate/60;
        double dailySalary = (hourlyRate * hoursWorked) + (minuteRate * minWorked);
        
        
        System.out.println("Total Time: " + hoursWorked + " hours and " + minWorked + " minutes");
        System.out.println("Estimated No. of Hours: " + roundedTime + " hours");
        System.out.println("Rate per Minute: " + df.format(minuteRate) + " per minute");
        System.out.println("Hourly Rate: " + df.format(hourlyRate) + " per hour");
        System.out.println("Daily Salary: " + df.format(dailySalary));
        
        timeScanner.close();
        
    }
}

