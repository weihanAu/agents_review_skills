## step1 looking for sytax error and naming issues (medium)
   error examples:  
   varianble called x, data2,user1,etc..
   variable called userIDs rather than UserIdList.
## step2 coding principal errors: (critical)
   error example:  
   looking for repeated code, against DIY principal.  
   looking for magic numbers, error like a random 86400 without any comments, rathen a named constant, seconds_in_a_day.    
   looking for over-sized functions, one function should do 1 things, single responsibility principal.  
   looking for dead code: like unreachable branches, unused import, commented-out days ago.  
   looking for abstraction boundaries error: error like business logic called database, error like UI does http calls.

## step3 logic and correctness (critical)
- ### **off by one errors：**
   error example:  
   the loops runs from zero to n where it should run from zero to n-1.  
   it uses less-than-or-equal-to when it should use less-than.

- ### **wrong comparision operators：**
  error example:  
   < sign where it should be >.  
   = where it should be !=.  

- ### **Incorrect Return Values：**
  error example:  
  function getTotlePrice return itemList.  

- ### **DATA type issues**
  error example:  
  compare string to a number.  
  compare object using reference when it wants value equality.  
  INTEGER overflow in a long calculation.  

- ### **State mutation bugs**
  error example:  
  function supposed to return a new list, but it quietly mutates the input instead.  

- ### **null handling**
  alway think 'what happends when return is null?'  

## step4 edge cases and errors handling (critical)

- ### edge cases
  walk through the code imaging the nastiest possible inputs: empty input? empty array? empty string? a Null Object.  
  single elements input. boundarys fail at size one more than ppl think.  
  huge inputs, does memory blow up?  
  special values. negative numbers. zero. very large numbers, unicode, timezone.  

- ### error handling
  External call fails: is the exception called? is the log has enough context to debug later? does the whole request just silently die?  
  Swallowed exceptions: has an empty catch block? a catch-all doing nothing? they hide bugs, make debug impossible.  

- ### retry logic   
  is there a backoff? is the operation indempotent(like you dont want charge customer twice)?

- ### Resource cleanup
  are file handle closed? are database connections returnd to the pool?




## step5 furthermore thinking as a senior level (recommand us)
 this part is a thinkg part, give your recommond is enough.
  - ### issues on concurrency,Concurrency is where the hard bugs live
       is there any shared state being accessed without lock?  
       any race conditions? (like stock only has one, but userA and userB buy it at the same time).  
       is there a check-and-pattern really atomic?  
  - ### Security
       does user's input got sanitized? 
       SQL injection?  
       secrect hardcoded?  
  - ### performance
       database query n+1 inside a loop?  
       a whole database table loaded into a memory?  
  - ### observability
       if it fails at 3am, how we know it?  
       error being tracked? trace? opentelemetry?  
  - ### testability
       it has tests? follow tdd?  
       hard dependencies, global state, static calls, all of these make test very hard.  