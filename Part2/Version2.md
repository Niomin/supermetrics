### Vision of situation
My hypothesis is that this is production code, so we expect here something maintainable and readable.
In this case this is a little weird code review, because here should be rewritten literally everything. 
However, I will try to list the main problems that need to be solved. 

### Code review
1. You should use `%library from our company, probably Guzzle/Http%` to send HTTP-requests, code should be uniform, if everybody will write in their own style, it will make more complicated to interact with our software.  
2. You should create an explicit interface: input object, output object. It can help to understand how to use your code. 
3. You shouldn't forget to process possible error codes. If API returns some error, our application shouldn't fail with a server error.  
4. You should write some tests to be sure that code works correctly, as you expected.