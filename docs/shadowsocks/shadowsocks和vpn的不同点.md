> 原文地址：
>
> https://qz.com/1072701/meet-shadowsocks-the-underground-tool-that-chinas-coders-use-to-blast-through-the-great-firewall/

This summer Chinese authorities deepened a crackdown on virtual private networks (VPNs)—tools that help internet users inside the mainland access the open, uncensored web. While not a blanket ban, the new restrictions are shifting the services out of their legal grey area and further toward a black one. In July alone, one popular made-in-China VPN abruptly [ceased operations](https://www.bloomberg.com/news/articles/2017-07-03/china-s-great-firewall-gets-tougher-as-popular-vpn-shut-down), Apple removed [dozens of VPN apps](https://www.reuters.com/article/us-china-apple-vpn/apple-says-it-is-removing-vpn-services-from-china-app-store-idUSKBN1AE0BQ)from its China-facing app store, and some international hotels [stopped offering](https://qz.com/1035554/visiting-china-dont-count-on-a-swanky-hotel-to-help-you-escape-the-great-firewall/) VPN services as part of their in-house wifi.

Yet the government was targeting VPN usage well before the latest push. Ever since president Xi Jinping took office in 2012, activating a VPN in China has been a constant headache—speeds are slow, and connectivity frequently lapses. Especially before major political events (like this year’s upcoming party congress in October), it’s not uncommon for connections to drop immediately, or not even form at all.

In response to these difficulties, China’s tech-savvy programmers have been relying on another, lesser-known tool to access the open internet. It’s called Shadowsocks, and it’s an open-source proxy built for the specific purpose of jumping China’s Great Firewall. While the government has made efforts [to curb its spread](http://chinadigitaltimes.net/2015/08/circumvention-tool-deleted-after-police-visit-developer/), it’s likely to remain difficult to suppress.

## How is Shadowsocks different from a VPN?

To understand how Shadowsocks works, we’ll have to get a bit into the cyberweeds. Shadowsocks is based on a technique called proxying. Proxying grew popular in China during the early days of the Great Firewall—before it was truly “great.” In this setup, before connecting to the wider internet, you first connect to a computer other than your own. This other computer is called a “proxy server.” When you use a proxy, all your traffic is routed first through the proxy server, which could be located anywhere. So even if you’re in China, your proxy server in Australia can freely connect to Google, Facebook, and the like.

But the Great Firewall has since grown more powerful. Nowadays, even if you have a proxy server in Australia, the Great Firewall can identify and block traffic it doesn’t like from that server. It still knows you are requesting packets from Google—you’re just using a bit of an odd route for it. That’s where Shadowsocks comes in. It creates an encrypted connection between the Shadowsocks client on your local computer and the one running on your proxy server, using an open-source internet protocol called [SOCKS5](https://nordvpn.com/blog/socks5-proxy/).

How is this different from a VPN? VPNs also work by rerouting and encrypting data. But most people who use them in China use one of a few large service providers. That makes it easy for the government to identify those providers and then block traffic from them. And VPNs usually rely on one of a few popular internet protocols, which tell computers how to talk to each other over the web. Chinese censors have been able to use machine learning to find “fingerprints” that identify traffic from VPNs using these protocols. These tactics don’t work so well on Shadowsocks, since it is a less centralized system.

Each Shadowsocks user creates his own proxy connection, and so each looks a little different from the outside. As a result, identifying this traffic is more difficult for the Great Firewall—that is to say, through Shadowsocks, it’s very hard for the firewall to distinguish traffic heading to an innocuous music video or a financial news article from traffic heading to Google or some other site blocked in China.

Leo Weese, a Hong Kong-based privacy advocate, likens VPNs to a professional freight forwarder, and Shadowsocks to having a package shipped to a friend who then re-addresses the item to the real intended recipient before putting it back in the mail. The former method is more lucrative as a business, but easier for authorities to detect and shut down. The latter is makeshift, but way more discreet.

What’s more, tech-savvy Shadowsocks users often customize their settings, making it even harder for the Great Firewall to detect them wholesale.

“People use VPNs to set up inter-company links, to set up a secure network. It wasn’t designed for the circumvention of censorship,” says Larry Salibra, a Hong Kong-based privacy advocate. With Shadowsocks, he adds, “Each person can configure it to look like their own thing. That way everybody’s not using the same protocol.”

## Calling all coders

If you’re a luddite, you’ll probably have a hard time setting up Shadowsocks. One common method to use it requires renting out a virtual private server (VPS) located outside of China and capable of running Shadowsocks. Then users must log in to the server using their computer’s terminal, and enter the Shadowsocks code. Next, using a Shadowsocks client app (there are many, both free and paid), users input the server location and password and access the server. After that, they can browse the internet freely.

Shadowsocks is often difficult to set up because it originated as a for-coders, by-coders tool. The software first reached the public in 2012 via Github, when a developer using the pseudonym “Clowwindy” uploaded it to the code repository. Word-of-mouth spread among other Chinese developers, as well as on Twitter, which has long been a hub for anti-firewall Chinese programmers. A community formed around Shadowsocks. Employees at some of the world’s largest tech companies—both Chinese and international—work together in their free time to maintain the software’s code. Developers have built third-party apps to run it, each touting various custom features.

One such developer is the creator behind Potatso, a Shadowsocks client for iOS. Based in Suzhou and employed at a US-based software company, he grew frustrated at the firewall’s block on Google and Github (the latter is blocked intermittently), both of which he relied on to code for work. He built Potatso during nights and weekends out of frustration with other Shadowsocks clients, and eventually put it in the app store.

“Shadowsocks is a great invention,” he says, asking to remain anonymous. “Until now, there’s still no evidence that it can be identified and get stopped by the Great Firewall.”

## Not quite underground, not quite above ground

It’s difficult to know how many people use Shadowsocks. The developers for Potatso and Surge, another iOS client, separately told Quartz their paid apps have gathered enough downloads to make for a lucrative hobby on top of other work. But neither could estimate the popularity of the core Shadowsocks software.

Still, anecdotes suggest that the software has reached at least some people in China who aren’t professional developers. One Shadowsocks user Quartz spoke to says he relies on it to watch videos on Vimeo and YouTube. Both sites are blocked in China, but he visits regularly for his job at a production company.

Another Shadowsocks user, 25-year-old Steffie Chao, told Quartz she began using the software four years ago. While preparing to study abroad, she used a VPN to access YouTube and watch university lectures. When her VPN stopped working, she searched for an alternative and discovered Shadowsocks on a Chinese-language internet forum. She ran it on her computer using some rudimentary coding skills she picked up in a class.

At the very least, Shadowsocks is widespread enough that Chinese authorities are aware of its existence. The government has made some attempts to clip its wings. In 2015, around the time of a parade in China celebrating the 70th anniversary of WWII, Clowwindy [posted a message](https://qz.com/488307/china-is-cracking-down-on-the-services-that-help-people-jump-the-great-firewall/)on Github announcing he had been visited by the police, and would have to stop working on Shadowsocks. And when [Apple removed dozens](https://qz.com/1044199/tim-cook-defends-apples-removal-of-vpn-apps-from-its-chinese-app-store/) of firewall-jumping apps from its Chinese-facing app store, it didn’t just target VPNs—several Shadowsocks apps were removed as well, including Potatso.

Yet Shadowsocks will continue to live on. That’s in part because the code is open-source, meaning that anyone can maintain, alter it, and release it in a different form (the source code remains on Github, it’s simply more difficult to find there than it was previously).

Should Shadowsocks give us hope for freedom on China’s internet? Yes and no.

On the one hand, it’s unlikely that any Shadowsocks app will ever become as widespread as brand-name VPNs, like VyperVPN or AnchorFree. According to Weese, the privacy advocate, Shadowsocks’s underlying technology is difficult to “scale” business-wise compared to a VPN. That means that even though Shadowsocks might be a better tool for jumping the Great Firewall, VPNs will have an advantage when it comes to reaching consumers.

Not that there’s a lot of incentive for an enterprising Chinese coder to build and promote a “mainstream,” easy-to-use Shadowsocks app. After all, if it gets popular enough in China, authorities could take notice, and there could be [serious consequences](http://www.williamlong.info/archives/5084.html) (link in Chinese)—or more government effort towards figuring out how to detect and block users.

Shadowsocks might not be the “perfect weapon” to defeat the Great Firewall once and for all. But it will likely lurk in the dark for some time.

*Echo Huang contributed to reporting*.