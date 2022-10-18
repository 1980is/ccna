# AAA - Authentication, Authorization, Accounting #
- Authentication (Who).
- Authorization (What can they do).
- Accounting (What they did).
- Two primary protocols we can use. TACACS+ and RADIUS. TACACS+ is used if we only have Cisco devices. RADIUS used for a mixed environment.
- Look at Cisco ISE.

![[ciscoise.png]]

### Connect a Router to AAA Server ###
1.  aaa new-model
2.  tacacs-server host 10.0.0.3 key aaa-cs-pw
3. aaa group server tacacs+ FB-TG. // This is optional.
4.  aaa authentication login Use-AAA group tacacs+ local
5.  It only uses local as the secondary backup login, it uses local usernames and passwords for that.
6.  aaa authentication enable default group tacacs+ local
7.  line vty 0 4
8.  login authentication Use-AAA

- To see authentication work do: debug aaa authentication
- Remember to not only allow AAA logins. What if the AAA or AD server is not available, then we can't login to the switch or router.