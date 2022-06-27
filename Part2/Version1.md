### Vision of situation
My hypothesis is that this is not code for production, only to send one HTTP-request. So, we don't need code, only result of this request.

### Code review
1. If you want to send POST-request via file_get_contents, you should add third parameter, `$context`. You can find an example [here](https://stackoverflow.com/questions/2445276/how-to-post-data-in-php-using-file-get-contents). 
2. In previous example you can also see, that to send POST parameters in request body (for POST requests we have to send them in body), you have to add them into `$context`
3. One more good practice from that example: use function `http_build_query` to serialize your data to string. It made easier to check every parameter.
4. About parameters: you used different name and email. Are you sure it is ok?