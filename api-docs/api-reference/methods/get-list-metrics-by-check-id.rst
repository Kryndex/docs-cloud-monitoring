.. _list-metrics-by-check-id:

List metrics by check ID
~~~~~~~~~~~~~~~~~~~~~~~~

.. code::

    GET /entities/{entityId}/checks/{checkId}/metrics

Lists the metrics associated with the specified ``checkId``.

This operation can be paginated. For information,
see :ref:`Paginated collections <paginated-collections>`.

This operation does not require a request body.

This operation returns a response body that lists the metrics associated
with your check. A single check usually generates several metrics.
For example, http checks generate the following metrics: bytes, code,
duration, truncated, tt_connect, tt_firstbyte.

Metrics generated by remote checks are generated for each monitoring
zone where the check is issued.

Metric names use the syntax:

``monitoringZone``.``metricName``

where:

``monitoringZone``
  is the monitoring zone where the check was issued.

``metricName``
  is the name of the metric.

For example a metric called ``tt_connect``, generated from the ``DFW``
monitoring zone, is labeled as ``mzdfw.tt_connect``.

.. note::
   Metrics generated by agent checks have no monitoring zone.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The request completed.   |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad request              |The system received an   |
|                          |                         |invalid value in a       |
|                          |                         |request.                 |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |The system received a    |
|                          |                         |request from a user that |
|                          |                         |is not authenticated.    |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |The system received a    |
|                          |                         |request that the user is |
|                          |                         |not authorized to make.  |
+--------------------------+-------------------------+-------------------------+
|405                       |Method Not Allowed       |The method specified in  |
|                          |                         |the request is not       |
|                          |                         |supported for the        |
|                          |                         |resource. A list of      |
|                          |                         |valid methods for the    |
|                          |                         |requested resource is    |
|                          |                         |included in the response.|
+--------------------------+-------------------------+-------------------------+
|413                       |Over Limit               |The response body is too |
|                          |                         |large.                   |
+--------------------------+-------------------------+-------------------------+
|500                       |Internal Server Error    |An unexpected condition  |
|                          |                         |was encountered.         |
+--------------------------+-------------------------+-------------------------+
|503                       |Service Unavailable      |The system is            |
|                          |                         |experiencing heavy load  |
|                          |                         |or another system        |
|                          |                         |failure.                 |
+--------------------------+-------------------------+-------------------------+

Request
-------

The following table shows the header parameters for the request:

+-----------------+----------------+-----------------------------------------------+
|Name             |Type            |Description                                    |
+=================+================+===============================================+
|X-Auth-Token     |String          |A valid authentication token with              |
|                 |*(Required)*    |administrative access. For details, see        |
|                 |                |:ref:`Get your credentials <get-credentials>`  |
+-----------------+----------------+-----------------------------------------------+


.. note:: This operation does not accept a request body.

Response
--------

**Example List metrics by check ID: JSON response**

.. code::

   {
       "values": [
           {
               "name": "mzdfw.available",
               "unit": "percent",
               "type": "D"
           },
           {
               "name": "mzdfw.average",
               "unit": "seconds",
               "type": "D"
           }
       ],
       "metadata": {
           "count": 2,
           "limit": null,
           "marker": null,
           "next_marker": null,
           "next_href": null
       }
   }
