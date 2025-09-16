#FlexLM licensing software

FlexLM is a software developed and maintained by 
<a href="http://www.openlm.com">OpenLM</a> that helps developer
securing their work by providing tools. 

With FlexLM you can obtain "floating" licenses, this means that you licenses
can be used on any computer that has a connection with the license server.

I've created this page because I've been facing a problem with
software that uses FlexLM licensig running on computers without a direct
connection the the FlexLM license Server.

After some investigation on internet I've found this solution:

* Force FlexLM vendor deamon to listen on a defined port, and forward all
 connections from the frontend host to the FlexLM Server.
This solution implies changes in FlexLM License file (add PORT=XXXX) to the
vendor daemon line.

Since I didn't have control on the FlexLM Server I decided to do some
dirty tricks, by forwarding the FlexLM connection to the server 
(this is done on a defined port - look in the license file), the problem
arises when you have to forward the connection to the vendor daemon,
since this port, if not defined in the license file is dynamically allocated.

The result is the code included in this repository,
that forwards connection to the License Server and parses the reply for the
vendor daemon port and dynamically forward connection on this port to 
the server.
