===============
Type Descriptor
===============

This section describes how type information for query input and results
is encoded.  Specifically, this is needed to decode the server response to
the "Describe" request.

The type descriptor is essentially a list of type information *blocks*:

* each *block* encodes one type;

* *blocks* can reference other *blocks*.

While parsing the *blocks*, a database driver can assemble an
*encoder* or a *decoder* of the EdgeDB binary data.

An *encoder* is used to encode objects, native to the driver's runtime,
to binary data that EdegDB can decode and work with.

A *decoder* is used to decode data from EdgeDB native format to
data types native to the driver.

In this section, the following nomenclature is used:

.. table::
   :widths: 25, 75

   ================ =========================================================
   Token            Description
   ================ =========================================================
   ``<uuid>``       A UUID, 16 bytes.
   ``<pos>``        A reference to the previously decoded *block*,
                    2 bytes, ``uint16``.
   ``<count>``      Number of elements, 2 bytes, ``uint16``.
   ``<str>``        A strings encoded as UTF-8; 2 bytes ``uint16`` *length*,
                    followed by the *length* number of bytes.
   ================ =========================================================


Base Types
==========

The following table lists all EdgeDB base types known IDs:

======================================== =====================================
ID                                       Type Name
======================================== =====================================
``00000000-0000-0000-0000-000000000100`` :eql:type:`std::uuid`
``00000000-0000-0000-0000-000000000101`` :eql:type:`std::str`
``00000000-0000-0000-0000-000000000102`` :eql:type:`std::bytes`
``00000000-0000-0000-0000-000000000103`` :eql:type:`std::int16`
``00000000-0000-0000-0000-000000000104`` :eql:type:`std::int32`
``00000000-0000-0000-0000-000000000105`` :eql:type:`std::int64`
``00000000-0000-0000-0000-000000000106`` :eql:type:`std::float32`
``00000000-0000-0000-0000-000000000107`` :eql:type:`std::float64`
``00000000-0000-0000-0000-000000000108`` :eql:type:`std::decimal`
``00000000-0000-0000-0000-000000000109`` :eql:type:`std::bool`
``00000000-0000-0000-0000-00000000010A`` :eql:type:`std::datetime`
``00000000-0000-0000-0000-00000000010B`` :eql:type:`std::local_datetime`
``00000000-0000-0000-0000-00000000010C`` :eql:type:`std::local_date`
``00000000-0000-0000-0000-00000000010D`` :eql:type:`std::local_time`
``00000000-0000-0000-0000-00000000010E`` :eql:type:`std::duration`
``00000000-0000-0000-0000-00000000010F`` :eql:type:`std::json`
======================================== =====================================
