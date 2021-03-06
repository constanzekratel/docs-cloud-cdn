
.. _cdn-update-a-service:

Update a service
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PATCH /v1.0/{project_id}/services/{service_id}

This operation updates the specified service.

You can use the HTTP PATCH method to ``add``, ``remove``, or ``replace`` service properties. For more information about the HTTP PATCH method, see `RFC5789 <https://tools.ietf.org/html/rfc5789>`__.

To update a service, send a JSON body that conforms to `RFC6902 <https://tools.ietf.org/html/rfc6902>`__ using paths and values for one or more of the service parameters, which are described in :ref:`Create a service <cdn-create-a-service>`. If no changes are specified for a parameter in the JSON body, all parameter values from the previous version of the service are carried over by default.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|202                       |Accepted                 |The request has been     |
|                          |                         |accepted for processing. |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad Request              |Invalid input JSON or    |
|                          |                         |service not deployed.    |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |Service not found.       |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""




This table shows the URI parameters for the request:

+-------------+-------------+--------------------------------------------------------------+
|Name         |Type         |Description                                                   |
+=============+=============+==============================================================+
|{project_id} |String       |The project ID for the user. If you do not set the ``X-       |
|             |             |Project-Id header`` in the request, use ``project_id`` in the |
|             |             |URI. For example: ``GET                                       |
|             |             |https://global.cdn.api.rackspacecloud.com/v1.0/{project_id}`` |
+-------------+-------------+--------------------------------------------------------------+
|{service_id} |String       |Specifies the service ID that represents distributed content. |
|             |             |The value is a UUID, such as 96737ae3-cfc1-4c72-be88-         |
|             |             |5d0e7cc9a3f0, that is generated by the server.                |
+-------------+-------------+--------------------------------------------------------------+





This table shows the body parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|\ **op**                  |String *(Required)*      |Specifies the operation, |
|                          |                         |``add``, ``remove``, or  |
|                          |                         |``replace``, to be       |
|                          |                         |executed.                |
+--------------------------+-------------------------+-------------------------+
|\ **path**                |String *(Required)*      |Specifies the JSON       |
|                          |                         |Pointer location within  |
|                          |                         |the service's JSON       |
|                          |                         |representation of the    |
|                          |                         |service parameter being  |
|                          |                         |added, replaced or       |
|                          |                         |removed.                 |
+--------------------------+-------------------------+-------------------------+
|\ **value**               |String                   |Specifies the actual     |
|                          |                         |value to be added or     |
|                          |                         |replaced. It is not      |
|                          |                         |required for the         |
|                          |                         |``remove`` operation.    |
+--------------------------+-------------------------+-------------------------+





**Example: Update a service HTTP and JSON request**


.. code::

   PATCH /v1.0/110011/services/96737ae3-cfc1-4c72-be88-5d0e7cc9a3f0 HTTP/1.1
   Host: global.cdn.api.rackspacecloud.com
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Content-type: application/json-patch+json


.. code::

     [
       {
           "op": "add",
           "path": "/domains/-",
           "value": {
               "domain": "newDomain.com",
               "protocol": "http"
           }
       },
       {
           "op": "replace",
           "path": "/domains/0",
           "value": {
               "domain": "replaceDomain.com",
               "protocol": "http"
           }
       },
       {
           "op": "add",
           "path": "/domains/-",
           "value": {
               "domain": "addDomain1.com",
               "protocol": "http"
           }
       },
       {
           "op": "add",
           "path": "/domains/-",
           "value": {
               "domain": "addDomain2.com",
               "protocol": "http"
           }
       },
       {
           "op": "add",
           "path": "/domains/-",
           "value": {
               "domain": "addDomain3.com",
               "protocol": "http"
           }
       },
       {
           "op": "remove",
           "path": "/domains/0"
       },
       {
           "op": "add",
           "path": "/domains",
           "value": [
               {
                   "domain": "addDomainList.com",
                   "protocol": "http"
               }
           ]
       },
       {
           "op": "replace",
           "path": "/name",
           "value": "newServiceName"
       },
       {
           "op": "replace",
           "path": "/origins/0",
           "value": {
               "origin": "1.2.3.4",
               "port": 80,
               "rules": [],
               "ssl": false
           }
       },
       {
           "op": "add",
           "path": "/origins/1",
           "value": {
               "origin": "1.2.3.4",
               "port": 80,
               "ssl": false,
               "rules": [
                   {
                       "name": "origin",
                       "request_url": "/origin.htm"
                   }
               ]
           }
       },
       {
           "op": "add",
           "path": "/origins/2",
           "value": {
               "origin": "4.2.5.4",
               "port": 80,
               "ssl": false,
               "rules": [
                   {
                       "name": "origin",
                       "request_url": "/origin.htm"
                   }
               ]
           }
       },
       {
           "op": "add",
           "path": "/origins/-",
           "value": {
               "origin": "1.2.3.4",
               "port": 80,
               "ssl": false,
               "rules": [
                   {
                       "name": "origin",
                       "request_url": "/origin.htm"
                   }
               ]
           }
       },
       {
           "op": "remove",
           "path": "/origins/0"
       },
       {
           "op": "replace",
           "path": "/caching/0",
           "value": {
               "name": "cache_name",
               "ttl": 111
           }
       },
       {
           "op": "remove",
           "path": "/caching/0"
       },
       {
           "op": "add",
           "path": "/caching/-",
           "value": {
               "name": "cache_name",
               "ttl": 111,
               "rules": [
                   {
                       "name": "index",
                       "request_url": "/index.htm"
                   }
               ]
           }
       },
       {
           "op": "replace",
           "path": "/log_delivery/enabled",
           "value": true
       } 
   ]





Response
""""""""""""""""







This operation does not return a response body.

**Example: Update a service HTTP response**


.. code::

   HTTP/1.1 202 Accepted
   Location: https://global.cdn.api.rackspacecloud.com/v1.0/services/96737ae3-cfc1-4c72-be88-5d0e7cc9a3f0




