So I recently had lunch with @hoosteeno, a generally smart guy when it comes to technology and in particular recently employed at Mozilla advancing the Web broadly and generally. I think I managed to sloppily state my current position that the technology of the Web is ill-suited for building Internet applications.

- The Internet, despite it's problems, is still fundamentally delivering on its tremendous potential and essentially working as envisioned. It's not all roses and there are cautions and caveats, but we hooked up all the computers to each other and it mostly works great. And once we had them all hooked up, everybody got a few computers.
- I think of the Internet of having a clear technical goal and purpose: connect all the computers in a robust way. Why? For what purpose? We're not really sure but we're confident it will be generally useful.
- I am making a clear and strong distinction between the Internet (TCP/IP, DNS, BGP, etc) and the Web (HTTP, HTML, CSS, JS, etc)
- The Web seems to have matured as the most impactful use of the Internet
- The web has a more humanitarian purpose and goal. Allow broad and accessible communication in a different paradigm enabled by the Internet.
  - The Web has strength in
    - equal footing for authors
    - relatively low barrier to entry
      - Technologies largely designed to be approachable to amateurs
      - inexpensive to publish independently on the web
    - one-to-many/broadcast flow of communication
    - text is the primary medium, supported by images (but really searchable text is what it's about)
    - really good search and hyperlinks are the lynchpins that make the magic happen
    - audio, video, animation, and interactivity are fundamentally not there on the web.
      - What video we have is because of the Internet. The Web is just a UI to choose which video to watch, and even then when you watch it the experience is shamefully bad (slow, low quality, can't pause/resume properly, can't download ahead of time, online only, etc)
    - most of the content is created by authors typing text on a keyboard
    - largely publish-once-and-leave-it interaction paradigm
    - The technologies of HTML/CSS/JS, at least as initially designed, encourage a mixing of markup, code, and content in particular formats that tends to cement content in unchangeable formats and create an ongoing backward compatibility problem that strongly stifles and delays technological advancements
    - The web is mostly an online-only experience
- Web Technologies (HTML, CSS, JS, browsers) are ill-suited for Internet application development
  - Internet applications simply don't consist of the things the web primarily serves
  - they are either isolated personal interactions or real-time group interactions
  - hyperlinks are not nearly as relevant, other than referencing the web
  - keyword search is still important, but in a different, reduced role
  - Application user interfaces are fundamentally a different UI paradigm then a text document with basic formatting and scrolling
  - App UIs are comprised of highly screen-specific layouts and widgets. Formatted text has a role in Apps, but it is quite minor compared to tabular data, visualized data, widgets, images, videos
  - The App ecosystem is vibrant enough to warrant well-tailored experiences on a broad range of devices. Popular or important apps will not settle for a least-common-denominator experience.
  - Many apps can provide value offline and seamlessly interact with the Internet when connected
  - The security story about how much trust you have in a web site vs how much trust you have in an app is quite different (maybe?). At the end of the day, the web has advocated highly restrictive sandboxing and hamstringing of web apps and native apps are far less sandboxed. Overall, I don't think either model has been really effective, so I'd rather have my developer effort spent building great apps that leverage the full capabilities of the device and the Internet than trying to come up with clever ways to store data when the sandbox only offers hamstrung options.

- Assorted web/app impedence mismatches
  - each page has a unique, permanent, shareaable URL - nope
  - screen is an rectangle of unspecified and dynamic dimensions - nope
  - there is no "screen", there's a document - nope
  - primary development abstractions are concepts from web documents - nope
  - keystrokes, hover, mouse movements - only on desktop
  - development environment: take your code, concat, minify, generate sourcemap, gzip, send to browser. Browser reverse engineers your filesystem layout. This is totally fucked.
  - No way to specify things that are equal size, centered, etc
