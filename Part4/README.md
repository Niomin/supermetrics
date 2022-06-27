## Would you use a class/library provided by an external framework in your code, why or why not?

The first thought in my head: of course, I would. But, of course, here are some exceptions.
## Time
If implementation takes less than one day, probably I won't try to find some external realization. Just because research, comparison of existing solutions can take more time. However, if I already know some good libraries, I can use them.

## Requirements
Our application will change. We should be sure this library is flexible enough to satisfy our expected requirements. For example if we need some library to create .xlsx files, but we know that our clients like not only .xlsx, but also Google Sheets, and this library supports only Microsoft Excel format, maybe we should look for something else.

## Performance
Sometimes we need something small and simple, but famous libraries provide a lot of stuff, which can make them slower. E.g., I like Doctrine. It's a powerful and flexible tool to work with databases. But I'm not sure if it's a good idea to connect Doctrine to a small project, where we need a database only for two small queries.
Even if Doctrine is already attached, but we need to maximize performance in some script (especially if Doctrine has problems with this task, like updating with where condition), we can use PDO.

## Security
It's impossible to review every line of code in external libraries, the only way is to trust other developers. If we work with really sensitive data, we should be 100% sure that the library is secure. From the other side: if we're talking about cryptography, I prefer not to write any lines of my own code, because I understand that this topic is really complex, and I should trust specialists in cryptography.

## License
Library can be distributed under a license that doesn't allow commercial use.
