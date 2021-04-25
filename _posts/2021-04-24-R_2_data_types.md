---
layout: post
title: "R(2), Data Types"
description: "R"
categories: [R]
tags: [R]
redirect_from:
  - /2021/04/24/
---

There are many types of objects, but the most commonly used are: Vectors, Lists, Matrices, Arrays, Factors, and Data Frames.

## Types of Atom Vector

1. logical: TRUE, FALSE
2. numeric: 12.3, 5, 999
3. **integer**: 2L, 34L, 0L
4. complex: 3+2i
5. character: 'a', "good", "TRUE", '23.4'
6. **raw**: "Hello"被存储为48 65 6c 6c 6f
7. ...

## Vectors

```R
# Create a vector.
apple <- c('red','green',"yellow")
```

## Lists

```R
# Create a list.
list1 <- list(c(2,5,3),21.3,sin)
```

## Matrices

```R
# Create a matrix.
M = matrix( c('a','a','b','c','b','a'), nrow = 2, ncol = 3, byrow = TRUE)
print(M)
```

results:

		[,1] [,2] [,3]
	[1,] "a"  "a"  "b" 
	[2,] "c"  "b"  "a"

## Arrays

Although Matrices are limited to TWO dimensions, the arrays can have any number of dimensions.

```R
# Create an array.
a <- array(c('green','yellow'),dim = c(3,3,2))
print(a)
```

results:

	, , 1

		[,1]     [,2]     [,3]    
	[1,] "green"  "yellow" "green" 
	[2,] "yellow" "green"  "yellow"
	[3,] "green"  "yellow" "green" 

	, , 2

		[,1]     [,2]     [,3]    
	[1,] "yellow" "green"  "yellow"
	[2,] "green"  "yellow" "green" 
	[3,] "yellow" "green"  "yellow" 

## Factors

Factors are R Objects built by using vectors. It stores the different values of elements between vectors as tags. Tags are always characters, no matter the type of them are numerical, logical or other types.

* the function we used is `factor()`;
* the function `nlevels()` count the number of distinct values

```R
# Create a vector.
apple_colors <- c('green','green','yellow','red','red','red','green')

# Create a factor object.
factor_apple <- factor(apple_colors)

# Print the factor.
print(factor_apple)
print(nlevels(factor_apple))
```

results:

	[1] green  green  yellow  red   red   red   green 
	Levels: green red yellow
	# applying the nlevels function we can know the number of distinct values
	[1] 3

## Data Frames

A data frame is a table data object. Different from the matrix in the data frame, each column can contain different data patterns. It's a list of vectors of equal length.

We use function `data.frame()` to create data frames.

```R
# Create the data frame.
BMI <- 	data.frame(
   gender = c("Male", "Male","Female"), 
   height = c(152, 171.5, 165), 
   weight = c(81,93, 78),
   Age = c(42,38,26)
)
print(BMI)
```

result:

	  gender height weight Age
	1   Male  152.0     81  42
	2   Male  171.5     93  38
	3 Female  165.0     78  26
