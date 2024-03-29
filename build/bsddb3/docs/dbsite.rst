.. $Id: dbsite.rst,v 7ca0b93a18ae 2011/06/16 00:52:48 jcea $

==========
DBSite
==========

Read `Oracle documentation
<http://download.oracle.com/docs/cd/E17076_02/html/programmer_reference/group_membership.html>`__
for better understanding.

You use the DB_SITE handle to configure and manage replication sites.

`More info...
<http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
C/repmgr_site.html>`__

DBSite Methods
------------------

.. function:: close(flags=0)

   Close a DBSite handle.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbsite_close.html>`__

.. function:: get_address()

   Returns a replication site's network address. That is, this method
   returns a tuple with the site's hostname and port. 
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbsite_get_address.html>`__

.. function:: get_config()

   Returns whether the specified which parameter is currently set.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbsite_get_config.html>`__

.. function:: get_eid()

   Returns a replication site's Environment ID (EID).
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbsite_get_eid.html>`__

.. function:: remove()

   Removes the site from the replication group. If called at the master
   site, repmgr updates the membership database directly. If called from
   a client, this method causes a request to be sent to the master to
   perform the operation. The method then awaits confirmation.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbsite_remove.html>`__

.. function:: set_config(which, value)

   Configures a replication site.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbsite_set_config.html>`__


