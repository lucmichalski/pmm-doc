########
Security
########

************
Introduction
************

Percona Monitoring and Management has a number of security-related features built into it. This section describes them and gives some general advice on how to use them.

*********
Isolation
*********

Where possible, run your server and clients within a firewall or on a separate network.

When using Docker containers, ...

**********
Networking
**********

Clients and servers can communicate via SSL if you have signed certificates installed.

Virtual and container images (Docker, OVF and AMI) come with self-signed certificates.

Use pmm-admin to configure clients to use SSL and a certificate from a Certificate Authority.

.. code-block:: bash

   pmm-admin config --server <server IP/hostname> --server-ssl


For self-signed certificates:

.. code-block:: bash

    pmm-admin config --server <server IP/hostname> --server-insecure-ssl

======
Docker
======

With Docker, this can be done in two ways.


1. Mount the certificates directory and only using port 443.

In this example, certificates are in ``/etc/pmm-certs`` and
mounted in the container to ``/srv/nginx``.

The certificate files are:

    certificate.crt
    certificate.key
    ca-certs.pem
    dhparam.pem


.. code-block:: bash

    docker run -d -p 443:443 \
  --volumes-from pmm-data \
  --name pmm-server \
  -v /etc/pmm-certs:/srv/nginx \
  --restart always \
  percona/pmm-server:2


2. Copy certificates inside the container.

    .. code-block:: bash

       docker cp certificate.crt pmm-server:/srv/nginx/certificate.crt
       docker cp certificate.key pmm-server:/srv/nginx/certificate.key
       docker cp ca-certs.pem pmm-server:/srv/nginx/ca-certs.pem
       docker cp dhparam.pem pmm-server:/srv/nginx/dhparam.pem



The web interface can be accessed via ports 80 (HTTP) or 443 (HTTPS).

Connection Traffic Encryption

HTTPS
SSL
SSL Certificates
  Self-signed
  Letsencrypt


*********
Passwords
*********

Choose strong passwords when:

- first logging into PMM and changing the default administrator's password -- do not skip this step;

- when creating users via *Configuration > Users*.