.. $Id: db.rst,v 6811a3039a18 2011/01/26 17:21:05 jcea $

==
DB
==

Read `Oracle documentation
<http://download.oracle.com/docs/cd/E17076_02/html/programmer_reference/index.html>`__
for better understanding.

`More info...
<http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
C/db.html>`__

DB Methods
----------

.. function:: DB(dbEnv=None, flags=0)

   Constructor.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbcreate.html>`__

.. function:: append(data, txn=None)

   A convenient version of put() that can be used for Recno or Queue
   databases. The DB_APPEND flag is automatically used, and the record
   number is returned.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbput.html#dbput_DB_APPEND>`__

.. function:: associate(secondaryDB, callback, flags=0, txn=None)

   Used to associate secondaryDB to act as a secondary index for this
   (primary) database. The callback parameter should be a reference to a
   Python callable object that will construct and return the secondary
   key or DB_DONOTINDEX if the item should not be indexed. The
   parameters the callback will receive are the primaryKey and
   primaryData values.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbassociate.html>`__

.. function:: close(flags=0)

   Flushes cached data and closes the database.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbclose.html>`__

.. function:: compact(start=None, stop=None, flags=0,
   compact_fillpercent=0, compact_pages=0, compact_timeout=0)

   Compacts Btree and Recno access method databases, and optionally
   returns unused Btree, Hash or Recno database pages to the underlying
   filesystem.

   The method returns the number of pages returned to the filesystem.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbcompact.html>`__

.. function:: consume(txn=None, flags=0)

   For a database with the Queue access method, returns the record
   number and data from the first available record and deletes it from
   the queue.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget.html#dbget_DB_CONSUME>`__

.. function:: consume_wait(txn=None, flags=0)

   For a database with the Queue access method, returns the record
   number and data from the first available record and deletes it from
   the queue. If the Queue database is empty, the thread of control
   will wait until there is data in the queue before returning.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget.html#dbget_DB_CONSUME_WAIT>`__

.. function:: cursor(txn=None, flags=0)

   Create a cursor on the DB and returns a DBCursor object. If a
   transaction is passed then the cursor can only be used within that
   transaction and you *must* be sure to close the cursor before
   commiting the transaction.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbcursor.html>`__

.. function:: delete(key, txn=None, flags=0)

   Removes a key/data pair from the database.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbdel.html>`__

.. function:: exists(key, txn=None, flags=0)

   Test if a key exists in the database. Returns True or False.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbexists.html>`__

.. function:: fd()

   Returns a file descriptor for the database.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbfd.html>`__

.. function:: get(key, default=None, txn=None, flags=0, dlen=-1, doff=-1)

   Returns the data object associated with key. If key is an integer
   then the DB_SET_RECNO flag is automatically set for BTree databases
   and the actual key and the data value are returned as a tuple. If
   default is given then it is returned if the key is not found in the
   database. Partial records can be read using dlen and doff, however be
   sure to not read beyond the end of the actual data or you may get
   garbage.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget.html>`__

.. function:: pget(key, default=None, txn=None, flags=0, dlen=-1, doff=-1)

   This method is available only on secondary databases. It will return
   the primary key, given the secondary one, and associated data.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget.html>`__

.. function:: get_transactional()

   Returns True if the database is transactional. False if not.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_transactional.html>`__

.. function:: get_priority()

   Returns the cache priority for pages referenced by the DB handle.
   This priority value is set using the DB->set_priority() method.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_priority.html>`__

.. function:: set_priority(priority)

   Set the cache priority for pages referenced by the DB handle.

   The priority of a page biases the replacement algorithm to be more
   or less likely to discard a page when space is needed in the buffer
   pool. The bias is temporary, and pages will eventually be discarded
   if they are not referenced again. The DB->set_priority() method is
   only advisory, and does not guarantee pages will be treated in a
   specific way.

   The value provided must be symbolic. Check the Oracle documentation.

   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_priority.html>`__

.. function:: get_dbname()

   Returns a tuple with the filename and the database name. If
   there is no database name, the value returned will be None.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_dbname.html>`__

.. function:: get_open_flags()

   Returns the current open method flags. That is, this method returns
   the flags that were specified when DB->open() was called.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_open_flags.html>`__

.. function:: set_private(object)

   Link an object to the DB object. This allows to pass around an
   arbitrary object. For instance, for callback context.

.. function:: get_private()

   Give the object linked to the DB.

.. function:: get_both(key, data, txn=None, flags=0)

   A convenient version of get() that automatically sets the DB_GET_BOTH
   flag, and which will be successful only if both the key and data
   value are found in the database. (Can be used to verify the presence
   of a record in the database when duplicate keys are allowed.)
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget.html#get_DB_GET_BOTH>`__

.. function:: get_byteswapped()

   May be used to determine if the database was created on a machine
   with the same endianess as the current machine.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_byteswapped.html>`__

.. function:: get_size(key, txn=None)

   Return the size of the data object associated with key.

.. function:: get_type()

   Return the database's access method type.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_type.html>`__

.. function:: join(cursorList, flags=0)

   Create and return a specialized cursor for use in performing joins on
   secondary indices.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbjoin.html>`__

.. function:: key_range(key, txn=None, flags=0)

   Returns an estimate of the proportion of keys that are less than,
   equal to and greater than the specified key.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbkey_range.html>`__

.. function:: open(filename, dbname=None, dbtype=DB_UNKNOWN, flags=0, mode=0660, txn=None)

   Opens the database named dbname in the file named filename. The
   dbname argument is optional and allows applications to have multiple
   logical databases in a single physical file. It is an error to
   attempt to open a second database in a file that was not initially
   created using a database name. In-memory databases never intended to
   be shared or preserved on disk may be created by setting both the
   filename and dbname arguments to None.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbopen.html>`__

.. function:: put(key, data, txn=None, flags=0, dlen=-1, doff=-1)

   Stores the key/data pair in the database. If the DB_APPEND flag is
   used and the database is using the Recno or Queue access method then
   the record number allocated to the data is returned. Partial data
   objects can be written using dlen and doff.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbput.html>`__

.. function:: remove(filename, dbname=None, flags=0)

   Remove a database.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbremove.html>`__

.. function:: rename(filename, dbname, newname, flags=0)

   Rename a database.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbrename.html>`__

.. function:: set_encrypt(passwd, flags=0)

   Set the password used by the Berkeley DB library to perform
   encryption and decryption. Because databases opened within Berkeley
   DB environments use the password specified to the environment, it is
   an error to attempt to set a password in a database created within an
   environment.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_encrypt.html>`__

.. function:: get_encrypt_flags()

   Returns the encryption flags.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_encrypt_flags.html>`__
 
.. function:: set_bt_compare(compareFunc)

   Set the B-Tree database comparison function. This can only be called
   once before the database has been opened. compareFunc takes two
   arguments: (left key string, right key string) It must return a -1,
   0, 1 integer similar to cmp. You can shoot your database in the
   foot, beware!  Read the Berkeley DB docs for the full details of
   how the comparison function MUST behave.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_bt_compare.html>`__

.. function:: get_bt_minkey()

   Returns the minimum number of key/data pairs intended to be stored on
   any single Btree leaf page. This value can be set using the
   DB->set_bt_minkey() method.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_bt_minkey.html>`__

.. function:: set_bt_minkey(minKeys)

   Set the minimum number of keys that will be stored on any single
   BTree page.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_bt_minkey.html>`__

.. function:: set_cachesize(gbytes, bytes, ncache=0)

   Set the size of the database's shared memory buffer pool.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_cachesize.html>`__

.. function:: get_cachesize()

   Returns a tuple with the current size and composition of the cache.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_cachesize.html>`__

.. function:: set_get_returns_none(flag)

   Controls what get and related methods do when a key is not found.

   See the DBEnv set_get_returns_none documentation.

   The previous setting is returned.

.. function:: get_flags()

   Returns the current database flags as set by the DB->set_flags()
   method.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_flags.html>`__

.. function:: set_flags(flags)

   Set additional flags on the database before opening.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_flags.html>`__

.. function:: get_h_ffactor()

   Returns the hash table density as set by the DB->set_h_ffactor()
   method.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_h_ffactor.html>`__

.. function:: set_h_ffactor(ffactor)

   Set the desired density within the hash table.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_h_ffactor.html>`__

.. function:: get_h_nelem()

   Returns the estimate of the final size of the hash table as set by the
   DB->set_h_nelem() method. 
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_h_nelem.html>`__

.. function:: set_h_nelem(nelem)

   Set an estimate of the final size of the hash table.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_h_nelem.html>`__

.. function:: get_lorder()

   Returns the database byte order; a byte order of 4,321 indicates a
   big endian order, and a byte order of 1,234 indicates a little endian
   order. This value is set using the DB->set_lorder() method.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_lorder.html>`__

.. function:: set_lorder(lorder)

   Set the byte order for integers in the stored database metadata.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_lorder.html>`__

.. function:: get_pagesize()

   Returns the database's current page size, as set by the
   DB->set_pagesize() method.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_pagesize.html>`__

.. function:: set_pagesize(pagesize)

   Set the size of the pages used to hold items in the database, in
   bytes.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_pagesize.html>`__

.. function:: get_re_delim()

   Returns the delimiting byte, which is used to mark the end of a
   record in the backing source file for the Recno access method.
   The return value will be a numeric byte value.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_re_delim.html>`__

.. function:: set_re_delim(delim)

   Set the delimiting byte used to mark the end of a record in the
   backing source file for the Recno access method. You can
   specify a char or a numeric byte value.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_re_delim.html>`__

.. function:: get_re_len()

   Returns the length of the records held in a Queue access method
   database. This value can be set using the DB->set_re_len() method.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_re_len.html>`__

.. function:: set_re_len(length)

   For the Queue access method, specify that the records are of length
   length. For the Recno access method, specify that the records are
   fixed-length, not byte delimited, and are of length length.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_re_len.html>`__

.. function:: get_re_pad()

   Returns the pad character used for short, fixed-length records used
   by the Queue and Recno access methods. The method returns a byte
   value.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_re_pad.html>`__

.. function:: set_re_pad(pad)

   Set the padding character for short, fixed-length records for the
   Queue and Recno access methods. You can specify a char or a numeric
   byte value.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_re_pad.html>`__

.. function:: get_re_source()

   Returns the source file used by the Recno access method. This file is
   configured for the Recno access method using the DB->set_re_source()
   method.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_re_source.html>`__

.. function:: set_re_source(source)

   Set the underlying source file for the Recno access method.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_re_source.html>`__

.. function:: get_q_extentsize()

   Returns the number of pages in an extent. This value is used only for
   Queue databases and is set using the DB->set_q_extentsize() method.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbget_q_extentsize.html>`__

.. function:: set_q_extentsize(extentsize)

   Set the size of the extents used to hold pages in a Queue database,
   specified as a number of pages. Each extent is created as a separate
   physical file. If no extent size is set, the default behavior is to
   create only a single underlying database file.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbset_q_extentsize.html>`__

.. function:: stat(flags=0, txn=None)

   Return a dictionary containing database statistics with the following
   keys.

   For Hash databases:

        +-----------+-------------------------------------------------+
        | magic     | Magic number that identifies the file as a Hash |
        |           | database.                                       |
        +-----------+-------------------------------------------------+
        | version   | Version of the Hash database.                   |
        +-----------+-------------------------------------------------+
        | nkeys     | Number of unique keys in the database.          |
        +-----------+-------------------------------------------------+
        | ndata     | Number of key/data pairs in the database.       |
        +-----------+-------------------------------------------------+
        | pagecnt   | The number of pages in the database.            |
        +-----------+-------------------------------------------------+
        | pagesize  | Underlying Hash database page (& bucket) size.  |
        +-----------+-------------------------------------------------+
        | nelem     | Estimated size of the hash table specified at   |
        |           | database creation time.                         |
        +-----------+-------------------------------------------------+
        | ffactor   | Desired fill factor (number of items per bucket)|
        |           | specified at database creation time.            |
        +-----------+-------------------------------------------------+
        | buckets   | Number of hash buckets.                         |
        +-----------+-------------------------------------------------+
        | free      | Number of pages on the free list.               |
        +-----------+-------------------------------------------------+
        | bfree     | Number of bytes free on bucket pages.           |
        +-----------+-------------------------------------------------+
        | bigpages  | Number of big key/data pages.                   |
        +-----------+-------------------------------------------------+
        | big_bfree | Number of bytes free on big item pages.         |
        +-----------+-------------------------------------------------+
        | overflows | Number of overflow pages (overflow pages are    |
        |           | pages that contain items that did not fit in    |
        |           | the main bucket page).                          |
        +-----------+-------------------------------------------------+
        | ovfl_free | Number of bytes free on overflow pages.         |
        +-----------+-------------------------------------------------+
        | dup       | Number of duplicate pages.                      |
        +-----------+-------------------------------------------------+
        | dup_free  | Number of bytes free on duplicate pages.        |
        +-----------+-------------------------------------------------+

   For BTree and Recno databases:

        +-------------+-----------------------------------------------+
        | magic       | Magic number that identifies the file as a    |
        |             | Btree database.                               |
        +-------------+-----------------------------------------------+
        | version     | Version of the Btree database.                |
        +-------------+-----------------------------------------------+
        | nkeys       | For the Btree Access Method, the number of    |
        |             | unique keys in the database.                  |
        |             |                                               |
        |             | For the Recno Access Method, the number of    |
        |             | records in the database. If the database has  |
        |             | been configured to not re-number records      |
        |             | during deletion, the number of records may    |
        |             | include records that have been deleted.       |
        +-------------+-----------------------------------------------+
        | ndata       | For the Btree Access Method, the number of    |
        |             | key/data pairs in the database.               |
        |             |                                               |
        |             | For the Recno Access Method, the number of    |
        |             | records in the database. If the database has  |
        |             | been configured to not re-number records      |
        |             | during deletion, the number of records may    |
        |             | include records that have been deleted.       |
        +-------------+-----------------------------------------------+
        | pagecnt     | The number of pages in the database.          |
        +-------------+-----------------------------------------------+
        | pagesize    | Underlying database page size.                |
        +-------------+-----------------------------------------------+
        | minkey      | Minimum keys per page.                        |
        +-------------+-----------------------------------------------+
        | re_len      | Length of fixed-length records.               |
        +-------------+-----------------------------------------------+
        | re_pad      | Padding byte value for fixed-length records.  |
        +-------------+-----------------------------------------------+
        | levels      | Number of levels in the database.             |
        +-------------+-----------------------------------------------+
        | int_pg      | Number of database internal pages.            |
        +-------------+-----------------------------------------------+
        | leaf_pg     | Number of database leaf pages.                |
        +-------------+-----------------------------------------------+
        | dup_pg      | Number of database duplicate pages.           |
        +-------------+-----------------------------------------------+
        | over_pg     | Number of database overflow pages.            |
        +-------------+-----------------------------------------------+
        | empty_pg    | Number of empty database pages.               |
        +-------------+-----------------------------------------------+
        | free        | Number of pages on the free list.             |
        +-------------+-----------------------------------------------+
        | int_pgfree  | Num of bytes free in database internal pages. |
        +-------------+-----------------------------------------------+
        | leaf_pgfree | Number of bytes free in database leaf pages.  |
        +-------------+-----------------------------------------------+
        | dup_pgfree  | Num bytes free in database duplicate pages.   |
        +-------------+-----------------------------------------------+
        | over_pgfree | Num of bytes free in database overflow pages. |
        +-------------+-----------------------------------------------+

   For Queue databases:

        +-------------+-----------------------------------------------+
        | magic       | Magic number that identifies the file as a    |
        |             | Queue database.                               |
        +-------------+-----------------------------------------------+
        | version     | Version of the Queue file type.               |
        +-------------+-----------------------------------------------+
        | nkeys       | Number of records in the database.            |
        +-------------+-----------------------------------------------+
        | ndata       | Number of records in the database.            |
        +-------------+-----------------------------------------------+
        | pagesize    | Underlying database page size.                |
        +-------------+-----------------------------------------------+
        | extentsize  | Underlying database extent size, in pages.    |
        +-------------+-----------------------------------------------+
        | pages       | Number of pages in the database.              |
        +-------------+-----------------------------------------------+
        | re_len      | Length of the records.                        |
        +-------------+-----------------------------------------------+
        | re_pad      | Padding byte value for the records.           |
        +-------------+-----------------------------------------------+
        | pgfree      | Number of bytes free in database pages.       |
        +-------------+-----------------------------------------------+
        | first_recno | First undeleted record in the database.       |
        +-------------+-----------------------------------------------+
        | cur_recno   | Last allocated record number in the database. |
        +-------------+-----------------------------------------------+

   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbstat.html>`__

.. function:: stat_print(flags=0)

   Displays the database statistical information.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbstat_print.html>`__

.. function:: sync(flags=0)

   Flushes any cached information to disk.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbsync.html>`__

.. function:: truncate(txn=None, flags=0)

   Empties the database, discarding all records it contains. The number
   of records discarded from the database is returned.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbtruncate.html>`__

.. function:: upgrade(filename, flags=0)

   Upgrades all of the databases included in the file filename, if
   necessary.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbupgrade.html>`__

.. function:: verify(filename, dbname=None, outfile=None, flags=0)

   Verifies the integrity of all databases in the file specified by the
   filename argument, and optionally outputs the databases' key/data
   pairs to a file.
   `More info...
   <http://download.oracle.com/docs/cd/E17076_02/html/api_reference/
   C/dbverify.html>`__

DB Mapping and Compatibility Methods
------------------------------------

These methods of the DB type are for implementing the Mapping Interface,
as well as others for making a DB behave as much like a dictionary as
possible. The main downside to using a DB as a dictionary is you are not
able to specify a transaction object.

.. function:: DB_length() [ usage: len(db) ]

   Return the number of key/data pairs in the database.

.. function:: DB_subscript(key) [ usage: db[key] ]

   Return the data associated with key.

.. function:: DB_ass_sub(key, data) [ usage: db[key] = data ]

   Assign or update a key/data pair, or delete a key/data pair if data
   is NULL.

.. function:: keys(txn=None)

   Return a list of all keys in the database. Warning: this method
   traverses the entire database so it can possibly take a long time to
   complete.

.. function:: items(txn=None)

   Return a list of tuples of all key/data pairs in the database.
   Warning: this method traverses the entire database so it can possibly
   take a long time to complete.

.. function:: values(txn=None)

   Return a list of all data values in the database. Warning: this
   method traverses the entire database so it can possibly take a long
   time to complete.

.. function:: has_key(key, txn=None)

   Returns true if key is present in the database.

