TODO
====

Stuff we didn't finish and where help is needed.  Cleaning up the below
list is another thing we need help with.


- Build with debug memory allocation or dmalloc library
  - http://dmalloc.com/
  - https://www.gnu.org/software/automake/manual/html_node/Public-Macros.html (`AM_WITH_DMALLOC`)

- Switch to npcap (win32)

- Take inventory of http://stackoverflow.com/questions/tagged/libnet#

- Add automatic tests for `make check`, IPv6 in particular

- change all `__WIN32` and `__WIN32__` preprocessor directives with the
  more universal `WIN32` and `_WIN32` directives (msvc + mingw)
  (eliminating the need for `-mwin32`)

- Improve documentation: FAQ, Examples, adding RFCs

- Fix "broken" samples (on win32?)

- Fix MSVC/Mingw collision


1.1.x TODO LIST
---------------

The following is possibly outdated and already fixed.
 
- Update the man page!

- Add a programmer's man page detailing the pblock architecture.

- Fix plist memory leak.

- Fix IPv6.  According to RFC 2992:

  > "Another difference from IPv4 raw sockets is that complete packets
  > (that is, IPv6 packets with extension headers) cannot be read or
  > written using the IPv6 raw sockets API.  Instead, ancillary data
  > objects are used to transfer the extension headers, as described
  > later in this document.  Should an application need access to the
  > complete IPv6 packet, some other technique, such as the datalink
  > interfaces BPF or DLPI, must be used.
  >
  > All fields in the IPv6 header that an application might want to
  > change (i.e., everything other than the version number) can be
  > modified using ancillary data and/or socket options by the
  > application for output.  All fields in a received IPv6 header (other
  > than the version number and Next Header fields) and all extension
  > headers are also made available to the application as ancillary data
  > on input.  Hence there is no need for a socket option similar to the
  > IPv4 `IP_HDRINCL` socket option."

- Add self-throttling logic to `libnet_write()`/`libnet_init()`?
  Advanced mode thing?

- Prune the include list in `libnet.h.in`.  Also add conditionals
  around the headers we use for building the library, but not when
  using it.

- Data marshalling API for unaligned structures (like STP).

- Make Cisco ISL work.  The issue is that we have build our Ethernet
  frame first, then encapsulate it inside of an ISL envelope.
    - We have to compute CRCs for both Ethernet and ISL.

- Tune advanced interface functionality that allow the application
  programmer to get inside `libnet_t`.

- Test HPUX 11 port.

- Test cywin32 port.

- Flesh out the advanced mode.

- Consider making a flag for "strict mode" where libnet will check
  things like when you build an IP options list there is an IP
  header preceding it (likewise for TCP)...  Other "smart" things
  could happen in this mode too.  When in non-strict mode, libnet
  will be less rigid but prone to user-error mode.

- If we have a problem building a header we might end up freeing it
  creating a NULL entry on the list and preventing us from getting to
  entries beyond it (to free or whatever).  Maybe we should mark it
  bad or something and rely on the cleanup at the end to free it up?

- Fix checksum support for CDP

- Verify Checksuming:  
  Currently verified working on OpenBSD/Linux/Solaris:
  - raw  IP/UDP         [with and without data]
  - raw  IP/TCP         [with and without data]
  - raw  IP/ICMP        [with and without data]
  - raw  IP/OSPF
    - hello packet      [with no auth data]
    - hello packet      [with no auth data and LSA sub-header (LSA check = bad)]
  - link IP/UDP         [with and without data]
  - link IP/TCP         [with and without data]

- Update the rest of the `libnet_link_*` files for the new format,
  already ported:
  - bpf                 [works]
  - linux packet socket [works]
  - linux sock packet   [works]
  - dlpi                [works]

- Port link stuff to use `writev()` in `libnet_write()` (sendto can't hang).

- Get IPsec code working.

- Add the following packet builders:
  - SNMP

- Update `__libnet_handle_dump` to dump everything in `l` verbosely.
