<!-- wp:paragraph -->
<p>Here are my CCNA notes on ACLs. I took notes from multiple sources, Cisco press, CBT Nuggets, Udemy, Cisco Learning Networks, etc., so hopefully it's comprehensive. Please let me know if something needs to be added or changed. I hope it's helpful as you either study for the CCNA, or if you just need a quick, to-the-point refresher on access control lists. :)</p>
<!-- /wp:paragraph -->

<!-- wp:simpletoc/toc /-->

<!-- wp:heading -->
<h2 id="general-info">General Info</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3 id="types-of-acls">Types of ACLs</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Standard numbered ACLs (1-99).</li><li>Extended numbered ACLs (100-199).</li><li>Additional ACL numbers (1300-1999 standard, 2000-2699 extended).</li><li>All IPv6 ACLs are extended.</li><li>ACLs are either named or numbered and they are also standard or extended. Extended ACLs have much more robust abilities in matching packets.</li><li>An ACL identifies traffic based on characteristics of the packet such as source IP address, destination IP address, port number. Standard numbered and standard named ACLs can <strong>only</strong> match based on source IP.</li><li>ACLs are supported on both routers and switches.</li><li>ACLs applied to an interface do not apply to traffic which originates from the router itself.</li><li>An ACL is read from top to bottom.<ul><li><strong>As soon as a rule matches the packet, the permit or deny action is applied and the ACL is not processed any further.</strong></li><li>The order of rules is important.</li></ul></li><li>The original use of ACLs was a security feature to decide if traffic should be allowed to pass through the router. By default a router will allow all traffic to pass between its interfaces. When ACLs are applied the router identifies the traffic and then decides if it will be allowed or not.</li><li>ACLs are also used in other software policies when traffic has to be identified, for example.<ul><li>Identify traffic to give better service in a (QoS) Quality of Service Policy.</li><li>Identify traffic to translate to a different IP address in a (NAT) Network Address Translation Policy.</li></ul></li><li>Access Control Lists are made up of Access Control Entries which are a series of permit or deny rules. Each ACE is written in a seperate line. Here is an example and notice the number, it's 100, which means it's an extended list which gives us more options.<ul><li><code>access-list 100 deny tcp 10.10.30.0 0.0.0.255 gt 49151 10.10.20.1 0.0.0.0 eq 23</code></li><li>The source number is gt (greater than) 49151. 10.10.30.0 is the source. 10.10.20.1 is the destination. 23 is the port.</li></ul></li><li>Remember, if this was our list, that without a ANY PERMIT as the last command we would block all traffic from coming through.</li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2 id="access-groups">Access Groups</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>ACLs are applied at the interface level with the Access-Group command.</li><li>ACLs can be applied in the inbound or outbound direction.</li><li>You can have a maximum of one ACL per interface per direction.</li><li>You can have both an inbound and an outbound ACL on the same interface, but not 2 inbound, or 2 outbound ACLs.</li><li>An interface can have no ACL applied, an inbound ACL only, an outbound ACL only, or ACLs in both directions.</li><li>Done on the interface level.&nbsp;<code>ip access-group 100 out</code>&nbsp;or&nbsp;<code>ip access-group 101 in</code></li><li><code>show ip interface f1/0 | include access list</code></li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2 id="standard-vs-extended-acls">Standard vs Extended ACLs</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>With Standard ACLs, all we can match on is the source IP address. For anything else we have to use extended ACL. Standard ACLs are numbered from 1 through 99. 100 through 199 are extended ACLs. We can also use NAMED ACLs which are easier to manage.</li><li>1300 - 1999 are IP standard access list (expanded range).</li><li>2000 - 2699 are extended access list (expanded range).</li><li>There is no default wildcard mask for Extended ACLs. You have to specify a wildcard mask.</li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2 id="extended-acls">Extended ACLs</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>First check to see if there are any access lists.<ul><li>show access-lists</li></ul><ul><li>show ip access-lists</li></ul></li><li>Extended ACL access-list command requires three matching parameters: the IP protocol type, the source IP address, and the destination IP address.</li><li>Remember that when matching a specific IP address, the extended ACL requires the use of the&nbsp;<strong>host</strong>&nbsp;keyword. You cannot simply list the IP address alone.</li><li>To create an extended numbered list, enter global configuration mode.<ul><li><code>access-list 100 deny icmp host 10.16.0.10 host 192.168.1.100 log</code></li></ul></li><li>To deny http traffic from a specific host to a specific server.<ul><li><code>access-list 100 deny tcp host 10.16.0.10 host 192.168.1.100 eq 80</code></li></ul></li><li>The eq shouldn't always be at the end of the line. Let's say we want to deny traffic from web server 10.2.3.4/23's subnet to clients in the same subnet as host 10.4.5.6/22. We would put the <code>eq www</code> after the source, since we are denying traffic&nbsp;<strong>from</strong>&nbsp;the web server.<ul><li><code>access-list 104 permit tcp 10.2.2.0 0.0.1.255 eq www 10.4.4.0 0.0.3.255</code></li></ul></li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3 id="extended-acls-and-ports">Extended ACLs and Ports</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>With extended ACLs we have the option of working with source and destination ports. Here are the syntax keywords:<ul><li><code>eq</code>&nbsp;| Stands for equal.</li><li><code>ne</code>&nbsp;| Stands for not equal.</li><li><code>lt</code>&nbsp;| Stands for less than.</li><li><code>gt</code>&nbsp;| Stands for greater than.</li><li><code>range</code>&nbsp;| Stands for, you guessed it, range. :)</li></ul></li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2 id="named-acls">Named ACLs</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Named ACL starts with the IP command.</li><li>To create a named access list named Our-ACL.<ul><li><code>ip access-list extended Our-ACL</code></li></ul></li><li>After issuing that command we are now in access list configuration mode.<ul><li><code>deny tcp host 10.16.0.10 any eq 21</code></li></ul></li><li>Another example<ul><li><code>deny ip 10.16.0.0 0.0.0.255 10.16.16.0 0.0.7.255</code></li></ul></li><li>Another example<ul><li><code>deny icmp 10.16.0.0 0.0.0.255 10.16.2.0 0.0.0.255</code></li></ul></li><li>Remember to allow the rest.<ul><li><code>permit ip any any</code></li></ul></li><li>Now we need to apply this named ACL to an interface. Select the interface.<ul><li><code>ip access-group Our-ACL | inbound | outbound</code></li></ul></li><li>Verify by checking the interface.&nbsp;<code>sh ip int</code>&nbsp;and look at the inbound and outbound access settings. Here we see a named inbound access list named My-List.</li></ul>
<!-- /wp:list -->

<!-- wp:image {"align":"center","id":1078,"sizeSlug":"full","linkDestination":"none"} -->
<div class="wp-block-image"><figure class="aligncenter size-full"><img src="https://icenetwork.is/main/wp-content/uploads/2022/03/aclinout.jpg" alt="CCNA notes on ACLs" class="wp-image-1078"/></figure></div>
<!-- /wp:image -->

<!-- wp:heading -->
<h2 id="to-create-and-verify-an-acl">To Create and Verify an ACL</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>First we should check to see if there are any access lists already defined. If there is a list already and we start typing away commands, we might be adding to a list that’s already in place, not creating a new one.</li><li><code>show access-lists</code></li><li><code>show ip access-lists</code></li><li><code>show run | sec access-list</code></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>It's also a good rule to put a remark on an ACL.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>To put a remark on an access list.<ul><li><code>access-list 1 remark this access list is for X</code></li></ul></li><li>Create the list.<ul><li><code>access list 1 deny host 10.16.0.10</code></li><li><code>access list 1 permit any</code></li><li>There is an implicit 'deny any any' rule at the bottom of ACLs.</li><li>If an ACL is not applied to an interface, all traffic is allowed.</li><li><strong>If an ACL is applied, all traffic is denied except what is explicitly allowed.</strong></li><li>Many companies put this statement at the end of the ACL to log any deny's.</li><li><code>access-list 1 deny any log</code></li><li>We know by now that the default behavior is deny any at the end of the ACL. Another way to know if things are being denied is to explicitly configure a command to deny all traffic (for example),&nbsp;<code>access-list 1 deny any</code>&nbsp;at the end of an ACL. Why would we do that when it does it by default? Because the ACL show command lists counters for the number of packets matched by each command in the ACL, but there is no counter for that implicit deny any concept at the end of the ACL. So, if you want to see counters for how many packets are matched by the deny any logic at the end of the ACL, configure an explicit deny any.</li></ul></li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>Once the ACL has been created, the next step is to go to the interface on the router and apply it to the correct interface. Make sure to pick the correct direction, in or out.<ul><li><code>ip access-group 1 | inbound | outbound</code></li></ul></li><li>Let's say we have to inject an Access Control Entry into the ACL. You can do it with numbered and named ACLs.<ul><li><code>ip access-list extended 110</code> (or if it's a named list, the name of the list)<ul><li>Now you're located in the (config-ext-nacl)#</li></ul></li><li><code>15 deny tcp host 10.10.10.11 host 10.10.50.10 eq telnet</code><ul><li>Verify your work with <code>sh ip access-lists</code></li></ul></li></ul></li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2 id="to-delete-acl-entry">To Delete ACL Entry</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Be careful to <strong>not</strong> do&nbsp;<code>no access-list 99 permit 10.16.0.7</code></li><li>This would remove the whole numbered access list 99, not just that specific entry.</li><li>The correct way would be to go into global configuration mode.<ul><li><code>ip access-list standard 99</code></li><li><code>no entry-number</code>&nbsp;Let's say you wanted to delete no 10.&nbsp;<code>no 10</code></li></ul></li></ul>
<!-- /wp:list -->

<!-- wp:image {"align":"center","id":1061,"sizeSlug":"full","linkDestination":"none"} -->
<div class="wp-block-image"><figure class="aligncenter size-full"><img src="https://icenetwork.is/main/wp-content/uploads/2022/03/acl-delete-entry.jpg" alt="" class="wp-image-1061"/></figure></div>
<!-- /wp:image -->

<!-- wp:list -->
<ul><li>Now our access list starts at 20, instead of 10. If we want to fix that and reorder the list we could do the following in global config mode. 99 is our list and the first 10 is the number we want to start from. The second 10 says we want to increment it by 10. First entry is 10, second one is 20, etc.<ul><li><code>ip access-list resequence 99 10 10</code></li></ul></li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2 id="final-best-practices-according-to-cisco-press-and-wendell-odom">Final Best Practices According to Cisco Press and Wendell Odom</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Place extended ACLs as close as possible to the source of the packet. This strategy allows ACLs to discard the packets early.</li><li>Place standard ACLs as close as possbile to the destination of the packet. This strategy avoids the mistake with standard ACLs (which match the source IPv4 address only) of unintentionally discarding packets that did no need to be discarded.</li><li>Place more specific statements early in the ACL.</li><li>Disable an ACL from its interface (using no ip access-group interface subcommand) before making changes to the ACL.</li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2 id="cisco-documentation">Cisco Documentation</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li><a href="https://www.cisco.com/c/en/us/support/docs/security/ios-firewall/23602-confaccesslists.html" target="_blank" rel="noreferrer noopener">Cisco's documentation on ACLs</a>.</li><li>I highly recommend the <a href="http://learningnetwork.cisco.com/" target="_blank" rel="noreferrer noopener">Cisco Learning Network.</a> Sign up and take their CCNA course. Anything that Andre Laurent teaches is fantastic. ;)</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Well these are my CCNA notes on ACLs. Hit me up on <a href="https://www.linkedin.com/in/armann-palsson/" target="_blank" rel="noreferrer noopener">LinkedIn</a> if you want to connect and chat, thanks.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"align":"center","id":1082,"width":411,"height":533,"sizeSlug":"full","linkDestination":"none"} -->
<div class="wp-block-image"><figure class="aligncenter size-full is-resized"><img src="https://icenetwork.is/main/wp-content/uploads/2022/03/bearbye.png" alt="" class="wp-image-1082" width="411" height="533"/></figure></div>
<!-- /wp:image -->