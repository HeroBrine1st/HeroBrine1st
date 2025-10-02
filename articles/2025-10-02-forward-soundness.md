# Forward soundness

Forward soundness (also called forward logic safety) is a technique I (independently) came up with to prevent *future* bugs in codebases by disallowing making inconsistent changes by delegating consistency checks to compiler. Generally, this includes *anything* that makes you, as a developer, go off the path to introduce a bug. This sounds, and works exactly like technical debt - but added in a strategic way.

Most straightforward ways to achieve it are:

- DRY - you can't introduce inconsistency if you can't desync the code[^1]
- Immutable data - you don't care if data you have is referenced as internal state in other module because you can't do anything with it.  
  Let's recall Java here. `java.lang.List` is mutable by default - which makes the language as a whole bad for forward soundness. There is `Collections.unmodifiableList`, which... throws an exception if you try to modify it. Which leads to another item:
- Type system that simply does not allow compiling faulty code. This is actually a backbone of forward soundness: everything is typed so that meaningless code does not compile. Examples:
  - Following previous item, compiler knows when data is immutable and, as such, disallows its mutation at compile time, instead of throwing an exception at runtime
  - Compiler can disallow converting an instance of e.g. `value class UserId(private val id: Int)` to `value class PostId(private val id: Int)` - which will immediately show you an error if you confuse your table primary keys
  - `DisposableEffect` in Jetpack Compose, which requires you to write `onDispose` hook, because it is the only way you can get required return value. It is also what makes it last statement in the effect, though you can store it in variable but this is what called to *go off the path*  
  Don't fall to "all or nothing" here! Anything can be messy as hell, just isolate it behind a contract and, optionally, cover with tests.
- Something about null safety is also encouraged. And of course strong static typing!
- Something that makes you throw no exceptions is encouraged too, because:
  - You don't know what exceptions will be thrown from a particular code
  - There's no way to make compiler warn you if you don't catch an exception. Checked exceptions? Looks like no one likes them  
  The reason is, exceptions are thrown when an application is in *exceptional state*, which is not expected. Is it expected for your application to have network issues? That's why you catch exception right there and transform it into a regular object.
- After you don't have exceptions, you introduce exceptions. Unexpected state? Log then throw, ideally crashing the whole application - smoke tests will quickly find it. So, asserts are also encouraged, and it makes `Collections.unmodifiableList` not that bad - just an assert you don't expect to exist, which still follows its rules. Yeah, this is last resort and largely intended for debugging, however there are cases when it is better to crash than do unexpected things.

<sup>Looks like I wrote it in order from most rewarding to least rewarding. Even better.</sup>

Following that, you won't make your software bugless, but each of the items wipes bugs by *whole classes*, because each adds limitations to your codebase, and, as such, removes "bug surface".

[^1]: There's also a good analogue that DRY works like 2NF, and SRP is 1NF then. Databases should be normalised - so why codebases should not?
