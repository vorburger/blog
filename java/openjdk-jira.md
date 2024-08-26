# OpenJDK JIRA

The JIRA instance of the OpenJDK at https://bugs.openjdk.org is "open" in the sense that many of its issues are publicly viewable.

In order to be able to create an account to file new issues, or comment on existing ones etc., one must however necessarily first already be an _author_ in the external OpenJDK project, see [this doc](https://openjdk.org/projects/#project-author) and [the bylaws](https://openjdk.org/bylaws#author). (There may also be some path through which one can start submitting something via https://bugreport.java.com/bugreport, and that then may or may not somehow end up over on https://bugs.openjdk.org; I've not further explored that.)

I guess that might makes sense, in that particular community's case. If I were able to have the privilege to create a new issue on that bug tracker, here is what one would be, coming from [enola-dev/enola#849](https://github.com/enola-dev/enola/issues/849):

* Type: Bug
* Priority: P3 or P4
* Summary: com.sun.net.httpserver.HttpServer should accept a custom ThreadFactory to create its HTTP-Dispatcher thread
* Description:

  The JDK's HttpServer internally creates its `"HTTP-Dispatcher"` named thread, in [the `start()` method of `ServerImpl`](https://github.com/openjdk/jdk21u-dev/blob/cd5ac19b4966741904314d42c6ee30ac1d9e0ca9/src/jdk.httpserver/share/classes/sun/net/httpserver/ServerImpl.java#L189). This makes it difficult to have one's registered custom `HttpHandler` "propagate" something stored in a "parent" `ThreadLocal` - even if setting a customer `Executor` - that won't work because however such an executor is implemented, it itself runs under said _"HTTP-Dispatcher"_ thread, which won't "see" a "parent" `ThreadLocal`.

  This issue suggests that `HttpServer` should accept a custom `ThreadFactory` to create its HTTP-Dispatcher thread, e.g. by adding a `create(InetSocketAddress addr, int backlog, ThreadFactory threadFactory)` method, in addition to the existing `create(InetSocketAddress addr, int backlog)` method on `HttpServer` (and then "piping it through", as required).

Perhaps someone will copy/paste this and create it on my behalf, as a sort of "sponsor."
