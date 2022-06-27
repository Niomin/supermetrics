1. We should decide what we will do with these bugs:
    1. ternary hell: lines 7-10 have implicit behaviour, `a ? b : c ? d : e` works like `(a ? b : c) ? d : e`, not `a ? b : (c ? d : e)`, and nested ternary expression are deprecated since PHP 7.4. If we're sure if exists `$_REQUEST['email']` we should use `$_REQUEST['masterEmail']`, we can save this behaviour explicit.  
    2. `'\n'` on line12 is just two symbols, `\` and `n`, not Newline. Maybe some of our clients got used to parse our answer, and it will break existing compatibility.
    3. SQL injection. I can't imagine world, where this is a feature, but our product manager have to know that we are going to fix it.
    4. If key `email` is not provided in the request, we can fall with server error (or we hide these errors). Probably we should return 400/404 HTTP-code.
    5. If user with given email will not be found, we also can fall with server error. As in previous suggestion, we should return 404 HTTP code.
    6. Minor bug, probably it doesn't matter: if we send email `'0'`, system will decide we didn't send anything. I consider we should distinguish invalid data (like email `0`) and absence of data.
2. We should split responsibilities. We can use this layers:
   1. Controller. Here we only create DTO from request (email+masterEmail)
   2. Fetcher. This service will call repository and return data from it. Also, here we can throw some exceptions (UserNotFound, InvalidEmail), maybe in future we will check some access. And here we will call mapper.
   4. Mapper. This service will map User to our ViewModel (this is useful, because in different services can request different fields). 
   5. Repository/Query. I'm not sure whether I should explain why we need them :) Of course we will use binding (PDO, probably). 
   6. Templates. I'm also consider it's clear that we shouldn't mix logic and templates.
3. We should write some tests. Just to be sure that code works. I know about TDD, also I understand, that if we have huge legacy system, and we don't know how it works, we should create tests at first, but I don't have this experience, so code first, then tests.