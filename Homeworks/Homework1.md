---
title: "Lab1Homework"
author: "Savita Sastry"
date: "Winter 2020"
output: 
  html_document: 
    keep_md: yes
---




```r
5 - 3 * 2
```

```
## [1] -1
```


```r
8 / 2 ** 2
```

```
## [1] 2
```

```r
#From the results of this calculation looks like * refers to multiplication and ** refers to exponentiation.
```


```r
#Write two programs that calculate each expression such that the result for the first example is 4 and the second example is 16.

(7-6)*3 + 1**2
```

```
## [1] 4
```

```r
(40/(2*5))**2
```

```
## [1] 16
```


```r
pi <- 3.14159265359
#Is pi an integer or numeric? Why? Show your code.
class(pi)
```

```
## [1] "numeric"
```

```r
#Results from the above show that pi is a numeric, which makes sense because the object is not a whole number
```


```r
#Here are your winnings and losses this week. Note that you don’t gamble on the weekends!
blackjack <- c(140, -20, 70, -120, 240, NA, NA)
roulette <- c(60, 50, 120, -300, 10, NA, NA)
days <- c('Mon','Tues', 'Wed', 'Thus', 'Fri', 'Sat', 'Sun')
names(blackjack) <- days
names(roulette) <- days

# Calculate how much you won or lost in blackjack over the week.

sum(blackjack, na.rm = TRUE)
```

```
## [1] 310
```

```r
#since NA is not numeric, it needs to be disregarded for the sum calculation, indicated by na.rm = TRUE

# Calculate how much you won or lost in roulette over the week.

sum(roulette, na.rm = TRUE)
```

```
## [1] -60
```

```r
# Build a total_week vector to show how much you lost or won on each day over the week. Which days seem lucky or unlucky for you?

total_week <- c(blackjack + roulette)
total_week
```

```
##  Mon Tues  Wed Thus  Fri  Sat  Sun 
##  200   30  190 -420  250   NA   NA
```

```r
#Monday, Tuesday, Wednesday, and Friday are lucky days because the gains are positive whereas Thursday is an unlucky day because the gains are negative. 

# Should you stick to blackjack or roulette? Write a program that verifies this below.

if (sum(blackjack, na.rm = TRUE)>sum(roulette, na.rm = TRUE)) { 
  print("Stick to blackjack")
  } else {
  print("stick to roulette")
}
```

```
## [1] "Stick to blackjack"
```

