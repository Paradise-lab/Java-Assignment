**DESCRIPTION**

This is a program that helps a bicycle rental company to determine the amount of money the customers will pay.
The shop will consider the start time to use the bicycle and the return time of the bicycle.

**Program Description**
The shop owner will enter two whole numbers:
1. The starting hour of rental
2. The ending hour of the rental

   **Rules to guide the rent**
   
   1. Only whole numbers are accepted
   2. The starting hour should be less than the ending hour
   3. The rent duration should not exceed an day
       Starting hour = 0-23
       Ending hour = 1-24

Rates per hour
HOUR                                           RATE
0hr-7hr and 21hr-24hr                         500RWF
7hr-14hr and 19hr-21hr                        1000RWF
19hr-21hr                                     1500RWF

**How it works**

1.The program shows the rates and the instructions.
2.It reads the starting and ending hours. If either is not a whole number, it stops with an error message.
3.It checks the rules (valid ranges and start < end). If a rule is broken, it stops with an error message.
4.A for loop runs once for each hour of the rental. In each pass, h is the hour that starts at h:
    1.If h < 7 or h >= 21, the rate is 500 RWF.
    2.Otherwise, if h < 14 or h >= 19, the rate is 1000 RWF.
    3. Otherwise, the rate is 1500 RWF.
5.Each hour is counted and its price is added to the total.
6.The program prints a breakdown and the total fee.

**Concepts Used**
1.Variables and data types: int for hours, counters and the total
2.Operators: arithmetic (+, -, *), comparison (<, >=), logical (||, !), and shortcut operators (+=, ++)
3.Decision control statements: if, else if, else
4.Repetition statements: for loop
5.Input and output: Scanner, System.out.println
