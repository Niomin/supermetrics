### Vision of situation
My hypothesis is that this is code for production, so we expect here something maintainable and readable.
In this case this is a little weird code review, because here should be rewritten everything. 
However, I will try to list the main problems that need to be solved. 

### Code review
1. You should use `%library from our company, probably Guzzle/Http%` to send HTTP-requests, code should be uniform, if everybody will write in their own style, it will make more complicated to interact with our software.  
2. You should create explicit interface: object on the input, object on the output. It can help to understand how to use your code. 
3. You shouldn't forget to process possible error codes. If API returns some error, our application shouldn't fall with server error.  
4. You should write some tests, it makes you sure that code works correctly, as you expected.