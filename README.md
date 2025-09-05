👋 Hi, I’m @HeroBrine1st, a random-time enthusiast developer.

I'm generally interested in cybersecurity and in self-hosting solutions that allow people to regain their control back (even if partially, like [spotify-dumper](https://github.com/HeroBrine1st/spotify-dumper)). My favourite language is Kotlin due to its great expressiveness combined with easibility of enforcing forward soundness[^1], together with the best UI library I ever used - Jetpack Compose.

[^1]: Forward soundness (also called forward logic safety) is a technique I (independently) came up with to prevent bugs in codebases by declaring and strictly enforcing data flow paths and contracts, using compiler typing engine where possible and falling back to asserts to prevent unnoticed undefined behaviors, which also allows for performance optimisations. This way, no complex code is exposed to unknown state. This technique requires language (or at least linter) support, which is what makes it "forward" (you need to fight compiler before introducing a bug). A primitive example is  `value class UserId(private val value: Int)` which is a way to prevent bugs like [this](https://github.com/tortoise/tortoise-orm/issues/1791), where id of wrong table was used most probably due to duck-typing (that's python though but you get the idea).  
The term is not fully verbally formed (because that's one of my skills I gained over time in an automatic way), so this definition may be silly. Also this may already be popularly used but I did not find it. Anyway that's how most of my bugs are visible in code immediately.

I'm on my slow way to provide the world with good software, where slow is because I like solving actual unsolved problems more than simply developing in the sake of development - and that's why you won't ever see me writing another notes, calendar or TODO application, unless there's oddly specific feature noone implements. For example, spotify-dumper has ability to run without any human interaction and was actually used for automatic "backups" of all my playlists.

<details>
  <summary>My personal advice for anyone who wants to learn software development with reasoning behind it, also being the background behind my skills</summary>
  
  It is split into two simple halves. First is: 
  
  ### Find the thing you are lacking and start developing it
  
  If you don't use your software, you won't do enough effort, because you will lose interest and the remaining "20% of code that take 80% of time" are only subject to your willpower. I think this is why most beginner projects are left in incomplete state - they are satisfied the interest and as such aren't needed anymore. This won't prevent incomplete projects[^2], but will drastically reduce the number of them. And if you use an "incomplete" project and there's no reason to do changes, is it really incomplete? It is most probably complete up to your expectations from it, so as long as you use it you can start second project, even go back-and-forth between the projects if they are both "complete" but occasionally you need yet another feature. A simple maintenance of a project is good too, and actually is a separate skill (especially if your project becomes popular but I don't recommend expecting that, do the software for yourself and people like you will find it themselves (though you can post on e.g. r/opensource but don't do it too early)).

  [^2]: Take [trixnity-bridge](https://github.com/HeroBrine1st/trixnity-bridge) as an example - I'm good with it in current state, so no reason to update it beyound maintenance:-( But I'm going to eventually return to that project

  Finding that "thing" is hard. It is hard even for me, and not because I have developed everything I need[^3], but because almost (almost!) everything is already developed. So, this advice has never worked for anyone I gave it. But that's the way I reached my level, and anyone following that should too. I think the reason behind that is because between learning new skill and pressing "Buy" in Play Market most people choose the latter. I don't judge them, but that's the habit that can interfere with search (and if removed, possibly transform into saved money, so it may seem like you already *earn* with your skills). In my case I additionally have self-hosting and privacy requirements and as such many paid alternatives are simply blocked for me - which is good because that's the stimuli that keeps me in shape.

  [^3]: The number of projects I have developed, use and that can be used by someone else (to exclude my NixOS flake, very niche CLI utilities etc) is probably less than 5

  When you learn for your own direct benefit - not for future employers - you empower your reinforcement learning with direct (very short) positive feedback loop, and leave yourself in dependency of your own skills, which will prevent you from abandoning the project. I can't say that employers are definitely encouraging it - but I can say that they benefit from such way of learning more, simply because you don't go "roadmap" way and get focused experience, but have a real, broad, possibly enterprise-level experience that is simply not backed by money. What's the difference? Only less responsibility, meaning you don't use e.g. monitoring systems in your pet projects and don't fortify your software like I do[^1] (and I do monitoring too) but that's because I went full self-hosted, so the level of responsibility is comparable.

  This also has two side effects: you will create better software, knowing the use cases; and you will likely have your own code style and your own favourite technologies (including testing ones) that limit you not to do serious bugs, because you use the project - you need to prevent bugs after all. And *practically* understanding that each pattern, library and framework is not about empowering but *limiting* yourself is the most impactful step of learning IMO.
  
  ### Learn to *read* code, not only write it
  
  ..of course after/if you are basically experienced. This applies experienced developers too.

  Reading code is more than half of your work, and, as such, your **core skill**, which includes reading documentation to fetch the info required for understanding code. By learning that, you will break free from the meme problems like "can't understand code that I wrote three months ago". And that's not the only effect, there are side effects:

  - You won't suffer from "why this doesn't work" in many simple cases. I have been asked to help finding the bug while it was a simple flaw in logic, easily spot if you understand your code not only via a mindmap.
  - You will have better agentic capabilities because you aren't thinking "if it works it works" or "don't touch it if it works"[^4], you are thinking "why it works?". Repeatedly thinking, each time you understand the code. Eventually you will dig deep into knowing how computer, OS and networks work, will know the backstages behind your everyday actions (like synced documents are not magically available on each device), and the sky is the limit.

  [^4]: A terrible statement in the age of version control systems, you even have `git bisect` if something goes wrong. I only understand it in corporate environments but simply because refactoring is time, and time is money. You save on refactoring - you get technical debt, and that's a positive feedback loop so no surprise.

  And the sweet-sweet part:

  - You will likely have no problems with onboarding into new codebases
  - You will likely have no problems with learning new languages! Furthermore, learning new languages will not feel like *learning*, it will deeply connect new language to all previously known languages. So you simply keep the reference documentation somewhere near and, knowing what you can do with known languages, simply look for the same thing. Or, in the age of LLMs, ask an LLM for alternative, but I recommend checking its response with documentation[^5]. Anyway it would be far faster because not only you can write the code in your language and ask the LLM to transpile it into other language, but also read the documentation and examples with full understanding, unwinding it into a graph of knowledge deeply linked with abilities of other languages.

[^5]: I use LLM as (additional) search engine in most cases (and try to limit its usage to last resorts), and if you think of it like that, it will lose the magic and will look as yet another tool in your collection like previous search engines were.

  Here's the funny thing: I have learned lua to start some small scripts only by reading code, having poor JavaScript experience as background, back in 2016. That was my second language, and both languages were likely learned (or, at least, bootstrapped) without reading official documentation because I simply didn't knew about such thing.

  Also, to fully understand this advice, you need to know two things:

  - This is an advice to become a developer like me. I do the software because I need it. Do not confuse it with "I do the software because I'm getting paid for that". That's not inherently a bad thing (they can be combined, each benefits from other), simply not what this advice is for. In short, don't expect a job in 1 month.
  - I started programming as a kid, simply seeing cool mobile minecraft mods (they were scripts back then) and having some free tutorials about that. That's also an idea for your pet project, if you are a gamer, but beware gamedev is hard if it is not scripted. I can probably recommend Factorio because mods are very small (haven't done any though) and Minecraft OpenComputers mod which has e.g. robots to go mining instead of you. The good thing about learning via games is that it is somewhat personal, there are many miners for said robots but because this is simple and gamified enough (if you use the original OpenComputers, not oc2 which uses VMs), you will gain some e.g. control flow skills and general understanding without much tiring. That's a good foundation for going into big world of development, but it is not a requirement.

  You probably can replace this text with virtually any skill and it should mostly work (though will require big investments because you need to buy actual equipment). I didn't extensively test that though, but I believe it is generic enough.

</details>

Yes, no fancy graphs. Want to see how I do? Scroll down :-)
