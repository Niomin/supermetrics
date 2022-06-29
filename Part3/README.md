1. We should decide what we will do with these bugs:
    1. ternary hell: lines 7-10 have implicit behaviour, `a ? b : c ? d : e` works like `(a ? b : c) ? d : e`, not `a ? b : (c ? d : e)`, and nested ternary expression are deprecated since PHP 7.4. If we're sure if exists `$_REQUEST['email']` we should use `$_REQUEST['masterEmail']`, we can keep this behaviour, but make it explicitly.  
    2. `'\n'` on line12 are just two symbols, `\` and `n`, not Newline. Maybe some of our clients got used to parsing our response, and it will break existing compatibility.
    3. SQL injection. I can't imagine a world, where this is a feature, but our product manager has to know that we are going to fix it.
    4. If `$_REQUEST['email']` is not provided in the request, it can cause the server error (or we hide these errors). Probably we should return the 400/404 HTTP-code.
    5. If user with a given email is not found, it also can cause a server error. As in previous suggestion, we should return the 404 HTTP code.
    6. Minor bug, probably it doesn't matter: if we send email `'0'`, system will decide we didn't send anything. I consider we should distinguish invalid data (like email `0`) and absence of data.
2. We should split the responsibilities. We can use this layers:
   1. Controller. Here we only create a DTO from the request (email+masterEmail)
   2. Fetcher. This service will call repository and return data from it. Also, here we can throw some exceptions (UserNotFound, InvalidEmail), maybe in future we will check some access. And, finally, we will call the mapper.
   4. Mapper. This service will map User to our ViewModel (this is useful, because different services can request different fields). 
   5. Repository/Query. I'm not sure whether I should explain why we need them :) Of course we will use binding (PDO, probably). 
   6. Templates. I'm also considering it's clear that we shouldn't mix logic and templates.
3. We should write some tests. Just to make sure that the code works. I know about TDD, also I understand, that if we have a huge legacy system, and we don't know how it works, we should create tests at first, but I'm not experienced in this enough, so code first, then tests.