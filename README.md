Orbit Async
============

Orbit Async implements async-await methods in java. It allows programmers to write asynchronous code in a sequential fashion.

If you're looking for async await on the .NET CLR, see [Asynchronous Programming with Async and Await](https://msdn.microsoft.com/en-us/library/hh191443.aspx).

License
=======
Orbit is licensed under the [BSD 3-Clause License](../LICENSE).

Simple Examples
=======
#### With Orbit Tasks
```java
@Async
public Task<Integer> getPageLength(URL url)
{
    Task<String> pageTask = getPage(url);

    // this will never block, it will return an promise
    String page = await(pageTask);

    return Task.fromValue(page.length());
}

Task<Integer> lenTask = getPageLength(new URL("http://example.com"));
System.out.println(lenTask.join());
    
```
#### With Java CompletableFuture
```java
import com.ea.orbit.async.Async;
import com.ea.orbit.async.Await;
import static com.ea.orbit.async.Await.await;

public class Page
{
    // has to be done at least once, usally in the main class.
    static { Await.init(); }

    @Async
    public CompletableFuture<Integer> getPageLength(URL url)
    {
        CompletableFuture<String> pageTask = getPage(url);
        String page = await(pageTask);
        return CompletableFuture.completedFuture(page.length());
    }
 }

CompletableFuture<Integer> lenTask = getPageLength(new URL("http://example.com"));
System.out.println(lenTask.join());

```

