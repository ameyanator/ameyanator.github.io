---
layout:     post
title:      Sieve of Eratosthenes
date:       2018-11-05 03:03:03
author:     Ameya Sinha
summary:    Explanation of the Sieve of Eratosthenes
categories: Algorithms
thumbnail:  heart
tags:
 - Algorithms
 - Prime Numbers
 - Sieve
---

The Sieve of Eratosthenes has been forever famously been used to calculate and store Prime Numbers. This article is an explanation of how to do so.

__What’s a prime number?__: A number that is **only** divisible by itself and 1.

Traditional Method of checking whether a number (n) is prime or not is by iterating through all the numbers from 2 to (n-1) and if we find that a particular number (x) in between divides the number then we say that the number is not a prime. This particular check takes O(n) {linear time as you need to check each number in between}.
Suppose you need to generate all the primes up to a given integer say N then you’ll spend O(N) time to iterate through the loop and to check whether each number (n) in between is prime or not you’ll have to spend O(n) time for each element.

Thus the total time is O(N^2). Much too expensive!!

So we improve this solution by using the Sieve of Eratosthenes

**Basic Logic of Sieve**:  
We start from 2 and proceed further for all numbers under n. For each number that we hit (which is 2 initially we strike of all it’s further multiples as they cannot be prime 4,6..). All the numbers that we haven’t stuck out at the end of this procedure will be prime. So basically this is how we proceed.  
If a number has already been struck out I won’t write it again. You’ll see why later! 😉 be with me.

*Conclude 2 is prime. 4,6,8,10….are not.  
Conclude 3 is prime. 9,15,21…are not.(6,12,18 were already struck out because of 2).  
Conclude 5 is prime 25,35….are not.  
Continue this process till we have only prime numbers left under n.*

Now as to why we didn’t write the numbers that were already struck out- If you observe that the first multiple of each prime number that is yet to be struck out is the square of the number. We”ll use this in our code :). You can also mathematically prove this. Conversely we’ll also only strike out multiples of numbers that are under sqrt(n) as the ones larger than it will be the prime numbers left which have no multiples under n.

**Coding Part**  
**Input:** n-the number under which we need to print all the prime numbers.  
**Output:** all the prime numbers under n  
**Logic:** All even numbers except 2 are not prime. So we iterate on all odd numbers from 3 to the max value (msz) and check to see if we have seen multiples of this before. If we have not it is a prime number and we strike out further multiples of it. If we have then its not a prime number and we move on ahead.  
At the end we store all the primes in a vector

```
const int msz=2e4+1;
vector<int> seen(msz);
vector<int> primes;

void shieve()
{
	for(int i=3;i*i<=msz;i+=2)
	{
		if(!seen[i])
		{
			for(int j=i*2;j<=msz;j+=i)
			{
				seen[j]=1;
			}
		}
	}
	primes.push_back(2);
	for(int i=3;i<=msz;i+=2)
	{
		if(!seen[i]) primes.push_back(i);
	}
}
```

The time complexity of the Sieve of Eratosthenes is O(n(logn)(loglogn))
