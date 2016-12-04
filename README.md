> ---
+ #title: "Caching the mean of a Vector"
+ #author: "Anees"
+ #date: "December 2, 2016"
+ #output: html_document
+ 

> ---
+ ## Caching the Inverse of a Matrix:
+ ## Matrix inversion is usually a costly computation and there may be some 
+ ## benefit to caching the inverse of a matrix rather than compute it repeatedly.
+ ## Below are a pair of functions that are used to create a special object that 
+ ## stores a matrix and caches its inverse.
+ 
+ ## This function creates a special "matrix" object that can cache its inverse.
+ 

> 
> makeCacheMatrix <- function(x = matrix()) {
+         inv <- NULL
+         set <- function(y) {
+                 x <<- y
+                 inv <<- NULL
+         }
+         get <- function() x
+         setInverse <- function(inverse) inv <<- inverse
+         getInverse <- function() inv
+         list(set = set,
+              get = get,
+              setInverse = setInverse,
+              getInverse = getInverse)
+ }
> 
> ## This function computes the inverse of the special "matrix" created by 
> ## makeCacheMatrix above. If the inverse has already been calculated (and the 
> ## matrix has not changed), then it should retrieve the inverse from the cache.
> 
> #source("ProgrammingAssignment2/cachematrix.R")
> my_matrix <- makeCacheMatrix(matrix(1:4, 2, 2))
> my_matrix$get()
     [,1] [,2]
[1,]    1    3
[2,]    2    4
> 
> my_matrix$getInverse()
NULL
> 
> cacheSolve(my_matrix)
     [,1] [,2]
[1,]   -2  1.5
[2,]    1 -0.5
> 
> cacheSolve(my_matrix)
getting cached data
     [,1] [,2]
[1,]   -2  1.5
[2,]    1 -0.5
> #getting cached data
> 
> my_matrix$getInverse()
     [,1] [,2]
[1,]   -2  1.5
[2,]    1 -0.5
> 
> my_matrix$set(matrix(c(2, 2, 1, 4), 2, 2))
> my_matrix$get()
     [,1] [,2]
[1,]    2    1
[2,]    2    4
> 
> my_matrix$getInverse()
NULL
> 
> cacheSolve(my_matrix)
           [,1]       [,2]
[1,]  0.6666667 -0.1666667
[2,] -0.3333333  0.3333333
> #getting cached data
> 
> cacheSolve(my_matrix)
getting cached data
           [,1]       [,2]
[1,]  0.6666667 -0.1666667
[2,] -0.3333333  0.3333333
> #getting cached data
> 
> my_matrix$getInverse()
           [,1]       [,2]
[1,]  0.6666667 -0.1666667
[2,] -0.3333333  0.3333333
> 
> setwd("~/Coursera")
> save.image("~/Coursera/Caching_the_Mean_of_a_Vector.html.RData")
> 
